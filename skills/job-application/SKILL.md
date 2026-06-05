---
name: job-application
description: >
  End-to-end job application workflow. Trigger immediately whenever the user shares a
  job description, job link, or says "here's a role", "I found a job at X", "check this JD",
  "what do you think about this role", "help me apply to X", or pastes text that looks like
  a job posting. Handles everything: fit assessment, company research, narrative, resume
  tailoring, and logging. Do NOT just answer conversationally — always run this full skill.
---

# Job Application Skill

Runs the full job application workflow from fit assessment to tailored resume to database log.
Each step has a human approval gate — do not skip gates or proceed without confirmation.

---

## Source Files

Find these in `Application Engine/` (paths are relative to the project root):

| File | Purpose |
|------|---------|
| `[YOUR_FULL_NAME]_Base_Resume.docx` | Base resume — formatting and structural template |
| `achievement_bank.docx` | Authoritative metrics and achievement inventory |
| `career_interview_transcript.md` | Full narrative and context |
| `application_database.xlsx` | Running application log |
| `resume_strategy.md` | Learned resume strategy by segment — **optional but used if present** |

If `[YOUR_FULL_NAME]_Base_Resume.docx` doesn't exist, stop:
> "You don't have a base resume yet. Run `base-resume-builder` first to create one."

If `achievement_bank.docx` doesn't exist, flag it before proceeding:
> "I notice you don't have an achievement bank yet. Building one first (via
> `career-interview` → `achievement-bank`) will significantly improve the quality of
> tailoring — every resume claim will be grounded in documented, quantified achievements.
> Want to do that now, or proceed with what's available?"
> Wait for their answer. If they want to proceed anyway, continue without the bank.

Replace `[YOUR_FULL_NAME]` with the actual name configured in `CLAUDE.md`.

---

## Workflow — Execute in Order, Human Gates Required

### STEP 1 — Fit Assessment

Run this immediately when a JD is shared. Do not wait for instructions.

**(a) Honest assessment — 3 parts:**
- **Strong fits:** Where the background clearly maps to this role
- **Partial matches:** Things that need framing or recontextualization
- **Genuine gaps:** Requirements not in the background — flag these explicitly, never paper over them

**(b) Creative encouragement pass:**
After the honest assessment, run a second pass:
1. Look for transferable skills — no matter how small — that could honestly map to the role
2. Identify every JD keyword and find every synonym or honest bridge
3. Re-examine partial matches through an optimistic lens: could framing shift this from gap to stretch?
4. Think like a PR consultant — always factual, but always finding the most compelling honest version

**(c) Output: Fit Range**
Express as a range, low end (honest) to high end (most optimistic): e.g., "62–78%"

Then ask: "Want me to research the company before we go further?" **(Gate 1)**

---

### STEP 2 — Strategic Research

*(Gate 1 required)*

Search the web for the company. Focus on:
- **Current business context:** Recent news, earnings (if public), funding, leadership changes,
  restructuring, headcount moves
- **The pain:** Based on JD + company news, what specific business problem is this role solving?
  (e.g., post-merger culture integration, critical talent gaps, scaling for growth, fixing attrition)
- **Strategic priorities:** CEO/CHRO's publicly stated goals for next 12–18 months
- **Fit adjustment:** Does the research change the fit assessment? If so, how?

Output: **Strategic Brief** — 4–6 bullets covering context, the pain, strategic priorities,
and any fit adjustment with rationale.

**Segment Classification (run after the Strategic Brief):**

Using what you now know from the JD and research, classify this opportunity:
- **Company size:** Enterprise (10k+ employees) / Large (1k–10k) / Mid-market (100–1k) / SMB/Startup
- **Role family:** VP-TM / VP-OE / VP-HRBP / VP-HR-Gen / Other
- **Industry:** Tech / Healthcare / Financial Services / Industrial / Consumer / Other

Then check `Application Engine/resume_strategy.md` (if it exists). Pull any guidance
applicable to the matched segments. Note the confidence level and whether it's [DEFAULT]
or [LEARNED]. Carry this into Step 4 — do not surface it here, just load it.

If `resume_strategy.md` doesn't exist, continue with no strategy guidance (Step 4 will
rely on JD-alignment only).

Then ask: "Ready to build the narrative?" **(Gate 2)**

---

### STEP 3 — Narrative

*(Gate 2 required)*

Write one paragraph (20-second elevator pitch equivalent):
- What story does this background tell that maps directly to what this employer needs right now?
- Be specific. Reference the pain from Step 2.
- Do not be generic. "Experienced talent leader" is not a narrative.

Then ask: "Does this narrative land? Adjustments before I move to the resume?" **(Gate 3)**

---

### STEP 4 — Edit List

*(Gate 3 required)*

Review the base resume with recruiter eyes. Ask: "Does this capture attention in 5 seconds?
Does it look like it was written for this specific job?"

**Before listing edits, open with a one-line segment summary:**
> *"This is an [Enterprise / Large / Mid-market / SMB] [Industry] company, [Role Family] role.
> Applying [N] strategy doc guidance items: [list them in one sentence, e.g. 'story-forward
> bullets for mid-market, skills section at top for this role family']. Strategy confidence:
> [Default / Low / Medium / High]."*

If no `resume_strategy.md` exists, skip this line and proceed on JD-alignment only.

---

**For each edit, use this format:**

> **Edit [N]: [Short label]**
> *What to change:* [Specific change — which bullet, which section, exact new language]
> *JD reason:* [Why the JD calls for this — keyword match, emphasis, gap coverage]
> *Strategy reason:* [What the strategy doc says that supports or informs this edit, with
> confidence level. If deviating from the strategy doc, say so explicitly and explain why.]

**If Claude is recommending a deviation from the strategy doc**, flag it clearly:

> **⚠ Override recommendation:** The strategy doc suggests [X] for this segment, but
> this JD signals [specific evidence] which suggests [Y] may perform better here.
> I'm recommending we deviate. You can revert to the default by telling me to apply
> the strategy doc guidance instead.

**Required edits to always consider:**

1. **Headline:** Mirror the JD's exact role title (or closest honest equivalent). A recruiter
   scanning for their requisition should see their title in the first line.

2. **JD-language alignment:** Build a checklist of every skill, competency, and responsibility
   in the JD. For each one the applicant genuinely has, find the corresponding resume bullet
   and reword it to use the JD's own terminology — not synonyms, the actual words.
   (If the JD says "internal mobility," say "internal mobility," not "career movement.")
   Substituting phrasing = allowed. Inventing experience = never.

3. **Achievement upgrades:** Where the achievement bank has stronger metrics than what's
   currently on the resume for a relevant bullet, flag the upgrade.

4. **Section reordering or emphasis shifts:** Driven by both the JD emphasis AND any
   strategy doc structural guidance for this segment (e.g., skills section placement).

5. **Bullet style calibration:** Apply strategy doc guidance on metrics density and
   narrative style for this segment. If the strategy doc has learned that story-forward
   works for this company type, weight toward qualitative framing on the 30–40% of bullets
   where either style is honest. If metrics-heavy is the learned preference, ensure 60–70%+
   have quantified outcomes.

Present the full edit list before asking for approval. Do not build anything yet.

Then ask: "Do these edits make sense? Push back on anything, or tell me to override any
strategy-based recommendation, before I build." **(Gate 4)**

---

### STEP 4.5 — Alignment Check

List all JD-stated skills, competencies, and responsibilities.
Mark each: **Covered / Partially covered / Absent** in the proposed edits.

Flag any genuine strength in the background that the JD names but the edit list hasn't
surfaced yet. Goal: cover every JD-named skill the applicant legitimately has.
Do not manufacture coverage for things they lack.

Report coverage and ask: "Coverage looks like [X covered, Y partial, Z absent] — proceed to build?" **(Gate 5)**

---

### STEP 5 — Build Tailored Resume

*(Gate 5 required)*

1. Open the base resume from `Application Engine/[YOUR_FULL_NAME]_Base_Resume.docx`
2. Make only the agreed edits. Do not rewrite from scratch.
3. Preserve all original formatting, fonts, section structure, and visual style exactly.
4. Save as: `Tailored Resumes/[YOUR_FULL_NAME]_Resume_[CompanyName].docx`
   (use the actual company name — e.g., `Tailored Resumes/Jane_Smith_Resume_Acme.docx`)
5. Present the file to the user.

---

### STEP 5.5 — Save the Job Description

Save the full JD text to: `Job Descriptions/[CompanyName]_JD.md`

If a URL was provided, include it at the top of the file.
This creates a searchable archive of every role pursued.

---

### STEP 6 — Update Application Database

Open `Application Engine/application_database.xlsx`. Add a row with **exactly these column names**:

| Column | Value to enter |
|--------|---------------|
| `Company` | Company name |
| `Title` | Exact title from the JD |
| `Link` | URL if provided, else blank |
| `Posting` | Full JD text |
| `Company_Narrative` | 2–3 sentence summary from Step 2 research |
| `My_Narrative` | The narrative from Step 3 |
| `Fit_Estimate` | The range from Step 1 (e.g., "62–78%") |
| `Date_Found` | Today's date (YYYY-MM-DD) |
| `Date_Tailored` | Today's date if resume was built, else blank |
| `Date_Applied` | **Leave blank** — user fills this in after submitting |
| `Round1_Date` | **Leave blank** |
| `Round2_Date` | **Leave blank** |
| `Round3_Date` | **Leave blank** |
| `Outcome` | "In Progress" |
| `Notes` | Blank |

Save the updated file. Confirm which row was added.

---

## Hard Rules

- **Never overwrite the base resume.** Every tailored version is a new file.
- **Never invent achievements.** Every claim must trace to the achievement bank or career transcript.
- **Never change employment dates.** Dates are fixed facts.
- **2-page maximum** for all tailored resumes (unless the user explicitly overrides).
- **Every gate requires explicit approval** before proceeding to the next step.
- **Headline must mirror the JD's exact title.** No creative reinterpretation.
- **JD language > synonyms.** Use the hiring manager's own words whenever the underlying fact is the same.
