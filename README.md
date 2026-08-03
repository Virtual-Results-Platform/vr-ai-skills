# VR Claude Skills

Claude Code plugin marketplace for Virtual Results skills.

## Install (once per machine)

```
/plugin marketplace add https://gitlab.com/ryan34/vr-claude-skills.git
/plugin install listing-blog-posts@vr-skills
```

Update later with `/plugin marketplace update vr-skills`.

## Skills

| Plugin | What it does |
| --- | --- |
| `listing-blog-posts` | Blog posts from property listings via the VR MCP connector (search listings, images via upload_media source_url, Yoast meta, draft + review flow). |

## Adding a skill

New folder under `plugins/<name>/skills/<name>/SKILL.md` + `plugins/<name>/.claude-plugin/plugin.json`, then list it in `.claude-plugin/marketplace.json`. Commit, push — installed copies pick it up on marketplace update.
