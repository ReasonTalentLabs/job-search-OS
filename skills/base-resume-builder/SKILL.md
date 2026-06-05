---
name: base-resume-builder
description: >
  Builds a polished base resume optimized for a specific role family, drawing from the
  achievement bank and personality profile. Trigger when the user says "build my resume",
  "create my base resume", "build my base", or when setup is complete and they're ready
  to start applying. Reads achievement_bank.docx and personality_superpowers.md.
  Produces [YOUR_FULL_NAME]_Base_Resume.docx in Application Engine/.
---

# Base Resume Builder

Builds the base resume — the foundation document from which every tailored application
will be created. This is not a tailored resume; it's an optimized starting point for a
specific role family that captures the user's strongest positioning and most compelling
achievements.

You may build more than one base resume if the user is targeting meaningfully different
role families (e.g., "VP Talent Management" vs. "VP HR Business Partnering" — these
warrant different bases). Each gets its own file.

**The base resume is sacred.** It is never overwritten. All tailoring creates new files.

---

## Step 1: Read Source Files

Locate and read the following from `Application Engine/`:
- `achievement_bank.docx` — required. If missing:
  > "You don't have an achievement bank yet — that's the foundation this skill builds from.
  > The recommended path is: `career-interview` → `achievement-bank` → then come back here.
  > The career interview takes 60–90 minutes and is the single highest-leverage thing you
  > can do before building your resume. Want to run it now?"
  Stop and wait. Do not proceed without the achievement bank.
- `personality_superpowers.md` — optional but strongly recommended. If missing, note that
  the summary section will be less personality-specific.
- `career_interview_transcript.md` — optional context for anything not in the bank.

---

## Step 2: Define the Target Role Family

Ask (in one conversational message):

- "What type of role is this base resume for? Give me a title or two that represents the
  target. For example: 'VP Talent Management' or 'Senior Director Organizational Effectiveness.'"
- "Is there a particular industry focus, or should this be as broadly applicable as possible?"
- "Do you have an existing resume I can use as a formatting template? If so, share it now.
  If not, I'll work from a clean structure."
- "Any specific requirements — page count, style preferences, sections to include or exclude?"

Do not proceed until you have the target role family and a formatting approach.

---

## Step 3: Achievement Selection

From the achievement bank, select the achievements that will appear on the base resume.

**Selection criteria:**
1. **Relevance to the target role family** — achievements that map to the core competencies
   and responsibilities of the target title. Use the tag taxonomy from the achievement bank.
2. **Strength of the story** — prefer quantified achievements over vague ones. Prefer
   outcomes over activities.
3. **Recency** — generally favor the last 10 years. Older achievements appear only if
   exceptionally strong and not duplicated by more recent ones.
4. **Variety** — don't stack 5 achievements from one competency. Aim for breadth across
   the top 4–5 competency areas the role family demands.
5. **2-page discipline** — be ruthless about what earns a line. Every bullet must justify
   its space.

**For each role on the resume**, select 3–5 bullets max (or 2–3 for older/shorter roles).
The most recent role gets the most real estate.

---

## Step 4: Resume Structure

Build the resume with these sections (adapt if the user has a preferred template):

**Header**
- Full name (prominent)
- Location (City, State — remote-friendly if applicable)
- Email | Phone | LinkedIn URL

**Headline / Professional Title**
- 2–5 words that position them precisely for the target role family
- Mirror the language hiring managers use, not creative alternatives
- Example: "VP, Talent Management & Organizational Effectiveness"

**Professional Summary** (3–4 lines max)
- Lead with scope and scale: how big is the "game" they play?
- Incorporate 1–2 personality superpowers if the profile exists
- Name the 2–3 things they are most known for
- End with a forward-looking hook (what they do for companies)
- No first-person pronouns. No "results-driven leader." Write like a journalist introducing
  a subject, not like a candidate selling themselves.

**Core Competencies** (optional, use if relevant to the role family)
- 8–12 brief skill labels in 2–3 columns
- Use the JD language that hiring managers search for in ATS, not creative rewrites

**Professional Experience** (reverse chronological)
- Company name | Title | Dates (month/year)
- 1 sentence context line if helpful (company size, industry, scope of role)
- 3–5 achievement bullets per role
- Bullet format: strong action verb → what you did (specific) → what resulted (quantified)
- Never start two consecutive bullets with the same verb

**Education**
- Degree, Institution, Year (if within last 20 years)
- Relevant honors, certifications, or notable thesis work only

**Additional** (optional)
- Certifications, board memberships, publications, speaking — only if genuinely differentiating

---

## Step 5: Writing Standards

**Every bullet must pass these tests:**
- Does it start with a strong action verb? (Built, Led, Designed, Reduced, Increased, etc.)
- Does it say what you did, not just that you were responsible for something?
- Does it quantify the outcome? (If not quantifiable, does it clearly describe the scale
  or significance of the result?)
- Could it be on anyone's resume, or does it feel specific to this person's experience?
  Generic bullets get cut or rewritten.

**Language rules:**
- No jargon unless it's the hiring manager's own language
- No acronyms without spelling out at least once
- No passive voice
- Numbers under 10 spelled out ("three programs"), numbers 10+ as numerals ("12 countries")
- Consistent tense: past tense for past roles, present tense for current role

**Personality integration:**
- If `personality_superpowers.md` exists, the summary should reflect the user's actual
  voice and strengths — not a generic executive summary
- One or two bullets across the resume should subtly reflect the signature working style
  (e.g., if a superpower is "builds through relationships," a bullet might note "partnered
  with [N] business unit leaders to co-design...")

---

## Step 6: Build and Save

1. If the user provided a formatting template: preserve fonts, margins, section styles,
   and visual layout exactly. Only change content.
2. If starting fresh: use a clean, ATS-friendly format — single-column or two-column header,
   10.5–11pt body font, consistent heading styles, no tables or text boxes that confuse
   parsers.
3. Name the file: `Application Engine/[YOUR_FULL_NAME]_Base_Resume.docx`
   (replace YOUR_FULL_NAME with the user's actual name from CLAUDE.md)
4. Save it. Present it to the user.

---

## Step 7: Review Gate

Before declaring done, ask:

> "Here's your base resume. A few questions before we lock it:
> 1. Does the headline feel like exactly the right positioning for the roles you're targeting?
> 2. Are there achievements you expected to see that aren't here?
> 3. Is there anything that shouldn't be here, or that feels off?
> I won't start tailoring from this until you've signed off."

Incorporate any feedback and re-save.

---

## After Saving

Tell the user:

> "Base resume locked and saved to `Application Engine/[YOUR_FULL_NAME]_Base_Resume.docx`.
> This is the file the `job-application` skill will tailor every time you find a new role.
> Never share this file directly — always share a tailored version.
>
> You're ready to start applying. Paste a job description anytime and the `job-application`
> skill will handle the rest."

---

## Note on Multiple Base Resumes

If the user is targeting two significantly different role families, they may need two base
resumes. Signs that a second base is warranted:
- Different core competency sections would be needed
- The headline would change meaningfully
- The achievement selection would shift substantially (not just reframing — different stories)

If this comes up: "You might benefit from a second base resume for [role family 2]. Want
to build that now, or come back to it after you've tested this one in the market?"
