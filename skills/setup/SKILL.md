---
name: sidecourt-setup
description: Connect this computer to the person's SideCourt account, or work out why the SideCourt tools are not answering. Use when they paste the SideCourt setup message ("Set up SideCourt for me…"), ask to connect, set up, sign in to, reconnect or disconnect SideCourt, say the SideCourt tools are missing or that a permission was denied, and right after this plugin is installed. Not for using the tools once they work — that is the sidecourt skill.
---

# Connecting SideCourt

The SideCourt connector talks to one person's own account on
[sidecourt.space](https://sidecourt.space). Signing in happens in **their browser**,
on SideCourt's own page. You never see or ask for a password or a sign-in code.

The person usually arrives with one message copied from SideCourt → Your Court → Your AI:

> Set up SideCourt for me. Reuse an existing connection when possible. I want to create
> and edit private drafts, add files I choose, and submit an exact version for review
> after I confirm it. Let me sign in and choose permissions in the browser, then verify
> the connection and help me get started.

Do exactly that, in this order.

## 1. Reuse what is already there

Call `sidecourt_list_works` before installing anything.

- **It answers with their posts** → the connection exists. Keep it. Go to step 4.
- **It answers `SCOPE_DENIED`** for something they asked for (create, edit, upload,
  submit) → the connection exists but was not given that action. Do **not** reconnect
  and do not add a second server. Tell them: SideCourt → Your Court → Your AI, find the
  connection's card, open **Add permissions**, tick the one you need, **Add**. The new
  action shows up the next time you list SideCourt tools.
- **The tools are absent, or it answers with an authorization error** → step 2.

## 2. Install or add the connector (only if the tools are absent)

Never add a second server with the same name; if `sidecourt` is already configured,
go straight to authenticating it.

**Claude Code** — the plugin route first, because it also carries these skills:

```
claude plugin marketplace add m1nga/sidecourt-plugin
claude plugin install sidecourt@sidecourt
```

Then they restart Claude Code, type `/mcp`, choose **sidecourt**, choose **Authenticate**.
If the plugin route is not available, add just the connector:

```
claude mcp add --transport http sidecourt https://mcp.sidecourt.space/mcp
```

**Codex:**

```
codex mcp add sidecourt --url https://mcp.sidecourt.space/mcp
codex mcp login sidecourt
```

Run the shell commands yourself when they ask you to; `/mcp` is theirs to type.

If the address they gave you contains `enoidjoytplapekhyxye`, it is SideCourt's
**review site**, which has separate accounts and is not connected to sidecourt.space.
Use the server name `sidecourt-review` and the address they gave you, do not install
the plugin for it, and never mix the two.

## 3. Sign in and choose permissions

A SideCourt page opens in their browser. They sign in and pick what the connection may
do: **Read** is the default; **Edit** to work on drafts; **Create** to start new drafts
("Create new drafts" — only on an "All my works" connection); **Upload** for small
files they choose; **Submit** to send a version they confirmed. Keeping it connected
means it stays until they disconnect it.

Never ask for, relay, or type a password or a sign-in code. If the sign-in page asks for
one, that is between the person and their browser.

## 4. Verify and report

Call `sidecourt_list_works` again and tell them, in four lines:

1. **Where**: the official site (sidecourt.space) or the review site.
2. **Who**: the account's `@handle` when the tools show it; otherwise "your account".
3. **Permissions**: which of Read, Edit, Create, Upload, Submit this connection has,
   and which of the ones they asked for are missing (with the Add permissions path).
4. **Next step**: an empty account → "tell me what you are making and I will save it as
   a new private draft"; an account with posts → name the most recent draft and offer to
   continue it or read what people replied.

## 5. What you never do

- Never scan, summarise or upload the current project, repository or any file the person
  did not explicitly hand over. Installing this plugin is not consent to write anything.
- Never publish, reply as them, or accept help for them. Those stay on the website.
- Never change their SideCourt account.

## When submitting needs a confirmation

`sidecourt_submit_review` needs a one-time `confirmation_id` the author makes in
**Your Court → Your AI → Authorize one review submission**. It covers one work at one
version. You cannot make one; ask for it and wait.

## Disconnecting

**Your Court → Your AI → Disconnect** on the connection's card, any time. Nothing they
posted is affected. A card that says "Waiting for your AI app to finish connecting" is a
half-finished connection: disconnect it and start again from step 2.

## What to say if they ask what it can do

It can list their posts, read and edit their private drafts (works and requests), create
a new work, request or work + request as a private draft, add small files they choose,
read replies and help offers, submit a version they confirmed, and read a public post by
link to help. It never publishes, never replies as them, never accepts help for them,
and never changes their account.
