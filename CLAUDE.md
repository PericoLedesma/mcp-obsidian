# mcp-obsidian

MCP server that connects Claude to Obsidian via the [Obsidian Local REST API](https://github.com/coddingtonbear/obsidian-local-rest-api) plugin.

## Architecture

```
src/mcp_obsidian/
├── obsidian.py   # HTTP client wrapping the Obsidian REST API
├── tools.py      # MCP tool handlers (one class per tool)
└── server.py     # MCP server wiring — registers handlers, exposes list_tools/call_tool
```

Each tool follows the same pattern:
- Add a method to `Obsidian` in `obsidian.py`
- Add a `*ToolHandler` class in `tools.py`
- Register it with `add_tool_handler(tools.*ToolHandler())` in `server.py`

## Environment variables

| Variable | Default | Description |
|---|---|---|
| `OBSIDIAN_API_KEY` | required | Bearer token from the REST plugin |
| `OBSIDIAN_HOST` | `127.0.0.1` | Host where Obsidian runs |
| `OBSIDIAN_PORT` | `27124` | Port of the REST plugin |
| `OBSIDIAN_PROTOCOL` | `https` | `http` or `https` |

## Running locally

```bash
uv run mcp-obsidian
```

## Tests

```bash
uv run pytest
```

## Git workflow

- `origin` → upstream public repo (`MarkusPfundstein/mcp-obsidian`)
- `fork` → personal fork (`PericoLedesma/mcp-obsidian`)

To add the fork remote if missing:
```bash
git remote add fork git@github.com:PericoLedesma/mcp-obsidian.git
```

Contribute via feature branches pushed to the fork, then open a PR against `MarkusPfundstein/mcp-obsidian:main`.

## Pending contributions (not yet PR'd)

- `feat/move-file` — pushed, PR open against upstream
- `move_folder` — local only (stashed on main)
- `delete_folder` — local only (stashed on main)
