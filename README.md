# Claude Imagine — MCP Server & Claude Code Plugin

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

**Claude Code — as a plugin (recommended):**

```bash
/plugin marketplace add lumian2015/claudeimagine-mcp
/plugin install claude-imagine@claudeimagine-mcp
```

The plugin ships nothing but this server's configuration, so installing it is
the same as adding the connector by hand — it just keeps the setup versioned
and lets `/plugin` manage updates. Claude Code reports the server as
`needs-auth` until you run `/mcp` and complete the browser login once.

**Claude Code — as a plain connector:**

```bash
claude mcp add --transport http claude-imagine https://claudeimagine.com/api/mcp
```

**claude.ai / Claude Desktop:** add it as a custom connector — Customize →
Connectors → **+** → Add custom connector → paste the URL above. Full
walkthrough (including Team/Enterprise setup): [claudeimagine.com/claude-image-mcp](https://claudeimagine.com/claude-image-mcp).

## Tools

| Tool | What it does |
| --- | --- |
| `generate_image` | Image from a text prompt. `model`: `nano-banana-2` (default), `gpt-image-2.5`, `seedream-4.5`, `flux-2-pro`, `z-image`. Optional `aspect_ratio` and `resolution` (`1k`/`2k`/`4k`). |
| `edit_image` | Change an existing image from one or more reference URLs, same model and size options. |
| `generate_video` | Video from a prompt, optionally from a starting image. `model`: `grok-imagine`, `seedance-1.5-pro`, `seedance-2.0-mini`, `veo-3.1-fast`, `kling-2.5-turbo`, `h3-max-turbo`, each with its own duration and resolution range. |
| `quote_generation` | Exact credit cost of a call **before** you make it, with your balance and plan eligibility. Free; nothing is reserved. |
| `check_generation` | Collect the result of a generation that outlived its original request. |
| `list_generations` | Your recent generations. |
| `list_models` | Available image and video models with the live credit cost for your plan tier. |
| `get_credits` | Your remaining credit balance. |
| `plan_product_ad` | Guided product-ad workflow with budget safeguards. |

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
