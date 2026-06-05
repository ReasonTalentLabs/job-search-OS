---
name: strategy-review
description: >
  Weekly learning loop. Reads new application database entries, identifies patterns by
  segment, proposes specific updates to resume_strategy.md, and writes approved changes.
  Trigger when the user says "run strategy review", "what have we learned", "update my
  strategy", or on a weekly scheduled basis. Never auto-updates the strategy doc —
  always proposes changes and waits for human approval first.
---

# Strategy Review Skill

Reads your application history, groups outcomes by segment, identifies what's converting
and what isn't, and proposes specific, data-backed updates to `resume_strategy.md`.

Nothing gets written to the strategy doc until you approve it. You can accept a proposed
update, reject it, or modify the language before it's committed.

---

## Step 1: Load the Data

Read both files:
- `Application Engine/application_database.xlsx` — required
- `Application Engine/resume_strategy.md` — required

If either file is missing, stop and say which one is absent and how to create it.

Check the Review History table in `resume_strategy.md` to find the date of the last review.
- If there's been a prior review: analyze only rows where `Date_Applied` is after the last
  review date. Say upfront: "Analyzing [N] new applications since your last review on [DATE]."
- If there's never been a review: analyze the full database.

If there are fewer than 5 new applications since the last review, note this: "You have
[N] new applications since the last review — that's a thin sample. I can still surface
patterns, but hold them loosely."

---

## Step 2: Classify Each Application by Segment

For each application, infer the segment from the `Company`, `Title`, and `Company_Narrative`
columns:

**Company size** — infer from Company_Narrative or web context:
- `Enterprise` — 10,000+ employees, F500/F1000, publicly traded majors
- `Large` — 1,000–10,000 employees
- `Mid-market` — 100–1,000 employees
- `SMB/Startup` — under 100 employees or clearly early-stage

**Role family** — infer from `Title`:
- `VP-TM` — titles containing Talent Management, Talent Strategy, Talent Development
- `VP-OE` — titles containing Org Effectiveness, Org Design, Workforce Planning
- `VP-HRBP` — titles containing HR Business Partner, HRBP, People Partner
- `VP-HR-Gen` — VP HR, CHRO, Chief People Officer, Head of People
- `Other` — anything else

**Industry** — infer from `Company` and `Company_Narrative`:
- `Tech` / `Healthcare` / `Financial Services` / `Industrial` / `Consumer` / `Other`

**Outcome classification:**
- Converted = `Round1_Date` is filled (got an interview)
- Did not convert = `Date_Applied` is filled, `Round1_Date` is blank, and either
  `Outcome` is "Rejected" or "No Response", or enough time has passed (30+ days)
- Too early to call = `Date_Applied` is recent (under 30 days) and no outcome yet

Build a segment matrix. For each segment with 3+ applications, compute:
- Total applied
- Total converted (reached Round 1)
- Conversion rate
- Any Round 2+ progression

---

## Step 3: Pattern Analysis

For each segment with enough data (3+ applications, at least one conversion or clear
non-conversion pattern), look for the following. Reference the `Notes` column and
`My_Narrative` column for qualitative signal.

**Signals to look for:**

*Resume structure:*
- Did applications with a skills section at top convert differently than those without?
  (Infer from Date_Tailored — check if the tailored resume file exists and review it
  if accessible, otherwise note you can't verify this dimension without seeing the files)

*Narrative style:*
- Compare `My_Narrative` text across converting vs. non-converting applications.
  Are converting narratives more metrics-focused? More story-focused? Shorter? Longer?
  Do they lead with a business problem or with credentials?

*Fit estimate calibration:*
- Are the actual conversion rates matching the fit estimates? If you're converting at
  50% on roles estimated 65–75%, but 10% on roles estimated 75–85%, the estimates
  may be systematically miscalibrated for certain segments.

*Role and company type patterns:*
- Which segment combinations are converting best? (e.g., "Enterprise × VP-TM has a
  40% Round 1 rate; Mid-market × VP-TM has 0% across 5 applications")

*Notes column signal:*
- Scan `Notes` for any recurring themes: objections raised in calls, what resonated,
  feedback given after rejections.

**Confidence ratings** — apply to every finding:
- `Low` — 3–5 applications in segment, one data point driving the pattern
- `Medium` — 6–10 applications, pattern holds across at least 2–3 data points
- `High` — 10+ applications, consistent pattern across multiple data points

Never assert a causal claim at Low confidence. State it as "early signal" only.

---

## Step 4: Draft Proposed Updates

For each pattern that has at least Low confidence, draft a specific proposed update to
the corresponding section of `resume_strategy.md`.

Format each proposed update as:

---
**PROPOSED UPDATE — [Segment Name]**

*What the data shows:*
[Specific finding — numbers, conversion rates, what's different between converting and
non-converting applications in this segment. Be concrete, not vague.]

*Confidence:* [Low / Medium / High] — based on [N] applications, [N] conversions

*Proposed change to strategy doc:*
> [Exact text to add or replace, formatted as it would appear in the strategy doc.
> Label as [LEARNED — DATE] not [DEFAULT].]

*What this means for future applications in this segment:*
[1–2 sentences on how this will change tailoring decisions going forward.]

---

Present ALL proposed updates before asking for any approvals. Let the user see the full
picture first.

---

## Step 5: Get Human Approval

After presenting all proposed updates, ask:

> "That's [N] proposed update(s) based on [N] new applications. How do you want to handle
> these? You can:
> - **Approve all** — I'll write all of them to the strategy doc
> - **Approve some** — tell me which ones (by segment name)
> - **Modify before approving** — give me edited language and I'll use that instead
> - **Reject** — I won't write anything; we can revisit next review
>
> You can also override any recommendation with your own judgment — you know context
> the data doesn't."

Wait for explicit instructions before writing anything.

---

## Step 6: Write Approved Changes

For each approved update:

1. Open `Application Engine/resume_strategy.md`
2. Find the relevant segment section
3. Replace or augment the guidance with the approved text
4. Change the label from `[DEFAULT]` to `[LEARNED — DATE]`
5. Update the confidence and sample size annotation at the top of that segment
6. If a prior [DEFAULT] assumption is being replaced, move it to the
   "Deprecated Guidance" section at the bottom of the doc with the date deprecated and reason

After all writes are complete:

7. Update the Review History table at the top of the doc:
   Add a new row with: today's date, number of applications reviewed, segments updated,
   and "Strategy Review Skill"

8. Confirm the save and tell the user which segments were updated and what changed.

---

## Step 7: Cross-Cutting Check

After writing segment-specific updates, check: did any patterns appear in 3+ different
segments? If so, consider whether a cross-cutting learning belongs in the
"Cross-Cutting Learnings" section.

Ask: "I noticed [pattern] appears across [segments]. Should I add this as a cross-cutting
learning that applies by default across all segments?"

Only write to Cross-Cutting Learnings with explicit approval.

---

## After the Review

Tell the user:

> "Strategy doc updated. Starting from your next application, the `job-application` skill
> will apply these learnings when tailoring your resume — and will explain which segments
> and guidance applied to each recommendation."
>
> "Want to schedule this review to run automatically each week? Say 'schedule strategy
> review weekly' and I'll set it up."
