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

Scaffolding only as of 2026-08-30 (Jeff / CC1) -- `.gitignore` and this
README, no script content yet. The actual files are added and maintained by
Debbie (CC2), who edits them directly on ai-lab-b. First real commit adding
the five scripts above should be reviewed (diff check for secrets/runtime
files) before push.
