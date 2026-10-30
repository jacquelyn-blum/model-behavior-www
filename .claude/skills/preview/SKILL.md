---
name: preview
description: Put the current changes on a private Vercel preview link so Karen can look at them before they go live. Use when Karen says "preview", "let me see it", "show me", or similar.
---

Get Karen a preview link for the current changes. The live site must not change.

1. Run `git status`. If there are no changes and no commits on this branch beyond `main`, tell Karen there's nothing new to preview and stop.
2. If you're on `main`, create a branch first: `git switch -c preview-<two-or-three-word-description>` (lowercase, hyphens), e.g. `preview-new-headline`. Never push changes to `main` from this skill.
3. Commit everything with a message that says what changed for a visitor ("New hero headline", not "Update index.html"). Then `git push origin <branch>`.
4. Find the preview link. Vercel builds it automatically in under a minute. Poll every 15 seconds, for up to 5 minutes:
   - `gh api "repos/jacquelyn-blum/model-behavior-www/deployments?sha=<full commit sha>"`. When a deployment appears, read its `statuses_url` with `gh api`.
   - A status with `"state": "success"` has the link in `environment_url`. If the state is `failure` or `error`, tell Karen the preview build failed, show the `target_url`, and suggest asking Jacquelyn.
5. Give Karen the link on its own line. Tell her what changed in one or two plain sentences. Remind her to check it on her phone too: she can text herself the link, or narrow the browser window.
6. Tell her: when she's happy, type `/publish` to put it live; or keep describing changes, and run `/preview` again for a fresh link.
