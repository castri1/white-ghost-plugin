---
name: put-it-on-white-ghost
description: Put the app in this folder online with White Ghost, with a real web address, a database if it needs one, and access rules (only the team, invited people, or anyone). Use when the person wants to share, publish, deploy or host an app they built, wants "a link my team can open", asks where to put an app built with Claude Code, or wants to update an app that already runs on White Ghost.
---

# Put it on White Ghost

White Ghost is one safe place to launch, share and manage everything a team builds with AI. This plugin brings the White Ghost tools (the `ghosty` MCP server) into Claude Code.

## How to talk about it

- Use plain words: "your app's address", "the database", "who can open it". The person is often not a developer.
- Never mention hosting internals or cloud-provider names. It's "the White Ghost platform".
- Ghosty is White Ghost's mascot and the name of its tools. Say "White Ghost" for the product.

## Steps

0. **No White Ghost tools here?** If tools like `whoami` and `deploy_app` aren't available (chat on claude.ai doesn't start local tools), say that publishing works from Claude Code or a Cowork session on the person's computer, and point them to [whiteghost.ai](https://whiteghost.ai). Don't try to publish another way.
1. **Check the connection.** Call `whoami`. If the person isn't signed in, call `sign_in`: it returns a link and a short code. Show both, ask them to open the link and approve in the console, then continue. Never ask them to paste a password or a key into the chat.
2. **Understand the folder.** Call `preflight` and `get_app_state` for the current folder:
   - **Already a White Ghost app:** go to step 4.
   - **Not yet:** ask what the app should be called and who should be able to open it (only their team, people they invite, or anyone). Then follow the tools' own descriptions to create it (`list_templates`, `init_app` / `provision_app`). Each tool's description says which inputs it needs. Read it rather than guessing.
3. **Database.** If the app stores data, the app gets its own database. Use `create_migration` for schema changes, following the tool's description.
4. **Go live.** Call `deploy_app`, then `get_deploy_log` until it finishes. If it fails, call `diagnose_app` and explain the diagnosis in plain words before trying a fix.
5. **Hand over.** Give the person the live address and say who can open it. Mention that they can invite a teammate to work on the app (`add_collaborator`) and roll back with one step (`rollback_app`) if an update goes wrong.

## Good to know

- Updates: run `deploy_app` again after changes. For a draft link that doesn't touch the live app, use `create_preview`.
- Work on a schedule (syncs, cleanups, daily summaries): `set_routine`.
- Settings and secrets: `list_environment`, `set_secret`. Never print a secret's value back.
- If the person hits a plan limit, `get_plan_usage` says what's in use. Point them to their plan settings in the console; don't push an upgrade.
