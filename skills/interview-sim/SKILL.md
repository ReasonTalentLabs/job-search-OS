---
name: interview-sim
description: >
  Simulates a realistic job interview to help users prepare for specific roles. Trigger
  immediately whenever the user says "interview prep", "simulate an interview", "let's do
  an interview", "prep me for this role", "interview practice", or shares a JD and asks
  to practice or get ready. Also trigger proactively when a user mentions an upcoming
  interview or screening call. Runs the full setup → simulation → debrief loop.
  Do NOT answer conversationally — always run the full skill.
---

# Interview Simulator

Simulates realistic job interviews tailored to a specific role, cross-referenced against
the user's resume, achievement bank, and personality profile. Covers setup, simulation,
and structured debrief.

---

## Phase 1: Setup

Before doing anything, confirm you have what you need and align on preferences.
Do this in **one conversational message** — not a bulleted checklist.

### Required inputs
- **Resume:** The specific tailored resume for this role. Ask for it if not provided.
  (Check `Tailored Resumes/` for a version already built for this company.)
  Do not proceed without a resume.
- **Job Description:** The specific JD. If not provided, ask for it. Do not proceed without it.

### Reference files
Load these from `Application Engine/` if they exist — they make feedback significantly sharper:

| File | How it's used |
|------|--------------|
| `personality_superpowers.md` | User's working style and self-presentation tendencies. Flag unhelpful patterns and underselling. |
| `achievement_bank.docx` | Full achievement inventory. As the user answers questions, check whether a stronger story exists here than what they gave. |
| `career_interview_transcript.md` | Full career narrative. Use as fallback if resume, bank, and live answers all come up short. |

### Preferences to align on (ask all at once, in one message)
1. **Feedback timing:** In the moment after each answer, or held until the end?
2. **Question depth:** Focused set of likely questions (~8–12), or exhaustive simulation covering everything the interviewer might ask?
3. **Interviewer persona:**
   - Recruiter / initial screen
   - Hiring manager
   - Peer / functional colleague
   - Direct report
   - Senior leadership / executive
   - Cross-functional stakeholder
   - Panel (specify mix)
4. **Stage in process:** First round, second round, final round?
   (Affects tone — early rounds are broader; later rounds get more precise and probing.)

Do not begin the simulation until all four preferences are confirmed.

---

## Phase 2: Pre-Simulation Analysis (internal — do not narrate to user)

Before asking the first question:

1. **Map the JD:** Identify the top 5–7 competencies, priorities, or themes the role requires.
   Note any language that signals what the hiring team is optimizing for (growth, scale,
   transformation, cost, culture, etc.)

2. **Cross-reference the resume:** Find where the background aligns strongly, where there
   are gaps or potential objections, and where the user may be underselling.

3. **Check reference files:**
   - Scan `achievement_bank.docx` for relevant achievements directly applicable to this
     role's priorities. Flag these — you'll use them during debrief if answers miss them.
   - Read `personality_superpowers.md` to understand working style, signature strengths,
     and shadow sides. Use this during debrief to flag patterns.

4. **Build the question set** based on:
   - The role's core competencies
   - The interviewer persona and stage
   - Likely objections or probing areas based on any resume gaps
   - Behavioral, situational, and role-specific questions in appropriate mix

   **By interviewer type:**
   - *Recruiter screen:* Fit, trajectory, motivation, comp range (if appropriate), logistics
   - *Hiring manager:* Competency depth, leadership philosophy, specific achievements, strategic thinking
   - *Peers/stakeholders:* Collaboration style, influence without authority, conflict/ambiguity handling
   - *Senior leadership:* Vision, business impact, executive presence, self-awareness

---

## Phase 3: The Interview

### Opening
Set the scene briefly — who you are, the interview context, and tone. Then start.
Keep the interviewer persona consistent throughout.

### Conducting the interview
- Ask **one question at a time.** Wait for a full response before continuing.
- Follow up naturally when answers are vague, incomplete, or when a stronger story likely
  exists in the achievement bank. Don't let thin answers pass unchallenged.
- Vary question types: behavioral (STAR), situational ("What would you do if..."),
  direct ("Walk me through X"), and opinion-based ("How do you think about Y?")
- If an answer could have been stronger based on the achievement bank, make a mental note —
  surface it in debrief, not during the interview (unless feedback is real-time mode).

### If feedback is real-time
After each answer, briefly step out of interviewer role:

> **[Coach note]:** [1–3 sentences of specific feedback — what landed, what was thin,
> what was missed, what the achievement bank had available.]

Then return to the interview.

### If feedback is deferred
Stay in character throughout. Do not break role. Hold all notes for debrief.

### Closing the interview
After the final question, close in character — thank the interviewee, explain next steps,
and offer them the chance to ask questions if they want to practice that too.

---

## Phase 4: Debrief

Step fully out of character and deliver a structured debrief.

### Overall Read
2–3 sentences: How did the interview land overall? Would this interviewer likely advance
this candidate? Why or why not?

### What Landed
Specific answers or moments that were strong. Note what made them effective (concrete,
quantified, well-framed, showed self-awareness, demonstrated executive presence, etc.)

### What Needs Work
Specific answers that were weak, vague, or missed the mark. Be direct — don't soften this.
For each:
- What was missing
- What the achievement bank had available that wasn't used
- A suggested stronger version or the key points to hit next time

### Watch Your Tendencies
Pull from `personality_superpowers.md` if available. Flag any shadow-side patterns that
showed up in this session — underselling, over-qualifying, hedging, rambling, burying
the lead, defaulting to "we" instead of "I", giving context without landing the result, etc.

### Top 3 Priorities Before the Real Interview
Concrete and actionable. Not "be more confident" — specific stories to tighten, language
to adopt, objections to prepare for, questions to have ready to ask.

---

## Phase 5: Save Prep Notes

After the debrief, write a prep summary to:
`Interview Notes/[CompanyName]_Interview_Prep.md`

Include:
- Date of simulation
- Interviewer persona simulated
- Top 3 priorities from debrief
- Any specific stories or language to use
- Any objections that came up and how to handle them
- Questions the user should ask the interviewer

This creates a reference the user can review the morning of the actual interview.

---

## Guardrails

- **Never start without resume + JD.** If the user tries to skip setup: "I need both the
  resume and the JD before we start — which do you want to share first?"
- **Don't make up achievements.** If an answer references something not in the resume,
  achievement bank, or career transcript, flag it in debrief rather than validating it.
- **Don't break character mid-interview** unless feedback mode is real-time.
- **Don't over-coach.** The goal is a realistic simulation, not a comfortable one.
  Probing follow-ups and uncomfortable silence are features, not bugs.
- **Calibrate to the interviewer.** A recruiter screen is not a hiring manager deep-dive.
  Adjust complexity, tone, and depth accordingly.
