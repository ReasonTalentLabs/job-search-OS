---
name: personality-interpreter
description: >
  Interprets a personality or strengths assessment and extracts job-search superpowers.
  Trigger when the user uploads or pastes personality assessment results, or says
  "interpret my assessment", "analyze my personality results", "what are my superpowers",
  or "run personality interpreter". Produces personality_superpowers.md in Application Engine/.
---

# Personality Interpreter

Takes any personality, strengths, or behavioral assessment result and translates it into
practical job-search language: what makes you distinctive, how you lead, how to talk about
yourself authentically, and what role types will play to your natural strengths.

**Supported assessments (and others):**
- DRiV (take it free at https://reasontestdriv.driv.lwfinsights.com/driv/)
- CliftonStrengths / StrengthsFinder
- Hogan (HPI, HDS, MVPI)
- DISC
- Myers-Briggs / MBTI
- Predictive Index (PI)
- Enneagram
- 360 feedback reports
- Custom leadership or culture fit assessments
- No formal assessment (interview-based, see below)

---

## Step 1: Get the Assessment

Ask the user to either:
1. Upload the assessment report (PDF, screenshot, or document)
2. Paste their results or scores directly
3. If they don't have a formal assessment: offer to conduct a light behavioral interview
   (see "No Assessment Option" at the bottom of this skill)

Once you have the material, read it fully before responding.

---

## Step 2: Calibrate to Job Search Context

Before interpreting, ask (in one message, not a list):
- "What role types are you targeting?" (If it's in CLAUDE.md, skip this question.)
- "Is there anything about how you show up professionally — good or bad — that you feel
  your resume or interviews don't capture?"
- "Have you ever received feedback about your leadership style, communication, or working
  style that surprised you?"

These answers sharpen the interpretation toward what actually matters for their search.

---

## Step 3: Interpret the Assessment

For each major dimension or theme in the assessment, extract:

**The raw finding** — what the assessment literally says

**Job-search translation** — what this actually means in a hiring context. Avoid
assessment jargon. Translate "Maximizer" into "drives quality standards and upgrades
what exists rather than building from scratch." Translate "High Dominance" into "moves
quickly, makes decisions, and expects the same from others."

**The superpower** — the version of this trait that is a genuine competitive advantage
for their target roles. Specific, not generic. Not "strong leader" — "moves large,
complex organizations through change without losing the people."

**The shadow side** — where this trait can work against them. Every strength has a
shadow. Name it honestly. This helps them self-manage and answer "what's your biggest
weakness" questions authentically.

**How to talk about it** — actual language they can use in interviews or cover letters
that is both authentic and strategically positioned.

---

## Step 4: Synthesize the Superpowers

After interpreting individual dimensions, synthesize into 3–5 "superpower" themes —
the things that make this person distinctively valuable in their target roles.

Format each superpower as:
- **Name**: A short, memorable label (2–4 words)
- **What it means**: 2–3 sentences on what this looks like in practice
- **Where it shows up most**: The role situations, contexts, or challenges where this
  strength is most valuable
- **The evidence**: Point to 1–2 specific career examples (cross-reference `achievement_bank.docx`
  if it exists) that illustrate this superpower in action
- **Interview language**: A sentence or two they can say naturally in an interview

---

## Step 5: Role Fit Implications

Given their superpowers and shadow sides, assess:

**High-fit role environments** — where this person will thrive (e.g., "transformation
contexts where there's a clear problem and room to build," "large, complex organizations
that need someone to operate with ambiguity and drive alignment across functions")

**Watch out for** — role types or environments where their profile is likely to chafe
(e.g., "highly political bureaucracies where influence requires slow consensus-building,"
"roles defined purely by execution without strategic input")

**Interview positioning** — 2–3 sentences on how to frame their profile to land with
different interviewer types (e.g., "With an operations-oriented hiring manager, lead
with the business outcomes. With a CHRO, lead with the capability-building narrative.")

---

## Output

Write the file `Application Engine/personality_superpowers.md`:

```markdown
# Personality & Strengths Profile
*[YOUR_FULL_NAME]*
*Assessment: [ASSESSMENT NAME AND VERSION]*
*Interpreted: [TODAY'S DATE]*

---

## Assessment Summary
[2–3 paragraph overview of key findings from the raw assessment]

---

## Superpower 1: [Name]
**What it means:** [Description]
**Where it shows up most:** [Contexts]
**Career evidence:** [Examples]
**Interview language:** "[Exact language they can use]"
**Shadow side:** [Where it can work against them + how to manage it]

## Superpower 2: [Name]
[same format]

## Superpower 3: [Name]
[same format]

[Continue for all superpowers identified]

---

## Role Fit Implications

### High-fit environments
[Description]

### Watch out for
[Description]

### Interview positioning
[Guidance for different interviewer types]

---

## Raw Assessment Notes
[Full interpretation of each assessment dimension, for reference]
```

Confirm the file was saved and tell the user:
> "Superpowers profile saved to `Application Engine/personality_superpowers.md`.
> Your top superpowers are: [list them].
> Next: Run `base-resume-builder` to build your base resume."

---

## No Assessment Option

If the user doesn't have a formal assessment, run a 10-minute behavioral interview instead:

Ask these questions (one at a time):
1. "When you're at your best at work — when everything clicks and you lose track of time —
   what are you doing?"
2. "What do people consistently come to you for that they don't go to others for?"
3. "What's a piece of feedback you've received more than once about how you show up?"
4. "When you're in a tough situation at work — high stakes, unclear path — what do you
   naturally do first?"
5. "What kind of work do you find draining, even if you're technically good at it?"
6. "If your best work colleague described you to someone who'd never met you, what would
   they say?"

From the answers, synthesize superpowers using the same format above, noting that these
are self-reported rather than assessment-derived.
