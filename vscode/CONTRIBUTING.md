# Reporting a problem with the VS Code and Cursor extension

Read the [general guide](../CONTRIBUTING.md) first, then add these details to your [issue](../../../issues/new/choose). Choose **RodiumAi Code for VS Code and Cursor** as the product.

## What to include

- The editor, VS Code or Cursor, and its version (**Help**, then **About**).
- The version of the extension, shown in the Extensions view.
- Your operating system, its version and the processor type (Intel, Apple Silicon, ARM).
- Whether the project is local, or opened through Remote SSH, WSL or a container.
- What you did, step by step, and what you saw. A screenshot of the RodiumAi tab helps.
- The exact error message, copied rather than retyped.

## Get the logs

1. Run **RodiumAi: Show Logs** from the Command Palette. It opens the RodiumAi output channel.
2. Copy the lines around the time of the problem.
3. Remove secrets and personal data before you paste them.

## First things to try

- Run **RodiumAi: Restart Backend**, then try again.
- If the tab stays empty or shows an error, run **RodiumAi: Show Logs** to see why the backend did not start.
- If the preferred port is already used by another program, change `rodiumai.backendPort` and restart the backend.
- If the editor says the extension is not available for your platform, check the supported platforms in the [guide](README.md#install).
- If you are asked to sign in again, sign out and sign in again from the RodiumAi tab.

More in the [troubleshooting guide](https://www.rodiumai.io/docs/code/troubleshooting).

## Never post

API keys (`rd_sk_...`), tokens, passwords, and private code or data.
