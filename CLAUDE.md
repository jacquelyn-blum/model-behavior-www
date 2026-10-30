# CLAUDE.md

## What this is

The public marketing site for Model Behavior, served at **www.getmodelbehavior.ai**.

Model Behavior is a brand intelligence platform. It tracks how AI assistants (Claude, ChatGPT, Gemini) describe, recommend, and cite brands when consumers ask them for advice, and turns that into a dashboard for brand teams.

This repo holds only the marketing site. The product (pipeline, backend, dashboards, admin) lives in a separate repo that Jacquelyn owns. Nothing here can break the product. One thing here *does* talk to the product: the waitlist form (see below).

## This repo is public

Anyone on the internet can read every file and every past commit. Only commit things that are meant to be on the live site. Never commit client or brand data, dashboards, demo exports, contact lists, drafts, notes, API keys, or tokens. If Karen asks you to add something that isn't for the public page, stop and say so. Deleting a file later doesn't help, because it stays in the history.

## Files

| Path | What |
|------|------|
| `index.html` | The whole site: HTML, CSS (in `<style>`) and JS (in `<script>`). No build step, no framework. |
| `assets/` | Images. Reference them with absolute paths (`/assets/hero.jpg`). |
| `robots.txt` | Crawler policy. The site is deliberately open to all crawlers, AI crawlers included, because we sell AI visibility. Don't block anything unless Karen asks you to. |

## Deploying

The repo is git-linked to the Vercel project `landing-page-2`.

- **Push to `main` → live on www.getmodelbehavior.ai within a minute or so.** There's no staging.
- **To preview without going live:** push a branch. Vercel builds a preview URL for every branch and posts it on the commit / PR.
- For anything bigger than a copy tweak, preview on a branch first, check it on desktop *and* phone width, then merge.

After a push to `main`, verify it's live: `curl -s https://www.getmodelbehavior.ai/ | grep "<some new text>"`.

## The waitlist form — don't break it

The email form POSTs to the product backend:

```
POST https://model-behavior-production.up.railway.app/api/waitlist
Content-Type: application/json
{"email": "someone@company.com"}
→ 200 {"success": true}   |   400 {"success": false, "error": "Invalid email"}
```

Each signup creates an access code on the backend, so this is how prospects get into the product. Rules:

- Don't change the URL, method, or payload shape. If Karen wants to collect more fields (name, company…), stop and tell her that needs a backend change from Jacquelyn.
- The endpoint is rate-limited to **5 requests/minute per IP**. Don't test it in a loop.
- Test with a real-looking address you own. Every test signup becomes a real access code.
- Keep both the success state and the visible error message (no `alert()`).

## Design system

Everything uses one font and one palette. The tokens are the CSS variables in `:root` at the top of `index.html`. Use them; don't add new hex colors.

- **Font:** JetBrains Mono only (loaded from Google Fonts), weights 300–800. Labels, buttons, chips, and headings are `text-transform: uppercase` with wide letter-spacing.
- **Palette ("Pressed Flower"):** lavender background `--bg #f5eef6`, near-white panels `--panel #fffbfd`, borders `--border #c9b8d4`, text `--text #3d2e4a` / `--muted #7a6889` / `--dim #a899b5`, purple accent `--brand-accent #7b4f9e`.
- **Model colors** (always these, always this order): Claude `--claude #d4872e`, ChatGPT `--chatgpt #3a8a5c`, Gemini `--gemini #7b4f9e`.
- **Shape language:** square corners (no border-radius), 2px solid borders, flat fills. The only shadow is the hard offset on hover (`3px 3px 0 var(--border)`).
- **Mobile:** there's a `@media (max-width: 520px)` block. Every change needs to look right at phone width.

## Other links on the page

- "Have an invite code?" → `https://trial.getmodelbehavior.ai`. That's a different site in a different repo. Keep the link; don't try to edit that site from here.
- Analytics: Vercel Web Analytics via `https://va.vercel-scripts.com/v1/script.js` at the bottom of the page. Keep it, and keep it the non-debug build.

## Working style

- Karen owns this site and ships on her own. Explain what you're changing in plain language, show the preview, then push.
- Keep it one static page unless Karen decides otherwise. If she wants multiple pages, add them as plain `.html` files plus shared CSS in `assets/`, not a framework.
- Optimize images before adding them (≤ 300 KB each, JPG for photos, PNG or SVG for graphics). Don't inline base64 images. That made `index.html` 130 KB of noise.
- Commit messages should say what changed for a visitor ("New hero copy", "Add pricing section"), not "Update index.html".
