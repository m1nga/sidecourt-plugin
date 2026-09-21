---
name: sidecourt-setup
description: Connect this computer to the person's SideCourt account, or work out why the SideCourt tools are not answering. Use when they ask to connect, set up, sign in to, reconnect or disconnect SideCourt, when they say the SideCourt tools are missing or say a permission was denied, and right after this plugin is installed. Not for using the tools once they work — that is the sidecourt skill.
---

# Connecting SideCourt

The SideCourt connector talks to one person's own account on
[sidecourt.space](https://sidecourt.space). Signing in happens in **their browser**,
on SideCourt's own page. You never see or ask for a password or a sign-in code.

## First, check whether it is already connected

Call `sidecourt_list_works`. If it returns their posts, it is connected — say so and get
on with what they actually asked for. Only if the tool is missing or answers with an
authorization error do you need anything below.

## Connect it

This plugin already declares the connector, so in Claude Code it is normally there after
an install and a restart. Tell them:

1. Restart Claude Code.
2. Type `/mcp`, choose **sidecourt**, choose **Authenticate**.
3. A SideCourt page opens in their browser. They sign in and pick what the connection
   may do. **Read** is the default; **Edit** is the one worth adding if they want you to
   work on drafts. Keeping it connected means it stays until they disconnect it.

If `/mcp` does not list sidecourt at all, add the connector directly:

```
claude mcp add --transport http sidecourt https://rwbwfokdipabwjparcwy.supabase.co/functions/v1/sidecourt-mcp/mcp
```

In Codex:

```
codex mcp add sidecourt --url https://rwbwfokdipabwjparcwy.supabase.co/functions/v1/sidecourt-mcp/mcp
codex mcp login sidecourt
```

Run the shell command yourself when they ask you to; `/mcp` is theirs to type.

## When a tool says a permission is missing

`SCOPE_DENIED` means the connection is real but was not given that action. They do not
need to reconnect. Tell them: **SideCourt → Your Court → Your AI**, find the connection's
card, open **Add permissions**, tick the one you need, **Add**. The new action shows up
the next time you list SideCourt tools.

The four permissions are **Read**, **Edit**, **Upload** and **Submit**.

## When submitting needs a confirmation

`sidecourt_submit_review` needs a one-time `confirmation_id` the author makes in
**Your Court → Your AI → Authorize one review submission**. It covers one work at one
version. You cannot make one; ask for it and wait.

## Disconnecting

**Your Court → Your AI → Disconnect** on the connection's card, any time. Nothing they
posted is affected.

## What to say if they ask what it can do

It can list their posts, read and edit private drafts, add small files they chose, read
public replies and offers of help, and submit a draft for review after they confirm that
version. It never publishes, never replies as them, never accepts help for them, and
never changes their account.
