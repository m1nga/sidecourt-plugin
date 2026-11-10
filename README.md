<img src="assets/mark-ring.svg" alt="" width="72" height="72">

# SideCourt for Claude Code and Codex

[SideCourt](https://sidecourt.space) is where you share what you are making.
Every post is a **Work**, with an optional **Need** for a specific way someone can help.

This plugin lets the AI you already work in do that with you. It can list your posts,
read and edit your private Work drafts, create a Work with an optional Need, add small
files you choose, read replies and help offers, ask you to publish an exact version, and
find or read public Works to help. If you allow it, it can also suggest changes to other
people's works (they decide) and make your own version of works that allow it.

**It never publishes, never replies as you, never accepts help or suggestions for you,
and never changes your account.** Those stay yours, on the website.

## Try one read

- **A public Work someone sent you.** Ask “Read this SideCourt Work and tell me what kind of help its author is asking for,” and include its link. Public Works are readable without signing into a SideCourt account. The assistant reports the author's Need separately from its own suggestions. [Browse public Works](https://sidecourt.space/drops/).
- **Your own drafts.** After connecting, ask “List my SideCourt Works.” The default Read permission is enough. Seeing no accessible Works on a successful call is a valid first result.

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
| `sidecourt_list_works` | Read | Posts this connection can access, drafts and published |
| `sidecourt_status` | Read | One draft's text, version and edit token |
| `sidecourt_replies` | Read | Public replies on your posts, and your own updates |
| `sidecourt_help_offers` | Read | Who offered to help, and where it stands |
| `sidecourt_save_draft` | Edit | Change the text of a private draft |
| `sidecourt_upload_file` | Upload | Add a small file you explicitly chose |
| `sidecourt_create_draft` | Create | Start a private Work draft with an optional Need, and where it stands (Idea, Prototype, In progress, Ready to try) |
| `sidecourt_submit_review` | Ask to publish | Ask you to publish one exact version; nothing is public until you click Publish |
| `sidecourt_suggest_change` | Suggest changes | Send your own suggested text change to another author's public Work, privately; they decide. Update, withdraw or list the ones you sent |
| `sidecourt_make_version` | Make your version | Start your own private version of a public Work whose author allows it, after you agree to their terms |
| `sidecourt_search_public_posts` | none — no sign-in | Find published Works by title; choose when names match |
| `sidecourt_get_public_post` | none — no sign-in | Read one public Work by link or SideCourt ID, public fields only |

You choose which of these a connection gets, the first time it asks. You can add a
permission later, or disconnect it, in **SideCourt → Your Court → Your AI**. Read is the
only default. Create, Suggest changes and Make your version can only be given to an "All
my works" connection. Suggest changes and Make your version are new in this version: a
connection you approved before never gets them by itself — tick them when you reconnect,
or add them in Your AI. Ask to publish is the permission earlier versions called Submit;
the tool keeps its original name so existing connections keep working.

## Publishing stays yours

SideCourt is publish-first: when you click **Publish** on the website, your Work is
public right away. There is no review queue; SideCourt checks public posts automatically
and may take down anything that breaks the rules. Your AI never presses that button. When
a version is ready it can *ask* you: the request waits on the Work's Publish & manage page,
and nothing changes until you publish there. If you edit the draft first, you simply
publish the newer version.

## Works and optional Needs

A new Work needs a title and description. If there is nothing to try yet (no link,
repository, image or file), say where it stands — Idea, Prototype or In progress — so it
can be published. Add a Need only when there is something specific you want help with. Its action can be Test this, Break this, Help me name it,
Tell me what doesn’t make sense, Find me a reference, Look into this, Introduce me to
someone, or Build this part with me.

Each Work has a permanent SideCourt ID. It stays the same across edits and published
versions; it never grants access to a private draft. Existing UUID links still work.

## Helping someone

Give your AI a Work’s name, permanent SideCourt ID, or public link — or use **Copy for
AI** on its share card — and ask how you could help. If several names match, choose
the right Work before continuing. Your AI reads the public post (no sign-in needed), separates
what the author actually asked from what people already replied, and suggests concrete
things you could bring. If you want to keep the plan, say so: it is saved as your own
private draft, linked to the original post. Replying and offering a hand stay on the
website, by you.

## Suggesting a change, or making your own version

With **Suggest changes**, your AI can send a text change you agreed to — a clearer
title, description or Need — to the author of someone else's public Work that takes
suggestions. The server first returns the exact wording without sending; your AI shows
it to you and confirms that same preview only after you agree. The author accepts, asks for changes
or declines it on SideCourt; nothing on their Work changes unless they accept and
publish, and the suggestion stays between the two of you. Follow yours in Your Court →
Suggestions.

With **Make your version**, your AI can start your own private draft from a public Work
whose author allows it. It shows you the author's terms word for word and goes ahead
only when you agree. Files, replies, the Need, links and access are not copied; the
original stays theirs, and nothing is public until you publish your version.

## What stays yours

- Publishing, replying, accepting help and deciding on suggestions are done by you,
  on the website.
- Private drafts and uploaded files stay private until you publish the Work.
- Other people's private messages are never included.
- Your login email never appears on your profile.

[Privacy](https://sidecourt.space/privacy) · [Terms](https://sidecourt.space/terms)

## Licence

MIT for this plugin's files. Works posted on SideCourt stay their authors'.

The branded endpoint uses the same SideCourt service with OAuth sign-in. Existing Supabase-address connections remain valid. When both the plugin and a Claude account connector use this same URL, supported Claude Code versions use one effective MCP connection. Updating from an older endpoint may require signing in once again.
