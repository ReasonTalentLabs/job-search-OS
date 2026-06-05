# Application Database — Column Reference

Create `Application Engine/application_database.xlsx` with one header row containing
these exact column names. The `job-application` skill writes to this file; the
`job-patterns` skill reads from it. Column name spelling and spacing must match exactly.

---

| Column | Type | Filled by | Description |
|--------|------|-----------|-------------|
| `Company` | Text | Claude | Company name |
| `Title` | Text | Claude | Exact job title as written in the posting |
| `Link` | URL | Claude | Link to the job posting, if available |
| `Posting` | Text | Claude | Full JD text, pasted or saved from the posting |
| `Company_Narrative` | Text | Claude | 2–3 sentence summary of what this company needs right now (from Step 2 research) |
| `My_Narrative` | Text | Claude | 1–2 sentence story of why your background fits this specific role |
| `Fit_Estimate` | Text | Claude | Score range from fit assessment, e.g. "65–78%" |
| `Date_Found` | Date | Claude | Date the role was identified (YYYY-MM-DD) |
| `Date_Tailored` | Date | Claude | Date the resume was tailored (YYYY-MM-DD), or blank |
| `Date_Applied` | Date | **You** | Date you submitted the application — fill this in yourself |
| `Round1_Date` | Date | **You** | Date of first interview, if reached |
| `Round2_Date` | Date | **You** | Date of second interview, if reached |
| `Round3_Date` | Date | **You** | Date of third or final interview, if reached |
| `Outcome` | Text | **You** | Final result: `In Progress` / `Offer` / `Rejected` / `Withdrew` / `No Response` |
| `Notes` | Text | **You** | Free-text notes — what came up in interviews, recruiter feedback, anything useful |

---

## Notes on usage

**`Date_Applied` is the most important column you fill in yourself.** Claude logs everything
up to the application, but only you know when you actually submitted. Keep this current —
the `job-patterns` analysis depends on it.

**Update `Outcome` as things progress.** When you get a rejection, withdraw, or receive an
offer, update this field. Outcomes data is what makes the pattern analysis meaningful over time.

**`Notes` is your running log.** Use it to capture anything that happened after the initial
application: recruiter call takeaways, hiring manager first impressions, interview questions
you got caught on, reasons given for a rejection. This becomes your searchable institutional
memory across the search.

**The `Posting` column stores the full JD text.** This enables future analysis (e.g., which
JD keywords are appearing in your winning applications vs. non-converting ones). Keep it.

---

## Excel setup tips

- Format date columns (`Date_Found`, `Date_Applied`, etc.) as Date type in Excel
- Freeze the header row (View → Freeze Panes → Freeze Top Row) for easier scrolling
- Add a filter to all columns (Data → Filter) so you can sort by outcome, date, company, etc.
- Do not add, remove, or rename columns — the skills depend on exact column names
