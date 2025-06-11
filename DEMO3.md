# DEMO3: Integrate "My Name" MCP Server in Semantic Kernel

## Step 6: use it in Semantic Kernel

Install SK package

```bash
uv add semantic-kernel
```

Add .env file

```env
AZURE_OPENAI_ENDPOINT=<your-endpoint>
AZURE_OPENAI_API_KEY=<your-api-key>
AZURE_OPENAI_CHAT_DEPLOYMENT_NAME=<your-deployment-name>
```

Add client.py

```python
# Copyright (c) Microsoft. All rights reserved.

import asyncio
import os

from semantic_kernel.agents import ChatCompletionAgent, ChatHistoryAgentThread
from semantic_kernel.connectors.ai.open_ai import AzureChatCompletion
from semantic_kernel.connectors.mcp import MCPStdioPlugin


# Simulate a conversation with the agent
USER_INPUTS = [
    "我叫什么？",
    "我的姓是什么？",
]


async def main():
    # 1. Create the agent
    async with MCPStdioPlugin(
        name="MyName",
        description="My Name Plugin",
        command="uv",
        # The command to run the MCP server, which should be available in your PATH
        args=[
                "--directory",
                "C:\\ABSOLUTE\\PATH\\TO\\PARENT\\FOLDER\\mcp-demo",
                "run",
                "myname.py"
            ],
    ) as my_name_plugin:
        agent = ChatCompletionAgent(
            service=AzureChatCompletion(),
            name="MyNameAgent",
            instructions="Answer questions about my name.",
            plugins=[my_name_plugin],
        )

        for user_input in USER_INPUTS:
            # 2. Create a thread to hold the conversation
            # If no thread is provided, a new thread will be
            # created and returned with the initial response
            thread: ChatHistoryAgentThread | None = None

            print(f"# User: {user_input}")
            # 3. Invoke the agent for a response
            response = await agent.get_response(messages=user_input, thread=thread)
            print(f"# {response.name}: {response} ")
            thread = response.thread

            # 4. Cleanup: Clear the thread
            await thread.delete() if thread else None

if __name__ == "__main__":
    asyncio.run(main())
```

Run the client.py

```bash
uv run client.py
```