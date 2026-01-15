# MEDDPIC Deal Analyzer

A Claude Code skill for analyzing sales call transcripts using the MEDDPIC qualification methodology.

## Live Demo

View a sample anonymized analysis: **[https://olivier-oref.github.io/meddppicc-sample/](https://olivier-oref.github.io/meddppicc-sample/)**

## What is MEDDPIC?

MEDDPIC is a B2B sales qualification framework:

| Element | Description |
|---------|-------------|
| **M** - Metrics | Quantifiable business impact the prospect expects |
| **E** - Economic Buyer | Person with final budget authority |
| **D** - Decision Criteria | Factors used to evaluate solutions |
| **D** - Decision Process | Steps and approvals required to purchase |
| **P** - Paper Process | Procurement, legal, and contract requirements |
| **I** - Identify Pain | Critical business issues driving the need |
| **C** - Champion | Internal advocate selling on your behalf |
| **C** - Competition | All alternatives being considered |

## Skill Features

- Fetches transcripts from Fireflies.ai or Fathom.video
- Auto-detects call participants and roles
- Scores each MEDDPIC element (1-10)
- Generates stakeholder matrix with pain points and blockers
- Produces gap analysis with recommended actions
- Outputs HTML report and 2-page PDF

## Installation

Copy the `skill/` folder to your Claude Code skills directory:

```bash
cp -r skill/ /path/to/project/.claude/skills/meddpic-analyzer/
```

## Usage

Invoke the skill by saying:
- "analyze this deal"
- "MEDDPIC analysis"
- "qualify this opportunity"

## Output

The skill generates:
1. **Full HTML report** - Complete analysis with all sections
2. **2-page PDF** - Executive summary format for sharing

## Skill Files

| File | Purpose |
|------|---------|
| `SKILL.md` | Workflow instructions and invocation triggers |
| `meddpic-framework.md` | Framework definitions and scoring guide |
| `template-full.html` | Full HTML analysis template |
| `template-2page.html` | Print-optimized 2-page PDF template |
