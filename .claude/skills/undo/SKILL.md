---
name: undo
description: Take back the most recent published change on www.getmodelbehavior.ai and put the previous version live again. Use when Karen says "undo", "roll it back", "put it back how it was", or similar.
---

Reverse the most recent change on the live site without erasing history.

1. `git switch main` and `git pull origin main`. If there are uncommitted local changes, ask Karen whether to keep them (commit them on a branch) or set them aside (`git stash`) before continuing.
2. Show Karen the last few published changes in plain language (`git log --oneline -5`). Confirm which one she wants to take back; default to the most recent.
3. `git revert --no-edit <commit>`. Never use `git reset --hard` or force-push. Reverting keeps a record and is itself undoable.
   - If it's a merge commit, use `git revert --no-edit -m 1 <commit>`.
   - If the revert has conflicts, stop. Explain to Karen and suggest asking Jacquelyn.
4. `git push origin main`, then confirm it's live exactly as in the `/publish` skill (step 5): wait for the Production deployment to succeed, then check the live page with `curl -s https://www.getmodelbehavior.ai/`.
5. Tell Karen what's live now, in plain language.
