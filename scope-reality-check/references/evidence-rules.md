# Evidence Rules

Use this reference only when factual verification can materially change the reality check.

## Core principle

Evidence is for deciding the verdict, not decorating it.

Verify the smallest set of claims that can flip the conclusion. Stop when additional evidence would not materially change the decision.

## Evidence hierarchy

Prefer, in order:

1. Current source code, runtime state, repository files, first-party product documentation, or direct system output.
2. Official filings, statistics, standards bodies, regulators, vendor documentation, or direct announcements.
3. Reputable reporting or research with clear sourcing.
4. Community reports for experience patterns, clearly labeled as anecdotal.

Do not treat repeated social-media claims as proof merely because they are popular.

## Freshness

Use a live source when the claim depends on current:

- headcount, revenue, users, pricing, limits, quotas, product features
- laws, regulations, platform policies, standards, compliance obligations
- repository state, releases, issues, PRs, dependencies, architecture
- outages, incidents, provider availability, market conditions

If live verification is unavailable, state that the point is not freshly verified and avoid false precision.

## Repo-specific checks

For a user-provided repository, inspect only what is needed to test the claim. Useful evidence may include:

- README promises versus actual tree contents
- dependency files
- entrypoints and core modules
- tests and evals
- CI configuration
- current branch/commit/PR state
- security-sensitive defaults
- missing files that documentation claims exist

Do not infer maturity from stars, screenshots, badges, or README polish alone.

## Reality-anchor quality

A good anchor attacks a decisive assumption.

Good:
- “The README claims evals exist, but the current tree has no eval directory.”
- “The provider requires production approval, so the proposed same-day launch depends on an external gate.”
- “The current repo has no persistence layer, so multi-user state is not implemented.”

Weak:
- “Big systems are hard.”
- “Security is important.”
- “AI is not magic.”

## Precision discipline

- Never invent exact numbers for rhetorical effect.
- Distinguish measured fact, sourced claim, inference, and scenario.
- Prefer qualitative language when the evidence does not support precision.
- Do not turn one anecdote into a universal rule.
- Do not use historical evidence as if it automatically represents the current state.

## Legal and regulated topics

Use regulations as feasibility constraints only when relevant. Avoid turning a reality check into definitive legal, financial, medical, or security advice.

When possible, identify jurisdiction and date and distinguish:

- confirmed requirement
- likely compliance work
- general risk requiring specialist review

## Stop rule

Stop gathering evidence when the material conclusion is already stable. More citations are not automatically more rigorous.
