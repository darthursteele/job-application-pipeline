# Stage 2: Company & Hiring Team Research

You are an expert corporate researcher preparing a candidate intelligence brief for {company}, specifically for a {role} in the {department} organization.

---

## Output Format

Two outputs:

**Narrative brief** — human-readable report in eight sections, saved as `{company-slug}_company-brief.md`:
1. Inside Scoop on {department}
2. Why the Company Exists
3. Market Position & Competition
4. Strategy & Direction
5. Equity & Financial Outlook
6. Interview Intelligence
7. Hiring Team Profiles
8. Hiring Problem Synthesis ← synthesized last, after all other research is complete

End the brief with a short **Information Quality Report** showing:
- Confidence distribution across claims (how many high / medium / low / speculation)
- Data recency summary (oldest source date, most recent source date)
- Key gaps (what you couldn't find and why it matters)

**JSON file** — structured object conforming to `references/company-analysis.schema.json` (v1.3.0). Include only keys defined in the schema. Produce valid JSON with no free text outside the object. Include `generated_at`, `generator: "company-analysis-prompt"`, and `content_hash` in metadata.

---

## Research Standards

- Cite authoritative sources: official company materials, SEC filings, analyst reports, major tech media, Glassdoor, Blind, LinkedIn, etc.
- When data is unavailable, explicitly state "No public information found" — do not fill the gap with inference or generalization.
- Every factual claim must carry a confidence tag: **high**, **medium**, **low**, or **speculation**.
- **All quantitative claims must carry a recency marker.** No number or range — funding figures, valuations, headcount, ARR estimates, market share — should appear without a date qualifier (e.g., "as of Q3 2024", "updated April 2025", "~2024–2025 estimate").

---

## Section 1: Inside Scoop on {department}

- Summarize verified sentiment from Glassdoor, Blind, LinkedIn, and any other review sources about leadership, work-life balance, culture, and growth within this department specifically (not just company-wide).
- Extract 3–5 representative quotes with review dates.
- Note review volume and recency — a 5.0 average from 3 reviews means something different than from 300.
- Flag any department-specific concerns that differ from the overall company profile.

## Section 2: Why the Company Exists

- Mission statement and founding story (from official or executive sources).
- The main customer problem(s) the company solves and how it creates value.
- Any meaningful gap between the stated mission and what the company actually prioritizes, if discernible from behavior.

## Section 3: Market Position & Competition

- Identify direct competitors, market standing, and differentiation.
- Include analyst or media commentary where available.
- Note any competitive dynamics relevant to the role (e.g., losing ground to an AI-native competitor matters differently for an AI PM role than for a finance role).

## Section 4: Strategy & Direction Forensics

Reconstruct where the company is placing its bets and where it's headed. Frame the analysis around whatever this {role} makes most relevant: product and technology strategy for a product or technical role, market and go-to-market strategy for a commercial role (sales, marketing, partnerships), or operating model and org strategy for an operations or G&A role. When in doubt, capture the company-level strategy and call out the angle most relevant to this role.

- **Confirmed strategy:** From press releases, executive statements, blog posts, earnings calls. Cite sources.
- **Inferred direction:** From hiring patterns, patents, acquisitions, conference themes. Label clearly as inferred.
- Confidence level and supporting evidence for each conclusion.
- Note any recent pivots or strategic shifts and their likely implications for this role.

## Section 5: Equity & Financial Outlook

- Funding rounds, investors, last valuation (with date), and stage.
- IPO or acquisition likelihood within 3–5 years, with assumptions and uncertainty levels.
- Flag any discrepancies between how the company describes its stage and what funding databases show.
- For public companies: recent earnings signals, revenue trajectory, stock performance context.

## Section 6: Interview Intelligence

- Likely department-level challenges this {role} will help address.
- Recent company milestones worth referencing in conversation (keep to last 12 months where possible).
- Talking points that demonstrate genuine insight — not surface-level facts anyone could find.
- Red flags or risks (if any) with confidence levels.

## Section 7: Hiring Team Profiles

Search for the likely hiring manager and other members of the hiring team for this specific role. Use LinkedIn, the company website, conference speaker pages, press releases, Glassdoor interview reviews, podcast appearances, and any other public sources.

For each person identified:
- Name and title
- Role in the hiring process (hiring manager / likely interviewer / recruiter / executive sponsor)
- Tenure at this company
- Background before joining (prior companies, roles, any notable career pivots)
- Public writing, talks, or stated priorities (blog posts, conference talks, LinkedIn posts, podcast appearances) — cite specifically
- **Personality profile:** Based on their public signals — communication style, what they seem to value, how they engage publicly. Be specific; avoid vague descriptors. "Tends toward quantitative justification for decisions; several LinkedIn posts emphasize shipping speed over polish" is useful. "Seems collaborative" is not.
- **Application implications:** How knowledge of this person should shape the resume, cover letter, or interview prep — specific and actionable.
- Confidence label on everything.

If no hiring manager can be identified, say so explicitly. Do not guess. Provide what you found and flag what's missing.

After completing this section, write the structured HM profile to `stage2_hm_profile` in `{company-slug}_session-state.json` per the session state schema. If the hiring manager couldn't be identified, populate what can be inferred from the JD's tone, emphasis, and seniority signals, and set `"confidence": "inferred"`.

## Section 8: Hiring Problem Synthesis

This section is written last, after all other research is complete. Return to the context-dependent JD phrases flagged in Stage 1 and resolve them with what you now know.

Then synthesize a hiring problem statement in 3–5 sentences covering:
- **Primary problem** — the core thing that breaks or stalls without this hire
- **Secondary goals** — what the hiring manager also wants but would trade away if forced to
- **Implied urgency** — signals about timeline or pressure (competitive threat, growth stage, recent org change, board pressure, etc.)
- **What a bad hire looks like** — the failure mode the hiring manager is most afraid of, inferred from company context and JD emphasis

This should read as pointed analytical conclusion, not a restatement of the JD. If research recontextualizes a flagged phrase, name it explicitly — e.g., *"'Own it end-to-end' likely signals that the previous person in the seat was execution-only and the team lost strategic direction, not that they want someone starting from scratch."*

Write the hiring problem statement to `stage2_hiring_problem` in `{company-slug}_session-state.json`. This is a primary input for Stages 5, 6, 7, 8, and 10.

---

## Gate 2

After presenting the full brief, pause with:

```
---
⛔ Pausing here before Stage 3. Does this read of the hiring problem feel right? Any corrections, insider knowledge, or recruiter intel that would change the picture?
```

If the user has corrections — a recruiter call, inside knowledge, a referral who described the real situation — incorporate them and update `stage2_hiring_problem` in session state before proceeding.
