# containerized-weather-mcp

A containerized version of the weather mcp at https://modelcontextprotocol.io/quickstart/server

## Quickstart

### Run Locally with Docker

`$ docker run -p 8000:8000 ghcr.io/mcp-getgather/containerized-weather-mcp`

Then add http://localhost:8000/mcp-weather as a model endpoint in your MCP client. If using Claude Desktop, you can add the following to your `claude_desktop_config.json` (which is found from `Claude` -> `Settings` -> `Developer` -> `Edit Config`):

```json
{
  "mcpServers": {
    "http-weather": {
      "command": "npx",
      "args": [
        "mcp-remote",
        "http://127.0.0.1:8000/mcp-weather",
        "--allow-http"
      ]
    }
  }
}
```

This isn't truly using streamable http as the transport, as Claude Desktop doesn't support that yet, but it works fine for testing (claude launches a proxy that hits your endpoint). If you want true streamable http support, you can use either inspector, Claude Code, or another MCP client that supports streamable http.

Remember for streamable http (including mcp-remote), you need your mcp server to be running [(as opposed to the client launching it for you as with stdio)](https://modelcontextprotocol.io/specification/2025-06-18/basic/transports#stdio).

### Connecting Your MCP Client to the Deployed Instance

For convenience, we have deployed the container using fly.io at https://containerized-weather-mcp.fly.dev/mcp-weather. If you so desire, you can connect your MCP client to this instance. For example, in Claude Desktop, you can add the following to your `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "http-weather": {
      "command": "npx",
      "args": [
        "mcp-remote",
        "https://containerized-weather-mcp.fly.dev/mcp-weather",
        "--allow-http"
      ]
    }
  }
}
```
