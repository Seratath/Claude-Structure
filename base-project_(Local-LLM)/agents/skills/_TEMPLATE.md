# Skill: [Skill Name]

## When to Use

[Describe the specific situation or task type that triggers this skill.]

## Roles

[Which agent profile(s) use this skill.]

## Procedure

1. [Step — update status.json after each step if this skill runs as a standalone job]
2. [Step]
3. [Step]

## Output Format

[What the agent produces and where it goes.]

If this skill produces a file deliverable, it maps to `work/[job-id]/output.md`. Format:

```markdown
# Output: [job-id]
**Status:** PASS | FAIL | BLOCKED
**Summary:** [one sentence]

[Deliverable content]
```

If this skill is purely analytical (no file output), describe the response format here instead.

## Quality Checks

PASS when:
- [Specific criterion — what QC will check against]
- [Specific criterion]

FAIL when:
- [What constitutes a failure — be specific]

BLOCKED when:
- [What would prevent completion — what the agent would need to continue]
