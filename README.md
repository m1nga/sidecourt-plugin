<img src="assets/mark-ring.svg" alt="" width="72" height="72">

# SideCourt for Claude Code and Codex

[SideCourt](https://sidecourt.space) is where you post something you made, or ask for a
hand with something you are making.

This plugin lets the AI you already work in do that with you. It can list your posts,
read and edit your private drafts (works and requests), create a new work, request or
work + request as a private draft, add small files you choose, read replies and help
offers, submit a version you confirmed, and read a public post by link to help.

**It never publishes, never replies as you, never accepts help for you, and never
changes your account.** Those stay yours, on the website.

## Install

In Claude Code:

```
/plugin marketplace add m1nga/sidecourt-plugin
/plugin install sidecourt@sidecourt
```

Then `/mcp` → **sidecourt** → **Authenticate**. You sign in on sidecourt.space and pick
what the connection may do; keep the defaults if you are not sure.

Or paste the one message from **SideCourt → Your Court → Your AI** into Claude Code or
Codex: it reuses a connection you already have, installs only what is missing, lets you
sign in and choose permissions in the browser, then checks the connection with you.

Try it: **"list my SideCourt posts"**.

### Without the plugin

The connector on its own works anywhere that speaks MCP:

```
claude mcp add --transport http sidecourt https://mcp.sidecourt.space/mcp
```

Codex:

```
codex mcp add sidecourt --url https://mcp.sidecourt.space/mcp
codex mcp login sidecourt
```

Codex gets the connector this way, not the plugin skills; the same setup message works
there because it spells out the commands. Never add a second server with the same name —
if `sidecourt` is already configured, just sign in to it again.

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
| `sidecourt_create_draft` | Create | Start a new work, request or work + request as a private draft |
| `sidecourt_submit_review` | Submit | Send one version you confirmed on the site |
| `sidecourt_get_public_post` | none — no sign-in | Read one public post by its link, public fields only |

You choose which of these a connection gets, the first time it asks. You can add a
permission later, or disconnect it, in **SideCourt → Your Court → Your AI**. Read is the
only default. Create can only be given to an "All my works" connection.

## Helping someone

Paste a public SideCourt post's link — or use **Copy for AI** on its share card — and
ask how you could help. Your AI reads the public post (no sign-in needed), separates
what the author actually asked from what people already replied, and suggests concrete
things you could bring. If you want to keep the plan, say so: it is saved as your own
private draft, linked to the original post. Replying and offering a hand stay on the
website, by you.

## What stays yours

- Publishing, replying, and accepting help are done by you, on the website.
- Private drafts and uploaded files stay private until a person reviews them.
- Other people's private messages are never included.
- Your login email never appears on your profile.

[Privacy](https://sidecourt.space/privacy) · [Terms](https://sidecourt.space/terms)

## Licence

MIT for this plugin's files. Works posted on SideCourt stay their authors'.

The branded endpoint uses the same Sidecourt service with OAuth sign-in. Existing Supabase-address connections remain valid. When both the plugin and a Claude account connector use this same URL, supported Claude Code versions use one effective MCP connection. Updating from an older endpoint may require signing in once again.
