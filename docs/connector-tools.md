# CoTailr connector: tools reference

The CoTailr connector is a remote [Model Context Protocol](https://modelcontextprotocol.io) server.

- **URL:** `https://mcp.cotailr.com/mcp` (Streamable HTTP, stateless, JSON responses)
- **Auth:** `Authorization: Bearer <access key>` (or `X-API-Key: <access key>`). Keys come from
  [Settings → Connected apps](https://cotailr.com/settings#connected-apps).
- **Access levels:** **Generate only** keys see the 7 tools marked **G**. **Full access** keys see all 52.
- **Credits:** charged tools use the account's normal CoTailr credits. Connected apps can spend at most
  **15 credits per day** (resets 00:00 UTC). Plan features still apply, so Job Fit needs Plus or Pro.
- **Undo:** every write is snapshotted. `undo_last_change(area)` restores the previous state, and the CoTailr web
  app shows a *Changed by &lt;app&gt;* marker with an Undo button.
- **Errors:** `{"error": code, "message": "...", "retry_with"?: field}`. Codes include `job_url_blocked`,
  `no_credits`, `plan_gate`, `daily_credit_limit_reached`, `rate_limited`, `bad_input`, `not_found` and
  `not_ready`.

The server also sends usage instructions to the AI app when it connects, and offers four one-click
**prompts** (workflows): *Apply to a job*, *Review my tracker*, *Answer application questions* and *Check my
profile*.

---

## Jobs and generation

| Tool | Access | Credits | What it does |
|---|---|---|---|
| `fetch_job(job_url)` | G | Free | Reads a job posting: company, role, location and a text preview. |
| `generate_resume(job_url \| job_text, template?, size?, special_instructions?, company?, role?, tone?, hide_fields?)` | G | 1 | Starts a tailored resume and cover letter pack. `size`: auto, snapshot, professional, portfolio, dossier. `tone`: AI Tone for this pack only (pass `match.tone_fit.suggested.tone` from `match_job` to use the suggestion; omit for the user's own tone). `tone.bullets` sets the experience bullet style for this pack: `off` (CoTailr Style), `auto`, `xyz`, `car` or `ao`. `hide_fields`: personal details to leave off this pack only, any of `dob`, `gender`, `nationality`, `location`, `onsite`, `phone` (the profile is not changed). Returns `job_id` and `warnings` for instructions CoTailr can't follow (each says which option does it). The finished pack is added to the tracker as *Ready to apply*. |
| `get_generation(job_id)` | G | Free | Status. When done, gives download links (valid for 10 minutes) and the tracker `application_id`. Also returns `warnings` (things to check before sending: a hidden detail still printed, a rewrite that kept the original wording because it added or dropped a fact, a cut-off line, too many pages, a section dropped to fit) and, when a bullet style was used, `bullet_style` and `bullet_rewrites` (`[{id, source, text}]`). Warnings never block the download. |
| `list_templates()` | G | Free | Template families available to the user, and which are active. Each family has a `tagline`, `best_for`, `avoid_if`, `ats_friendliness` (high or medium) with `ats_note`, `layout` (columns, photo, look) and `sizes` (what each size contains). Use it to recommend a template for the job. |
| `get_usage()` | G | Free | Credits left, plan, and today's connected-app spend against the daily cap. |

## Tracker

| Tool | Access | Credits | What it does |
|---|---|---|---|
| `list_applications(query?, status?, limit?)` | G | Free | Searches the tracker, newest first (up to 100 rows plus counts by status). |
| `get_application(application_id)` | G | Free | One application with fit scores and notes. |
| `create_application(company, role, ...)` | Full | Free | Adds a job by hand. |
| `update_application(application_id, fields)` | Full | Free | Changes status, notes, dates, company, role or link. Moving *Ready to apply* to *Applied* sets the applied date to today. |
| `delete_application(application_id)` | Full | Free | Deletes an application (undoable). |

**Statuses:** `draft` (*Ready to apply*), `applied`, `in_progress`, `interview_1`, `interview_2`, `interview_3`,
`offer`, `got_the_job`, `rejected_no_interview`, `rejected`, `withdrawn`.

## Profile

| Tool | Access | Credits | What it does |
|---|---|---|---|
| `get_master()` | Full | Free | The organised master resume (Markdown) and its headings. |
| `update_master_section(heading, text)` | Full | Free | Replaces one section of the master resume. |
| `upload_master(text)` | Full | Free | Saves new raw resume text. |
| `parse_master()` | Full | 1 | Organises the raw resume with CoTailr AI. |
| `sync_master_from_components(apply?, item_ids?)` | Full | Free preview / 0.5 | Finds Resume Component items missing from the master, and merges them if `apply=true`. |
| `get_components(section?)` | Full | Free | Structured Resume Components. |
| `update_component_item(section, item_id, fields, parent_id?)` | Full | Free | Edits one item. |
| `add_component_item(section, item, ...)` | Full | Free | Adds an item. |
| `remove_component_item(section, item_id, parent_id?)` | Full | Free | Removes an item. |
| `reorder_items(section, ordered_ids, ...)` | Full | Free | Reorders a list. |
| `replace_role_bullets(role_id, section_id, bullets)` | Full | Free | Rewrites the bullets of one role. |
| `save_bullet_rewrite(bullet_id, text)` | Full | Free | Saves one rewritten bullet from `get_generation`'s `bullet_rewrites` as that bullet's profile wording. Locked bullets are refused. Undo with `undo_last_change('components')`. |
| `get_contact()` / `update_contact(fields, confirm?)` | Full | Free | Contact details. Updating returns a preview and saves on `confirm=true`. |
| `get_brief()` | Full | Free | The Brief: targets, locations, salary, preferences, stories. |
| `add_brief_chunk(title, body, kind?)` / `update_brief(chunk_id, ...)` / `remove_brief_chunk(chunk_id)` | Full | Free | Manage Brief notes. |
| `organise_brief(notes)` | Full | 0.1 | Turns freeform notes into Brief notes. |
| `get_tone()` / `update_tone(fields)` | Full | Free | Tone settings: seniority, style, authority, language, personality, and `bullets` (experience bullet style: `off` = CoTailr Style, `auto`, `xyz`, `car`, `ao`). |
| `update_cover_letter(section, text?, url?, link_text?, enabled?, signoff?)` | Full | Free | Writes your own wording into the profile cover letter: `opening`, `differentiator` or `closing` (`{{COMPANY}}` becomes the employer's name). `signoff` (closing only, up to 60 characters) sets the line above the signature; empty means "Warm Regards,". Paragraphs set to Preferred are tuned to each job from saved facts only. Read the current text with `get_components('cover_letter')`. Undo with `undo_last_change('components')`. |
| `add_tone_sample(axes?)` | Full | 0.2 | A two-paragraph sample in the user's voice. |

## Templates

| Tool | Access | Credits | What it does |
|---|---|---|---|
| `get_template_settings(template, template_id)` | Full | Free | Colours and section order. |
| `activate_template_family(template, enabled)` | Full | Free | Turns a family on or off. |
| `set_colors(template, template_id, values)` | Full | Free | Sets colours (hex). They apply to that template's resume and cover letter. |
| `set_section_order(template, template_id, order)` | Full | Free | Sets section order. |

## TailrMe (personal page)

TailrMe turns the profile into a one-page personal site at `cotailr.com/@handle`. Edits go to a draft;
the public page only changes when the draft is published. Private details (date of birth, gender,
nationality, phone, street address) are off by default. These tools need TailrMe to be enabled for the
account (`feature_off` otherwise).

| Tool | Access | Credits | What it does |
|---|---|---|---|
| `list_tailrme_templates()` | Full | Free | Page templates with name, description, tags and which sections each supports. |
| `get_tailrme_page()` | Full | Free | The draft, handle, page URL, status, and whether the draft has changed since the last publish. |
| `get_tailrme_content()` | Full | Free | What the page would show right now, built from the profile and the draft (hero, about, experience, skills, links and so on). |
| `check_tailrme_handle(handle)` | Full | Free | Whether an address is valid and free. Lookalikes of a taken handle (case or hyphens only) count as taken. |
| `update_tailrme_draft(changes?, handle?)` | Full | Free | Edits the draft. `sections`, `contact`, `text`, `theme` and `link_labels` are merged; `template_id`, `order`, `shown_items`, `hidden_items` and `indexable` are replaced. `handle` claims the address. Extra links from Resume details (listed in `get_tailrme_page`'s `checklist.links`) stay off until their `id` is in `shown_items`; `link_labels` (`{id: text}`) renames one for this page only. Undo with `undo_last_change('tailrme')`. |
| `cook_tailrme()` | Full | 0.3 | *Let CoTailr AI cook*: writes the page headline, about text and highlights from the profile. Facts not in the profile are dropped. Saves to the draft only. |
| `publish_tailrme(confirm?)` | Full | Free | Publishes the draft. Without `confirm=true` it only says where the page will go live and whether search engines can see it; show the user `get_tailrme_content` first. |
| `unpublish_tailrme()` | Full | Free | Takes the page offline. The draft and handle are kept. |

## AI writing and scoring

| Tool | Access | Credits | What it does |
|---|---|---|---|
| `match_job(job_text \| job_url, company?, role?)` | Full | 0.5 | Job Fit score before applying, plus `tone_fit`: the user's AI Tone scored for this job (strong, partial or weak) and, when clearly better, a suggested tone with the changed settings and reasons. The suggestion can include a bullet style (for example `xyz` for a metrics-heavy role when the relevant bullets contain numbers). |
| `rematch_application(application_id, job_text?, force?)` | Full | 0.5 | Scores a tracked application. Free if it's already scored. |
| `answer_application_questions(questions \| text, job_text? \| application_id?, length?, guidance?)` | Full | 0.3 | Drafts screening-question answers from the profile. |
| `generate_cover_letter(section, current?, save?)` | Full | 0.2 | Drafts a cover-letter block: opening, differentiator, closing or achievements. |
| `get_cover_letter(job_id)` / `edit_cover_letter(job_id, html)` | Full | Free | Reads or edits a generated cover letter and re-renders its PDF. |

## Undo

| Tool | Access | Credits | What it does |
|---|---|---|---|
| `undo_last_change(area, confirm?)` | Full | Free | Reverts the latest connected-app change in `templates`, `tracker`, `components`, `master`, `contact`, `brief`, `tone`, `cover_letter` or `tailrme`. Asks for confirmation if the user has edited since. |
