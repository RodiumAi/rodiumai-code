# RodiumAi Code for VS Code and Cursor

RodiumAi Code is a coding agent that plans, edits files and runs commands in your workspace, with your approval at every step. The extension brings RodiumAi into your editor: the same sessions and the same agent as RodiumAi Code Desktop and the `rodium` CLI, in a compact chat tab that works on the folder open in the editor and follows your editor theme.

Full guide: [rodiumai.io/docs/code/editor](https://www.rodiumai.io/docs/code/editor)

## Install

| Editor | Where to get it |
| --- | --- |
| VS Code | [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=rodiumai.rodiumai-code), or search **RodiumAi Code** in the Extensions view |
| Cursor | [Open VSX](https://open-vsx.org/extension/rodiumai/rodiumai-code). Cursor installs extensions from Open VSX: search **RodiumAi Code** in its Extensions view |

Requirements:

- VS Code 1.95 or later, or Cursor.
- A trusted workspace: RodiumAi can edit files and run commands, so it does not run in restricted mode.
- Windows (x64), macOS (Apple Silicon and Intel) or Linux (x64 and ARM64).
- A RodiumAi account, or a RodiumAi API key.

## Open RodiumAi

- Command Palette (`Ctrl+Shift+P` / `Cmd+Shift+P`), then **RodiumAi: Open in New Tab**
- `Ctrl+Alt+R` (`Cmd+Alt+R` on macOS)
- The RodiumAi button in the editor title bar, or **RodiumAi** in the status bar

RodiumAi opens as an editor tab: drag it to any editor group, split it beside your code (**RodiumAi: Open in Side Panel**), or open several tabs side by side. Open tabs are restored when the editor restarts.

## Sign in

- **RodiumAi account**: sign in with your RodiumAi account in the browser. Your FRODI balance is shown in the app. You can also type `/login`.
- **API key (BYOK)**: paste a RodiumAi API key (`rd_sk_...`).

Then pick the model you want to work with from the model selector, or type `/model`.

## Work with your code

- **RodiumAi: Add Selection to Chat** (`Ctrl+Alt+K` / `Cmd+Alt+K`, or the editor context menu) sends the selected lines, with the file path and the line range, to the chat.
- **RodiumAi: New Session** starts a fresh session.
- Files referenced by RodiumAi open in your editor, next to the RodiumAi tab.
- Type `@` in the chat to add a file to the context.

## Slash commands

Type `/` in the chat to open the command menu, then type a few letters to filter it. Built-in commands run in the interface and never send a message to the agent.

| Command | What it does |
| --- | --- |
| `/new` | Start a new session |
| `/clear` | Clear the conversation and start an empty session |
| `/resume` (alias `/history`) | Resume a session from this workspace |
| `/model` | Choose the model |
| `/provider` | Switch between RodiumAi Forge and RodiumAi BYOK |
| `/plan` | Plan mode: the agent proposes a plan before changing anything |
| `/act` | Act mode: the agent edits files and runs commands |
| `/status` | Show the provider, model, workspace and FRODI balance |
| `/account` | Show your account, FRODI and RODI usage and billing preference |
| `/login` | Sign in to your RodiumAi account |
| `/logout` | Sign out of your RodiumAi account |
| `/settings` | Open the settings |
| `/mcp` | Manage the MCP servers |
| `/skills` | Browse the installed skills |
| `/workspace` | Choose the editor folder new sessions open in (only when several folders are open) |
| `/voice` | Voice input settings (RodiumAi Code Desktop only: the editor shows a notice) |
| `/help` | List the available commands |

Two agent commands appear in the same menu: `/fork` creates a copy of the current session in a new session, and `/team` starts the task with an agent team. Your skills, workflows and plugin commands are listed below the built-in commands.

## VS Code commands

All commands are in the Command Palette, under the **RodiumAi** category.

| Command | Shortcut | What it does |
| --- | --- | --- |
| RodiumAi: Open in New Tab | `Ctrl+Alt+R` / `Cmd+Alt+R` | Open RodiumAi in a new editor tab |
| RodiumAi: Open in Side Panel | | Open RodiumAi in a new tab beside the active editor |
| RodiumAi: New Session | | Bring the RodiumAi tab forward (it opens one if needed) and start a new session |
| RodiumAi: Add Selection to Chat | `Ctrl+Alt+K` / `Cmd+Alt+K` | Send the selected lines to the chat with their file path and line range. Also in the editor context menu when text is selected |
| RodiumAi: Sign In | | Bring the RodiumAi tab forward, where you sign in |
| RodiumAi: Sign Out | | Bring the RodiumAi tab forward, where you sign out |
| RodiumAi: Show Logs | | Open the RodiumAi output channel with the backend logs |
| RodiumAi: Restart Backend | | Restart the local RodiumAi backend. Use it if something gets stuck |

## How it works

The extension starts a local RodiumAi backend on `127.0.0.1` (one per editor, shared by all of its windows) and shows the RodiumAi interface it serves inside the tab. Nothing is exposed outside your machine.

The **RodiumAi** item in the status bar shows the state of the backend (starting, ready or error). Click it to open RodiumAi.

## Setting

| Setting | Default | Description |
| --- | --- | --- |
| `rodiumai.backendPort` | `3137` | Preferred local port of the backend |

Changing it offers to restart the backend so that it takes effect.

## Report a problem

See [CONTRIBUTING.md](CONTRIBUTING.md) for what to include, then [open an issue](../../../issues/new/choose).
