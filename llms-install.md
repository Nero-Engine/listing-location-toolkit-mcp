# Installing Listing Location Toolkit (remote MCP server, no install needed)

Listing Location Toolkit is a hosted remote MCP server. There is nothing to download, build or run, and no API key.

Add this to the MCP settings file (in Cline: MCP Servers, Configure, then cline_mcp_settings.json):

```json
{
  "mcpServers": {
    "listing-location-toolkit": {
      "type": "streamableHttp",
      "url": "https://listing-location-toolkit.nerolabs.workers.dev/mcp",
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

Save the file. The server's tools appear straight away. To check it works, ask the assistant to list the server's tools.

Docs: https://listing-location-toolkit.nerolabs.workers.dev/docs
