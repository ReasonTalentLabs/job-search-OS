---
name: achievement-bank
description: >
  Converts a career interview transcript into a structured achievement bank document.
  Trigger when the user says "build my achievement bank", "create my achievement bank",
  "convert the transcript", or immediately after the career-interview skill completes.
  Reads career_interview_transcript.md, produces achievement_bank.docx in Application Engine/.
---

# Achievement Bank Builder

Takes the raw career interview transcript and produces a comprehensive, structured achievement
bank — the single source of truth for every accomplishment, metric, and deliverable in the
user's career. Every future resume, cover letter, and interview prep session pulls from this file.

**The guiding principle:** If an achievement is real, it belongs here. No achievement is too
small, too old, or too role-specific to include. Breadth now saves time later.

---

## Input

Read `Application Engine/career_interview_transcript.md`.

If the file doesn't exist, stop and say: "I don't see a career interview transcript yet.
Run the `career-interview` skill first to generate it, then come back."

If the file exists but is very short (fewer than 500 words), flag this:
"The transcript looks thin — it may not have captured enough depth. The achievement bank
will only be as good as the interview. Do you want to run `career-interview` again before
we build the bank?"

---

## Achievement Extraction Logic

For every role in the transcript, extract:

**Quantified achievements** — anything with a number attached:
- Percentage improvements (engagement, retention, time-to-fill, cost, etc.)
- Dollar amounts (savings, budget managed, revenue impact)
- Headcount (team built, workforce affected, org scale)
- Timeframes (delivered X in Y months)
- Scale (global, multi-site, enterprise-wide)

**Qualitative achievements** — things without hard numbers that are still meaningful:
- Programs or functions built from scratch
- Organizations restructured or turned around
- Technology or processes implemented
- Culture changes led
- Relationships built (board access, C-suite partnerships, cross-functional influence)
- External recognition (awards, publications, speaking, patents)

**Leadership signal** — evidence of leadership capability:
- Decision-making under ambiguity
- Stakeholder management complexity
- Scope of influence (matrixed, cross-functional, global)
- Situations they inherited vs. situations they created

For each achievement, capture:
1. **The situation** (what was the business context/problem)
2. **The action** (what they specifically did — not "we", not "the team")
3. **The result** (quantified if possible)
4. **The scale** (how big was the impact — individual, team, org, company, industry)
5. **Tags** (competency areas this maps to — see tag list below)

---

## Tag Taxonomy

Tag every achievement with 1–3 of the following so they're searchable by JD requirement:

- `talent-management` — performance, succession, career development, talent review
- `org-effectiveness` — org design, change management, culture, workforce planning
- `learning-development` — L&D programs, leadership development, training
- `talent-acquisition` — recruiting, employer brand, hiring strategy
- `hrbp` — HR business partnership, executive advising, org consulting
- `people-analytics` — data, measurement, dashboards, workforce insights
- `executive-development` — C-suite coaching, senior leader programs, succession
- `scale` — built something from scratch or scaled an existing function
- `transformation` — drove significant change in a org, culture, or business
- `leadership` — built/led teams, managed managers, led cross-functional work
- `global` — international scope, multi-country, cross-cultural complexity
- `financial-impact` — direct cost, revenue, or ROI connection
- `technology` — HCM systems, people tech, digital transformation
- `stakeholder` — board, C-suite, or complex stakeholder navigation

---

## Output Format

Write the file `Application Engine/achievement_bank.docx` with this structure:

---

**ACHIEVEMENT BANK**
*[YOUR_FULL_NAME]*
*Last updated: [TODAY'S DATE]*
*Source: Career interview transcript, [INTERVIEW DATE]*

---

**HOW TO USE THIS DOCUMENT**
This is your complete career achievement inventory. When tailoring a resume or preparing
for an interview, search this document by tag or keyword to find the strongest story
for each job requirement. Never add new claims here that aren't grounded in actual experience.
To update, re-run the `career-interview` skill and then this skill.

---

**ACHIEVEMENT BANK — [ROLE TITLE] at [COMPANY]**
*[START DATE] – [END DATE]*

**[Achievement Title — short, punchy label]**
- Situation: [context]
- Action: [what they did]
- Result: [outcome, quantified where possible]
- Scale: [scope of impact]
- Tags: [tag1, tag2, tag3]

[Repeat for each achievement in this role]

---
[Repeat section for each role, most recent first]

---

**CROSS-ROLE STRENGTHS**
[3–5 paragraphs summarizing the recurring themes and signature strengths across all roles —
what this person consistently does well regardless of context]

**SKILLS & EXPERTISE INVENTORY**
[Structured list: Hard skills / Methodologies / Tools & Systems / Domain expertise]

**ACHIEVEMENTS NOT ON CURRENT RESUME**
[Anything surfaced in the interview that hasn't appeared on previous resumes — flag these
explicitly so they get considered during tailoring]

---

## Quality Check Before Saving

Before writing the file, verify:
- Every role from the transcript has at least one achievement entry
- At least 60% of achievements have a quantified result (if fewer, flag which roles need more data)
- Tags are applied to every achievement
- The "Cross-Role Strengths" section identifies 3–5 genuine patterns (not generic platitudes)

If the bank has fewer than 15 total achievements, flag it:
"The bank has [N] achievements — that's on the thin side. Consider re-running the career
interview to surface more depth before tailoring resumes."

---

## After Saving

Confirm the file was written and tell the user:

> "Achievement bank saved to `Application Engine/achievement_bank.docx`. Here's a quick summary:
> - [N] total achievements across [N] roles
> - Strongest tag clusters: [top 3 tags by count]
> - [N] achievements not currently on your resume (flagged for consideration)
>
> Next: Run `personality-interpreter` if you have a personality assessment to upload,
> or go straight to `base-resume-builder` to build your base resume."
