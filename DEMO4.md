# DEMO4: Change stdio to streamable-http

## Step 1: Update `server.py`

In `server.py`, change the `stdio` transport to `streamable-http`. This allows the MCP server to communicate over HTTP instead of standard input/output.

```python
if __name__ == "__main__":
    # Initialize and run the server
    mcp.run(transport="streamable-http")
```

Run the server with the following command:

```bash
uv run server.py
```

## Step 2: Update `client.py`

In `client.py`, update the client to use the HTTP transport. This will allow it to communicate with the MCP server over HTTP.

```python
async with MCPStreamableHttpPlugin(
    name="MyName",
    description="My Name Plugin",
    url="http://127.0.0.1:8000/mcp",
) as my_name_plugin:
```