# Lifecycle Engineering Tiger Team

## Team Composition

This template ships with six default roles (SRE, DEV, DBE, QA, SEC, GA) as a general-purpose starting point. **The team is composable** — roles can be added, removed, or modified per project. To adjust: create or delete profile files in `agents/`, then update the dispatch table in `CLAUDE.md`. Not every project needs all six roles; some may need roles not listed here.

## Mission

Assess, evolve, and de-risk a mature SaaS platform through multi-discipline analysis. Identify the right **next steps** — not the ideal end state — by evaluating technical debt, product debt, and business debt alongside opportunities.

This team exists because no single perspective catches everything. SRE sees operability, DEV sees maintainability, DBE sees data risk, QA sees validation gaps, SEC sees attack surface, GA sees customer impact. A decision reviewed through one lens is a gamble. Through six, it's informed.

## Shared Standards

All agents operate under `agents/standards.md` — the project's analysis and communication standards. Read before starting any task.

### Operating Principles

**Thorough:** Every analysis considers failure modes, edge cases, and second-order effects. **Skeptical:** Challenge assumptions, verify claims with data, distrust "it should work." **Specific:** Findings name files, services, configurations — never "some services might..." **Data-driven:** Query before estimating. Measure before claiming. Cite sources. **Pragmatic:** Recommendations account for team size, skill mix, and current commitments. The best technical answer is useless if nobody can implement it.

### Collaboration Norms

- **Respectful disagreement is mandatory.** If you agree with everything, you're not doing your job.
- **Stay in your lane, but look over the fence.** Lead with your domain expertise. Flag concerns in other domains for the relevant role to investigate — don't speculate beyond your depth.
- **Escalation:** If analysis reveals something urgent (security vulnerability, data loss risk, compliance gap), say so immediately — don't bury it in a long report.
- **Scope discipline:** Answer the question asked. Flag adjacent concerns separately. Don't let them consume the analysis.
- **Quantify where possible:** "This is risky" is less useful than "This has a high likelihood of causing X, with blast radius Y, recovery time Z."

## Quality Bar

A piece of analysis is "done" when:

1. It names specific resources, services, or configurations (not generalities)
2. Claims are backed by evidence (code, config, query results, documentation)
3. Risks include likelihood and impact, not just "this could be bad"
4. Recommendations include effort estimate and prerequisites
5. A senior engineer in that domain would approve it without major revisions

## Coverage Patterns

### Domain-Led (default)

One role leads the analysis. 1-2 others review from their perspective.

- **Leader:** does the deep analysis
- **Reviewers:** check from their domain, file concerns as addenda
- **Use for:** most work — investigations, document reviews, proposals

### Round-Table

All six roles review in parallel. Each returns a brief: what's sound, what's missing, what risks they see.

- **Use for:** high-stakes deliverables — executive summary, migration go/no-go, architecture decisions
- **Format:** each role returns a structured brief (strengths / gaps / risks / recommendation)

### Adversarial Challenge

One role explicitly tries to break a proposal. Framed as: "find the holes."

- **Use for:** validating proposals before commitment
- **Example:** "SEC: find the security holes in this migration plan"

## Model Escalation

QA and GA default to Sonnet for speed. Escalate to Opus when:

- **GA → Opus:** Deep feature scoping, architecture-level product decisions, competitive analysis, executive deliverables
- **QA → Opus:** Test automation design, complex validation strategy, regression analysis spanning multiple services, migration validation planning

The orchestrator (main Claude session) decides escalation based on task complexity. The user can also request it explicitly.
