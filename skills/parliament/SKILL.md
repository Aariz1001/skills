---
name: parliament
description: Apply proportionate adversarial scrutiny and evidence-based deliberation to consequential agent decisions. Use when selecting architectures, evaluating competing implementations, making irreversible or high-impact changes, resolving significant trade-offs, or challenging assumptions that could produce costly mistakes. Generate credible alternatives, construct strong objections, investigate uncertainty, revise proposals, and reach a justified decision without endless debate or artificial consensus.
---

# Parliament — No Proposal Passes Without Scrutiny

## Identity

Parliament is inspired by the British parliamentary system's mechanisms of proposal, opposition, scrutiny, amendment, debate, and recorded decisions.

Its purpose is not to simulate politics or reproduce parliamentary ceremony.

Its purpose is to prevent an AI agent from treating its first plausible solution as automatically correct.

**Governing principle: Challenge the proposal, investigate the objections, improve the decision, and then act.**

Parliament addresses premature commitment, confirmation bias, weak alternatives analysis, insufficient scrutiny, and unjustified confidence.

It must not create bureaucracy for trivial decisions.

---

## 1. Mission

Parliament must:

1. Recognise decisions that deserve scrutiny.
2. Distinguish assumptions from established facts.
3. Generate credible alternative approaches.
4. Construct substantive objections to the preferred approach.
5. Investigate meaningful uncertainty.
6. Evaluate trade-offs against explicit criteria.
7. Revise proposals when criticism reveals weaknesses.
8. Reach decisions based on evidence and requirements.
9. Record consequential decisions and their rationale.
10. Avoid endless deliberation.
11. Escalate decisions requiring user authorisation.
12. Recognise when no available option is sufficiently justified.

Parliament should improve decision quality, not merely increase reasoning length.

---

## 2. Activation

Use Parliament when:

- Selecting a software architecture.
- Choosing between significantly different implementations.
- Introducing major dependencies.
- Planning migrations.
- Making consequential security or privacy decisions.
- Changing data storage or persistence.
- Evaluating potentially irreversible operations.
- Choosing between competing agent strategies.
- Assessing high-impact performance trade-offs.
- Resolving conflicting requirements.
- Evaluating substantial design changes.
- Making decisions where failure would be costly.

Do not invoke full parliamentary scrutiny for:

- Routine formatting.
- Obvious bug fixes.
- Small visual adjustments.
- Straightforward implementation details.
- Decisions already settled by explicit user requirements.
- Changes with negligible risk and clear conventions.

---

## 3. Initial Inspection

Before deliberation, understand the actual decision.

### 3.1 Define the question

Express the decision as a concrete question.

Bad:

"What architecture is best?"

Good:

"Should this feature use native components, an embedded web view, or a hybrid approach, given the project's requirements for accessibility, performance, isolation, and dynamic content?"

A poorly defined question produces a poorly defined debate.

### 3.2 Establish the objective

Identify:

- What outcome is required?
- Who benefits?
- What constraints apply?
- What constitutes success?
- What failure modes matter?
- What existing commitments must be preserved?

### 3.3 Gather relevant evidence

Inspect:

- Existing code.
- Repository instructions.
- Technical documentation.
- Relevant tests.
- Performance evidence.
- Compatibility requirements.
- Security boundaries.
- Existing architectural decisions.
- User requirements.

Do not begin a lengthy debate when a simple inspection can settle the question.

### 3.4 Separate facts and assumptions

Classify important claims as:

- Verified fact.
- Strongly supported inference.
- Working assumption.
- Unknown.

Do not present assumptions as established evidence.

---

## 4. Adaptive Scrutiny

Parliament operates at three levels.

### Level 1: Routine scrutiny

Use for low-risk, reversible decisions.

Procedure:

1. Identify the obvious approach.
2. Check for one significant flaw.
3. Proceed if the approach remains justified.
4. Verify the result.

Do not create formal decision documents.

### Level 2: Structured scrutiny

Use for moderately consequential decisions with plausible alternatives.

Procedure:

1. Define the decision.
2. Identify the preferred approach.
3. Identify at least one credible alternative.
4. Construct the strongest relevant objection.
5. Compare trade-offs.
6. Select an approach.
7. Verify important assumptions.

### Level 3: Full scrutiny

Use for high-impact, expensive, difficult-to-reverse, or security-sensitive decisions.

Procedure:

1. Define objectives and constraints.
2. Gather evidence.
3. Generate credible alternatives.
4. Evaluate feasibility.
5. Conduct adversarial review.
6. Investigate material uncertainties.
7. Amend proposals.
8. Compare remaining options.
9. Record the decision.
10. Obtain necessary approval.
11. Implement and verify.

Scrutiny level should depend on consequence, uncertainty, reversibility, and complexity.

Do not use arbitrary numeric scoring as a substitute for judgement.

---

## 5. The Parliamentary Procedure

### Stage 1: First Reading — Proposal

Construct the initial proposal.

Include:

- Intended outcome.
- Proposed approach.
- Key assumptions.
- Expected benefits.
- Known costs.
- Relevant risks.
- Alternatives already considered.

The proposal must be specific enough to evaluate.

Avoid vague statements such as:

"This approach is scalable and modern."

Explain what makes it appropriate for the actual requirements.

### Stage 2: The Opposition — Strongest Objection

Construct the strongest reasonable objection to the proposal.

The opposition must challenge substance, not invent superficial criticism.

Investigate:

- Hidden assumptions.
- Failure modes.
- Maintenance burden.
- Compatibility issues.
- Security implications.
- Performance concerns.
- Operational complexity.
- User experience consequences.
- Long-term constraints.
- Opportunity costs.

The objective is not to defeat the proposal.

The objective is to discover whether it deserves to survive scrutiny.

### Stage 3: Committee Stage — Investigation

Investigate objections that could materially change the decision.

Use available evidence:

- Source inspection.
- Documentation.
- Existing tests.
- Benchmarks.
- Small prototypes.
- Relevant technical references.
- Measurable requirements.

Do not run experiments merely to create the appearance of rigour.

Investigate the uncertainties that matter.

### Stage 4: Amendments — Improve the Proposal

If criticism reveals weaknesses, revise the proposal.

Possible amendments:

- Reduce scope.
- Introduce isolation.
- Change dependencies.
- Add safeguards.
- Simplify architecture.
- Improve compatibility.
- Adjust implementation boundaries.
- Introduce staged migration.
- Add verification.
- Select a different approach.

Do not defend the original proposal merely because it was proposed first.

### Stage 5: Division — Decision

Evaluate remaining options against explicit criteria.

Possible criteria:

- Requirement satisfaction.
- Correctness.
- Maintainability.
- Performance.
- Security.
- Accessibility.
- Operational cost.
- Complexity.
- Reversibility.
- Compatibility.
- Delivery time.
- User impact.

Criteria must reflect the actual task.

Do not assign arbitrary numerical scores merely to make a subjective decision appear scientific.

When quantitative evidence exists, use it appropriately.

### Stage 6: Royal Assent — Authorisation

Determine whether the selected action requires user approval.

Examples:

- Destructive data migration.
- Publishing externally.
- Spending money.
- Changing security-sensitive settings.
- Deleting important resources.
- Performing irreversible operations.

Parliament does not grant permissions.

It only identifies when authorisation is required.

### Stage 7: Hansard — Decision Record

For consequential decisions, record:

- The question.
- The chosen approach.
- Alternatives considered.
- Main objections.
- Evidence.
- Accepted trade-offs.
- Remaining uncertainty.
- Validation requirements.
- Conditions for revisiting the decision.

Do not create permanent records for trivial decisions.

---

## 6. Opposition Quality Rules

The opposition must be credible.

Bad objections:

- "This might be bad."
- "There could be performance problems."
- "Another approach may be better."
- "The implementation might be complicated."

Good objections:

- "The proposed WebView implementation introduces a separate accessibility surface and may require additional focus-management work."
- "The migration cannot be rolled back safely without preserving the previous data representation."
- "The proposed shared mutable state could produce conflicting updates during concurrent execution."
- "The new dependency duplicates capabilities already available in the project."

An objection should identify a plausible mechanism of failure or disadvantage.

Avoid strawman alternatives.

Avoid objections that are irrelevant to the requirements.

---

## 7. Evidence Standards

Evidence should be proportional to the decision.

Prefer:

1. Direct observation of the relevant system.
2. Reproducible tests or measurements.
3. Authoritative technical documentation.
4. Established project constraints.
5. Strongly supported engineering reasoning.
6. Explicitly labelled assumptions.

Do not invent benchmarks, documentation claims, or test outcomes.

If evidence is unavailable, acknowledge uncertainty.

A decision may still be made under uncertainty when justified.

---

## 8. Avoid Artificial Consensus

Do not pretend that multiple roles generated by the same model constitute independent expert review.

The labels "Government", "Opposition", and "Committee" are reasoning structures.

They do not automatically provide independent evidence.

When genuine independent agents or reviewers are available and the decision warrants them, they may contribute separate evaluations.

When they are unavailable, use explicit self-critique and external evidence without claiming independent consensus.

---

## 9. Avoid False Balance

Not every alternative deserves equal consideration.

If one option clearly violates a mandatory requirement, reject it.

If one option is demonstrably unsafe, do not treat it as equally viable merely to create a balanced debate.

If established evidence strongly favours one approach, recognise that.

Parliament requires scrutiny, not artificial symmetry.

---

## 10. Avoid Endless Debate

Deliberation must terminate.

Stop when:

- The requirements are understood.
- Credible alternatives have been considered.
- Material objections have been addressed or accepted.
- Remaining uncertainty is tolerable.
- The decision is justified.
- Further analysis is unlikely to change the outcome.

Do not continue generating objections after the decision has become sufficiently clear.

If the decision remains blocked by missing information, identify exactly what information is needed.

---

## 11. Decision Examples

### Example A: Database selection

Question: "Should the application introduce a new database library?"

Government: proposes a new library for improved developer ergonomics.

Opposition: notes that the project already uses a supported persistence framework and that introducing another library may duplicate functionality.

Committee: inspects actual requirements and existing persistence capabilities.

Amendment: use the existing framework unless a demonstrated requirement cannot be met.

Decision: avoid the new dependency unless its benefit is established.

### Example B: UI architecture

Question: "Should dynamic AI-generated interfaces use native components or WebView?"

Government: proposes WebView for flexibility.

Opposition: raises accessibility, performance, lifecycle, and isolation concerns.

Committee: examines actual UI requirements and platform constraints.

Amendment: consider a hybrid architecture with native controls for trusted application functionality and isolated WebView content where appropriate.

Decision: select based on demonstrated requirements rather than assuming one technology is universally superior.

### Example C: Data migration

Question: "Should existing stored records be converted to a new schema?"

Government: proposes direct migration.

Opposition: identifies rollback and compatibility risks.

Committee: inspects schema differences, migration tooling, and test coverage.

Amendment: introduce a tested migration path with backups or another suitable recovery mechanism.

Decision: proceed only when required safeguards and approvals are satisfied.

---

## 12. Interaction With Other Skills

### Spoons

Spoons governs proportionality and practical implementation.

Parliament governs scrutiny of consequential choices.

Spoons should prevent Parliament from turning trivial decisions into elaborate debates.

Parliament should prevent Spoons from oversimplifying genuinely consequential decisions.

### The Queue

The Queue coordinates concurrent execution.

Parliament may evaluate competing coordination strategies when the choice is consequential.

Parliament does not independently implement locks, queues, or runtime scheduling.

### Other specialised skills

Respect security, privacy, recovery, and deployment requirements.

Parliament does not override mandatory constraints.

---

## 13. Good and Bad Practices

### Good

- Defining the decision clearly.
- Identifying credible alternatives.
- Challenging assumptions.
- Using evidence.
- Considering failure modes.
- Revising weak proposals.
- Recognising uncertainty.
- Making proportionate decisions.
- Recording consequential trade-offs.
- Stopping when further debate adds little value.

### Bad

- Accepting the first solution automatically.
- Inventing superficial objections.
- Treating all alternatives as equally credible.
- Fabricating evidence.
- Creating fake independent consensus.
- Debating trivial decisions endlessly.
- Ignoring mandatory constraints.
- Defending a proposal after it has been disproven.
- Confusing a decision with user authorisation.
- Producing elaborate reports without improving the outcome.

---

## 14. Optional Decision Record

For major decisions, use a concise structure.

```markdown
# Decision: [Title]

## Question
What decision must be made?

## Requirements
What must the solution satisfy?

## Options
Which credible approaches were considered?

## Evidence
What observations or sources support the evaluation?

## Opposition
What were the strongest objections?

## Decision
Which approach was selected?

## Rationale
Why was it selected?

## Trade-offs
What disadvantages were accepted?

## Remaining uncertainty
What is not yet established?

## Validation
How will the decision be tested?

## Revisit conditions
What evidence or change would justify reconsideration?
```

Do not create such records automatically for routine decisions.

---

## 15. Verification

After implementation, verify whether the chosen approach actually delivered the expected result.

Check:

- Requirements satisfied.
- Assumptions validated where possible.
- Important risks addressed.
- Tests completed.
- Expected trade-offs understood.
- No unacceptable regressions.
- Remaining uncertainty accurately reported.

If implementation evidence contradicts the original decision, reconsider it.

A recorded decision is not permanently correct merely because it was documented.

---

## 16. Expected Result

Successful Parliament behaviour produces:

- Better-justified technical decisions.
- Fewer unchallenged assumptions.
- More credible alternatives analysis.
- Reduced premature commitment.
- Explicit trade-offs.
- Appropriate risk awareness.
- Clear decision rationale.
- Less unnecessary rework.
- Decisions that can be revisited when evidence changes.

Parliament should improve the quality of decisions without making the agent unnecessarily slow.

## Final Principle

**The purpose of opposition is not to prevent progress. It is to ensure that progress survives scrutiny.**
