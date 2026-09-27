# Stage 8: Full Resume Customization

Extended prompt and standards for resume optimization. SKILL.md behavioral rules take precedence where there is any conflict.

---

## Inputs — read from session state before writing a single word

Pull all of the following from `{company-slug}_session-state.json`:

- `stage2_hiring_problem` — editorial filter for what stays and what goes
- `stage2_hm_profile` — Hiring Manager Filter for framing and tone
- `stage3_ats_keywords.high_priority_additions` — terms to weave in verbatim
- `stage4_gap_answers` — experience the user surfaced that isn't on the resume yet
- `stage5_strategy.approved_positioning` — the narrative angle everything should serve
- `stage6_headline.approved_headline` — the promise the resume body must substantiate
- `stage7_summary.approved_summary` — already written; do not rewrite it here
- `preferences.bullets_voice` — grammatical voice for bullets and context sentences (default `implied` if unset)

If any of these fields are missing or null, flag it before proceeding. Do not fabricate inputs. (`preferences.bullets_voice` is the one exception — if it's absent, fall back to the `implied` default rather than flagging.)

---

## Resume Structure

Produce the resume in this order:

1. **Name and contact block** — unchanged from the original
2. **Headline** — from `stage6_headline.approved_headline`
3. **Professional summary** — from `stage7_summary.approved_summary`
4. **Skills** — reordered and recategorized (see below)
5. **Experience** — each role rewritten (see below)
6. **Education** — unchanged unless a credential is directly relevant and currently buried
7. **Additional sections** (publications, patents, certifications, etc.) — keep only if they directly support the positioning strategy

---

## Skills Section

**Category headers** should reflect the JD's own organizational logic — not generic headers like "Technical Skills" or "Soft Skills." If the JD organizes around domains (e.g., "AI/ML," "Go-to-Market," "Design Systems," "Revenue Operations"), mirror that structure.

**Ordering within categories:** highest-relevance to this role first. Not chronological, not alphabetical.

**Inclusion rule:** only skills the candidate actually has. If a skill from `high_priority_additions` isn't on the original resume, add it only if the Stage 4 answers confirm it's real. If it's absent-gap (flagged in `stage3_ats_keywords.absent_gaps`), do not add it.

**ATS pass:** after writing the skills section, confirm every term in `high_priority_additions` appears somewhere in the resume — either here or in a bullet. Note any that couldn't be placed honestly.

---

## Voice

Render every context sentence and bullet in the register set in `preferences.bullets_voice` (default `implied`). Keep it consistent across all roles — do not mix registers.

- **`implied`** (default, standard resume register) — verb-led, no pronoun. Context: *"Led product for a 40-person fintech startup…"* Bullet: *"Shipped X in six weeks by [method], resulting in Z."*
- **`first_person`** — lead with "I". Context: *"I led product for a 40-person fintech startup…"* Bullet: *"I shipped X in six weeks by [method], resulting in Z."*
- **`third_person`** — the candidate's name/pronoun as subject where it reads naturally; name on first mention, pronouns after. Context: *"Maya led product for a 40-person fintech startup…"* Bullet: *"Shipped X in six weeks by [method], resulting in Z"* or, where a subject is natural, *"She shipped X in six weeks…"* Stay verb-forward; never use "I".

The quantification, selection, and no-fabrication rules below are voice-independent — apply them the same way regardless of register.

---

## Experience Section

### For each role:

**Context sentence** (one sentence, italicized or in a subdued style): Sets the stage before bullets. Answers: what did this company do, what was the scale, and what was the candidate's mandate. This is especially important for companies the hiring manager may not recognize.

> Example: *Ran growth marketing for a 40-person fintech startup building embedded-lending infrastructure for regional banks; owned demand generation from top-of-funnel through pipeline handoff.*

**Bullets:** Rewrite for relevance, not just polish.

- **Selection:** Choose bullets that connect to the hiring problem or the approved positioning. An impressive bullet that has nothing to do with either should be cut or condensed — resume length discipline signals judgment.
- **Quantification target:** ≥80% of bullets should include a number, percentage, timeframe, or scale indicator. If the original bullet has no number and the user didn't provide one in Stage 4, either prompt for it (if the gate hasn't passed) or write the bullet in a way that implies scale without fabricating.
- **Verb choice:** Start with a strong past-tense verb. Avoid: *managed, helped, worked on, supported, assisted, collaborated.* Prefer: verbs that imply agency and outcome — *built, launched, reduced, increased, redesigned, negotiated, recovered, shipped.*
- **Structure:** Lead with the action and outcome, not the context. Wrong: *"Working cross-functionally with engineering and design teams, I led the development of..."* Right: *"Shipped X in Y weeks by [method], resulting in Z."* (The "Right" example is in the default `implied` voice; for `first_person` prepend "I", for `third_person` use the name/pronoun as subject — the lead-with-action principle holds in every register.)
- **No fabrication:** Every claim must trace to the original resume or a Stage 4 answer. If a Stage 4 answer is vague ("it did pretty well"), don't invent a number — write the bullet without one or flag it for the user.

### Chronological completeness

Keep all roles. Do not drop jobs to make the resume shorter — gaps are worse than a long resume. If a role is genuinely irrelevant, reduce it to a one-line context sentence with no bullets rather than removing it.

---

## Hiring Manager Filter — Stage 8

Before finalizing, read the resume as `stage2_hm_profile` would:

1. **Values alignment:** For each bullet you kept, ask: does its framing match what this HM demonstrably values? The same accomplishment can be framed around speed, rigor, scale, collaboration, or mission depending on who's reading. Choose the frame that matches.

2. **Skepticism check:** Review `likely_skeptical_if`. Does anything in the current resume trigger those concerns? If yes, either remove the signal or counter it explicitly elsewhere. Examples:
   - If the HM is skeptical of candidates who've only worked at large companies, make sure early-stage or scrappy experience is visible and prominent.
   - If the HM values technical depth and the resume reads as purely strategic, surface any hands-on technical work even if it feels minor.

3. **Skills ordering:** Does the skills section ordering reflect what this HM would scan for first? Reorder if not.

---

## Anti-Patterns — these degrade the resume

**Responsibility-framed bullets** describe what the candidate was supposed to do, not what they did. *"Responsible for the sales pipeline"* tells the reader nothing. *"Rebuilt the pipeline-management process after two consecutive missed quarters, hitting target the next four"* tells them something.

**Vague scale:** *"Worked with a large team"* — how large? *"Improved performance"* — by how much? Either quantify or cut.

**Keyword stuffing:** Weaving in ATS terms in ways that read unnaturally damages credibility with the human reader. Every added keyword must read as if it was always there.

**Identical bullets across roles:** If the same type of achievement appears in three jobs with slightly different wording, cut two. Show range, not repetition.

**Passive voice:** *"A new onboarding process was implemented"* obscures agency. Always: who did what.

**Burying the lead:** If the most impressive result is in the middle of a five-bullet list, move it to the top.

---

## Output

Save as `{company-slug}_resume-optimized.md`.

Present the full resume. Then present a brief "what changed" summary: which bullets were rewritten, which were cut, which ATS terms were added and where, and any terms that couldn't be placed. This helps the user review efficiently rather than doing a line-by-line diff.

Gate question: *"How does this look? Any bullets you want changed, anything that doesn't sound like you?"*
