---
name: listing-blog-posts
description: Create WordPress blog posts from property listings via the Virtual Results
  MCP connector — search listings, write the post, attach images, set SEO, request review.
  Trigger: "blog post from listings", "new listings roundup", "feature this listing".
---

# Blog posts from listings (Virtual Results MCP)

## Workflow order
1. `get_site_info` / `list_sites` — confirm which site; pass `site` explicitly on every
   call when the account has more than one.
2. `search_listings` ONCE with filters (city, price range, beds, `exclusive_only`,
   `max_days_on_market` for "new this week") — it returns address, price, beds/baths,
   status, description, `listing_url`, and `primary_photo` for every result. Do NOT
   follow up with per-listing `get_listing` calls unless you need a field search
   didn't return. Each extra call costs ~1s; a 10-listing loop is 10 wasted seconds.
3. Write the post. Draft only — `create_draft`. Never anything else first.
4. Images (rules below), categories/tags (`list_terms` for IDs), Yoast meta.
5. `request_review` — give the owner the review_link. STOP. Publish only after they
   approve in their own words, with the approval_token.

## Listing data rules
- Use ONLY fields the API returned. Never invent or "remember" price, beds, sqft,
  open-house times. If a field is null, omit the fact — don't guess.
- Link each listing with its returned `listing_url` verbatim. Never construct listing
  URLs by hand.
- State the listing status when it isn't a normal active listing ("Coming Soon").
- Keep MLS descriptions paraphrased, not pasted wholesale — the raw description is
  feed content that appears on the listing page already.

## Image rules
- `upload_media` with `source_url` is THE way to move images — pass the image's URL,
  the server fetches it. Never generate base64 unless the image truly exists nowhere
  on the web. jpeg/png/webp/gif/avif, 15MB max, public URLs only.
- Featured image: `upload_media` (source_url = the lead listing's `primary_photo`) →
  pass returned id as `featured_media` on create_draft/update_draft. A featured image
  must be a media-library id; a hotlink cannot be one.
- Body images: hotlinking the `primary_photo` URLs in <img> tags is acceptable (they
  are the same CDN the site itself uses), but pair each image with ITS OWN listing —
  never reuse a photo from listing A next to listing B, and never pick photos from
  anywhere except that listing's own returned photo fields.
- URL FORMAT for photos embedded in post content: use the API's URLs VERBATIM.
  Both `primary_photo` and every entry in `photos[]` come back already wrapped in
  the site's ImageKit proxy (`https://ik.imagekit.io/virtualresults/absurl/...`) —
  never unwrap, decode, shorten, or reconstruct them, and never substitute a bare
  MLS CDN link (`photos.prod.cirrussystem.net`, `dvvjkgh94f2v6.cloudfront.net`) from
  anywhere else: bare links skip optimization/caching and break permanently when the
  MLS rotates the photo. Safety check: if a photo URL you are about to embed does
  NOT start with `https://ik.imagekit.io/`, wrap it first:
  `https://ik.imagekit.io/virtualresults/absurl/tr:di-noimage.png,t-true,f-auto,pr-true/`
  + URL-encoded original. (upload_media source_url is the exception — raw URL fine
  there; the file gets copied into the media library.)
- Give uploads a descriptive filename ("2106-garden-place-atlanta.jpg") and put the
  address in the img alt text.

## Post construction
- Title: keyword-rich, local ("New Listings in Atlanta, Orlando & Houston — August 2026").
- Structure: intro → group listings by area with h2/h3 → per listing: photo, linked
  address heading, price · beds/baths · status line, 1–2 sentence hook → closing CTA
  to contact the team.
- Set `excerpt`.
- Categories/tags: `list_terms` first, pass term IDs — never invent IDs. Create
  nothing new without being asked.
- Yoast via `meta`: `_yoast_wpseo_title`, `_yoast_wpseo_metadesc` (~155 chars),
  `_yoast_wpseo_focuskw`. Only set others if asked.

## Hard rules
- Draft-first always; publish/unpublish ONLY with an approval_token from
  request_review after explicit owner approval. Show the review_link and wait.
- One `update_draft` with all fields beats many single-field updates (~1s per call).
- If a tool errors "Invalid parameter(s)" or capability errors, report it verbatim —
  don't silently retry with degraded content.
