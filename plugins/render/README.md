# Render

Use Render from Cursor to deploy apps, debug failed deploys, monitor services, and run code in Render Sandboxes.

## Included

- `rules/`: Render best practices and render.yaml validation checklist
- `skills/`: Skills for deployment, debugging, monitoring, and [Sandboxes](skills/render-sandboxes/SKILL.md) (synced from [render-oss/skills](https://github.com/render-oss/skills))
- `agents/`: Render deployment assistant
- `commands/`: Deploy to Render and check service status
- `.mcp.json`: Render MCP server configuration (OAuth via the pre-registered Cursor client)
- `hooks/`: Validates render.yaml after edits

## Get started

Ask Cursor to:

- `Help me deploy this project to Render.`
- `Debug a failed Render deployment.`
- `Run this Python script in a Render Sandbox with network access disabled. Show the output, then delete the sandbox.`

### Sandbox tasks

The [sandbox skill](skills/render-sandboxes/SKILL.md) guides Cursor through running commands, transferring files, inspecting results, and cleaning up. Use a Render workspace with Sandboxes access.

If the connected MCP server does not expose sandbox tools, the skill can use the Render CLI instead. See the [CLI workflow](skills/render-sandboxes/references/cli.md) for setup and supported network policies.

## Render MCP in Cursor

This plugin declares the hosted Render MCP server in `.mcp.json` with the pre-registered Cursor OAuth client id `cursor`. After installing or updating the plugin, Cursor connects to `https://mcp.render.com/mcp` and prompts for Render OAuth the first time MCP tools are used.

No `RENDER_API_KEY` or manual `~/.cursor/mcp.json` entry is needed for the plugin-provided MCP connection. For the CLI fallback, authenticate separately with `render login`.

## Skills sync

Skills in `skills/` are synced automatically from the [render-oss/skills](https://github.com/render-oss/skills) repository. A GitHub Action runs daily and opens a PR when changes are detected. To sync manually:

```bash
./scripts/sync-skills.sh
```

Make skill changes in the shared repository before syncing them here. For sandbox support, coordinate the release with the [Render MCP server](https://github.com/render-oss/render-mcp-server) maintainers so the hosted connection exposes the required tools.
