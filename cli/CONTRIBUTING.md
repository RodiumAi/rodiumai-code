# Reporting a problem with the CLI

Read the [general guide](../CONTRIBUTING.md) first, then add these details to your [issue](../../../issues/new/choose). Choose **RodiumAi Code CLI** as the product.

## What to include

- The version: the output of `rodium version`.
- The output of `rodium status`, without your account name or email if you prefer not to share them.
- The output of `rodium doctor`.
- Your operating system, its version and the processor type (Intel, Apple Silicon, ARM).
- The terminal and the shell you use.
- The exact command you ran and the error text. For a one-shot run, say whether you used `--json`, `--yolo` or a pipe.
- The time of the problem, so that we can match it to the log.

## Get a more detailed log

Run the command again with a debug log level, then paste the relevant lines:

```bash
RODIUMAI_LOG_LEVEL=debug rodium
```

`rodium doctor log` opens the log file. Check it for secrets before you paste anything.

## First things to try

- `rodium update`, then try again.
- `rodium doctor`, then `rodium doctor fix` if the agent seems stuck.
- `rodium logout`, then `rodium login`, if the app keeps asking you to sign in.
- If `rodium` is not found after install, check that the folder of your global packages is in your `PATH`.

More in the [troubleshooting guide](https://www.rodiumai.io/docs/code/troubleshooting).

## Never post

API keys (`rd_sk_...`), tokens, the content of `~/.rodiumai` credentials, and private code or data.
