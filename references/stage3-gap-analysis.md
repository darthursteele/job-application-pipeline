# Stage 3: Resume Gap Analysis + ATS Keyword Matching

## Purpose

Systematically compare the candidate's resume against the JD. Identify what's strong, what's weak, and what's missing. Feed the Stage 4 Q&A and inform Stage 5 strategy. Do not ask questions here — just analyze.

---

## Part A: Alignment & Gap Analysis

### Business Problem Frame

Before the alignment table, write 2–3 sentences answering: *What problem is the hiring manager trying to solve by filling this role?* This should reference `stage2_hiring_problem` from session state — don't restate it verbatim, but use it to frame what "strong alignment" means for this specific situation. This anchors the whole analysis.

### Alignment Table

| JD Requirement | Candidate's Evidence | Keyword Match | Alignment |
|---|---|---|---|
| [Top 7–10 critical requirements, ordered by importance] | [Specific bullets or roles from resume] | Present / Partial / Missing | Outstanding / Strong / Moderate / Weak / Missing |

Pull requirements from both the responsibilities AND qualifications sections. Don't just hit the bullet points — read for implicit requirements too (domain knowledge, pace expectations, tool fluency, organizational dynamics).

### Gap List

After the table, categorize gaps in three tiers:

**Critical gaps** — required qualifications or experience the JD explicitly demands that the candidate clearly lacks. These are hard stops that Stage 4 may or may not be able to address.

**Partial gaps** — areas where the candidate has adjacent experience but the resume doesn't express it in the right language, with the right emphasis, or with enough evidence. May be addressable through reframing in Stage 8, or may reveal hidden depth in Stage 4.

**Addressable gaps** — experience the candidate likely has but hasn't articulated. These become the priority questions for Stage 4.

---

## Part B: ATS Keyword Matching

ATS filters rank resumes by keyword density before a human reads them. This analysis ensures the resume uses the JD's own language where it's truthful to do so.

### Step 1 — Extract JD keyword inventory

Pull:
- Role-specific titles and seniority language (e.g., "Principal," "Staff," "Solutions Architect")
- Technical skills, tools, platforms, and frameworks named explicitly
- Methodologies and processes called out (e.g., "agile," "discovery," "go-to-market," "demand generation," "zero-based budgeting")
- Domain terms that signal industry fluency
- Soft-skill phrases that appear more than once (repetition signals weighting)

### Step 2 — Map each keyword against the resume

For each keyword:
- **Present** — the word or a close synonym appears on the resume
- **Absent but supportable** — the candidate likely has this experience but the resume doesn't use the JD's language (high-priority rewrite target for Stage 8)
- **Absent, not supportable** — the experience genuinely doesn't exist (do not add)

### Step 3 — Produce the ATS keyword table

| Keyword / Phrase | JD Weight | Resume Status | Priority |
|---|---|---|---|
| [keyword] | High / Med / Low | Present / Absent-supportable / Absent-gap | Must-include / Should-include / Nice-to-include |

Cap at the 15 highest-weighted terms. JD Weight: High = appears in required qualifications or multiple times; Med = once in responsibilities; Low = only in nice-to-haves.

Priority tiers:
- **Must-include:** High-weight terms that are absent but supportable — these go into Stage 8 with the highest priority
- **Should-include:** Medium-weight terms, or terms that need light reframing to fit naturally
- **Nice-to-include:** Low-weight terms where inclusion would help but absence won't hurt

### Step 4 — Write ATS data to session state

Write to `stage3_ats_keywords` in `{company-slug}_session-state.json`:
```json
{
  "high_priority_additions": ["keyword1", "keyword2"],
  "present_keywords": ["keyword3"],
  "absent_gaps": ["keyword4"]
}
```

Stage 8 reads this directly — it is the source of truth for which terms to weave in.

---

## What Not to Do

- Do not write any resume copy here
- Do not ask gap questions here — that's Stage 4
- Do not assess overall competitiveness here — that's Stage 5
- Do not fabricate evidence of qualifications not present in the resume
- Do not add absent-gap keywords to the must-include list — if the experience doesn't exist, the keyword cannot be placed honestly
