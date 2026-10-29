# VEDUTUM plugin for Claude Code

Floor plan to measured 3D model from Claude Code: read a plan from a link, list rooms and areas, furnish, set roof and facade, lay out solar modules, set the site and surroundings, create the client share link. Images and videos stay in the VEDUTUM app.

## Install

```
/plugin marketplace add kalenadesigns/vedutum-claude-plugin
/plugin install vedutum@vedutum
```

Without the plugin, the server alone:

```
claude mcp add --transport http vedutum https://www.vedutum.com/mcp
```

The public tools work right away. The first tool on your own projects asks for sign-in: run `/mcp`, choose `vedutum`, sign in with your VEDUTUM account and allow the connection. Disconnect any time in VEDUTUM under Account → Connections.

## Contents

- `plugins/vedutum/.mcp.json` — the remote MCP server `https://www.vedutum.com/mcp` (Streamable HTTP, OAuth 2.1 for account tools)
- `plugins/vedutum/skills/floor-plan-to-3d/` — the skill "Floor plan to 3D with VEDUTUM"

## Privacy and support

Privacy: https://www.vedutum.com/datenschutz (section 6) · Documentation: https://www.vedutum.com/en/ai-assistants · Support: office@vedutum.com

VEDUTUM is a product of EA Digital Solutions e.U., Graz, Austria.
