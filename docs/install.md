# Connect Claude to Your Virtual Results Website

Claude can write blog posts, edit pages, upload images, and handle your SEO fields —
working directly on your website. Everything is saved as a draft. Nothing goes live
until you approve it.

Setup takes about a minute. There is nothing to install and nothing to download.

---

## Step 1 — Add the connector (one time)

**In the Claude app or at claude.ai:**

1. Open **Settings → Connectors**
2. Click **Add custom connector**
3. Name it `Virtual Results Website`
4. Paste this URL:

   ```
   https://mcp.virtualresultsplatform.com/mcp
   ```

5. Click **Add**, then **Connect**, and sign in when the browser window opens.

Sign in with **the same email address as your WordPress account on your website**.
That is how Claude knows which site is yours.

That's it. You're connected.

---

## Step 2 — Use it

Start a **new chat** and just ask. For example:

- *"List my websites"* — confirms the connection is working
- *"Write a blog post about our new listings in Atlanta this week"*
- *"Find my post about spring market trends and fix the SEO description"*
- *"Show me my most recent drafts"*

Claude already knows how to write your listing posts properly — the instructions come
with the connector, so there is nothing extra to set up. If you want to point at them
directly, they appear in Claude's prompt menu as **"Write a blog post from listings"**
and **"Blogging standards."**

## Step 3 — Approve before anything publishes

When a post is ready, Claude gives you a **review link**. Open it, read the post, and
tell Claude to publish only if you're happy. Claude cannot publish without that step,
and it cannot delete anything, ever.

---

## Using ChatGPT instead

ChatGPT works too, on paid plans:

1. **Settings → Apps & Connectors → Advanced settings** — turn on **Developer mode**
2. Back in **Apps & Connectors**, click **Create**
3. Name: `Virtual Results Website` · MCP server URL: the same URL as above ·
   Authentication: **OAuth**
4. Save and sign in when prompted, then add the connector to your chat with the
   **+** menu

---

## If something doesn't work

**"Claude can't see my website"** — start a brand-new chat. Connectors load when a chat
begins, so an older chat won't see it.

**"Not entitled" or "no sites"** — the email you signed in with doesn't match your
WordPress user. Contact us and we'll line them up.

**Sign-in won't complete** — disconnect the connector in Settings, add it again, and
retry in a new chat.

Still stuck? Email support@virtualresults.net and tell us which step you're on.

---

<details>
<summary>For developers: Claude Code (terminal)</summary>

Add the connector:

```bash
claude mcp add --transport http virtual-results-website https://mcp.virtualresultsplatform.com/mcp
```

Then `/mcp` to sign in. The playbooks arrive as prompts
(`/mcp__virtual-results-website__write_listing_blog_post`).

Optional — the same playbooks as installable skills, plus future VR tooling:

```
/plugin marketplace add Virtual-Results-Platform/vr-ai-skills
/plugin install vr-website@vr-ai-skills
/plugin install listing-blog-posts@vr-ai-skills
/plugin install exceptional-blogging@vr-ai-skills
```

Note: `/plugin` is a Claude Code command. It does not exist in the Claude desktop or
web app — those use the connector above.

</details>
