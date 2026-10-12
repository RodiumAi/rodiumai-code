# RodiumAi Code Desktop

RodiumAi Code as a native app for macOS, Windows and Linux. No editor required: open a project, chat with the agent and review its work in one window.

> **Status: not public yet.** Downloads for macOS, Windows and Linux will appear in the [documentation](https://www.rodiumai.io/docs/code/desktop) at launch. [Join the waitlist](https://www.rodiumai.io/code) to hear the day it opens.

Once installed, the app is named **RodiumAi** in your applications list and in its window title. It runs the same agent as the [CLI](../cli) and the [VS Code and Cursor extension](../vscode): same plan and act modes, checkpoints, MCP servers, skills and rules.

Full guide: [rodiumai.io/docs/code/desktop](https://www.rodiumai.io/docs/code/desktop)

## Sign in

Choose how to connect on the first screen: with your **RodiumAi account** (a browser window opens, and your FRODI balance is shown in the app) or with a RodiumAi **API key** (`rd_sk_...`). Then pick a model from the model selector. See [RODI and FRODI credits](https://www.rodiumai.io/docs/code/credits) for the difference.

## Work on a project

- Pick a folder with the workspace selector, or **Add project** to open a new one. Recent workspaces are remembered.
- Chat with the agent. Use `@` to add a file to the context and `/` for commands such as `/model`, `/plan`, `/act`, `/status`, `/settings`, `/mcp` and `/skills`.
- Switch between **plan** mode (the agent explores and proposes) and **act** mode (it edits and runs commands, with your approval).
- Open **Settings** to manage MCP servers, skills and rules.

## Pull requests and CI

The composer shows the pull request of the current branch, its merge status, the number of changed lines and its CI checks. Click the PR number to open it in your browser, or expand CI to inspect each check and its logs. The status refreshes every 30 seconds while visible and when the app regains focus.

- It needs the GitHub CLI (`gh`) installed and signed in (`gh auth login`), and a GitHub.com `origin` remote.
- The row is hidden on the default branch, on a detached HEAD and on unsupported repositories.
- If the branch has no pull request yet, **Create PR** opens GitHub's comparison form. Push your commits first: the app does not push or submit anything itself.

## Remote machines over SSH

Work on a project that lives on another machine without leaving the app.

1. Open **Settings**, then **Remote**, and add an SSH host. You can test it before using it. Saving or testing a host does not activate it.
2. From the welcome chat, open the environment selector beside the workspace picker and choose the saved host. The SSH connection starts at the remote user's home directory.
3. Use **Add project** in the workspace selector to browse that machine and pick a project.
4. Choose **Local** in the environment selector to disconnect.

SSH config aliases are supported: leave **Port** blank to use the one defined by the alias. Recent and last-used workspaces are remembered separately for each SSH host and for your local machine.

## Good to know

Apps launched from the Dock or Finder get a minimal `PATH`. At startup RodiumAi asks your login shell for its `PATH`, so tools such as `gh` found in a terminal are found by the agent too.

## Report a problem

See [CONTRIBUTING.md](CONTRIBUTING.md) for what to include, then [open an issue](../../../issues/new/choose).
