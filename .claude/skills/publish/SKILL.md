---
name: publish
description: Put Karen's changes live on www.getmodelbehavior.ai and confirm they're live. Use when Karen says "publish", "make it live", "ship it", "push it", or similar.
---

Put the current work live on www.getmodelbehavior.ai. Pushing to `main` is what makes it live.

1. Run `git status` and `git log --oneline main..HEAD`. Summarize for Karen, in plain language, what is about to go live. If there's nothing new, say so and stop.
2. Commit any uncommitted changes with a visitor-facing message ("New pricing section", not "Update index.html").
3. Get onto `main` with the work:
   - If you're on a preview branch: `git switch main`, `git pull origin main`, then `git merge <branch>`. If the merge has conflicts, stop. Don't resolve them by guessing. Explain to Karen and suggest asking Jacquelyn.
   - If you're already on `main`: `git pull origin main` first.
4. `git push origin main`. Never force-push.
5. Confirm it's live. Vercel deploys in under a minute. Poll every 15 seconds, for up to 5 minutes:
   - `gh api "repos/jacquelyn-blum/model-behavior-www/deployments?sha=<full commit sha>&environment=Production"`, then read its `statuses_url` with `gh api` until the state is `success`, `failure`, or `error`.
   - On `success`: pick a piece of text that's new in this change and check it's on the live page: `curl -s https://www.getmodelbehavior.ai/`. If the change has no new text (e.g. a color change), check a changed line of CSS instead.
   - On `failure` or `error`: tell Karen the live site was not updated (it still shows the previous version), show the `target_url`, and suggest asking Jacquelyn.
6. If you merged a preview branch, delete it: `git branch -d <branch>` and `git push origin --delete <branch>`.
7. Tell Karen it's live at https://www.getmodelbehavior.ai. She may need to refresh. Remind her that `/undo` takes it back if needed.
