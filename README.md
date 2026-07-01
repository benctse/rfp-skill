# commercetools-rfp — Claude Code Skill

A Claude Code skill for answering RFPs (Requests for Proposal) with commercetools. It turns a customer RFP document into a structured, accurate proposal response — with requirement scoring, gap analysis, and a complete response document.

## What it does

```
/commercetools-rfp init       → drop RFP_CONFIG.md and folder structure
/commercetools-rfp analyze    → extract and score requirements from the RFP document
/commercetools-rfp generate   → produce the full proposal response
/commercetools-rfp review     → final completeness check before sending
```

**init**: Creates `RFP_CONFIG.md` (company profile, capabilities, case studies, team, pricing) and the `RFP/` folder structure. Drop the customer's RFP document in `RFP/source/`.

**analyze**: Reads the RFP, extracts all requirements, scores each one against CT capabilities (✅ Full / ⚠️ Partial / ❌ Gap / ❓ Unknown), identifies risks and differentiators, and outputs `RFP/analysis/requirements-analysis.md`.

**generate**: Reads the config and analysis, then produces `RFP/response/proposal-<customer>.md` — a complete proposal with executive summary, requirements response table, architecture, implementation plan, pricing, team, and case studies.

**review**: Runs a coverage checklist — every requirement addressed, no `[TODO]` placeholders, no unsupported claims, case studies are real — and flags blockers before the proposal is sent.

## Key design principles

- **Verify before claiming**: before writing any CT capability claim, the skill queries the CT docs MCP (`commercetools-documentation-search`) to confirm the feature exists and its scope. No hallucinated platform features.
- **Never hide gaps**: requirements the platform doesn't support are acknowledged directly, with a proposed alternative. Evaluation committees find gaps — it's better to name them.
- **Config-driven**: all company-specific content (capabilities, case studies, team, pricing) comes from `RFP_CONFIG.md`. The skill never invents references or pricing.
- **Review gate**: the `review` mode enforces a checklist before the document is sent — coverage, tone, claims, and placeholders.

## Install

This skill lives in `~/.claude/skills/`. To use it, clone this repo there:

```bash
git clone https://github.com/benctse/rfp-skill ~/.claude/skills/commercetools-rfp
```

Or pull updates to an existing install:

```bash
git -C ~/.claude/skills/commercetools-rfp pull
```

Then invoke from Claude Code:

```
/commercetools-rfp init
```

## File structure

```
commercetools-rfp/
  SKILL.md                              ← main skill instructions (loaded by Claude Code)
  README.md                             ← this file
  references/
    rfp-config-template.md              ← RFP_CONFIG.md template
    rfp-analysis-template.md            ← requirements analysis report template
    rfp-response-template.md            ← full proposal response template
    requirement-scoring-guide.md        ← scoring calibration and examples
```

## Usage flow

```
1. /commercetools-rfp init
   → Fill in RFP_CONFIG.md
   → Drop the customer's RFP in RFP/source/

2. /commercetools-rfp analyze
   → Review RFP/analysis/requirements-analysis.md
   → Resolve any ❓ unknowns before generating

3. /commercetools-rfp generate
   → Review RFP/response/proposal-<customer>.md
   → Fill in any [TODO] placeholders

4. /commercetools-rfp review
   → Fix any ⚠️ blockers flagged
   → Send
```
