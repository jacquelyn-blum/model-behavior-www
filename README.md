# www.getmodelbehavior.ai

The Model Behavior marketing site. Karen runs it with Claude Code.

You can describe a change in plain English ("make the headline say X", "add a section about pricing"). Claude edits the page, shows you a preview link, and puts it live when you say so.

---

## One-time setup (about 20 minutes)

You need:
- a **Claude account on a paid plan** (Pro, Max, Team, or Enterprise; the free plan doesn't include Claude Code)
- your **GitHub account** (the one that got the invite to this repo; accept the invite first)

Follow the section for your computer. If you're not sure which you have: an Apple logo in the top-left corner means **Mac**, a Start button in the bottom-left means **Windows**.

### Mac

1. **Open Terminal.** Press `Cmd + Space`, type `Terminal`, press Enter. Every command below gets pasted into this window, followed by Enter.
2. **Install Git.** Paste `git --version`. If a box pops up offering to install "command line developer tools", click **Install** and wait for it to finish. If it prints a version number instead, you already have it.
3. **Install the GitHub app for the terminal.** Go to https://cli.github.com, click **Download for Mac**, open the downloaded file, and click through the installer.
4. **Install Claude Code.** Paste:
   ```
   curl -fsSL https://claude.ai/install.sh | bash
   ```
5. **Close Terminal and open a new one** so it picks up the new programs. Then go to [Get the site onto your computer](#get-the-site-onto-your-computer).

### Windows

1. **Install Git.** Go to https://git-scm.com/downloads/win, download **Git for Windows**, and run the installer. Click **Next** on every screen; the defaults are fine.
2. **Install the GitHub app for the terminal.** Go to https://cli.github.com, click **Download for Windows**, and run the installer.
3. **Open PowerShell.** Press the Windows key, type `PowerShell`, press Enter. Every command below gets pasted into this window (right-click pastes), followed by Enter.
4. **Install Claude Code.** Paste:
   ```
   irm https://claude.ai/install.ps1 | iex
   ```
   If it says `'irm' is not recognized`, you opened Command Prompt instead of PowerShell. Go back to step 3.
5. **Close PowerShell and open a new one** so it picks up the new programs.

### Get the site onto your computer

Same on Mac and Windows. Paste these one at a time:

1. Sign in to GitHub. Choose **GitHub.com**, then **HTTPS**, then **Yes**, then **Login with a web browser**. Copy the code it shows, press Enter, and paste the code into the browser page that opens.
   ```
   gh auth login
   ```
2. Let Git use that sign-in:
   ```
   gh auth setup-git
   ```
3. Download the site into a folder called `model-behavior-www` in your home folder:
   ```
   cd ~
   gh repo clone jacquelyn-blum/model-behavior-www
   ```

### Start Claude for the first time

```
cd ~/model-behavior-www
claude
```

- A browser window opens to log in to Claude. Log in with your Claude account. When the terminal says `Login successful`, press Enter.
- Claude asks whether you **trust this folder**. Say **yes**. That's what loads the instructions and shortcuts in this repo.

You're set up. Next time, you only need the two lines above (`cd ~/model-behavior-www`, then `claude`).

---

## Everyday use

Open Terminal or PowerShell and run:

```
cd ~/model-behavior-www
claude
```

Then just talk to it. For example:
- "Change the headline to 'See what AI says about your brand'"
- "The waitlist button should say 'Request access'"
- "Add a short section under the description explaining the three AI models we track"
- "Make it look better on phones"

Claude makes the change on your computer. **Nothing is public until you publish.** When you like it, use the shortcuts:

| Type this | What happens |
|-----------|--------------|
| `/preview` | Puts your changes on a private test link so you can look at them in your browser (and on your phone). The live site doesn't change. |
| `/publish` | Puts your changes live on www.getmodelbehavior.ai, then checks they actually went live. |
| `/undo` | Takes back the most recent published change and puts the previous version live again. |

You can also just say "preview this" or "publish it".

### Good habits

- **Preview before you publish** anything bigger than a small wording fix. Open the preview link on your phone too.
- **Claude will ask before it runs things.** If you don't understand what it wants to do, ask it: "what does that do?" It's fine to say no.
- To exit Claude, type `/exit` or press `Ctrl + C` twice.
- If something seems broken, tell Claude what you see ("the image is gone", "the button doesn't work"). If you're stuck, ask Jacquelyn.

### Things to know

- **This repo is public.** Anyone can read every file in it. Only put things here that belong on the website.
- **The waitlist form is wired to the product.** Every email submitted creates a real access code, so don't test it with fake addresses. If you want the form to collect more than an email, that needs Jacquelyn.
