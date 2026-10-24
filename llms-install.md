# Installing the email59 MCP server (for AI coding assistants)

This is a hosted remote MCP server. Nothing to clone, build or install.

1. Add a remote (Streamable HTTP) server named `email59` with the URL `https://email59.com/v1/mcp` to the MCP settings.
   For an `mcpServers` JSON file:
   ```json
   { "mcpServers": { "email59": { "type": "http", "url": "https://email59.com/v1/mcp" } } }
   ```
2. No API key is needed to start. To get one, call the `auth` tool with the user's email address, ask the user for
   the 6-digit code they receive, and call `auth` again with `email` and `otp`. Then add the header
   `Authorization: Bearer <session key>` to the server entry.
3. Check it works: call `tools/list`; you should see the tools listed in README.md.
