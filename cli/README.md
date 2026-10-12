# RodiumAi Code CLI

RodiumAi Code in your terminal. Type `rodium`: the agent reads your code, edits files, runs commands and works through a task with you, interactively or as a one-shot command you can script.

> **Status: not public yet.** The install command will be published in the [documentation](https://www.rodiumai.io/docs/code/cli) at launch. [Join the waitlist](https://www.rodiumai.io/code) to hear the day it opens.

- Native binaries for macOS, Linux and Windows, on `x64` and `arm64`.
- The command is `rodium`. `rodiumai` is installed as an alias, so existing scripts keep working.
- `rodium update` updates it, and a quiet check also runs at startup.

Full guide: [rodiumai.io/docs/code/cli](https://www.rodiumai.io/docs/code/cli)

## Sign in

| Connection | How it works | Billing |
| --- | --- | --- |
| **RodiumAi account** | Browser sign-in. The CLI waits for the browser to call back on a local port. | The weekly **FRODI** allowance of your plan |
| **RodiumAi API key** | An `rd_sk_...` key from your dashboard, checked before it is saved. | The balance of the key, in RODI |

```bash
rodium login                      # choose: RodiumAi account or API key
rodium login --with-account       # browser sign-in
rodium login --with-account --no-browser   # print the URL instead of opening it
rodium login --api-key rd_sk_...  # non-interactive, e.g. in CI
rodium logout                     # remove the saved credentials
rodium status                     # connection, account, FRODI left, default model
```

For scripts, skip `login` and pass a key through the environment (`RODIUMAI_API_KEY`), or for a single run with `--key`.

## Interactive mode

```bash
cd my-project
rodium                        # interactive session in the current directory
rodium -i "first message"     # start and send a first prompt
rodium --id <session-id>      # resume a saved session
rodium --worktree             # work in a fresh detached git worktree
rodium --plan                 # start in plan mode (read-only)
```

| Key or command | What it does |
| --- | --- |
| `Tab` | Switch between plan mode (read-only) and act mode |
| `Shift+Tab` | Turn tool auto-approval on or off |
| `@path` | Mention a file in your prompt |
| `Esc` | Close a menu or stop the running agent |
| `Esc Esc` | Restore a previous checkpoint |
| `Ctrl+P` | Open the command palette |
| `/model` | Pick a model (and switch connection) |
| `/account`, `/status` | Account, plan and weekly FRODI allowance |
| `/login`, `/logout` | Sign in or out |
| `/settings` | General, MCP servers, skills, rules and tools |
| `/history`, `/fork`, `/undo`, `/compact`, `/clear` | Manage the session |
| `/team <task>` | Run the task with a team of agents |
| `/help` | All shortcuts and commands |

## One-shot runs and pipes

```bash
rodium "explain this repository"
git diff origin/main | rodium "review these changes for bugs"
cat error.log | rodium "find the root cause"
rodium --json "list the TODO comments" | jq -c 'select(.type == "run_result")'
rodium --yolo -t 900 "run the tests and fix the failures"
```

- The prompt must be a single quoted argument.
- `--json` streams NDJSON events and needs a prompt or piped input.
- `--yolo` approves every tool call and exits when the task completes.
- `-t, --timeout <seconds>` stops the run after a deadline.
- The exit code is `0` on success and `1` on failure, so it fits CI.

## Tools and approvals

Tool calls are approved automatically by default. Turn that off to review each call: every call that reads files, fetches the web, edits or runs commands then asks first. Plan mode explores and proposes changes without editing files.

```bash
rodium --auto-approve false   # ask before every tool call
rodium --plan                 # explore and propose, never edit
```

## Models

```bash
rodium -m <model-id> "write a unit test for utils.ts"
rodium --thinking high "find why the build is slow"   # none | low | medium | high | xhigh
```

## MCP servers and skills

```bash
rodium mcp                                   # interactive manager
rodium mcp install fs -- npx -y @modelcontextprotocol/server-filesystem /tmp
rodium mcp install docs --transport http https://example.com/mcp
rodium mcp uninstall fs
rodium config mcp                            # list the configured servers
```

`mcp install` opens the add wizard with the fields prefilled (pass `--yes` to skip it). Skills are added with `rodium skill add <owner/repo>` and listed with `rodium skill list`. Skills and workflows also appear as slash commands in a session: type `/skills` to browse them.

## Sessions and history

- `rodium history` opens a picker to resume a session (`--json` for scripts).
- `rodium history export <id>` and `rodium history delete <id>` export or remove one.
- `rodium --id <session-id>` resumes a saved session directly.

## Schedules

Run the agent on a schedule. Without `--provider` and `--model`, a schedule uses your current connection and model.

```bash
rodium schedule create "Daily review" \
  --cron "0 9 * * MON-FRI" \
  --prompt "Review yesterday's commits and summarize the risks." \
  --workspace /path/to/repo
rodium schedule list
rodium schedule trigger <schedule-id>
rodium schedule history <schedule-id>
```

Running `rodium schedule` in a terminal opens an interactive wizard.

## Use it from another editor (ACP)

`rodium --acp` runs RodiumAi as an [Agent Client Protocol](https://agentclientprotocol.com) agent over stdio, for editors that support ACP:

```json
{
  "agent_servers": {
    "RodiumAi": { "command": "rodium", "args": ["--acp"] }
  }
}
```

The editor signs in with your RodiumAi account. Credentials saved by `rodium login` and `RODIUMAI_API_KEY` are picked up automatically.

## Configuration

Settings, sessions and credentials live in `~/.rodiumai`. Use `--config <dir>` to point at another configuration directory, or `--data-dir <dir>` for isolated local state. `rodium config` prints the current configuration (`--json` for scripts).

| Variable | Purpose |
| --- | --- |
| `RODIUMAI_API_KEY` | API key (`rd_sk_...`) for the API key connection |
| `RODIUMAI_NO_AUTO_UPDATE` | `1` disables the background update check |
| `RODIUMAI_LOG_LEVEL` | `trace`, `debug`, `info` (default), `warn`, `error` or `silent` |
| `RODIUMAI_LOG_PATH` | Log file path |

## Updates and diagnostics

```bash
rodium update        # update now (a quiet check also runs at startup)
rodium version
rodium doctor        # inspect local processes and the background hub
rodium doctor fix    # stop stale RodiumAi processes
rodium doctor log    # open the log file
```

The CLI trusts your operating system's certificate store, so it works behind TLS-inspecting proxies.

## Report a problem

See [CONTRIBUTING.md](CONTRIBUTING.md) for what to include, then [open an issue](../../../issues/new/choose).
