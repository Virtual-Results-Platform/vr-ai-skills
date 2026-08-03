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
/plugin marketplace add Virtual-Results-Platform/vr-ai-skills
/plugin install vr-website@vr-ai-skills
/plugin install listing-blog-posts@vr-ai-skills
```

Update later with `/plugin marketplace update vr-ai-skills`.

## Plugins

| Plugin | What it does |
| --- | --- |
| `vr-website` | **Install first.** Connects Claude Code to your Virtual Results website (MCP). Browser sign-in on first use — no keys to copy. |
| `listing-blog-posts` | Blog posts from property listings (search listings, images, Yoast SEO, draft + review flow). Uses the `vr-website` connection. |

## Adding a Claude skill

New folder `claude/plugins/<name>/skills/<name>/SKILL.md` + `claude/plugins/<name>/.claude-plugin/plugin.json`, then list it in `.claude-plugin/marketplace.json` (source `./claude/plugins/<name>`). Commit, push — installed copies pick it up on marketplace update.
