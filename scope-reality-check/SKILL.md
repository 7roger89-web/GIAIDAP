---
name: scope-reality-check
description: Pressure-test ambitious plans, AI-hype claims, unrealistic timelines, architecture bets, product ideas, automation proposals, or “clone X quickly” assumptions with evidence, hidden-complexity analysis, and a smaller shippable alternative. Trigger only when the user explicitly asks for a hard reality check, brutal critique, roast, red-team, “phản biện gắt”, “tạt nước lạnh”, “tao có đang ngáo không”, “xé kế hoạch này ra”, or equivalent. Do not trigger for ordinary planning, repo review, implementation help, debugging, or neutral evaluation unless the user explicitly asks to be challenged hard.
---

# Scope Reality Check

Pressure-test an explicit user claim without turning skepticism into theater. The skill exists to answer one question:

**“What part of this plan survives contact with reality, and what is the smallest version worth shipping next?”**

The skill is not a general personality. It is a bounded reasoning mode that runs under higher-priority system, project, Supreme-Law, safety, and user instructions.

## Operating contract

When triggered:

1. Preserve the user's actual goal.
2. Deconstruct the plan into its load-bearing assumptions.
3. Verify only the assumptions whose truth materially changes the verdict.
4. Distinguish real difficulty from merely unfamiliar work.
5. Separate compressible work from irreducible constraints.
6. Reconstruct one smaller path that still produces useful evidence.
7. End with a clear next action.

Do not merely criticize. **Deconstruction without reconstruction is incomplete.**

## Trigger discipline

Trigger on explicit requests such as:

- “Phản biện gắt kế hoạch này.”
- “Tạt nước lạnh cho tao xem có đang ngáo không.”
- “Roast this architecture.”
- “Tear this idea apart.”
- “Be brutally honest: can one person clone this in a weekend?”
- “Red-team this AI automation plan hard.”

Do **not** trigger on:

- “Xem repo này.”
- “Giúp tao build MVP.”
- “Review kiến trúc này.”
- “Debug lỗi này.”
- “Lập kế hoạch triển khai.”

For ordinary requests, help normally. Do not smuggle the skill in just because the plan looks ambitious.

## Reasoning sequence

### 1. Model the claim

Reduce the request to the smallest falsifiable claim you can test:

- outcome promised
- deadline
- scale
- staffing
- reliability level
- architecture bet
- automation assumption
- dependency assumption

Do not caricature the user's position to make it easier to attack.

### 2. Calibrate before criticizing

Use one of three internal states:

**Clearly unrealistic** — the plan contradicts a material constraint or compresses essential work beyond plausibility.

**Aggressive but plausible** — the core outcome may work, but scope, reliability, or operational expectations are too broad.

**Actually realistic** — say so. Challenge only the next-order risks that matter.

Never invent hidden doom to justify the skill's existence.

### 3. Verify decisive assumptions

Read `references/evidence-rules.md` when current facts, laws, platform behavior, repo state, pricing, product limits, scale claims, or provider capabilities affect the conclusion.

Verification should be proportional:

- verify what can flip the verdict;
- do not research ten facts when two are decisive;
- do not use precise numbers merely for rhetorical impact;
- if fresh evidence is unavailable, downgrade precision instead of bluffing.

### 4. Expose hidden complexity as failure modes

Select only constraints that can actually break this plan. Translate each into a concrete failure mode.

Useful lenses include:

- product demand and user behavior
- data model and consistency
- auth and permissions
- payments and reconciliation
- security and abuse
- reliability, backup, recovery, observability
- third-party dependencies and approvals
- data quality and migration
- moderation, fraud, trust and safety
- legal or regulatory obligations
- support and offline operations
- distribution and marketplace cold start
- maintenance and ownership after launch

Bad: “Security is important.”

Good: “The automation can submit refunds, but no approval boundary exists, so one hallucinated action becomes a real financial mutation.”

### 5. Run the compression test

Split only relevant work into two buckets.

**AI can often compress:** scaffolding, CRUD/UI assembly, repetitive code, documentation drafts, test generation, code search, refactoring assistance, structured analysis when inputs are available.

**AI does not erase:** unclear product decisions, missing users, absent data, production accountability, real-world operations, security ownership, legal obligations, third-party approval, trust, adoption, organizational change, physical constraints.

Do not repeat these lists mechanically. Adapt them to the task.

### 6. Reconstruct a shippable alternative

Preserve the user's real outcome while removing vanity scope.

Prefer:

- one core loop over a platform
- one user segment over universal support
- one integration over an integration framework
- manual operations behind the scenes over premature automation
- fake scale over premature scale architecture
- a reversible pilot over irreversible rollout
- one measurable decision over a giant dashboard

State what evidence would justify expanding scope later.

Ask internally:

**“Is there a simpler path that produces material evidence sooner?”**

If yes, use it.

## Reality-bound humor

Sharp language is optional; truth is not.

When the user asks for a brutal, playful, sarcastic, or mildly profane tone:

- attach every jab to a real mismatch, hidden cost, contradiction, or failure mode;
- attack the plan, architecture, assumption, bug, deadline, or workflow — not the user's intelligence, identity, family, appearance, or worth;
- prefer analogies that clarify the engineering or business problem;
- after the punchline, return immediately to evidence or the fix.

For Vietnamese users, natural Vietnamese satire is welcome: everyday life, school, office politics, logistics, football, neighborhood drama, traffic, business, social media, folk sayings, or familiar cultural references. Do not mechanically imitate any creator or repeat catchphrases.

A useful sharp line should make the diagnosis clearer. If removing the joke loses no insight, the joke was probably decorative.

## Self-correction

If fresh evidence contradicts the current theory:

1. drop the theory;
2. state what changed;
3. update the verdict;
4. continue from the new state.

Do not defend an earlier critique for consistency. Do not repeat failed arguments with stronger wording.

Keep this correction operational. Do not interrupt the user with ceremonial meta-analysis unless the changed reasoning materially affects the decision.

## Output shape

Use this structure when it helps; do not force headings for short answers.

### Opening hit
State the strongest assumption beside the decisive reality anchor in 1–3 sentences.

### Reality anchors
Give the 2–5 facts or verified observations that matter most. Cite when tools provide citations.

### What actually breaks
Explain the few hidden constraints that materially change feasibility. Use concrete failure modes.

### What AI changes — and what it does not
Show where effort genuinely shrinks and where the plan still carries irreducible work.

### Shippable version
Give one smaller version with:

- what to build now
- what to defer, fake, or operate manually
- what result would justify expansion

### Bottom line
Give a crisp verdict and the next practical action.

Default compact. Expand only when the user asks for a deep teardown or the problem genuinely requires depth.

## Authority and compatibility

- Higher-priority system, project, Supreme-Law, safety, and explicit user instructions remain authoritative.
- This skill must not invent a competing persona or governance layer.
- If a project requires reading a canonical law or current repo state before reasoning, do that first.
- Match the user's technical level in explanation while keeping expert-level rigor in analysis.
- Do not add process rituals, governance, services, databases, agents, or frameworks merely to support the critique itself.

## Failure modes to avoid

- confidence mistaken for evidence
- straw-manning the user's claim
- stale facts used as current proof
- generic checklist dumping
- “AI cannot replace humans” sermons
- scale lectures unrelated to the actual bottleneck
- shaming ambition instead of testing assumptions
- criticism without a smaller executable path
- humor untethered from evidence
- turning ordinary planning/debugging/review into a roast
- meta-dialogue that delays the actual task

## Evaluation

Read `references/evals.md` when testing or revising the skill. Trigger precision, evidence quality, self-correction, and reconstruction quality are all part of correctness.
