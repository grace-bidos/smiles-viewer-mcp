# SMILES Viewer MCP

A small Model Context Protocol server that exposes a `render_smiles` tool and an
OpenAI Apps SDK widget for drawing SMILES strings as 2D molecule diagrams.

The widget uses `smiles-drawer` in the browser and is served as a
`text/html+skybridge` resource for OpenAI-compatible MCP clients.

## What it does

- Registers a `render_smiles` MCP tool.
- Accepts a SMILES string as structured input.
- Renders the structure in an embedded widget.
- Serves the MCP endpoint over Streamable HTTP at `/mcp`.

## Project layout

```text
apps/smiles-viewer/
  server/src/index.ts   MCP server and tool registration
  web/widget.html       OpenAI Apps SDK widget UI
```

## Requirements

- Bun
- Node-compatible runtime dependencies from `package.json`

## Run locally

```sh
bun install
bun nx start smiles-viewer
```

By default the server listens on:

```text
http://localhost:2091/mcp
```

Set `PORT` to choose a different port:

```sh
PORT=3001 bun nx start smiles-viewer
```

## Tool

`render_smiles`

Input:

```json
{
  "smiles": "CCO"
}
```

The tool returns structured content containing the SMILES string and asks the
client to render `ui://widget/smiles-viewer.html`.

## Notes

This is a prototype/demo app. It does not require API keys or external secrets.
