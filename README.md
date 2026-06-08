# Job Search OS

A structured, skill-based AI workflow for serious job seekers — built as a plugin for Claude (Anthropic's AI) via the Cowork desktop app.

This isn't a resume template or a prompt collection. It's a complete operating system for your job search: from extracting your career history, to building your achievement bank, to tailoring every application, to learning what's working and adjusting strategy over time.

---

## What You Get

Eight skills that work together as an end-to-end system:

| Skill | What it does | When |
|-------|-------------|------|
| `career-interview` | AI interviews you to extract your complete career history | Once (setup) |
| `achievement-bank` | Converts your interview into a structured, tagged achievement inventory | Once (setup) |
| `personality-interpreter` | Translates a personality/strengths assessment into job-search superpowers | Once (setup) |
| `base-resume-builder` | Builds a polished base resume for your target role family | Once per role family |
| `job-application` | Full application workflow: fit → research → narrative → tailored resume → log | Every application |
| `job-patterns` | Analyzes your application history to surface what's converting | Monthly |
| `interview-sim` | Simulates realistic interviews with structured coaching and debrief | Every interview |
| `strategy-review` | Weekly learning loop: updates resume strategy from accumulated outcomes | Weekly |

---

## Requirements

- A **paid Claude account** (Pro, Team, or Enterprise)
- The **Claude desktop app** with **Cowork mode** — download at [claude.ai](https://claude.ai)
- No coding required

---

## Install the Plugin (30 seconds)

This repo is structured as a Claude plugin. Install it directly from Claude:

```
/plugin marketplace add ReasonTalentLabs/job-search-OS
/plugin install Job-Search-OS@[ReasonTalentLabs]/job-search-OS
```

Once installed, all eight skills are available automatically. Claude will invoke them
based on context — no slash commands needed for most workflows.

---

## Project Setup (Do This Once After Installing)

The plugin installs the skills. You still need to set up your personal project folder,
which is where all your files will live.

### Step 1: Create your project folder

Create a folder on your computer for your job search with these four subfolders:

```
Job Search/
├── Application Engine/
├── Tailored Resumes/
├── Job Descriptions/
└── Interview Notes/
```

### Step 2: Connect the folder in Cowork

Open the Claude desktop app, go to Cowork mode, and connect your `Job Search/` folder
as your workspace. Claude will read and write files here throughout your search.

### Step 3: Add your project configuration

Copy `setup/CLAUDE.md` from this repo into the root of your `Job Search/` folder.
Open it and replace every `[PLACEHOLDER]` with your information:
- Your full name
- Your target role titles
- Your location and work preferences

This file tells Claude who you are and how to behave across all sessions.

### Step 4: Copy the templates

Copy `setup/templates/application-database-columns.md` and
`setup/templates/resume_strategy_template.md` into your `Application Engine/` folder
for reference. Rename `resume_strategy_template.md` to `resume_strategy.md` to
activate the strategy learning loop.

### Step 5: Create your application database

Create a blank Excel file at `Application Engine/application_database.xlsx`.
Add one header row with these exact column names:

```
Company | Title | Link | Posting | Company_Narrative | My_Narrative |
Fit_Estimate | Date_Found | Date_Tailored | Date_Applied |
Round1_Date | Round2_Date | Round3_Date | Outcome | Notes
```

See `setup/templates/application-database-columns.md` for descriptions of each column.

---

## Running the Setup Sequence

With the folder connected, tell Claude: **"Let's get started."** The `career-interview`
skill will take over and walk you through everything.

If you prefer to run steps manually:

**Step A — Career Interview** (30-60 minutes)

> *"Run the career interview."*

Claude interviews you about your entire career — every role, every metric, every
deliverable. Answer using voice-to-text if you prefer. Be thorough: the quality of
everything downstream depends on this.

Output: `Application Engine/career_interview_transcript.md`

---

**Step B — Achievement Bank** (~10 minutes)

> *"Build my achievement bank."*

Claude organizes every achievement from the transcript into a structured, tagged
inventory — the single source of truth for all future resumes and interview prep.

Output: `Application Engine/achievement_bank.docx`

---

**Step C — Personality Interpreter** (optional but recommended)

Upload or paste results from any personality or strengths assessment (CliftonStrengths,
Hogan, DISC, MBTI, Predictive Index, or others) and say:

> *"Run the personality interpreter."*

No formal assessment? Claude will run a short behavioral interview instead.

Output: `Application Engine/personality_superpowers.md`

---

**Step D — Base Resume Builder**

> *"Build my base resume for [target role family]."*

Claude reads your achievement bank and personality profile, builds a polished base resume,
and waits for your approval before locking it. If you're targeting meaningfully different
role families, you can build a separate base resume for each.

Output: `Application Engine/[YOUR_NAME]_Base_Resume.docx`

---

## Daily Use

### Applying for a job

Paste a job description (or a link) into Claude. The `job-application` skill triggers
automatically and runs a five-gate workflow:

1. Fit assessment (honest range + optimistic ceiling)
2. Company research (identifies the business pain this role is solving)
3. Narrative draft (the specific story your background tells for this employer)
4. Edit list with reasoning (JD-language alignment + strategy doc guidance)
5. Tailored resume build

You approve each gate before Claude proceeds.

Outputs: tailored `.docx`, saved JD, and a new row in your application database.

### Interview prep

> *"I have an interview at [Company]. Let's prep."*

Claude simulates the interview in the persona of the actual interviewer type you're
facing, then delivers a structured debrief: what landed, what to sharpen, what your
achievement bank had that you didn't use.

Output: `Interview Notes/[Company]_Interview_Prep.md`

### Weekly strategy review

> *"Run the strategy review."*

Claude reads new entries in your application database, groups outcomes by segment
(company size, industry, role family), identifies conversion patterns with confidence
ratings, and proposes specific updates to your `resume_strategy.md`. Nothing gets
written until you approve it.

### Monthly pipeline analysis

> *"What patterns are you seeing in my applications?"*

Claude surfaces what's converting, where the funnel is breaking down, and where to
adjust targeting.

---

## How the Skills Connect

```
career_interview_transcript.md
        ↓
  achievement_bank.docx ──────────────────────────────────────────┐
        ↓                                                          ↓
personality_superpowers.md                                  interview-sim
        ↓                                                          ↑
  Base_Resume.docx          resume_strategy.md (learning loop)    ↑
        ↓                          ↑         ↓                    ↑
  job-application ────────────────────→ Tailored Resume ──────────┘
        ↓
  application_database.xlsx
        ↓              ↑
  job-patterns    strategy-review (weekly)
```

Every skill reads from and writes to named files in your connected folder. Nothing
is stored in conversation history — your data lives on your computer.

---

## Design Principles

**You own your data.** Everything lives in files on your computer. Claude reads and
writes those files.

**Every resume traces to real evidence.** No claim on a resume can be written unless
it appears in the achievement bank or career transcript. Claude will not invent or
embellish.

**Gates, not automation.** The job-application workflow requires your explicit sign-off
at five points. Speed is not the goal — quality and fit are.

**Advisory, not prescriptive learning.** The strategy doc accumulates signal from your
application outcomes. Claude cites which learnings informed each recommendation and
flags deviations. You can override any recommendation.

**The base resume is sacred.** It is never overwritten. Every tailored version is a
new file.

---

## Repo Structure

```
ai-job-search-system/
├── .claude-plugin/
│   └── plugin.json          ← plugin manifest
├── skills/
│   ├── career-interview/
│   ├── achievement-bank/
│   ├── personality-interpreter/
│   ├── base-resume-builder/
│   ├── job-application/
│   ├── job-patterns/
│   ├── interview-sim/
│   └── strategy-review/
├── setup/
│   ├── CLAUDE.md            ← copy to your Job Search/ folder
│   └── templates/
│       ├── application-database-columns.md
│       └── resume_strategy_template.md
└── README.md
```

---

## FAQ

**Do I need to be technical?**
No. You're not writing code. The only manual steps are filling in placeholders in
`CLAUDE.md` and creating a blank Excel file with the right column headers.

**What if I don't have a personality assessment?**
The `personality-interpreter` skill includes a behavioral interview option. Claude
asks you six questions and synthesizes your superpowers from your answers.

**Can I use my existing resume?**
Yes — `base-resume-builder` will ask if you have one to use as a formatting template.
It preserves your layout and replaces the content.

**How long does setup take?**
Career interview: 60–90 minutes. Everything else: 10–30 minutes each. Total: 2–3
hours, usually spread across one or two sessions.

**What if I'm targeting multiple role types?**
Build a separate base resume for each. `base-resume-builder` will flag when this is
warranted. `job-application` can tailor from any base you point it to.

**How do I update my achievement bank after a promotion or big project?**
Re-run `career-interview` (choose "update" when prompted), then re-run `achievement-bank`.

---

## Contributing

Built by Chris Coultas, PhD, Founder and Principal at Reason Talent (www.reasontalent.com)
and a senior HR executive during an active VP-level job search. If you use it
and build improvements — new skills, better prompts, workflow refinements — pull
requests are welcome.

---

## License

MIT. Use it, adapt it, share it.
