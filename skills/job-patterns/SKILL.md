---
name: job-patterns
description: >
  Analyzes job application history to surface what's working, what isn't, and where to
  shift strategy. Trigger when the user says "what's working", "review my applications",
  "analyze my search", "am I getting interviews", "what should I change", "what patterns
  do you see", "job search retrospective", or "search strategy review". Reads
  application_database.xlsx and surfaces patterns across titles, companies, fit scores,
  and outcomes. Always run this skill — never guess from memory.
---

# Job Patterns — Application Analytics

Reads the application database and surfaces what's working, what isn't, and where to
adjust strategy. Designed to run every few weeks throughout an active search.

---

## Data Source

Read `Application Engine/application_database.xlsx`.

**Expected columns** (these match exactly what `job-application` writes):

| Column | What it contains |
|--------|-----------------|
| `Company` | Company name |
| `Title` | Exact job title from the posting |
| `Link` | URL to posting |
| `Posting` | Full JD text |
| `Company_Narrative` | What this company needs right now |
| `My_Narrative` | Why this applicant fits |
| `Fit_Estimate` | Score range e.g. "62–78%" |
| `Date_Found` | Date role was found (YYYY-MM-DD) |
| `Date_Tailored` | Date resume was tailored (YYYY-MM-DD) |
| `Date_Applied` | Date submitted (YYYY-MM-DD) |
| `Round1_Date` | First interview date |
| `Round2_Date` | Second interview date |
| `Round3_Date` | Third interview date |
| `Outcome` | In Progress / Offer / Rejected / Withdrew / No Response |
| `Notes` | Free text notes |

If the file doesn't exist, stop: "No application database found at
`Application Engine/application_database.xlsx`. Start applying with the `job-application`
skill and check back after a few applications."

If fewer than 5 applications exist, note this upfront: "You have [N] applications — that's
a very small sample. I'll surface what I can, but hold conclusions loosely until you have
at least 10–15."

---

## Analysis Framework

Run all six analyses. Surface findings in the output format below.

---

### 1. Pipeline Health

- Total applications in database
- Applied (Date_Applied filled in) vs. not yet applied (backlog)
- Tailored (Date_Tailored filled in) vs. untailored at time of application
- Average days from Date_Found to Date_Applied
- Average days from Date_Applied to Round1_Date (for roles that reached Round 1)

**Flag:** If backlog > 5 unapplied roles, surface as priority action item.
**Flag:** If any applications were submitted without tailoring, note the count.

---

### 2. Title & Role Patterns

- What title categories are in the pipeline? Group by title family
  (e.g., "VP Talent Management", "Sr. Director OE", "VP HRBP")
- Which title categories are advancing to Round 1+?
- Which title categories are generating zero responses after 5+ applications?
  Flag for strategy review.
- Is there a title where the fit estimates are consistently low (below 60%)?
  That may signal poor targeting.

---

### 3. Company Type Patterns

- Industry breakdown of applications
- Company size / type breakdown (public/private, startup/enterprise, etc.)
  — infer from company names and JD context where possible
- Which company types are advancing further in the process?
- Any industry or company type consistently reaching Round 2+?
  That's a signal to weight the search toward similar orgs.

---

### 4. Fit Score vs. Outcome Correlation

Parse the `Fit_Estimate` column. Extract the midpoint of each range (e.g., "62–78%" → 70).

- Are high fit-estimate roles (midpoint 75+) converting to interviews at higher rates?
- Are low fit-estimate roles (midpoint below 65%) converting at all?
- Is there a sweet spot fit range that correlates with interview conversion?
- Are there roles with high fit estimates that didn't convert? That may signal a resume
  or narrative issue, not a targeting issue.

**Note:** With small sample sizes, express uncertainty. "3 of the 4 roles that reached
Round 1 had fit scores above 70, but with N=4 this is suggestive, not conclusive."

---

### 5. Resume Tailoring vs. Outcome

- Applications with tailored resumes vs. base resume — any difference in Round 1 rate?
- If tailored resumes aren't converting at higher rates, flag for resume strategy review.
- Look at tailoring timing: were any resumes tailored after applying? Flag those as
  a workflow issue.

---

### 6. Interview Progression

- Roles that reached Round 1 (`Round1_Date` filled)
- Of those, roles that reached Round 2 (`Round2_Date` filled)
- Of those, roles that reached Round 3 or final (`Round3_Date` filled)
- Conversion rate: Applied → Round 1, Round 1 → Round 2, Round 2 → Round 3
- Review `Notes` column for any patterns in what came up in interviews (common objections,
  what went well, what didn't)
- Review `Outcome` column — any patterns in rejections? (If documented in Notes)

---

## Output Format

Present findings in this structure:

---
**JOB SEARCH PATTERN ANALYSIS**
*Based on [N] total applications, [N] with outcome data*
*Data through: [MOST RECENT Date_Applied]*

**PIPELINE SNAPSHOT**
Applications: [N total] | Applied: [N] | Backlog: [N unapplied]
Tailored: [N] | Untailored: [N]
Avg. time to apply: [N days from found to submitted]
[Flag any pipeline issues]

**WHAT'S WORKING**
[2–3 specific patterns with data support. E.g., "VP Talent Management roles at
enterprise tech companies are your strongest conversion category — 3 of 5 reached
Round 1."]

**WHAT'S NOT CONVERTING**
[2–3 specific patterns. E.g., "Roles in healthcare have generated 8 applications and
0 Round 1 callbacks. Consider whether the industry language in your resume is translating."]

**FIT SCORE REALITY CHECK**
[What the fit score distribution looks like vs. what's converting.
Are you targeting the right difficulty level?]

**INTERVIEW FUNNEL**
Applied → Round 1: [X%]
Round 1 → Round 2: [X%]
Round 2 → Round 3: [X%]
[Any patterns in what advances vs. stalls]

**STRATEGIC RECOMMENDATIONS**
[3–5 concrete, actionable adjustments. Not "apply more" — specific changes to title
targeting, company type focus, resume strategy, or narrative framing. Each recommendation
should connect to a specific data finding above.]

**CONFIDENCE LEVEL**
[Be explicit: "With [N] applications, these are early-signal patterns. [X] of the
recommendations are high-confidence; [Y] should be tested before over-indexing."]
---

## After the Analysis

Ask:
"Want to dig into any of these patterns in more depth, or adjust your targeting strategy
based on what we're seeing?

If a resume issue is surfacing, suggest: "Try running `job-application` on a recent
non-converting role with a different narrative angle to see if reframing changes the picture."

If a title targeting issue is surfacing, suggest: "You might want to weight your search
more toward [title family that's converting] and less toward [title family with 0 conversion]."
