# Claude Imagine MCP Server

A remote [Model Context Protocol](https://modelcontextprotocol.io) server that
gives Claude the ability to generate images and videos — something it can't
do natively. Connect once, then ask Claude for an image or video in plain
English.

This is an **independent, unofficial** server built on top of the
[Claude Imagine](https://claudeimagine.com) API. It is not affiliated with,
sponsored by, or endorsed by Anthropic.

This repository documents the connector and its manifest (`server.json`, as
published to the [official MCP
Registry](https://registry.modelcontextprotocol.io)). The server itself runs
as part of the Claude Imagine web app, whose source is closed.

## Endpoint

```
https://claudeimagine.com/api/mcp
```

Transport is Streamable HTTP. Auth is OAuth 2.1 with PKCE and dynamic client
registration — there's no API key to paste. Your Claude client discovers the
auth endpoints automatically and opens a browser window to log in and
consent.

New accounts start with 9 free credits. The first authenticated MCP
connection unlocks a one-time 6-credit bonus (valid 14 days), for up to 15
free credits total before you need to pay anything.

## Setup

**Claude Code (CLI):**

```bash
claude mcp add --transport http claude-imagine https://claudeimagine.com/api/mcp
```

**claude.ai / Claude Desktop:** add it as a custom connector — Customize →
Connectors → **+** → Add custom connector → paste the URL above. Full
walkthrough (including Team/Enterprise setup): [claudeimagine.com/claude-image-mcp](https://claudeimagine.com/claude-image-mcp).

## Tools

| Tool | What it does |
| --- | --- |
| `generate_image` | Generate an image from a prompt. `model` picks between `nano-banana-2` (default), `gpt-image-2`, `seedream-4.5`, `flux-2-pro`, `z-image`; `aspect_ratio` defaults to `1:1`. |
| `generate_video` | Generate a video. `model` picks between `grok-imagine` (default), `seedance-1.5-pro`, `seedance-2.0-mini`, `veo-3.1-fast`, `kling-2.5-turbo`, each with its own duration/resolution ranges; optional `image_url` for image-to-video. |
| `list_models` | Lists available image and video models with their live credit cost for your plan tier. |
| `get_credits` | Returns your remaining credit balance. |

Credits are consumed on a successful generation and refunded automatically
if one fails. Full tool reference, per-model duration/resolution tables, and
pricing: [claudeimagine.com/docs/mcp](https://claudeimagine.com/docs/mcp).

## Skill or MCP?

Claude Imagine also ships a [Claude Code
Skill](https://github.com/lumian2015/nano-banana-claude-skill) that calls the
same API with a plain API key instead of OAuth — useful when you want a
single generation written straight into a repo from Claude Code specifically.
The MCP server works everywhere: Claude Code, claude.ai, and Claude Desktop,
sharing one credit balance with the Skill and the web app.

## License

MIT — see [LICENSE](LICENSE). This covers the documentation and manifest in
this repository; it does not grant rights to the Claude Imagine service
itself.
