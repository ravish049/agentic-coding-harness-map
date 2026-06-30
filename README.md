# AI Coding Agent Harness Map

A single-file HTML diagram showing how a production codebase wires AI coding agents into its development workflow — mapped against three industry frameworks, with the 4 gaps that remain after extended iteration.

**Open `harness-map.html` in any browser.** That's the artifact. The rest of this README is context.

## What this is

Not a tool. Not a product. A **case study artifact**: one team's working setup with product and internal names removed, mapped against published frameworks so you can see what's strong, what's weak, and what's missing — without having to guess.

The diagram answers three questions in one view:
1. Where does each control (rule, gate, skill, agent) live in the workflow?
2. Which industry framework does it satisfy?
3. What's still missing, and where would it plug in?

## What this is not

- Not a template you copy. Your gates and rules will be different.
- Not a tool. There is nothing to install.
- Not maintained as a product. No issues triaged, no support, no roadmap. PRs welcome but no commitment.
- Not benchmarked. The "strong / weak / gap" labels are one team's self-assessment, not a measured comparison.

## The three frameworks mapped

| Framework | Source | What it captures |
|---|---|---|
| **CNCF four pillars** | platform engineering tradition; surfaced in [Faros 2026](https://www.faros.ai/blog/harness-engineering) | golden paths · guardrails · safety nets · manual review |
| **Five-layer harness** | [Faros 2026](https://www.faros.ai/blog/harness-engineering) | tool orchestration · verification loops · context+memory · guardrails · **observability** |
| **Three loops** | [codagent.beehiiv — Slot Machines & Safety Nets](https://codagent.beehiiv.com/p/slot-machines-and-safety-nets) | outer (project) · orchestration (feature) · inner (task) |

The Beehiiv piece is great but partial — it omits observability and background execution. Cross-referencing with Faros and the SWE-CI direction is what surfaces the real gaps.

## The 4 gaps (after ~12 months of harness iteration)

1. **Scheduled cleanup / drift agent** — cron-fires existing skills against the whole repo, not the diff. Outputs a weekly tracking issue, not 19 PRs.
2. **Cross-model reviewer on money / security paths** — scoped to the security-critical subtree. Concrete evidence: [GPT found 3 critical bugs in Claude Code's own source](https://medium.com/@ribrewguy/what-i-found-when-claude-reviewed-codexs-work-5d83a348a2d9).
3. **Agent observability — the 5th harness layer** — token cost, cycle time, bypass count, rework rate per story. Without it you can't tell which of your N rules pay rent.
4. **Background draft-PR agent (Devin/Copilot-cloud style)** — listed mainly so you can deliberately decide *not* to build it for a small team.

Full reasoning, effort estimates, and "what existing primitive does this build on" are in the HTML.

## Context (the codebase this came from)

- A multi-tenant, RLS-based SaaS in active development
- A small team + Claude Code as the coding harness
- ~11 domain-specialist subagents (backend, frontend, data, security, QA, infra, docs, orchestration)
- ~20 pre-commit + CI gates, each bypassable only with an audited written reason
- A short inviolable-invariants doc + an operational-rules doc + architecture decision records
- Spec-first gate: no implementation until a spec markdown exists
- Bug-fix verification loop: reproduce → root-cause → fix → re-reproduce → regression test

Product, customer, and internal names are removed. The workflow structure is real.

## How to read the diagram

1. Top — three industry frameworks scored: green = strong, yellow = partial, red = gap
2. Middle — **workflow swimlane**, six columns (Intent → Epic → Story → Implement → Review → Ship), five rows (Outer / Orchestration / Inner / Observability / Async)
3. Cells with `GAP N` are missing. The bottom of the diagram details each gap.

## How to adapt this to your project

1. Replace the lane content with your own gate names / skill names / file paths
2. Score each cell honestly (green / blue / yellow / red — legend at bottom of HTML)
3. Look for whole *rows or columns* that are mostly red — that's a systemic gap, not a one-off
4. Compare against the four CNCF pillars and five harness layers — if any of them are entirely missing from your map, that's likely a real blind spot

## Why publish this

Most public writeups of AI coding harnesses are vendor blog posts ("buy our agent") or speculation ("imagine if…"). This is one concrete data point from a real working codebase, framed against named industry frameworks so you can argue with it.

If you build something similar and your gap list looks different, that's the conversation worth having.

## Sources

- [codagent.beehiiv — Slot Machines and Safety Nets](https://codagent.beehiiv.com/p/slot-machines-and-safety-nets) — three-loop framing
- [Faros — Harness Engineering 2026](https://www.faros.ai/blog/harness-engineering) — five-layer harness + CNCF pillars
- [Martin Fowler — Spec-Driven Development (Kiro / Spec Kit / Tessl)](https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html) — the three SDD levels
- [GitHub Copilot cloud agent docs](https://docs.github.com/copilot/concepts/agents/coding-agent/about-coding-agent) — background-agent reference
- [SWE-CI benchmark](https://arxiv.org/abs/2603.03823) — long-term codebase maintenance evaluation
- [alecnielsen/adversarial-review](https://github.com/alecnielsen/adversarial-review) — cross-model debate loop
- [What I Found When Claude Reviewed Codex's Work](https://medium.com/@ribrewguy/what-i-found-when-claude-reviewed-codexs-work-5d83a348a2d9) — concrete evidence of model-family blind spots

## Meta

The diagram was generated by Claude Code itself, working on the same codebase it maps. The harness reviewing the harness.

## License

MIT. See `LICENSE`.
