# VR AI Skills

Shared skills/instructions for Virtual Results AI agents — Claude Code, Codex, and whatever comes next.

## Layout

| Path | What |
| --- | --- |
| `.claude-plugin/marketplace.json` | Claude Code plugin marketplace manifest (must stay at repo root) |
| `claude/plugins/<name>/` | Claude Code plugins (skills, agents, commands) |
| `codex/` | Codex instruction sets (AGENTS.md snippets, prompts) — empty so far |

## Claude Code install (once per machine)

```
/plugin marketplace add git@gitlab.com:vr-group8491216/vr-ai-skills.git
/plugin install listing-blog-posts@vr-ai-skills
```

Update later with `/plugin marketplace update vr-ai-skills`.

## Skills

| Plugin | What it does |
| --- | --- |
| `listing-blog-posts` | Blog posts from property listings via the VR MCP connector (search listings, images via upload_media source_url, Yoast meta, draft + review flow). |

## Adding a Claude skill

New folder `claude/plugins/<name>/skills/<name>/SKILL.md` + `claude/plugins/<name>/.claude-plugin/plugin.json`, then list it in `.claude-plugin/marketplace.json` (source `./claude/plugins/<name>`). Commit, push — installed copies pick it up on marketplace update.
