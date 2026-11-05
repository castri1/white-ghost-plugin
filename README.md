# White Ghost for Claude Code

Put the apps you build with Claude online for your team. Each app gets a real web address, a database if it needs one, and you decide who gets in: only your workspace, the people you invite, or anyone with the link. White Ghost is one safe place to launch, share and manage everything your team builds with AI.

## Install

Inside Claude Code:

```
/plugin install white-ghost --marketplace castri1/white-ghost-plugin
```

Or from your shell:

```
claude plugin marketplace add castri1/white-ghost-plugin
claude plugin install white-ghost@white-ghost
```

Then, in the folder of the app you built, ask Claude:

> Put this on White Ghost for my team, members only.

The first time, Claude shows you a link and a short code. Open the link, approve, and Claude carries on. A free account is enough to start: [whiteghost.ai](https://whiteghost.ai).

## What's inside

- **One skill, `put-it-on-white-ghost`.** It walks Claude through publishing an app, updating it, draft links that don't touch the live app, rollbacks, scheduled work and inviting teammates.
- **The White Ghost tools**, as an MCP server named `ghosty` (Ghosty is White Ghost's mascot).

## Requirements

- Node.js 20 or later.
- Works in Claude Code, and in Cowork sessions that run on your computer. Chat on claude.ai doesn't start local tools, so the skill loads there but can't publish.

## What this plugin runs and sends

- **Runs** `npx -y ghosty-cli@0.46.2 mcp`: the White Ghost command-line tool, downloaded from the public npm registry at that exact version.
- **Connects to** `console.whiteghost.ai` and your own workspace on White Ghost. Once a day it also asks the npm registry whether a newer version exists (set `GHOSTY_NO_UPDATE_CHECK=1` to turn that off).
- **Sends, only when you ask Claude to publish or update an app:** the app's code from the current folder. Files your `.gitignore` excludes stay on your computer, and so do `.env` files, always. If the app's code lives in your own GitHub repository, publishing pushes there with your own git.
- **Sends, only when you ask:** the settings and secrets you tell Claude to set for an app.
- **Stores on your computer:** your sign-in, in `~/.ghosty/`. Delete that folder to sign out.
- **No analytics or tracking** in the plugin or the command-line tool.

## Privacy, terms and support

- Privacy: [whiteghost.ai/privacy](https://whiteghost.ai/privacy)
- Terms: [whiteghost.ai/terms](https://whiteghost.ai/terms)
- Docs: [whiteghost.ai/docs](https://whiteghost.ai/docs)
- Help: hello@whiteghost.ai

## License

The files in this repository are MIT licensed. The White Ghost service has its own [terms](https://whiteghost.ai/terms).
