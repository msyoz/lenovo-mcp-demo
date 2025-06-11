# DEMO1: Develop "My Name" MCP Server with Python

## Step 0: install required tools

Make sure you have installed the following tools:
- [uv](https://docs.astral.sh/uv/getting-started/installation/)
- [VSCode](https://code.visualstudio.com/)
- [GitHub Copilot](https://github.com/features/copilot)

## Step 1: install MCP library

Linux

```bash
# Create a new directory for our project
uv init mcp-demo
cd mcp-demo

# Create virtual environment and activate it
uv venv
source .venv/bin/activate

# Install dependencies
uv add "mcp[cli]"

# Create our server file
touch server.py
```

Windows

```powershell
# Create a new directory for our project
uv init mcp-demo
cd mcp-demo

# Create virtual environment and activate it
uv venv
.venv\Scripts\activate

# Install dependencies
uv add mcp[cli]

# Create our server file
new-item server.py
```

## Step 2: importing and setting up for server.py

```python
from mcp.server.fastmcp import FastMCP

# Initialize FastMCP server
mcp = FastMCP("my name")
```

## Step 3: logic for server.py

```python
@mcp.tool()
async def get_my_name(position:str="full") -> str:
    """Get my name, full name, first name or last name

    Args:
        position: full or first or last
    """
    if position == "full":
        return "Yongguang Zhu"
    elif position == "first":
        return "Yongguang"
    elif position == "last":
        return "Zhu"
    else:
        return "Invalid position"
```

## Step 4: running the server

```python
if __name__ == "__main__":
    # Initialize and run the server
    mcp.run(transport='stdio')
```
