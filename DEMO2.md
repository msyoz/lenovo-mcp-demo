# DMEO2: Use "My Name" MCP Server in VSCode

## Step 5: use it in VSCode

Add `mcp.json` into .vscode

```json
{
    "servers": {
        "my name": {
            "type": "stdio",
            "command": "uv",
            "args": [
                "--directory",
                "C:\\ABSOLUTE\\PATH\\TO\\PARENT\\FOLDER\\mcp-demo",
                "run",
                "server.py"
            ]
        }
    }
}
```

Start "my name" mcp server, then chat in GitHub Copilot chat.
