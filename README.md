# PE Deal Screening Prototype

A file-based prototype for preliminary private-equity deal screening, built with [Claude Code](https://claude.com/claude-code). A reusable Claude Code skill assesses synthetic deals against a fund's investment criteria and produces structured, source-bound screening memos.

> **Note:** All companies, deals, and the fund are fictional. Output supports preliminary screening only; investment decisions remain with humans.

## How It Works

1. **Criteria:** [`criteria/investment_criteria.md`](criteria/investment_criteria.md) defines the fund's screening criteria and is the single source of truth.
2. **Deals:** Each file in [`deals/`](deals/) describes one synthetic deal, containing only case-specific facts.
3. **Screening:** The [`screen-deal`](.claude/skills/screen-deal/SKILL.md) skill reads both files, rates each criterion **Met**, **Not met**, or **Insufficient information**, and writes a memo to [`outputs/`](outputs/).

## Repository Structure

```
.
├── .claude/skills/screen-deal/
│   └── SKILL.md          # Screening procedure and memo template
├── criteria/
│   └── investment_criteria.md
├── deals/
│   ├── deal_alpha.md
│   └── deal_beta.md
├── outputs/              # Generated screening memos (versioned)
├── CLAUDE.md             # Project rules for Claude Code
└── README.md
```

## Screening Memo Format

Each memo contains:

- **Deal Snapshot:** a neutral restatement of the deal file's facts
- **Criteria Assessment:** one status and a cited justification per criterion
- **Missing Information:** absent facts that matter for screening or diligence
- **Preliminary Risks:** only risks supported by explicit facts in the deal file
- **Diligence Questions:** specific questions covering every material gap and risk
- **Human Review:** a fixed disclaimer

## Design Principles

- **Source-bound:** Every factual claim traces back to the deal file. No outside data, no invented facts.
- **No verdicts:** Memos report on each criterion and never give an overall score or recommendation.
- **Unknowns stay separate from risks:** Missing facts go under Missing Information. Risks require an explicit, present signal in the source.
- **Non-destructive versioning:** Existing memos are never overwritten. New runs write `_v2`, `_v3`, and so on.
- **Human in the loop:** Every memo ends with a human-review disclaimer.

## Skill Iteration Example

The Deal Beta memos document one refinement cycle:

| Version | What happened |
|---|---|
| `deal_beta_screening_memo_v2.md` | A regression review found a Not met criterion duplicated as a risk, and material gaps lost by merging them into broader questions. |
| — | The skill's Missing Information, Preliminary Risks, and Diligence Questions steps were refined with general rules, with no deal-specific patches. |
| `deal_beta_screening_memo_v3.md` | A re-screen was verified against acceptance criteria: statuses unchanged, the duplicate risk removed, and the material gaps restored. |

## Usage

Open the project in Claude Code and ask:

```
Screen deal_beta using the screen-deal skill.
```

To screen a new deal, add `deals/deal_<name>.md` and run the skill on it.

## Sample Deals

| Deal | Company | Description |
|---|---|---|
| Alpha | Northstar Workflow Systems | B2B software for field-service companies |
| Beta | Summit Industrial Intelligence | Industrial inspection services using proprietary software |
