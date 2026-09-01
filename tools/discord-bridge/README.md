# discord-bridge

Scripts bridging cc-sync and Discord `#labchan` for the AI Lab LabChan
messaging pipeline.

## Tracked here

- `Listen-DiscordRX.py`
- `Message-Router.py`
- `Post-CCSyncToDiscord.ps1`
- `Post-CloudTXToDiscord.ps1`
- `Start-DiscordListener.bat`

## Never tracked

- `bot-token.secret.txt`
- `webhook-url.secret.txt`

This repo is public. These two files must live **outside this git working
tree entirely** -- not just `.gitignore`'d alongside the tracked files. A
`.gitignore` entry only prevents *accidental* staging; it does not protect a
file that's already been committed, and it does not block a forced add
(`git add -f`). If either secret is ever committed, treat it as compromised
(rotate it) rather than trying to scrub history.

**Known risk to resolve before the first real commit:** these two secret
files have previously been placed directly inside
`C:\Users\Tony B\AI-Lab-Tools\discord-bridge\` -- the same folder this
working tree maps to. Confirm they've been moved to a sibling location
(outside this tree) before running `git add` here, not just excluded by the
patterns above.

## Excluded as runtime state, not source

- `discord-inbox.jsonl`
- `.discord-posted.txt`
- `.cloud-tx-posted.txt`
- `__pycache__/`

## Status

Superseded as of 2026-09-01. This scaffolding (`.gitignore` and this
README only, no script content was ever added here) has moved to a
private operational repository, kept separate from this public repo since
that code sits next to a bot token and a webhook URL. No name or path
given here by design -- this repo is public.
