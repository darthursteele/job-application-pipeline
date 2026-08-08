# Stage 5: Application Strategy

## Purpose

Before any resume writing begins, establish a shared strategic direction. This prevents the resume and cover letter from being shaped by instinct rather than analysis. The conversation here is consequential — a wrong positioning choice propagates across every downstream document.

---

## Anchor: Read the Hiring Problem First

Before any analysis, pull `stage2_hiring_problem` and `stage2_hm_profile` from session state. Every element of the strategy — applicant pool framing, competitiveness verdict, positioning options — should be evaluated against both: *does this angle answer the problem the hiring manager is actually trying to solve, and does it land with this specific person?*

---

## Applicant Pool Analysis

Describe the likely applicant pool for this role with specificity:

**Typical strong candidate:** What does the person who usually gets this interview look like? Their background, prior companies, seniority level, and the specific signal that makes them an obvious fit.

**Typical weak candidate:** Who applies but doesn't get through? Name the common failure modes — overqualified, underqualified, wrong domain, wrong level, right skills wrong framing.

**Wild card candidates:** Is there a non-obvious background that could be competitive? (E.g., a founder, a domain expert without the standard title, a technical leader making a function switch.) Flag this — it may be this candidate's angle.

---

## Competitiveness Assessment

Give a clear, honest verdict on where this candidate sits in the pool. Use a plain rating with reasoning:

- **Top quartile** — likely to get an interview if the application is strong
- **Competitive** — in the mix; application quality will matter a lot
- **Long shot** — real gaps the candidate cannot paper over; be explicit about what they are
- **Unlikely** — the gaps are structural; recommend reconsidering whether to apply

**If the verdict is Long Shot or Unlikely, say so directly.** Opportunity cost is real. A candidate spending hours on a long-shot application might be better served applying elsewhere. Recommend accordingly, but let the candidate decide.

Explain the reasoning: what's working for them, what's working against them, what the deciding factor is likely to be.

---

## Positioning Options

Propose 2–3 distinct positioning strategies. These should represent meaningfully different choices — different narratives, different emphases, different risks — not stylistic variations of the same angle.

For each strategy:
- **Name** — short, descriptive label
- **Core narrative** — one sentence: what story does this strategy tell?
- **What it emphasizes** — which parts of the background it foregrounds
- **What it de-emphasizes** — what it backgrounds or doesn't address directly
- **Hiring problem connection** — how this positioning answers the specific problem from `stage2_hiring_problem`; if it doesn't connect, it's the wrong angle
- **Best for** — what type of hiring manager or interview process this works for (e.g., "HM who came up through engineering and values technical credibility" vs. "HM who cares primarily about business outcomes")
- **Risk** — what could go wrong with this framing

Run the Hiring Manager Filter before presenting:
> *Given `stage2_hm_profile`, which of these positioning angles would make this HM lean in vs. put them off? Flag any mismatch between what the applicant pool analysis suggests and what this specific person is likely to respond to.*

---

## The Conversation

Present the analysis and ask:
*"Which of these directions feels right to you, or is there an angle I'm not seeing? This choice will shape the headline, summary, and cover letter, so it's worth getting right."*

Wait for the user's answer. If they want to adjust a strategy or propose a hybrid, work it out together. Record the agreed-upon positioning to `stage5_strategy` in session state — including the competitiveness verdict, the chosen strategy name, core narrative, emphasizes/de-emphasizes, and the hiring problem connection.

---

## What Not to Do

- Do not start writing resume copy here
- Do not present the positioning as a foregone conclusion — these are options to discuss
- Do not soften a "long shot" verdict to spare feelings; honest assessment is the service
- Do not skip the hiring problem connection for each option — a positioning angle that doesn't answer the hiring problem is the wrong angle
