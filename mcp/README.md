# RodiumAi MCP server

The RodiumAi API, inside your AI assistant. Generate images and videos, speak and transcribe, embed and chat with any model, and read the docs, from Claude, Cursor or VS Code, with nothing but your API key.

The server is the npm package [`rodiumai-mcp`](https://www.npmjs.com/package/rodiumai-mcp). It runs on your computer over stdio, uses your own RodiumAi key, and saves what it generates on your computer. It needs Node.js 22 or newer.

Full guide: [rodiumai.io/docs/guides/mcp](https://www.rodiumai.io/docs/guides/mcp)

## Quick start

1. **Get a key.** Create an `rd_sk_` API key in your [RodiumAi dashboard](https://www.rodiumai.io/dashboard) and keep some RODI in the wallet.
2. **Add the server** to your client. Example for Claude Desktop, in `claude_desktop_config.json`:

   ```json
   {
     "mcpServers": {
       "rodiumai": {
         "command": "npx",
         "args": ["-y", "rodiumai-mcp"],
         "env": { "RODIUMAI_API_KEY": "rd_sk_..." }
       }
     }
   }
   ```

3. **Restart the client and ask.** For example: *"Generate an image of a red fox in the snow with Nano Banana Pro."*

For Claude Code:

```bash
claude mcp add rodiumai --env RODIUMAI_API_KEY=rd_sk_... -- npx -y rodiumai-mcp
```

For Cursor, add the same entry as above to `.cursor/mcp.json` (this project) or `~/.cursor/mcp.json` (all projects). For VS Code, use `.vscode/mcp.json` with an input prompt so that the key never sits in a file: the [guide](https://www.rodiumai.io/docs/guides/mcp) has the exact entry.

On Windows, if the client cannot start `npx` directly, use `"command": "cmd"` with `"args": ["/c", "npx", "-y", "rodiumai-mcp"]`.

Check the setup at any time, without spending anything:

```bash
RODIUMAI_API_KEY=rd_sk_... npx rodiumai-mcp --check
```

It tests the key, reads the wallet, loads the catalogue and the docs index, and never prints the key.

## Tools

| Tool | What it does | Costs RODI |
| --- | --- | :---: |
| `generate_image` | Create or edit images. Images are shown and saved to disk | yes |
| `generate_video` | Start a video from text or from an image. It runs in the background and is saved to disk. Billed per second, so the assistant asks you first | yes |
| `get_video` | Check a video in progress, or list this session's videos | no |
| `text_to_speech` | Turn text into an audio file | yes |
| `transcribe_audio` | Transcribe a local audio file (mp3, mp4, m4a, wav, webm, ogg, flac, up to about 10 MiB) | yes |
| `embed_text` | Create embedding vectors, saved to a JSON file | yes |
| `ask_model` | Send a prompt to any text model, or let RodiumAi route it by priority | yes |
| `list_models` | The catalogue with prices, tiers and rate limits, filtered by task or provider | no |
| `recommend_model` | Which model the server would use for a task, and why | no |
| `get_wallet` | Your spendable RODI balance and what this session has spent | no |
| `search_docs` | Search the RodiumAi documentation | no |
| `read_doc` | Read a docs page as markdown | no |

You do not need to know model ids. Name a model if you care, or say what matters (`cheapest`, `best`) and the server chooses. Every result says which model was used.

## Cost and safety

- Every paid call reports about how much RODI it used, plus the session total.
- **Spend limit.** The default is 1000 RODI per session, and new paid calls stop once it is reached. Raise it with `RODIUMAI_MCP_MAX_SPEND`, or set it to `off`.
- **Ask first for video.** The price per second is on each model's page, so the assistant asks you before it starts a video.
- **Your key stays put.** It lives in the server's environment and is never put in tool results or error messages.
- **Only audio and images are read from disk**, checked and size limited.
- **Untrusted text stays data.** Text from other models, transcripts and documents is treated as data, not as instructions.

What leaves your machine: prompts, text to speak, audio and reference images are sent to the RodiumAi API, and from there to the provider of the model you chose. There is no telemetry.

## Configuration

| Variable | Default | Meaning |
| --- | --- | --- |
| `RODIUMAI_API_KEY` | none | Your `rd_sk_` key. Without it the docs and model listing still work, generation does not |
| `RODIUMAI_MCP_MAX_SPEND` | `1000` | Spend limit per server session, in RODI. `off` removes it |
| `RODIUMAI_MCP_OUTPUT_DIR` | `~/RodiumAi/generated` | Where images, audio, video and embeddings are saved |

## Troubleshooting

| Symptom | What to do |
| --- | --- |
| The tools do not show up | Restart the client fully. Run `npx rodiumai-mcp --check` in a terminal to see what is wrong |
| `RODIUMAI_API_KEY is not set` | Add the key to the `env` block of the server configuration, then restart the client |
| `401` or "API key was rejected" | The key is revoked or mistyped. Create a new `rd_sk_` key in the dashboard |
| "The wallet does not hold enough RODI" | Top up from the [dashboard](https://www.rodiumai.io/dashboard) |
| `Spend ceiling reached` | The session hit its limit. Raise `RODIUMAI_MCP_MAX_SPEND` and restart the server |
| `429` or rate limit | The model's per-key limit was reached. Wait a moment or choose another model. Video models are the strictest |

## Report a problem

See [CONTRIBUTING.md](CONTRIBUTING.md) for what to include, then [open an issue](../../../issues/new/choose).
