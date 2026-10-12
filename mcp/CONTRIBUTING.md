# Reporting a problem with the MCP server

Read the [general guide](../CONTRIBUTING.md) first, then add these details to your [issue](../../../issues/new/choose). Choose **RodiumAi MCP server** as the product.

## What to include

- The version of the `rodiumai-mcp` package you run.
- The client that runs the server (Claude Desktop, Claude Code, Cursor, VS Code or another) and its version.
- Your Node.js version (`node --version`) and your operating system and processor type.
- The tool that failed (`generate_image`, `generate_video`, `transcribe_audio`...) and what you asked the assistant.
- The exact error text, copied rather than retyped. The server never puts your key in an error message, but check before you paste.
- The output of the setup check:

```bash
RODIUMAI_API_KEY=rd_sk_... npx rodiumai-mcp --check
```

The check prints a result for the key, the wallet, the catalogue and the docs index, and never prints the key. Replace `rd_sk_...` with your own key on your machine only, and never paste the command with the key in an issue.

## First things to try

- Restart the client fully, not only the chat.
- Run the check above to see which step fails.
- On Windows, if the client cannot start `npx`, use `"command": "cmd"` with `"args": ["/c", "npx", "-y", "rodiumai-mcp"]`.
- If paid calls stop, you may have reached the spend limit of the session: raise `RODIUMAI_MCP_MAX_SPEND` and restart the server.

## Account and wallet questions

A balance, a payment or a rate limit on your account is a question for [RodiumAi support](https://www.rodiumai.io/dashboard/support), not for a public issue.

## Never post

API keys (`rd_sk_...`), the content of your client configuration if it holds a key, tokens, and private files or audio you sent to the server.
