# Security

## Reporting a vulnerability

Please report security issues privately to **connect@nexnimbus.com** with the subject "CoTailr security". Include
steps to reproduce and the impact you observed. Please don't open a public GitHub issue for security reports.

We aim to acknowledge reports within 3 business days.

## What this repository contains

Documentation, a Claude skill (plain Markdown instructions) and connector configuration only. It contains **no
credentials and no server code**. Every key shown in these files is a placeholder (`ctl_...`, `<your-key>`,
`${COTAILR_API_KEY}`).

## Keeping your CoTailr access key safe

- Put your key only in your AI app's connector settings, an environment variable or a secret prompt (VS Code
  `inputs`). Never commit it to a repository, and never paste it into a chat.
- Use a **Generate only** key when you don't need profile or tracker edits.
- If a key may have leaked, revoke it in [Settings → Connected apps](https://cotailr.com/settings#connected-apps).
  It stops working immediately. Then create a new one.
- Review **Recent activity** on the same page to see every tool call made with your keys.

## How the connector protects your account

- Keys are 256-bit random values, stored only as SHA-256 hashes, scoped to *Generate only* or *Full access*, and
  revocable instantly.
- Requests without a valid key are rejected before reaching any tool.
- Charged actions are capped at 15 credits per day for connected apps.
- Every write is snapshotted and can be undone, and contact-detail changes require explicit confirmation.
- Job postings and other fetched content are treated as data, not instructions, both by CoTailr's own AI and in
  the guidance given to connected assistants.
