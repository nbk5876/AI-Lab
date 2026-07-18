# Claude Code — AI Lab Portal Workflow Guide

## Repo
- Path: `C:\Users\gb105\OneDrive\Tony1\AI-Lab\Portal`
- Remote: `github.com/nbk5876/AI-Lab.git`
- Deploy: push to `main` → GitHub Actions (`.github/workflows/deploy.yml`) → `lftp mirror -R --delete` to DreamHost `/home/dh_92keyc/core3.com/AI-Lab/`
- Live: `https://www.core3.com/AI-Lab/`
- No `.htaccess` — DreamHost's default Apache MIME types already serve `.xlsx` and other static assets correctly.

## Recurring workflow: ChatGPT-authored handoffs

Tony works through problems live with ChatGPT (sometimes multi-hour sessions), then hands Claude Code a `CC-*.md` / `CC-Task-*.md` file in `C:\Users\gb105\Downloads\`, alongside the HTML/image/spreadsheet files it references. Claude Code's job is to deploy and verify what the handoff specifies — not to re-derive or second-guess the content itself.

### Before deploying
1. **Read the handoff file first.** It lists exactly what to deploy, what to skip, and any decision that's still pending a human call.
2. **Normalize filenames.** Downloads often carry a browser `" (n)"` suffix (`always-on-server (1).html`, `Part5-spec (2).md`) from repeated re-downloads of the same session output. Strip it — the canonical name is the one without the suffix.
3. **Don't trust a "replace" instruction blindly.** A handoff may claim the live file is "stale," but the live repo can have moved on since the handoff was drafted (e.g. a later "make images clickable" commit). `diff` the incoming file against the current live file before overwriting. If the only difference would be a regression relative to a later commit, skip the replace and say why — don't silently follow the handoff over the evidence.
4. **Respect the do-not-deploy list.** Internal diagnostic tools (`ollama-timing-bench.html`, `openwebui-timing-bench.html`, `serve_tools.py`, `Start-Lab-Tools.bat`, `Stop-AI-Lab.bat`) live on Lab PC 2 and are never portal content, even if they show up in the same Downloads batch.
5. **Honor claim tags literally.** Field Guide content specs (e.g. `Part5-spec.md`) tag every claim `[PROVEN]` / `[HYPOTHESIS]` / `[PENDING]`. PROVEN = state as fact. HYPOTHESIS = "likely/suspected," never fact. PENDING = leave a placeholder, invent nothing. `AI_Lab_Test_Log.xlsx` is the source of truth for every number; if a spec number disagrees with it, the spreadsheet wins — flag it, don't guess.
6. **"Living document" pages get a visible in-progress banner.** If a handoff wants a page to read as in-progress rather than finished, that means a `status-pending` banner near the top (and usually echoed at the bottom) stating plainly what's still open. Don't soften or remove it, even if the rest of the page reads confidently.
7. **Hold anything marked "needs a human decision."** e.g. where a new page should be linked from. Wait for that decision to arrive in a follow-up handoff rather than picking for Tony.

### After deploying
- `gh run list --repo nbk5876/AI-Lab --limit 3` to confirm the workflow run succeeded.
- Live-verify with a direct `curl`, not only WebFetch — WebFetch has its own ~15-minute cache and can return a pre-deploy snapshot immediately after a push looks stale even though the deploy succeeded.
- Log the change in the Lab Journal at `C:\Users\gb105\OneDrive\Tony1\AI-Lab\Lab-Journal.md` (date, purpose, files changed, verification, rollback, next steps — follow the format of existing entries).

## Portal structure
- `field-guide/` — the Local LLM Field Guide, numbered Parts (`mobile-lan-access.html` = Part 2, `reliable-remote-access.html` = Part 3, `always-on-server.html` = Part 4, `where-the-seconds-go.html` = Part 5). Each links back/forward via a "What's Next" card grid and a bottom nav `<p>` line — when adding a new Part, wire both directions plus the "Field Guide Parts" table of contents in `field-guide/index.html`.
- `field-guide/test-log.html` — mobile-friendly readable test log; `field-guide/AI_Lab_Test_Log.xlsx` is the downloadable source-of-truth spreadsheet it links to.
- Shared stylesheet: `assets/style.css` — reuse existing classes (`chapter`, `spec-table`, `lessons`, `status-banner`/`status-success`/`status-pending`, `code-block`, `card`/`grid`, `figure.img-70` and siblings) rather than inventing new ones.

## See also
- Project background: AI Lab memory (`project-ai-lab`)
- Operating rules (approval gates, docs-first, Lab Journal): `feedback-ai-lab-workflow`
- Handoff-deploy judgment calls: `feedback-ai-lab-portal-handoff-deploys`
- Public-repo privacy scrub convention: `feedback-ai-lab-portal-privacy`
