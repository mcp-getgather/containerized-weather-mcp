# containerized-weather-mcp

A containerized version of the weather mcp at https://modelcontextprotocol.io/quickstart/server

## Quickstart

### Connecting Your MCP Client to a Deployed Instance

For convenience, we have deployed the container using fly.io at https://getgather-weather.fly.dev/mcp. 

If you so desire, you can connect your MCP client directly to this instance. Clients like Claude offer an option to add custom connectors directly from the settings. Open Claude, navigate to settings, and go to the "Connectors" tab. Click on "Add custom connector" and give your connector a name. Then, in the second box for "Remore MCP server URL" you can paste `https://getgather-weather.fly.dev/mcp`. Finish by clicking "Add" (no advanced settings necessary for this!). You should see the new weather MCP appear in your list of connectors. Open a new chat in Claude and look for the server under the "Tools" icon. You should see it appear under the name you set for it.

For clients that don't use custom connectors in the UI, you can always set up the weather MCP using a simple URL in the configuration JSON. For example, in Cursor/VS Code you can add the following to your `mcp.json`:

```json
{
  "mcpServers": {
    "weather": {
      "url": "https://getgather-weather.fly.dev/mcp"
    }
  }
}
```

### Run Locally with Docker

Alternatively, you can build the Docker image locally and add the running endpoint to your client config. The following command pulls and runs the latest public image for the weather MCP.

`$ docker run -p 8000:8000 ghcr.io/mcp-getgather/containerized-weather-mcp`

Then add http://localhost:8000/mcp as a model endpoint in your MCP client. If using Claude Desktop, you can add the following to your `claude_desktop_config.json` (which is found from `Claude` -> `Settings` -> `Developer` -> `Edit Config`):

```json
{
  "mcpServers": {
    "http-weather": {
      "command": "npx",
      "args": [
        "mcp-remote",
        "http://127.0.0.1:8000/mcp",
        "--allow-http"
      ]
    }
  }
}
```

If you're not using Claude, and you're client supports http streaming directly, you will just need the local URL and `/mcp` extension as in the VS Code/Cursor example above.

Remember for streamable http (including mcp-remote), you need your mcp server to be running [(as opposed to the client launching it for you as with stdio)](https://modelcontextprotocol.io/specification/2025-06-18/basic/transports#stdio).
