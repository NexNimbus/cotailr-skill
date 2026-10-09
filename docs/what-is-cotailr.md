# What is CoTailr?

**CoTailr** ([cotailr.com](https://cotailr.com)) is an AI resume and cover-letter tailoring app. You paste a job
description or a job link, and CoTailr builds a resume and cover letter tailored to that role in about a minute,
**using only content you've stored in your own profile**. It then renders them through ATS-safe layouts as PDFs.

> *JD-specific resumes, tailored in under a minute. Every line earns its place. Nothing gets invented.*

Around the tailoring engine, CoTailr gives you a job-fit scorer, an application tracker, a screening-question
helper, a private preferences memory (the Brief), tone controls and region-aware presentation rules. With the
**CoTailr connector**, AI assistants like Claude and Cursor can use all of it for you.

CoTailr is a product of **NexNimbus LLP**, Bangalore, India.

---

## Who it's for

Professionals actively applying to several roles who want each application to be specific to the job, without
spending 45–60 minutes rewriting a resume each time, without an AI inventing experience, and without layouts
that break when an applicant tracking system (ATS) parses them.

---

## How it works

1. **Build your profile once.** Upload or paste your resume (PDF, DOCX, TXT or Markdown, polished or messy).
   *Organise with CoTailr AI* turns it into a structured master resume and Resume Components.
2. **Paste or fetch the job.** Paste the job description, or give a link and CoTailr reads the posting.
3. **One tailoring pass.** CoTailr matches your profile to the job's actual requirements and writes the resume
   and cover letter in your chosen tone.
4. **Render and download.** You get a resume PDF, a cover letter PDF and a combined application pack, rendered by
   a real browser engine in flow-based layouts that ATS parsers read in the right order.

---

## Why it's different

### You decide what the AI may touch: line modes

Every line of your resume and cover letter carries a mode you set once:

| Mode | What CoTailr may do |
|---|---|
| **Locked** | Prints exactly as written. Never reworded, never dropped. |
| **Preferred** | May be lightly reworded, never replaced. |
| **Flexible** | Swapped in only when it matches the job better than what's already there. |
| **CoTailr AI** | An open slot CoTailr fills from the job and your master resume. |

### Built from your facts

Tailoring draws only on your profile. After each pass, an **invent-check** compares the numbers and dates in the
output against your master resume and Locked content. On Plus and Pro, anything that doesn't trace back shows
up as a warning so you can review it before you send.

### Built for real ATS parsers

Templates render as flow-based HTML to PDF through a real browser engine, not absolutely positioned text boxes,
which are known to scramble word order when ATS software extracts text. ATS Classic is a single-column,
parser-first family for Workday, Greenhouse and LinkedIn Easy Apply.

### One pass, full pack

The resume, the cover letter and the combined pack come from the same job match in one run, not three separate
prompts.

---

## Features

### Generate
- Paste a job description (up to 20,000 characters) or fetch it from a URL.
- Choose a template family and size, or let **Auto** pick the size from how much of the job your profile covers.
- Add a short special instruction if you want something emphasised.
- Preview, edit the generated document in place (re-saving re-renders the PDF at no extra cost) and download.

### Job link reading
Dedicated support for Workday, Greenhouse, Lever, Ashby, SmartRecruiters, Workable, Recruitee, Personio, BambooHR,
LinkedIn, Welcome to the Jungle, Teamtailor, Pinpoint, Rippling, JobAdder, Oracle Candidate Experience and more,
with a generic fallback for other career pages. Company, role, location and work mode are extracted
automatically. If a site blocks automated reads, you paste the text instead.

### Job Fit (Analyse fit)
Scores your fit with a job from 0 to 100 overall, plus skills, experience, tools, domain, seniority, keyword
coverage and ATS alignment. You also get a fit label (strong to poor), a recommendation (apply / maybe / skip)
with the reason, your top strengths and gaps, and constraints such as visa or relocation. If you've filled in your
Brief, Fit also checks the job against your salary band, seniority, relocation and red lines.

### Resume details
- **Master resume:** your full career source. Raw text goes in, *Organise with CoTailr AI* produces the
  structured version that tailoring reads.
- **Resume Components:** structured sections (experience, education, skills, projects, contact, photo,
  cover-letter blocks) that print on your documents, each line with its mode.

### Templates and sizes

| Family | Style | Sizes |
|---|---|---|
| **Tech Style** | Modern, visual | Snapshot (1 page), Professional (2), Portfolio (3–4), Dossier (5+) |
| **ATS Classic** | Single-column, parser-first | Professional (2 pages) |
| **Minimal** | Clean single-column | Professional |
| **Coral** | Two-column | Professional |

Some templates let you change colours and reorder sections.

### AI Tone
Set the voice for your summary and cover letter:
- **Seniority:** Junior, Mid, Senior, IC, Manager, Director / C-level
- **Style:** Professional, Friendly, Direct, Executive
- **Authority:** Evidence-first, Balanced, Vision-forward
- **Language:** British, American, Neutral international
- **Personality:** Balanced, Collaborative, Individual-first, Mentor, Operator

Every setting also has a Custom option, and you can generate a live sample to hear the voice.

### Answers (application questions)
Drafts answers to screening questions from your profile:
- finds the questions on Greenhouse, Ashby and Lever postings, or you paste them;
- up to 12 questions per run, in short, medium or long answers;
- facts CoTailr doesn't have come back as "Not on file" rather than made up;
- on Pro, you can upload screenshots of a form (up to 3 images). They're processed in memory and never saved;
- CoTailr never submits forms for you.

### CoTailr Brief
Your private memory: target roles, salary expectations, notice period, relocation, red lines, the stories you
want told. Write it messily and CoTailr organises it into notes. The Brief steers Fit, Answers and tailoring, and
is never printed on your documents.

### Logic (regional presentation rules)
IF / AND / OR rules for regional conventions (name prefixes, photos, location formats), keyed to the job's region:
Middle East, India, Asia Pacific, Europe, United States and United Kingdom.

### Tracker
Every generation is tracked automatically with company, role, fit and ATS scores and the documents you sent.
Statuses: *Ready to apply*, *Applied*, *In progress*, *Interview (1st, 2nd, 3rd+ round)*, *Offer*, *Got the job*,
*Rejected (no interview)*, *Didn't get it*, *Withdrawn*.

### Connected apps (CoTailr connector)
Let Claude, Cursor, VS Code or any MCP-compatible AI app use CoTailr for you through an access key created in
Settings. There are 44 tools across jobs, tracker, profile, templates and AI writing, with a daily credit cap and
undo for every change. See [the connector tools reference](connector-tools.md).

---

## Plans and pricing

Every new account starts with a **7-day Pro trial with 25 credits, no card required**.

| | **Free** | **Plus** | **Pro** |
|---|---|---|---|
| Price | $0 | $9.99 / month (₹499 in India) | $19.99 / month (₹999 in India) |
| Credits | 1.5 per day | 100 per month, then 2 per day | 175 per month, then 2.5 per day |
| Template families | ATS Classic | ATS Classic + Tech Style | ATS Classic + Tech Style |
| Sizes | Professional (ATS Classic) | All sizes, Snapshot to Dossier | All sizes, Snapshot to Dossier |
| Output | Resume PDF | Resume, cover letter and combined pack | Resume, cover letter and combined pack |
| Job Fit | – | ✓ | ✓ |
| Invent-check warnings | – | ✓ | ✓, with a richer report |
| Tracker | 10 active applications | Unlimited | Unlimited |
| Screenshot answers | – | – | ✓ |

Daily credits reset at midnight India Standard Time. Prices are shown in ₹ in India and $ elsewhere, and current
pricing is always at [cotailr.com/pricing](https://cotailr.com/pricing/).

### What things cost (credits)

| Action | Credits |
|---|---|
| Tailored resume + cover letter pack (any size) | 1 |
| Generic resume download (no job) | 1 |
| Organise master resume | 1 |
| Job Fit | 0.5 (included when run as part of a pack) |
| Sync Resume Components into master | 0.5 |
| Application answers | 0.3 |
| Tone sample | 0.2 |
| Cover-letter section draft | 0.2 |
| Organise Brief notes | 0.1 |
| Editing, tracker, reading jobs, previews | Free |

Failed generations are refunded.

---

## Privacy and security

- **We do not sell your personal information.** Full details in the
  [Privacy Policy](https://cotailr.com/privacy/).
- You own your content (see [Terms](https://cotailr.com/terms/)).
- Each account's data is isolated at the database level (row-level security).
- Generated files on CoTailr's servers expire after a few days by default.
- Answer screenshots are processed in memory and never written to disk.
- Job descriptions, your resume and your Brief are handled as data, never as instructions, which protects
  tailoring from prompt-injection text hidden in job postings.
- Connected-app access keys are stored hashed, scoped (*Generate only* or *Full access*), revocable instantly and
  fully logged.

---

## Company and contact

- **Product:** CoTailr ([cotailr.com](https://cotailr.com))
- **Company:** NexNimbus LLP, Bangalore, India ([nexnimbus.com](https://nexnimbus.com))
- **Contact:** connect@nexnimbus.com
- **More:** [FAQ](https://cotailr.com/faq/) · [Blog](https://cotailr.com/blog/) · [Pricing](https://cotailr.com/pricing/)
