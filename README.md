# Job Application Pipeline

A ten-stage Claude skill that turns "help me apply to this job" into an actual collaborative process: research, gap analysis, positioning strategy, then a resume and cover letter built through back-and-forth instead of generated in one shot and handed back to you.

Most AI resume tools pattern-match against a job description and spit out a rewrite. This skill treats an application for what it really is: an argument that a specific candidate solves a specific hiring problem, for a specific person who's going to read it. It researches who that person is, figures out what problem they're actually trying to solve by hiring, and uses that as the editorial lens for every decision downstream, from the headline to the summary to which bullets survive to what the cover letter opens with.

## Why it's a pipeline, not a prompt

Application quality depends on the conversation that produces it, not just the model writing it. So the skill runs as ten sequential stages, each one feeding the next with intelligence or pausing to ask you something only you can answer. Nothing gets skipped, and nothing gets bypassed even if your first message asks for the whole thing end to end.

| # | Stage | What happens |
|---|---|---|
| 1 | JD Review | Parses the job description into role, responsibilities, requirements, and culture signals. Flags vague phrases ("drive AI adoption," "own the roadmap") to reinterpret once the company is understood. |
| 2 | Company & Hiring Team Research | Researches the company and tries to identify the actual hiring manager: background, values, communication style, what makes them lean in or get skeptical. Synthesizes a hiring problem statement, the real reason this role exists. **Gate: you confirm the read is right.** |
| 3 | Resume Gap Analysis + ATS Keywords | Maps your resume against the JD requirement by requirement, and separately extracts the JD's keyword inventory to check what's present, absent but supportable, or a genuine gap. |
| 4 | Experience Gap Questions | Asks you five or six targeted questions, one at a time, to surface experience that exists but isn't on the resume yet. |
| 5 | Application Strategy | Assesses the applicant pool, gives you an honest competitiveness read, and proposes two or three real positioning angles. **Gate: you pick a direction.** |
| 6 | Headline Brainstorm | Generates five headline options, each built on a distinct literary device, each with its strategic logic spelled out. No "results-driven" superlatives, no keyword tag clouds. **Gate: you pick or iterate.** |
| 7 | Professional Summary | Three-part structure (credibility, approach, impact) written in the register the hiring manager actually responds to. **Gate.** |
| 8 | Full Resume Customization | Rewrites the resume bullet by bullet against the hiring problem, weaves in ATS keywords honestly, reframes accomplishments the way this specific hiring manager would read them. **Gate.** |
| 9 | Additional Materials | Catches anything else the application asks for (essays, short answers, portfolio links) before cover letter work starts. |
| 10 | Cover Letter | Asks for a personal story, proposes a structure, then drafts and iterates. The letter answers the hiring problem directly instead of restating the resume. **Gate, multiple points.** |

Every stage marked with a gate stops and waits for you. An AI that plows through those gates for speed produces a worse application, faster.

## What comes out the other end

One folder per application, named `{company-slug}_{role-slug}/`, containing:

- `{company}_company-brief.md`, a narrative research report covering mission, market position, product strategy, funding, interview intel, and hiring team profiles. It doubles as interview prep.
- `{company}_company-analysis.json`, the same research structured and confidence-labeled
- `{company}_session-state.json`, every approved decision across stages, so later stages never lose context from earlier ones
- `{company}_resume-optimized.md`
- `{company}_cover-letter.md`
- `{company}_additional-materials.md`, if the application needed it

## What makes it different

**It researches the hiring manager, not just the company.** Every downstream stage (strategy, headline, summary, resume, cover letter) runs a "Hiring Manager Filter": given this person's background and values, what lands as credible and what reads as noise? A data-driven, operationally-minded manager reads compressed, specific language as confident and abstract framing as unsubstantiated. Someone who came up through brand or storytelling reads it the opposite way. The output is shaped by who's actually reading it.

**It won't tell you what you want to hear.** Stage 5's competitiveness assessment is honest by design: top quartile, middle of the pack, or long shot, with reasoning. If you're not a strong fit, the skill says so. Your time is worth more than a polished application that doesn't land.

**Everything traces back to a source.** No fabricated skills, no invented scale, no claims the resume, your answers, or the job posting don't support. Confidence labels carry through to the cover letter, where anything below medium confidence gets softened language instead of a direct assertion.

**Nothing gets copy-pasted.** Resume bullets get rewritten around what the hiring problem actually needs, not just reshuffled. The cover letter interprets significance instead of repeating stats already on the resume.

## Using it

New here? Jump to [Installation](#installation) first.

Trigger it naturally: "I want to apply to [company]," "help me optimize my resume for this role," "I have a job posting I want to apply to." Have the job description (URL or pasted text) and your current resume ready. The skill asks for both before Stage 1 if you haven't provided them.

Expect a real conversation. Stage 4 alone asks several questions one at a time. Stage 6 might hand you five headlines and none of them land, and that's fine, just iterate. The gates exist because ten minutes of back-and-forth produces a materially better application than a single prompt does.

## Project structure

```
job-application-pipeline/
  .claude-plugin/
    plugin.json                               ← plugin manifest
    marketplace.json                          ← lets the repo act as its own plugin marketplace
  skills/
    job-application-pipeline/
      SKILL.md                                ← pipeline definition, stage logic, gate rules
      references/
        stage1-jd-review.md
        stage2-company-research.md
        stage3-gap-analysis.md
        stage5-application-strategy.md
        stage6-headline.md
        stage8-resume-customization.md
        stage10-cover-letter.md
        company-analysis.schema.json
        session-state.schema.json
      subagents/
        stage2-agent-a-fundamentals.md
        stage2-agent-b-culture.md
        stage2-agent-c-hm.md
        stage2-agent-d-jd-resolution.md
```

## Installation

This is a Claude Skill: a `SKILL.md` file plus supporting reference docs that Claude reads to know how to run the pipeline. No build step, no dependencies.

**Claude Code — install as a plugin (recommended)**

The repo doubles as its own plugin marketplace, so you can install it directly from inside Claude Code:

```bash
claude plugin marketplace add darthursteele/job-application-pipeline
```

```bash
claude plugin install job-application-pipeline@job-application-pipeline
```

Or from within a session: `/plugin marketplace add darthursteele/job-application-pipeline`, then `/plugin install job-application-pipeline`. Updates arrive with `/plugin marketplace update`.

**Claude Code — manual clone**

Personal skills work in every project:

```bash
git clone git@github.com:darthursteele/job-application-pipeline.git /tmp/jap && cp -r /tmp/jap/skills/job-application-pipeline ~/.claude/skills/
```

For a project-scoped skill shared through git, copy `skills/job-application-pipeline/` into your repo's `.claude/skills/` instead. Claude Code picks up new skills automatically — no restart needed.

**Claude (web, desktop, or mobile app)**

Zip the `skills/job-application-pipeline/` folder (the `SKILL.md` plus `references/` and `subagents/`) into a `.skill` file, then upload it from Settings → Capabilities → Skills. Anyone in the org can trigger it from a normal conversation after that.

**Cowork**

Drop `skills/job-application-pipeline/` into your Cowork skills directory the same way as Claude Code above, or package and upload it as a `.skill` file if you're distributing it to a team.

Once installed, check that it's live by asking Claude something like "help me apply to [company]." It should open with Stage 1 and ask for the job description and your resume.
