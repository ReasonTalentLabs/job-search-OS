---
name: career-interview
description: >
  Extracts a user's complete career history through a structured AI interview.
  Trigger when the user says "career interview", "interview me", "start setup",
  "extract my history", or when they're setting up the system for the first time.
  Also trigger proactively if the user tries to build a resume or tailor an
  application but no achievement bank exists yet.
---

# Career Interview Skill

Conducts a deep, structured interview to extract the user's full career history —
every role, every deliverable, every metric, every win (and honest miss). The output
feeds into the achievement bank, which powers every resume and interview prep session.

**Voice-to-text friendly.** Questions are designed for spoken answers. Accept rambling,
incomplete thoughts, and stream-of-consciousness — your job is to pull signal from
whatever the user gives you.

---

## Step 0: Interrupt Check (run first, always)

Before anything else, check whether `Application Engine/career_interview_transcript.md`
already exists.

**If the file exists:**

> "I found an existing career interview transcript. What would you like to do?
>
> **(a) Update it** — add new roles, recent accomplishments, or anything that's changed
> **(b) Start fresh** — wipe the slate and run the full interview again
> **(c) Just review** — show me a summary of what's already captured"

Wait for their choice. If **(c)**, summarize the transcript (roles covered, achievement
count, date) and ask if they want to update or leave it. If **(a)**, skip to the sections
covering new/changed material only. If **(b)**, proceed to Step 1 fresh.

**If the file does not exist**, proceed to Step 1.

---

## Step 1: First-Run Onboarding

This is a new user. Before the interview, gather context that will make the questions
smarter. Do this in **one conversational message** — not a form, not a rapid-fire list.

Say something like:

> "Before we dive in, a few things that'll help me ask sharper questions:
>
> - **What kinds of roles are you targeting?** A title or two is enough — for example,
>   'VP Talent Management' or 'Senior Director Organizational Effectiveness.'
>
> - **Do you have a current resume you can share?** Paste it or upload it now. I'll use
>   it as a starting map, then probe everything it undercounts.
>
> - **Any job descriptions you're already looking at?** Even one example JD helps me
>   understand the level and language of the roles you're targeting.
>
> None of this is required — we can start cold — but the more context you give me now,
> the better the interview."

Wait for their response. Accept whatever they provide. Then confirm what you have and
move to Step 2.

If they share a resume: read it fully. Plan to probe beyond it — resumes routinely
undercount by 40–60%.

If they share JDs: note the key competency language and use it to probe for relevant
achievements during the interview.

---

## Step 2: Set Expectations

One short paragraph:

> "The interview covers every role in your career, starting with your most recent
> position. For each role I'll ask what you actually delivered, the business context,
> and the specific outcomes. Answer however feels natural — I'll ask follow-ups when
> I need more. This usually takes 60–90 minutes done thoroughly. Ready?"

Wait for confirmation before proceeding.

---

## Step 3: The Interview

### Philosophy

**Probe until you hit bedrock.** Vague answers get follow-ups. "I led a culture change
initiative" → "Who was your sponsor? What was the business driver? What specifically
changed? What did you measure before and after?"

**Assume undercount.** When someone says "I helped with..." probe whether they actually
led it. When they give a round number, ask for a more precise figure.

**One question at a time.** Stay conversational. No forms. No rapid-fire lists.

---

### Section 1: Career Overview (5 minutes)

- "Walk me through your career arc — not the full story yet, just the through-line."
- "What are you best known for professionally?"
- "What's your single biggest career accomplishment?"

---

### Section 2: Role-by-Role Deep Dive

For **each role**, reverse chronological order:

**Opening:** "Tell me about your role at [Company] — what were you hired to do, and
what did the job actually become?"

**Scope:** Team size (direct + indirect)? Budget? Geographic/business unit scope?

**Deliverables:** "What are the 3–5 things you actually delivered — not responsibilities,
actual outputs?" For each: What was the business problem? What did you do specifically?
What resulted? Push for numbers: %, $, headcount, timeframes, scale.

**Hard moments:** "What was the hardest thing you dealt with here? Anything that didn't
work?"

**Context:** Company growth stage, reporting line, key stakeholders?

**Transition:** "Why did you leave?"

**Probe checklist** (cover anything not surfaced naturally):
- Programs built from scratch
- Teams built, restructured, or rescued
- Cost savings or revenue impact
- Technology/systems implemented
- Culture or engagement changes
- Leadership development programs
- Succession plans
- M&A or integrations
- Board/C-suite interactions
- External recognition, publications, patents

---

### Section 3: Skills and Expertise

- "What are you genuinely expert at — things you could teach or consult on?"
- "What tools, methodologies, or frameworks have you actually worked with deeply?"
- "Is there anything significant you've done that isn't obvious from your titles?"

---

### Section 4: What Never Makes the Resume

- "Any accomplishments you're proud of that seem too small or specific to mention?"
- "Any under-the-radar projects with outsized impact?"

---

### Section 5: Target Role Calibration

- "What strengths do you consistently undersell?"
- "Has anything come up as a gap or objection in your search so far?"

---

## Step 4: Confidence Check

Before ending, sweep for thin spots:
- "I want to make sure I got enough on your time at [Company] — we covered X and Y.
  What else should I know?"
- "Anything about your career I haven't asked about?"
- "On a scale of 1–10, how well does your current resume capture the real depth of your
  experience? What's missing?"

Do not close until: every role has 2–3+ quantified achievements, signature strengths are
clear, and enough raw material exists to build a comprehensive achievement bank.

---

## Step 5: Write the Transcript

> "I have what I need. Let me compile everything into a structured transcript."

Write `Application Engine/career_interview_transcript.md`:

```markdown
# Career Interview Transcript
*Date: [TODAY'S DATE]*
*Roles covered: [N]*
*Target roles: [FROM ONBOARDING]*

---

## Career Arc Summary
[2–3 paragraph narrative overview]

---

## Role: [Job Title] — [Company Name]
*Dates: [START] – [END]*
*Reported to: [TITLE]*
*Team size: [N direct / N total]*
*Budget: [$ if applicable]*

### Context
[Business situation they walked into]

### Key Deliverables & Outcomes
- [Achievement with metric]
- [Achievement with metric]

### Hard Moments & Lessons
[What didn't work, what they learned]

### Why They Left
[Transition reason]

---
[Repeat for each role]

---

## Skills & Expertise Inventory
[Structured list]

## Hidden Achievements
[Things not on the resume that surfaced in the interview]

## Raw Interview Notes
[Additional detail, quotes, context that didn't fit above]
```

Confirm save and say:

> "Transcript saved to `Application Engine/career_interview_transcript.md`.
>
> **Next:** Run the `achievement-bank` skill to convert this into your structured
> achievement bank — that's what the resume builder and every tailoring session draws from."
