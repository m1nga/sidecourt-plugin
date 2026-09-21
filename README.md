<img src="assets/mark-ring.svg" alt="" width="72" height="72">

# SideCourt for Claude Code and Codex

[SideCourt](https://sidecourt.space) is where you post something you made, or ask for a
hand with something you are making.

This plugin lets the AI you already work in do that with you: save a work or a request
straight from what you just built, keep the draft up to date, read the replies and the
offers of help, and submit for review when you say so.

**It never publishes, never replies as you, never accepts help for you, and never
touches your account.** Those stay yours, on the website.

## Install

In Claude Code:

```
/plugin marketplace add m1nga/sidecourt-plugin
/plugin install sidecourt@sidecourt
```

Then `/mcp` → **sidecourt** → **Authenticate**. You sign in on sidecourt.space and pick
what the connection may do; keep the defaults if you are not sure.

Try it: **"list my SideCourt posts"**.

### Without the plugin

The connector on its own works anywhere that speaks MCP:

```
claude mcp add --transport http sidecourt https://rwbwfokdipabwjparcwy.supabase.co/functions/v1/sidecourt-mcp/mcp
```

Codex:

```
codex mcp add sidecourt --url https://rwbwfokdipabwjparcwy.supabase.co/functions/v1/sidecourt-mcp/mcp
codex mcp login sidecourt
```

ChatGPT and Claude on the web or desktop: paste that same address as a custom connector.

The plugin adds the connector *and* a skill that teaches your AI when to reach for it and
how SideCourt drafts actually work, so you get better results than the bare connector.

## What it can do

| Tool | Permission | What it does |
|---|---|---|
| `sidecourt_list_works` | Read | Every post on your account, drafts and published |
| `sidecourt_status` | Read | One draft's text, version and edit token |
| `sidecourt_replies` | Read | Public replies on your posts, and your own updates |
| `sidecourt_help_offers` | Read | Who offered to help, and where it stands |
| `sidecourt_save_draft` | Edit | Change the text of a private draft |
| `sidecourt_upload_file` | Upload | Add a small file you explicitly chose |
| `sidecourt_submit_review` | Submit | Send one version you confirmed on the site |

You choose which of these a connection gets, the first time it asks. You can add a
permission later, or disconnect it, in **SideCourt → Your Court → Your AI**. Read is the
only default.

## What stays yours

- Publishing, replying, and accepting help are done by you, on the website.
- Private drafts and uploaded files stay private until a person reviews them.
- Other people's private messages are never included.
- Your login email never appears on your profile.

[Privacy](https://sidecourt.space/privacy) · [Terms](https://sidecourt.space/terms)

## Licence

MIT for this plugin's files. Works posted on SideCourt stay their authors'.
