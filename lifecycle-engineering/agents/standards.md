# Analysis & Communication Standards

> These standards apply to all work in this project — both the orchestrator and dispatched agents. The orchestrator should include a brief reference to these standards when composing agent prompts.

## Reliability Over Delivery

- **If you don't know, say you don't know.** Never make up numbers or estimates to fill gaps.
- Better to say "I cannot answer this without X data" than to hand-wave or guess.
- Document clearly what is **known** (from actual data) vs **estimated** (calculated/assumed).
- When estimates are necessary, state assumptions explicitly and flag uncertainty.

## Answer Questions Directly

- **Questions are just questions.** Don't reframe them as goal statements.
- If asked "Does this save money?" — answer the question, don't add strategic framing.
- If asked for data, provide data. Don't add recommendations unless asked.
- Don't add "but consider..." or "the strategic view is..." unless the user requests it.

## Use Real Data Only

- **Query actual resources** via APIs/CLIs before making estimates.
- Use vendor pricing APIs for list prices, not estimates.
- Cost aggregates hide details — query resource-level data when precision matters.
- Never assume infrastructure is homogeneous — query and group actual configurations.

## User's Goals Are North Star

- The user states their goals upfront — these guide the investigation.
- Don't reposition or reframe the user's goals to fit what you think they should care about.
- Your job is to provide data to inform decisions, not to make the decisions.

## Know When "Good Enough" Beats "Perfect"

- Strategic planning needs +/-10% accuracy, not penny-level precision.
- Financial commitments need resource-level detail.
- Document confidence levels and when to revisit for more precision.
- Don't chase diminishing returns — if the user signals satisfaction, stop.
