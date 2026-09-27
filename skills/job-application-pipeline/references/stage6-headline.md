# Stage 6: Headline Brainstorm

## Purpose

The resume headline is the first thing a hiring manager reads. It sets the frame for everything that follows. A generic headline does nothing. The goal is a headline that signals the exact persona the hiring manager is looking for, in language that sounds like a person rather than a LinkedIn template — and that implicitly answers the hiring problem identified in Stage 2.

---

## Inputs

Pull from session state before doing anything:
- `stage5_strategy.approved_positioning` — the narrative angle everything should serve
- `stage2_hiring_problem` — the headline should imply this candidate solves it
- `stage2_hm_profile` — tone and register should match what this person responds to
- Stage 3 gap analysis — what to foreground, what to background
- Candidate's most distinctive credentials from the resume

---

## Process

**Step 1 — React to the current headline**

State the candidate's current headline (or their current title if no headline exists) and give a hiring-manager-eye reaction in 2–3 sentences. What does it signal? What does it miss? Does it help or hurt this specific application? This anchors the improvement work.

**Step 2 — Identify the three qualities the winning headline must signal**

For this specific role and this specific HM, what three things must the headline communicate? Name them explicitly before generating options.

**Step 3 — Run the Hiring Manager Filter**

> *Given `stage2_hm_profile`: what tone and framing register as credible vs. off-putting to this person? A data-driven, operationally-minded HM will read compressed, specific language as confident; they'll read visionary or abstract framing as unsubstantiated. An HM who came up through storytelling or brand will respond to the opposite. Let this shape the register of every option.*

**Step 4 — Generate five alternative headlines**

Use distinct literary devices — one dominant device per headline, not a pile of them. Draw from the toolkit below, but don't feel limited to it. Unusual combinations often stick better than the obvious ones.

For each headline:
1. The headline itself
2. The dominant literary device used
3. One sentence of strategic logic: what it emphasizes, what it implies, why it serves this application

---

## Literary Device Toolkit

*Sound and rhythm* — Alliteration, assonance, and meter make a phrase memorable without the reader knowing why. Use sparingly — it should feel crafted, not forced.

*Compression / parataxis* — Stripping conjunctions for speed. "Build. Ship. Learn." Three ideas, six words. Useful when the candidate's value is a sequence or process.

*Tension and contrast* — Juxtaposition, oxymoron, and paradox force the reader to resolve a contradiction, which creates recall. "Rigorous systems, fast decisions" implies someone who doesn't sacrifice one for the other.

*Specificity as device* — A single concrete noun or number outpunches an adjective every time. Naming a real domain, tool, or outcome differentiates more than claiming to be "results-oriented."

*Implied metaphor* — A phrase that carries a structural analogy without stating it. "Translating AI into market motion" implies precision without saying "communication skills."

*Chiasmus or reversal* — Flipping a familiar structure forces a re-read. Use when the candidate's value is counterintuitive.

*Zeugma* — One verb governs two different things. "Building systems and the teams that run them." Efficient, implies breadth without listing.

*Rule of three* — Three parallel phrases that build. Powerful when the candidate has a clear triptych of value.

*Negative space* — What's intentionally not said. A tight, specific headline implies everything it excludes.

---

## Standards

- Maximum ~15 words; shorter is usually better
- **Banned patterns:**
  - "From [X] to [Y]" constructions — overused, signal nothing distinctive
  - Keyword strings: "AI | Strategy | Data | Growth | Enterprise" — this is a tag cloud, not a headline
  - Superlatives: "world-class," "visionary," "results-driven," "passionate," "dynamic," "innovative"
  - Generic title + modifier: "Senior Strategic Operations Leader"
- The headline should work for this role specifically, not as a generic personal brand
- It should sound like something a smart person wrote, not a template filled in
- No fabrication: no skills, credentials, or scope not supported by the resume

---

## After Presenting

Ask the user to pick one, request changes, or say "none — try again." Iterate without complaint. Write the approved headline to `stage6_headline` in `{company-slug}_session-state.json`, including the literary device used and strategic logic.
