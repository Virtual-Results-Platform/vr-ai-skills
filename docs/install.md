# Connect Your AI to Your Virtual Results Website

Let Claude or ChatGPT work directly on your website: write blog posts, edit pages,
upload images, manage SEO — always saved as drafts until you approve publishing.

One browser sign-in. No passwords to copy, no API keys.

**Connector URL (used in every option below):**

```
https://mcp.virtualresultsplatform.com/mcp
```

---

## Option 1 — Claude on the web or desktop app (easiest)

Works at claude.ai and in the Claude desktop app. Requires a paid Claude plan.

1. Open **Settings → Connectors**
2. Click **Add custom connector**
3. Name: `Virtual Results Website` — URL: the connector URL above
4. Click **Connect** and sign in when the browser window opens
5. Start a new chat and try: *"List my websites"*

## Option 2 — Claude Code (terminal)

The recommended install also adds ready-made skills (like `/listing-blog-posts`).
Type these inside Claude Code:

```
/plugin marketplace add Virtual-Results-Platform/vr-ai-skills
/plugin install vr-website@vr-ai-skills
/plugin install listing-blog-posts@vr-ai-skills
```

Then type `/mcp` and sign in when the browser opens. Done.

Prefer just the connector, no skills? One line instead:

```
claude mcp add --transport http virtual-results-website https://mcp.virtualresultsplatform.com/mcp
```

## Option 3 — ChatGPT

Requires a paid ChatGPT plan; custom connectors live behind developer mode.

1. **Settings → Apps & Connectors → Advanced settings** — turn on **Developer mode**
2. Back in **Apps & Connectors**, click **Create** (custom connector)
3. Name: `Virtual Results Website` — MCP server URL: the connector URL above —
   Authentication: **OAuth**
4. Save, then sign in when prompted
5. In a chat, add the connector via the **+ / tools** menu and try: *"List my websites"*

## Coming soon

- Codex CLI instructions

---

## Tips & troubleshooting

- **The AI says it can't see the website tools** — start a new chat (tools load at
  chat start), or disconnect/reconnect the connector.
- **Sign-in loops or "not entitled"** — your login email may not be linked to your
  site yet. Contact us and we'll connect it.
- **Nothing goes live without you.** Everything is drafted; the AI sends you a review
  link and publishes only after you approve.

Questions? support@virtualresults.net
