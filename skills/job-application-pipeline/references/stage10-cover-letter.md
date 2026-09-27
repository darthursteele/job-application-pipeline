# Stage 10: Cover Letter

Extended prompt and standards for cover letter drafting. SKILL.md behavioral rules take precedence where there is any conflict.

---

## What the Cover Letter Is For

The resume proves qualifications. The cover letter makes the argument.

A cover letter answers one question the resume can't: *why does this particular person, with this particular background, solve the problem this company is trying to solve right now?* If the cover letter restates resume bullets, it's wasted space. If it makes the hiring manager feel like they're already in a conversation with someone who understands their situation, it's doing its job.

The hiring manager reads the cover letter either before or after the resume — rarely both with equal attention. Assume they skim. The first two sentences determine whether they keep reading. The last paragraph determines what they remember.

---

## Inputs — read from session state before writing anything

Pull all of the following from `{company-slug}_session-state.json`:

- `stage2_hiring_problem` — the argument the letter must make
- `stage2_hm_profile` — shapes tone, register, and what the opening leads with
- `stage5_strategy.approved_positioning` — the narrative angle
- `stage6_headline.approved_headline` — the promise; the letter should echo and deepen it
- `stage7_summary.approved_summary` — read it, do not repeat it
- `stage9_additional_materials` — if additional materials exist, the letter must not contradict them
- `stage10_personal_story` — if provided, integrate it; do not manufacture one if not
- `stage2_hm_profile.likely_skeptical_if` — things to avoid or preempt

---

## Step 10a: Personal Story

Ask: *"Is there a specific story, moment, or personal connection to this company's mission that you'd want in the cover letter? Something that doesn't appear in the resume."*

If the user provides one: write it to `stage10_personal_story` and plan to integrate it in the body — not the opening (which should hook on the hiring problem) and not the close (which should drive action). The body paragraph is where personal narrative earns its place.

If the user says no: write `{"provided": false}` and proceed without one. Do not manufacture a personal connection.

---

## Step 10b: Pre-Draft Strategy

Before writing, present the structure and get a green light. This prevents wasted drafting.

**Hiring Manager Filter — pre-draft:**

Before building the structure, run through `stage2_hm_profile`:
- What tone will make this person lean in? (direct and data-forward, or narrative and mission-driven?)
- What opening angle connects the hiring problem to the candidate's specific background?
- What would make them put this down in the first two sentences? (avoid that)
- Is there anything in `likely_skeptical_if` that the letter should preempt?

**Structure to present:**

```
Opening hook: [one sentence describing the angle you'll lead with — not "I am excited to apply"]
¶1 — [What it accomplishes: connects hiring problem to candidate's most relevant credential]
¶2 — [What it accomplishes: deepens the argument with a specific example or story]
¶3 — [What it accomplishes: addresses any key gap or differentiates from the likely applicant pool]
Close — [What it accomplishes: drives action without being obsequious]
```

Ask: *"Does this structure feel right?"* Wait for a green light before drafting.

---

## Step 10c: Draft

### Opening — the one sentence that determines everything

Never open with:
- "I am excited / thrilled / delighted to apply for..."
- "I have X years of experience in..."
- "My name is [name] and I am applying for..."
- Any sentence that could be copy-pasted onto a different letter

Open with something that signals you understand the company's actual situation. The best openings make the reader think *this person already gets it.*

**Opening patterns that work:**

*Lead with the hiring problem:*
> "Most companies racing to put AI into the business discover too late that the bottleneck isn't the models — it's not having someone who can hold the technical context and the customer context at the same time."

*Lead with a counterintuitive observation:*
> "The hardest part of scaling an AI initiative isn't the infrastructure — it's convincing the rest of the business to change how they work around it."

*Lead with a specific relevant result:*
> "In three years at [company], I reduced time-to-insight for enterprise customers from six weeks to four days by rebuilding how we scoped and handed off data products."

*Lead with a pointed observation about the company's situation:*
> "[Company]'s move into [market] is the right bet — and it's the kind of bet that only pays off if execution keeps pace with the go-to-market motion."

The opening should be one sentence. Two at most.

### Body paragraphs

**Paragraph 1 — the core argument:**
Connect the hiring problem directly to the candidate's most relevant credential. This is not a biography. It's a claim: *I have done the specific thing you need done.* Make that claim, then support it with one concrete example. One. Don't list three things — go deep on one.

**Paragraph 2 — the story or differentiator:**
Either: integrate the personal story if one was provided, or use this paragraph to address the most important gap or differentiator — the thing that separates this candidate from the likely applicant pool. This is the paragraph that earns the interview for a non-obvious candidate. For an obvious candidate, use it to show intellectual alignment with where the company is going, not just where it's been.

**Paragraph 3 (optional, use only if needed):**
Address a meaningful gap or make a specific observation about the company that demonstrates real research. This paragraph is often cut — only keep it if it adds something the first two paragraphs don't.

### Close

Short. Two to three sentences. Do not grovel. Do not repeat what you just said.

A close that works: restates the core claim in one sentence, expresses genuine interest without desperation, and makes asking for a conversation feel like a natural next step rather than a request for a favor.

> "I'd welcome the chance to talk through how I'd approach the first 90 days. [Contact info or 'happy to connect at your convenience.']"

Avoid: "I look forward to hearing from you," "Thank you for your time and consideration," "I am confident I would be a great fit." These are filler.

---

## Structural Rules

**Length:** One page. If it runs over, cut — don't shrink the font or the margins. A long cover letter signals poor editing judgment.

**No resume repetition:** Do not repeat statistics from the resume verbatim. Interpret them instead. Wrong: *"I increased revenue by 40%."* Right: *"The revenue growth came from restructuring how we segmented the market — which is directly relevant to what you're trying to do in [segment]."*

**Factual discipline:** Every claim must be true and traceable to the resume, Stage 4 answers, or verified company research. Only use company-analysis facts where `confidence >= medium`.

**Contradiction check:** If Stage 9 produced additional materials, read them before finalizing. The cover letter cannot contradict anything submitted elsewhere in the application.

**First person, active voice:** "I built" not "a system was built." "I decided" not "the decision was made." Agency matters.

---

## Anti-Patterns

**The HR mirror:** A letter that restates the job requirements back at the reader. *"You're looking for someone with X and Y — I have X and Y."* This demonstrates reading comprehension, not fit.

**Excessive hedging:** *"I believe I could potentially be a strong contributor to your team."* Either you are or you aren't. Confidence is not arrogance.

**The résumé in prose form:** Listing accomplishments in paragraph form instead of making an argument. If the paragraphs could be bullets, they should be bullets — on the resume, not here.

**Flattery as strategy:** *"[Company] is an incredible organization doing truly innovative work."* This tells the reader nothing and often reads as insincere. Replace with a specific, informed observation.

**The apologetic letter:** Any framing that pre-apologizes for a gap or non-traditional background before making a positive case. Lead with your strongest argument. Address gaps only if they're large enough that the reader will notice them anyway, and only after you've established credibility.

---

## Output

Save final approved letter as `{company-slug}_cover-letter.md`.

After the user approves, offer: *"Want me to format this for pasting into an application form, or as a PDF-ready document?"*
