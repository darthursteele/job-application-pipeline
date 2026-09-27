# Stage 1: JD Review

## Purpose

Parse the job description into structured intelligence before any research or resume work begins. A misread JD poisons every downstream stage. This stage also flags language whose meaning depends on company context — those flags get resolved at the end of Stage 2 after company research.

---

## Fetch Behavior

If given a URL:
- Fetch it immediately.
- If the page is JavaScript-rendered and returns no meaningful content (e.g., only a page title or meta tags), **stop and tell the user explicitly**: *"The page didn't render the job description — can you paste the text directly?"*
- Do not proceed with partial content. Do not say you have "enough to work with." Either you have the full JD or you stop and ask for it.

If given pasted text, use it as-is.

---

## Output Structure

Present a structured interpretation — not a copy-paste — organized as follows:

**Role Basics**
- Company name, role title, seniority level (if stated)
- Location / remote policy
- Compensation range (if listed; flag if absent)
- Reporting structure (if stated)

**Core Responsibilities**
- Top 5–7 things this person will actually do day-to-day, in plain language
- Note if any responsibilities are ambiguous or seem unusual for the role type

**Requirements**
- Hard requirements (must-haves explicitly stated)
- Nice-to-haves (explicitly flagged as preferred/bonus)
- Implicit requirements — things the JD signals but doesn't state outright. Examples: "moves fast in ambiguous environments" implies startup tolerance; "partners cross-functionally" implies political skill; "owns outcomes" implies no excuses culture. Identify these — they're often more predictive of fit than the explicit list.

**Team & Culture Signals**
- Any language revealing team size, culture, pace, or values
- Red flags or green flags worth noting (e.g., "wear many hats" = small team, "world-class team" = often meaningless filler)

**Gaps in the JD**
- Anything important that's missing (comp, team size, tech stack, reporting line)
- Anything ambiguous that could affect positioning

**Context-Dependent Phrases** ← hold for Stage 2
- List any JD phrases whose meaning depends on knowing the company's actual situation. Do not interpret them yet — that happens at the end of Stage 2 after company research.
- Examples of phrases that commonly need reinterpretation: "drive AI adoption," "build from scratch," "partner with the business," "own it end-to-end" (which shows up role-specifically as "own the roadmap," "own the number," "own the funnel," or "own the process"), "define the strategy," "scale the team."
- For each, note briefly *why* it's ambiguous (e.g., "'build from scratch' could mean greenfield or could mean cleaning up a failed prior effort").

---

## What Not to Do

- Do not reproduce the JD verbatim
- Do not analyze the candidate's fit yet — that's Stage 3
- Do not search for company information yet — that's Stage 2
- Do not guess at the meaning of context-dependent phrases — flag them and move on
