# Job Application Pipeline — Claude Code Instructions

This file is read automatically by Claude Code at session start. It configures the pipeline for CLI execution with subagents.

---

## Recommended Setup

```bash
claude --model claude-sonnet-4-6 \
       --permission-mode acceptEdits
```

For best research quality, use a Max plan subscription — Stage 2 spawns four parallel subagents and burns tokens quickly. Pro plan will work but may hit rate limits mid-pipeline.

---

## Stage 2 Subagent Configuration

When executing Stage 2, the `Task` tool should be available. Spawn all four agents simultaneously — do not run them sequentially.

**Working directory:** all partial JSON files write to the current session folder alongside the main output files. Clean them up after merging.

**Agent invocation pattern:**
```
Task: Run company fundamentals research for {company}
Prompt: [contents of subagents/stage2-agent-a-fundamentals.md, with variables substituted]
```

Substitute these variables in each subagent prompt before spawning:
- `{company}` — company name from the JD
- `{role}` — role title from the JD  
- `{department}` — department if identifiable from the JD, otherwise "unknown"
- `{jd_text}` — full JD text
- `{company-slug}` — kebab-case company name (e.g., "williams-sonoma")
- `{stage1_jd_flags}` — JSON array from session state (Agent D only)

**Merge order:** A → B → C → D. If two agents produced conflicting confidence levels on the same claim, keep the higher-confidence value and log the discrepancy in the Information Quality Report section of the company brief.

---

## File Permissions

Claude Code will need to:
- Read/write files in the current working directory
- Make web search requests (requires web search tool enabled)
- Write JSON and Markdown files

All file writes are to the current directory only. No system files are touched.

---

## Session Structure

Each pipeline run creates a folder:
```
{company-slug}_{role-slug}/
  {company-slug}_company-brief.md
  {company-slug}_company-analysis.json
  {company-slug}_session-state.json
  {company-slug}_resume-optimized.md
  {company-slug}_cover-letter.md
  {company-slug}_additional-materials.md   ← if needed
```

Point Claude Code at the directory containing `SKILL.md` as the project root. Output files write to a subdirectory created at pipeline start.

---

## Gate Behavior

The pipeline has explicit stop points (⛔ markers). Claude Code should pause and wait for user input at each gate — do not attempt to auto-continue past gates even if the previous output seems complete. The gates exist because user judgment at those points materially affects output quality.

---

## Resuming a Pipeline

If a session is interrupted mid-pipeline, resume by pointing Claude Code at the existing `{company-slug}_session-state.json` and stating which stage to resume from. Session state captures all approved decisions — no need to re-run completed stages.
