---
name: sidecourt-setup
description: Connect this computer to the person's SideCourt account, or work out why the SideCourt tools are not answering. Use when they paste the SideCourt setup message ("Connect SideCourt for me…" or "Set up SideCourt for me…"), ask to connect, set up, sign in to, reconnect or disconnect SideCourt, say the SideCourt tools are missing or that a permission was denied, and right after this plugin is installed. Not for using the tools once they work — that is the sidecourt skill.
---

# Connecting SideCourt

The SideCourt connector talks to one person's own account on
[sidecourt.space](https://sidecourt.space). Signing in happens in **their browser**,
on SideCourt's own page. You never see or ask for a password or a sign-in code.

The person usually arrives with one message copied from SideCourt → Your Court → Your AI
(it starts "Connect SideCourt for me"). It asks you to reuse an existing connection,
install only what is missing, let them sign in and choose permissions in the browser,
then check the connection with `sidecourt_list_works` — without creating, editing,
uploading, asking to publish, suggesting a change or making a version during setup.

Do exactly that, in this order.

## 1. Reuse what is already there

Call `sidecourt_list_works` before installing anything.

- **The list succeeds, including an empty list** → Read works for this connection. Keep it and go to step 4.
- **It answers `SCOPE_DENIED`** for something they asked for (create, edit, upload,
  ask to publish, suggest changes, make your version) → the connection exists but was
  not given that action. Do **not** reconnect
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

If the address they gave you contains `mcp-review` or `enoidjoytplapekhyxye`, it is SideCourt's
**review site**, which has separate accounts and is not connected to sidecourt.space.
Use the server name `sidecourt-review` and the address they gave you, do not install
the plugin for it, and never mix the two.

## 3. Sign in and choose permissions

A SideCourt page opens in their browser. They sign in and pick what the connection may
do: **Read** is the default; **Edit** to work on drafts; **Create** to start new drafts
("Create new drafts" — only on an "All my works" connection); **Upload** for small
files they choose; **Ask to publish** ("Ask me to publish a version") so you can ask
them to publish an exact version — nothing goes public until they click Publish on
SideCourt. Two more act toward other people's public works, each ticked on its own and
only on an "All my works" connection: **Suggest changes** ("Suggest changes to other
people’s works (they decide)") sends a change they agreed to, privately, to that work's
author, and **Make your version** ("Make your own version of works that allow it")
starts their own private draft from a public work whose author allows it. A connection
approved before these two existed never gets them by itself. Keeping it connected means
it stays until they disconnect it.

Never ask for, relay, or type a password or a sign-in code. If the sign-in page asks for
one, that is between the person and their browser.

## 4. Verify and report

Call `sidecourt_list_works` again and tell them, in four lines:

1. **Where**: the official site (sidecourt.space) or the review site.
2. **Who**: the account's `@handle` when the tools show it; otherwise "your account".
3. **Permissions**: which of Read, Edit, Create, Upload, Ask to publish (earlier
   versions called it Submit), Suggest changes and Make your version this connection has,
   and which of the ones they asked for are missing (with the Add permissions path).
4. **Next step**: if the list is empty, say that this connection has no accessible
   Works. Offer to read a public Work or explain how to start a private draft. Offer to
   create a draft only if Create is available. If the list contains a draft, offer to
   read it. If it contains published Works, offer to read the replies on one of them.

## 5. What you never do

- Never scan, summarise or upload the current project, repository or any file the person
  did not explicitly hand over. Installing this plugin is not consent to write anything.
- Never publish, reply as them, or accept help or suggestions for them. Those stay on
  the website.
- Never change their SideCourt account.

## Publishing

SideCourt is publish-first: the author's Publish click on the website makes a Work public
right away, with no review queue. `sidecourt_submit_review` only asks them to publish an
exact version; it needs no confirmation code. Publishing itself is always theirs.

## Disconnecting

**Your Court → Your AI → Disconnect** on the connection's card, any time. Nothing they
posted is affected. A card that says "Waiting for your AI app to finish connecting" is a
half-finished connection: disconnect it and start again from step 2.

## What to say if they ask what it can do

It can list their posts, read and edit private Work drafts, create a Work with an
optional Need, add small files they choose, read replies and help offers, ask them to
publish an exact version, and find public Works by name or read them by link or
SideCourt ID to help. If they allow it, it can also suggest changes to other people's
works (the author decides) and make their own version of works that allow it. It never
publishes, never replies as them, never accepts help or suggestions for them, and never
changes their account.
