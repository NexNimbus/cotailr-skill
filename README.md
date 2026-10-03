<div align="center">

<img src="https://cotailr.com/brand/svg/cotailr-icon-color.svg" alt="CoTailr" width="72" height="72" />

# CoTailr for Claude, Cursor and other AI apps

**Your AI assistant, connected to your real resume.** Send it a job link and it reads the posting, scores your fit,
builds a tailored resume and cover letter, tracks the application, and drafts the answers for the form, all from
your own CoTailr profile.

[![Create a free CoTailr account](https://img.shields.io/badge/1.%20Create%20free%20account-cotailr.com-6552F6?style=for-the-badge)](https://cotailr.com/login?mode=signup&next=%2Fsettings%23connected-apps)
[![Get an access key](https://img.shields.io/badge/2.%20Get%20access%20key-Settings-1a1b26?style=for-the-badge)](https://cotailr.com/settings#connected-apps)

[![Add CoTailr to Cursor](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/en/install-mcp?name=CoTailr&config=eyJ1cmwiOiJodHRwczovL21jcC5jb3RhaWxyLmNvbS9tY3AiLCJoZWFkZXJzIjp7IkF1dGhvcml6YXRpb24iOiJCZWFyZXIgJHtlbnY6Q09UQUlMUl9BUElfS0VZfSJ9fQ%3D%3D)
[![Download the Claude skill](https://img.shields.io/badge/Claude%20skill-download%20.zip-D97757?style=for-the-badge)](https://cotailr.com/static/cotailr-claude-skill.zip)

</div>

---

## What is CoTailr?

[**CoTailr**](https://cotailr.com) is an AI resume and cover-letter tailoring app. Paste a job description or a
link, and in about a minute you get a resume, cover letter and combined application pack tailored to that job,
**built only from facts in your own profile** and rendered in ATS-safe layouts.

> *JD-specific resumes, tailored in under a minute. Every line earns its place. Nothing gets invented.*

- **You decide what the AI may touch.** Every line is *Locked* (never changed), *Preferred* (may be reworded),
  *Flexible* (swapped in only if it fits the job better) or *CoTailr AI* (filled from your profile).
- **Built for real ATS parsers.** Flow-based layouts rendered by a real browser engine, so text extracts in
  reading order. Families: Tech Style (1 to 5+ pages), ATS Classic, Minimal and Coral.
- **One pass, full pack.** Resume PDF, cover letter PDF and a combined pack from one job match.
- **Everything around the application:** Job Fit scoring, a tracker, screening-question answers, a private
  Brief for your preferences and salary expectations, tone controls and regional presentation rules.
- **Start free:** a 7-day Pro trial with 25 credits and no card. Then Free, Plus ($9.99/mo) or Pro ($19.99/mo).

**This repo connects CoTailr to your AI assistant**, so you can do all of that from a conversation.

📖 [Full product guide](docs/what-is-cotailr.md) · 🧰 [Connector tools](docs/connector-tools.md) ·
❓ [FAQ](docs/faq.md) · 💳 [Pricing](https://cotailr.com/pricing/)

---

## What you get with the connector

| | |
|---|---|
| **Job links, handled** | Paste a URL. Your assistant fetches the posting and summarises company, role, location, work mode and the requirements that matter, then asks what you want next. |
| **Fit before effort** | A fit score against your actual experience before you spend time applying. |
| **Tailored packs** | A resume and cover letter tailored to the job, in your chosen template, as downloadable PDFs. |
| **A tracker that stays true** | Every pack lands in your CoTailr tracker as *Ready to apply*, and moves to *Applied* when you say you've submitted. Ask for a status review any time. |
| **Form answers** | Screening questions, "why us", salary and notice period, answered from your profile and your Brief instead of guesswork. |
| **Profile upkeep** | New achievement or changed salary expectation mid-conversation? Your assistant offers to save it, so every future application uses it. |
| **Undo everything** | Every change made through an AI app shows a *Changed by* marker in CoTailr with one-click Undo. |

There are two parts, and they work together:

- **The CoTailr connector (MCP server)** gives your AI app access to your CoTailr account: about 40 tools across
  jobs, tracker, profile, templates and AI writing.
- **The CoTailr skill** teaches Claude *how* to use it well: fetch first and ask before spending credits, read
  your Brief before answering salary questions, don't duplicate tracker entries, flag stale applications.

The connector already ships good default guidance and one-click workflows, so the skill is optional. It makes
Claude noticeably more consistent.

---

## Quick start (3 minutes)

### 1. Create your CoTailr account

**[Sign up free at cotailr.com](https://cotailr.com/login?mode=signup&next=%2Fsettings%23connected-apps)**

Then give CoTailr something to work with:

1. **Resume details → Master resume**: upload or paste your resume, then **Organise with CoTailr AI**.
2. **Brief**: add a few notes: target roles, locations, salary expectations, notice period, anything an
   assistant should know about you.

> **Install CoTailr as an app (optional).** CoTailr is a web app you can install like a native one:
> - **Desktop (Chrome, Edge):** click the install icon at the right of the address bar on cotailr.com.
> - **iPhone / iPad (Safari):** Share → **Add to Home Screen**.
> - **Android (Chrome):** menu ⋮ → **Install app**.

### 2. Create an access key

Open **[Settings → Connected apps](https://cotailr.com/settings#connected-apps)**, name the key (for example
"Claude on my laptop"), pick the access level and click **Create key**.

| Access | What the app can do |
|---|---|
| **Generate only** | Fetch jobs, generate resumes, check status, read templates, tracker and usage. |
| **Full access** | Everything above, plus edit your tracker, profile, Brief, tone and templates, and run the other AI tools (fit score, answers, cover letter text). Needed for the full skill. |

The key is shown **once**. Copy it straight away. You can revoke it any time from the same page.

### 3. Connect your AI app

Pick your app below. The server URL is always:

```
https://mcp.cotailr.com/mcp
```

and authentication is a request header: `Authorization: Bearer <your-key>`.

---

## Connect your app

<details open>
<summary><b>Claude (claude.ai and Claude Desktop)</b></summary>

1. In Claude, open **Settings → Connectors → Add custom connector**.
2. Fill in:
   - **Name:** CoTailr
   - **Remote MCP server URL:** `https://mcp.cotailr.com/mcp`
   - **Authentication:** **No sign-in**
   - **Request header:** name `Authorization`, value `Bearer <your-key>`
3. Save, then start a new chat. CoTailr's tools appear under the tools menu.

Then **add the skill** (recommended):

1. **[Download cotailr-claude-skill.zip](https://cotailr.com/static/cotailr-claude-skill.zip)**
2. In Claude's **Settings**, find **Skills** and choose **Upload skill**, then select the zip.

**One-click workflows:** in any chat, open the **+** menu → **CoTailr** for *Apply to a job*, *Review my
tracker*, *Answer application questions* and *Check my profile*.

</details>

<details>
<summary><b>Claude Code</b>: skill and connector in one install</summary>

This repo is a Claude Code plugin marketplace. Installing the plugin adds both the skill and the connector.

```bash
# 1. Open your shell profile (~/.zshrc or ~/.bashrc) in an editor, add the line below with your key,
#    save, and open a new terminal. Editing the file keeps the key out of your shell history.
#      export COTAILR_API_KEY="<your-key>"

# 2. In Claude Code
/plugin marketplace add NexNimbus/cotailr-skill
/plugin install cotailr@cotailr
```

Restart Claude Code, then try: *"Here's a job: https://… what do you think?"*

Prefer just the connector?

```bash
# reads the key from the COTAILR_API_KEY environment variable set above, so it stays out of your shell history
claude mcp add --transport http cotailr https://mcp.cotailr.com/mcp \
  --header "Authorization: Bearer $COTAILR_API_KEY"
```

</details>

<details>
<summary><b>Cursor</b></summary>

**Easiest:** after you create a key in [Settings → Connected apps](https://cotailr.com/settings#connected-apps),
click **Add to Cursor** next to it. Your key is filled in for you.

**From here:** click the button below. It reads the key from the `COTAILR_API_KEY` environment variable, so
set that first (and restart Cursor).

[![Add CoTailr to Cursor](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/en/install-mcp?name=CoTailr&config=eyJ1cmwiOiJodHRwczovL21jcC5jb3RhaWxyLmNvbS9tY3AiLCJoZWFkZXJzIjp7IkF1dGhvcml6YXRpb24iOiJCZWFyZXIgJHtlbnY6Q09UQUlMUl9BUElfS0VZfSJ9fQ%3D%3D)

**Manually:** add this to `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "cotailr": {
      "url": "https://mcp.cotailr.com/mcp",
      "headers": { "Authorization": "Bearer ctl_..." }
    }
  }
}
```

</details>

<details>
<summary><b>VS Code (GitHub Copilot agent mode)</b></summary>

**Easiest:** click **Add to VS Code** next to your new key in
[Settings → Connected apps](https://cotailr.com/settings#connected-apps).

**Manually:** add this to your user or workspace `mcp.json`. VS Code asks for the key once and stores it securely:

```json
{
  "inputs": [
    { "type": "promptString", "id": "cotailr-key", "description": "CoTailr access key", "password": true }
  ],
  "servers": {
    "cotailr": {
      "type": "http",
      "url": "https://mcp.cotailr.com/mcp",
      "headers": { "Authorization": "Bearer ${input:cotailr-key}" }
    }
  }
}
```

</details>

<details>
<summary><b>Claude Desktop (config file, older versions)</b></summary>

If your Claude Desktop has no **Add custom connector** option, use `mcp-remote` (needs Node.js) in
`claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "cotailr": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://mcp.cotailr.com/mcp", "--header", "Authorization: Bearer ctl_..."]
    }
  }
}
```

</details>

<details>
<summary><b>Any other MCP app</b></summary>

CoTailr is a standard remote MCP server over Streamable HTTP.

- **URL:** `https://mcp.cotailr.com/mcp`
- **Auth:** `Authorization: Bearer <key>`, or `X-API-Key: <key>` if your app only supports custom headers.
- No OAuth. Choose "no sign-in" or "API key / header" style authentication.

</details>

---

## Try it

Once connected, talk to your assistant normally:

- *"Here's a job I like: https://… Is it a fit?"*
- *"Make me a tailored resume and cover letter for it."*
- *"I've applied to Light, update the tracker."*
- *"Give me an update on everything in my tracker. Anything I should follow up on?"*
- *"This form asks for expected salary and why I want to join. Help me answer."*
- *"I just led a migration that cut costs 30%. Add that to my profile."*
- *"Check my profile for gaps before I start applying to Head of AI roles."*

---

## Credits and limits

AI actions use your normal CoTailr credits. Everything else is free.

| Action | Credits |
|---|---|
| Fetch a job, read tracker/profile, edit tracker/profile/templates | Free |
| Tailored resume + cover letter pack | 1 |
| Organise your master resume | 1 |
| Fit score | 0.5 |
| Merge Resume Components into master | 0.5 |
| Application answers | 0.3 |
| Cover letter section | 0.2 |
| Tone sample | 0.2 |
| Organise Brief notes | 0.1 |

Connected apps can spend at most **15 credits per day** (resets 00:00 UTC). Your assistant can check what's left
with `get_usage`, and you can see today's total and recent activity in Settings → Connected apps.

Your plan's features apply here too. For example, fit scores and cover letters need Plus or Pro (or the trial).

| | Free | Plus | Pro |
|---|---|---|---|
| Price | $0 | $9.99 / mo (₹499 in India) | $19.99 / mo (₹999 in India) |
| Credits | 1.5 / day | 100 / month, then 2 / day | 175 / month, then 2.5 / day |
| Templates | ATS Classic | + Tech Style, all sizes | + Tech Style, all sizes |
| Cover letter + full pack | – | ✓ | ✓ |
| Job Fit | – | ✓ | ✓ |
| Tracker | 10 active | Unlimited | Unlimited |

New accounts start with a **7-day Pro trial (25 credits, no card)**. See [cotailr.com/pricing](https://cotailr.com/pricing/).

---

## Privacy and security

- **Your key, your control.** Keys are stored hashed. Revoke one and every app using it stops working immediately.
- **Scoped access.** *Generate only* keys can't edit your profile or tracker.
- **Everything is logged** in Settings → Connected apps → Recent activity: which tool, which key, when and what
  it cost. Logs never include the content of your resume or the job.
- **Undo.** Changes made by an AI app are marked in CoTailr with one-click Undo.
- **Never paste your key into a chat.** It belongs in the app's connector settings only.

---

## Troubleshooting

| Problem | Fix |
|---|---|
| `401 unauthorized` / "Access key missing, invalid or revoked" | Check the header is exactly `Authorization: Bearer ctl_...` (one space after Bearer). Create a new key if you revoked or lost it. |
| Claude says the header isn't allowed | Use the header name `Authorization` (or `X-API-Key`). Custom names are rejected by Claude. |
| Claude tries to sign in / opens an OAuth window | Set authentication to **No sign-in** and add the header instead. |
| Tools don't appear | Start a new chat (or restart the app) after adding the connector. |
| "This job site blocked the request" | Some job boards block automated reads. Paste the job text into the chat instead. |
| `daily_credit_limit_reached` | The 15-credit daily cap for connected apps. It resets 00:00 UTC, and the CoTailr web app itself isn't affected. |
| A tool says it needs Full access | Create a **Full access** key and swap it into your app. |

---

## What's in this repo

```
.
├── README.md                     ← this page
├── llms.txt                      ← summary + index for AI models (llmstxt.org format)
├── docs/
│   ├── what-is-cotailr.md        ← full product guide: features, templates, plans, privacy
│   ├── connector-tools.md        ← all 42 connector tools, access levels and costs
│   └── faq.md
├── skills/cotailr/SKILL.md       ← the CoTailr skill (also published as a .zip on cotailr.com)
├── .mcp.json                     ← connector config for the Claude Code plugin
└── .claude-plugin/
    ├── plugin.json               ← Claude Code plugin manifest
    └── marketplace.json          ← lets `/plugin marketplace add` find it
```

To use the skill somewhere other than Claude, the instructions in `skills/cotailr/SKILL.md` are plain Markdown.
Paste them into your app's custom instructions or rules.

**License:** the files in this repo are MIT licensed. CoTailr itself is a proprietary, hosted service by
NexNimbus LLP. This repo contains no CoTailr source code, and using the service is subject to the
[CoTailr Terms](https://cotailr.com/terms/).

**For AI models and answer engines:** start with [`llms.txt`](llms.txt), then
[`docs/what-is-cotailr.md`](docs/what-is-cotailr.md) for the complete, current product facts.

---

<div align="center">

**[cotailr.com](https://cotailr.com)** · [Create account](https://cotailr.com/login?mode=signup&next=%2Fsettings%23connected-apps) · [Connected apps](https://cotailr.com/settings#connected-apps)

</div>
