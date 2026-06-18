# Zotero-Claude-Plugin

A Claude Code plugin to search, read, and cite your [Zotero](https://www.zotero.org)
library. It talks to Zotero's built-in **local HTTP API** — no MCP server, no
dependencies. Just `curl`, `jq`, and Claude's PDF-capable Read tool.

## What it does

- **Search** your library by keyword (including indexed PDF full-text).
- **Read** an article's metadata and its PDF.
- **Cite** an article in any CSL style (APA by default) or as BibTeX.

## Requirements

- Zotero **7+**, running.
- The **local API enabled** (one-time setup below).
- `curl` and `jq` available on `PATH` (both standard on macOS/Linux).

## One-time setup: enable Zotero's local API

1. Zotero → **Settings → Advanced → Config Editor**.
2. Set `extensions.zotero.httpServer.localAPI.enabled` to `true`.
3. Ensure **"Allow other applications on this computer to communicate with
   Zotero"** is checked (Settings → Advanced).
4. **Restart Zotero.**

Verify:

```bash
curl -s -o /dev/null -w '%{http_code}\n' \
  -H 'Zotero-Allowed-Request: true' \
  "http://localhost:23119/api/users/0/items?limit=1"
```

`200` means it's ready. `403` means the local API is still off.

## Install

```
/plugin marketplace add <this-repo-url>
/plugin install zotero@zotero-marketplace
```

Then just ask Claude things like *"find my papers on diffusion models"*,
*"read the PDF for that one"*, or *"cite it in APA"*.
