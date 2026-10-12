# Reporting a problem with the desktop app

Read the [general guide](../CONTRIBUTING.md) first, then add these details to your [issue](../../../issues/new/choose). Choose **RodiumAi Code Desktop** as the product.

## What to include

- The version of the app.
- Your operating system, its version and the processor type (Intel, Apple Silicon, ARM).
- Whether the project is on your machine or on a remote machine over SSH.
- Whether you are signed in with a RodiumAi account or with an API key. Never post the key.
- What you did, step by step, and what you saw on screen. A screenshot or a short screen recording helps a lot. Hide your email address, project names and file contents first if they are private.
- The exact error message, copied rather than retyped.

## First things to try

- Quit the app completely and open it again.
- If a tool such as `gh` is not found, make sure it works in a new terminal, then restart the app. The app imports the `PATH` of your login shell at startup.
- If the pull request row does not appear, check that `gh auth status` reports that you are signed in, and that the repository has a GitHub.com `origin` remote.
- If the app asks you to sign in again, sign out and sign in again.

More in the [troubleshooting guide](https://www.rodiumai.io/docs/code/troubleshooting).

## Never post

API keys (`rd_sk_...`), tokens, SSH private keys and passwords, and private code or data.
