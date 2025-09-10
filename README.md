# Weather MCP Server

This is [the weather server](https://modelcontextprotocol.io/quickstart/server) from the official [MCP documentation](https://modelcontextprotocol.io/docs/), packaged in a container. It only works with MCP clients that support [streamable HTTP transport](https://modelcontextprotocol.io/docs/learn/architecture#transport-layer).

## Quickstart

For [VS Code](https://code.visualstudio.com/docs/copilot/customization/mcp-servers), [Cursor](https://docs.cursor.com/en/context/mcp), [LM Studio](https://lmstudio.ai/docs/app/plugins/mcp), [Jan](https://docs.jan.ai/jan/mcp/), and similar apps, add the following to the MCP servers configuration, typically called `mcp.json`:

```json
{
  "mcpServers": {
    "weather": {
      "url": "https://getgather-weather.fly.dev/mcp"
    }
  }
}
```

For [Claude](https://claude.ai/), use its [custom connectors feature](https://support.anthropic.com/en/articles/11175166-getting-started-with-custom-connectors-using-remote-mcp):

1. Open Claude, navigate to _Settings_, and go to the _Connectors_ tab.
2. Click _Add custom connector_ and give the connector a name.
3. In the second box for _Remote MCP server URL_, paste `https://getgather-weather.fly.dev/mcp`.
4. Click _Add_ to finish (no advanced settings necessary for this server).

The new weather MCP server will appear in the list of connectors. Open a new chat in Claude and look for the server under the _Tools_ icon.

### Run Locally

Use [Docker](https://docker.com) or [Podman](https://podman.io) to pull the container image and run it:

```bash
docker run -p 8000:8000 ghcr.io/mcp-weather
```

Then use `http://localhost:8000/mcp` as the remote URL in the MCP server configuration `mcp.json` (works for [VS Code](https://code.visualstudio.com/docs/copilot/customization/mcp-servers), [Cursor](https://docs.cursor.com/en/context/mcp), [LM Studio](https://lmstudio.ai/docs/app/plugins/mcp), [Jan](https://docs.jan.ai/jan/mcp/), etc.):

```json
{
  "mcpServers": {
    "weather": {
      "url": "http://localhost:8000/mcp"
    }
  }
}
```

For [Claude](https://claude.ai/), note that its [custom connectors feature](https://support.anthropic.com/en/articles/11175166-getting-started-with-custom-connectors-using-remote-mcp) only supports HTTPS, not HTTP. To use the local server with Claude, set up a reverse tunnel to make this local server accessible over a secure connection.
