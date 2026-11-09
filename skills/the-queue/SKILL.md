---
name: the-queue
description: Coordinate concurrent or dependent agent work safely and efficiently. Use when multiple agents, tasks, tools, processes, or operations may compete for shared resources, modify overlapping files, depend on one another, or create race conditions. Establish ownership, execution order, safe parallelism, conflict handling, fairness, and completion barriers without unnecessarily serialising independent work.
---

# The Queue — Order Before Execution

## Identity

The Queue is inspired by the British cultural convention of orderly queueing: establish who is next, respect the order, avoid pushing ahead without justification, and ensure that everyone is served fairly.

In agent systems, however, blindly processing everything one at a time is inefficient.

The Queue therefore exists to establish **safe ordering where ordering is necessary, and safe parallelism where it is not**.

**Governing principle: No pushing in, no trampling shared work, and no waiting unnecessarily when independent work can proceed.**

The Queue addresses coordination failures involving multiple agents, concurrent tools, shared resources, dependent operations, and asynchronous workflows.

---

## 1. Mission

The Queue must:

1. Identify tasks that can run independently.
2. Identify dependencies that require ordered execution.
3. Detect shared resources and potential conflicts.
4. Assign clear ownership of mutable work.
5. Prevent avoidable race conditions.
6. Avoid duplicate or conflicting operations.
7. Establish completion barriers where necessary.
8. Detect stalled work and unsafe assumptions.
9. Handle failures without corrupting shared state.
10. Preserve useful parallelism.
11. Avoid unnecessary coordination overhead.
12. Produce a coherent integrated result.

The Queue is a coordination protocol, not an instruction to execute everything sequentially.

---

## 2. Activation

Use The Queue when:

- Multiple coding agents are working on the same repository.
- Multiple tasks may modify overlapping files.
- Parallel operations depend on shared state.
- Background processes and foreground actions interact.
- Several tool calls affect the same resource.
- A workflow contains dependencies.
- A task involves potentially conflicting writes.
- An agent needs to merge parallel results.
- Operations require ordering to maintain correctness.
- Shared resources have limited capacity.
- Work must be resumed or reassigned after a stalled operation.

Do not invoke a heavyweight coordination process for a single independent action.

---

## 3. Runtime Limitations

A Markdown skill cannot independently provide:

- Operating-system locks.
- Atomic transactions.
- Distributed consensus.
- Persistent queues.
- Cross-process mutual exclusion.
- Durable job scheduling.
- Reliable worker heartbeats.
- Automatic deadlock detection.
- Transactional rollback.

These require runtime support or appropriate tools.

The Queue can define procedures, ownership conventions, manifests, and checks.

Never assume a written ownership declaration provides an actual lock.

When enforcement is unavailable, use conservative scheduling and verify shared state before modifying it.

---

## 4. Initial Inspection

Before starting concurrent work, inspect the execution environment.

### 4.1 Identify active work

Determine:

- What tasks exist?
- Which tasks are currently running?
- Which tasks are pending?
- Which tasks are complete?
- Which tasks have failed?
- Which tasks are blocked?
- Which tasks have unknown status?

Do not infer that an operation has completed merely because sufficient time has passed.

### 4.2 Identify available execution capabilities

Determine whether the current environment supports:

- Parallel tool calls.
- Multiple agent instances.
- Subagent delegation.
- Isolated working directories.
- Git worktrees.
- Branch-based isolation.
- Background processes.
- Shared files.
- Task tracking.
- Process status inspection.

Use only capabilities actually available.

Do not invent unavailable orchestration tools.

### 4.3 Identify shared resources

Resources may include:

- Source files.
- Git branches.
- Databases.
- Configuration files.
- Build outputs.
- Dependency manifests.
- Generated artifacts.
- Network services.
- API quotas.
- Browser sessions.
- Authentication state.
- Temporary files.
- User-facing application state.

Shared resources are not automatically conflicting resources.

Two tasks reading the same file can usually proceed concurrently.

Two tasks writing the same file require more careful coordination.

### 4.4 Identify dependencies

Classify dependencies as:

- **Independent:** No meaningful dependency.
- **Read dependency:** Requires information produced elsewhere.
- **Write dependency:** Requires another modification to complete.
- **Exclusive resource:** Must not overlap with another operation.
- **Integration dependency:** Requires several outputs before proceeding.
- **External dependency:** Requires a service, user action, or event.

Build a dependency graph when complexity warrants it.

---

## 5. Task Decomposition

Break work into meaningful units.

Each task should have:

- A clear objective.
- Defined inputs.
- Expected outputs.
- Relevant dependencies.
- Resource requirements.
- Ownership boundaries.
- Completion criteria.
- Failure handling expectations.

Avoid splitting work into units so small that coordination costs exceed the benefit.

### Example

User request: "Implement authentication, settings, and onboarding."

Potential decomposition:

Task A: Authentication implementation. Task B: Settings implementation. Task C: Onboarding implementation.

Task D: Integration and verification.

A, B, and C may be parallelisable if their interfaces and file ownership are sufficiently independent.

D depends on the required outputs from A, B, and C.

Do not assume independence merely because the feature names differ.

Inspect shared navigation, dependency injection, configuration, and state ownership first.

---

## 6. Dependency Graph Procedure

For each task:

1. Identify prerequisites.
2. Identify resources it reads.
3. Identify resources it writes.
4. Identify external side effects.
5. Determine whether it can execute concurrently.
6. Establish its completion condition.
7. Determine its failure impact.

Represent the relationship conceptually as:

```text
A ─────┐
       ├── D ── E
B ─────┤
       │
C ─────┘
```

A, B, and C may execute concurrently.

D begins after its prerequisites are satisfied.

E begins after D completes successfully.

A dependency is satisfied by verified completion, not by an optimistic status message.

---

## 7. Resource Ownership

For concurrent work, establish ownership of mutable resources.

### Preferred isolation

Where supported, prefer:

1. Independent worktrees or isolated environments.
2. Separate branches with controlled integration.
3. Non-overlapping file ownership.
4. Explicitly serialised modifications to shared resources.

Isolation does not remove the need for integration checks.

### Ownership rules

- A task should have a clearly defined write scope.
- Avoid assigning overlapping write scopes unnecessarily.
- Shared read access is generally acceptable.
- Shared write access requires coordination.
- Ownership changes must be explicit.
- A task must not silently expand its write scope.
- If an unexpected shared file requires modification, reassess ownership before editing.

### Example

Agent A owns:

```text
features/auth/
```

Agent B owns:

```text
features/settings/
```

Shared file:

```text
app/navigation/AppNavGraph.kt
```

Both agents may need navigation changes.

A safer approach is to assign shared navigation integration to a separate task after both feature implementations are ready.

This avoids concurrent modifications to the same integration point.

---

## 8. Queue Scheduling

Choose an execution strategy based on actual dependencies and risk.

### 8.1 Sequential execution

Use when:

- Operations mutate the same resource.
- One operation depends on another's output.
- The system cannot safely isolate work.
- Side effects must occur in a strict order.

### 8.2 Parallel execution

Use when:

- Tasks are independent.
- Resource conflicts are absent or safely isolated.
- Results can be integrated deterministically.
- The runtime supports the required concurrency.

### 8.3 Bounded parallelism

Limit concurrency when:

- Resources are constrained.
- APIs enforce rate limits.
- Builds consume substantial memory.
- Excessive workers would increase conflicts.
- Integration overhead would outweigh throughput.

Do not maximise worker count merely because parallelism is available.

### 8.4 Priority scheduling

Priority may be justified by:

- Critical failures.
- Blocking dependencies.
- Time-sensitive operations.
- User-defined urgency.
- Resource availability.
- Risk reduction.

Priority must not silently override safety constraints.

---

## 9. Fairness and Starvation Prevention

A task should not remain indefinitely blocked because newer work repeatedly takes precedence.

When the runtime supports queue management:

- Track waiting tasks.
- Identify long-running blockers.
- Reassess priority periodically.
- Avoid repeatedly postponing low-priority tasks.
- Escalate unresolved dependencies when necessary.

Do not interrupt critical operations solely to enforce fairness.

Fairness is subordinate to correctness and justified operational priorities.

---

## 10. Conflict Detection

Before a potentially conflicting modification:

1. Inspect the target resource.
2. Determine whether another task owns or is modifying it.
3. Check whether the resource changed since planning.
4. Identify overlapping modifications.
5. Decide whether to wait, isolate, reassign, or integrate.

### Example

Agent A is refactoring a shared interface.

Agent B is implementing a feature using that interface.

Bad:

Both proceed using different assumptions.

Good:

Agree on the interface contract before implementation, or sequence the dependent work.

### Git considerations

Use repository state and diffs to detect unexpected modifications.

Useful checks may include:

```bash
git status --short
git diff
git diff --check
```

Do not reset, overwrite, or discard changes merely to resolve a conflict.

Existing changes may belong to the user or another agent.

---

## 11. Safe Parallelism

Parallel execution is useful only when it reduces total completion time without introducing unacceptable risk.

Before parallelising, ask:

1. Are the tasks genuinely independent?
2. Are their inputs stable?
3. Are their outputs clearly defined?
4. Are write scopes isolated?
5. Are external side effects safe?
6. Is integration straightforward?
7. Is the expected speed improvement worth the coordination overhead?

If the answers are uncertain, investigate before launching parallel work.

---

## 12. Completion Barriers

A completion barrier prevents downstream work from proceeding before prerequisites are satisfied.

Examples:

- Build after required source changes are integrated.
- Deploy after tests pass.
- Generate documentation after interfaces stabilise.
- Run integration tests after component changes are merged.

A barrier must rely on actual evidence.

Bad:

"Agent A probably finished."

Good:

"Agent A's changes are present, the expected output exists, and the required verification completed."

---

## 13. Failure Handling

When a task fails:

1. Identify the failed operation.
2. Determine which resources it may have modified.
3. Identify dependent tasks.
4. Determine whether retrying is safe.
5. Preserve useful completed work.
6. Reconcile partial state.
7. Retry, reassign, or escalate appropriately.

Do not automatically repeat non-idempotent operations.

Examples include:

- Payments.
- Sending messages.
- Creating accounts.
- Publishing content.
- Destructive database changes.

These may require explicit state verification before any retry.

---

## 14. Stalled Tasks

A stalled task is not necessarily a failed task.

Possible causes:

- Waiting for a dependency.
- Waiting for user input.
- Network delay.
- Tool execution delay.
- Resource contention.
- Process failure.
- Lost status reporting.

Before reassigning work:

- Check available status evidence.
- Inspect partial outputs.
- Determine whether the original task remains active.
- Prevent duplicate side effects.
- Establish safe ownership transfer.

If runtime status cannot be verified, do not claim exclusive ownership.

---

## 15. Deadlocks and Circular Dependencies

Detect circular dependency patterns: task A waits for B, task B waits for A, and neither can proceed.

Resolve by:

- Revising task boundaries.
- Establishing a shared contract.
- Introducing an independent prerequisite.
- Reordering operations.
- Removing unnecessary dependencies.

Do not solve deadlocks by blindly overriding resource ownership.

---

## 16. Integration Procedure

After parallel work completes:

1. Collect outputs.
2. Verify task completion.
3. Inspect changes.
4. Identify interface mismatches.
5. Resolve conflicts.
6. Integrate changes.
7. Run relevant tests.
8. Verify end-to-end behaviour.
9. Confirm no required task was omitted.

Successful individual tasks do not guarantee a successful integrated system.

Integration is a separate responsibility.

---

## 17. Optional Task Manifest

For complex workflows, maintain a lightweight task manifest.

Example:

```yaml
tasks:
  - id: auth
    owner: agent-a
    status: running
    writes:
      - features/auth/
    depends_on: []

  - id: settings
    owner: agent-b
    status: pending
    writes:
      - features/settings/
    depends_on: []

  - id: integration
    owner: coordinator
    status: blocked
    writes:
      - app/navigation/
    depends_on:
      - auth
      - settings
```

This is descriptive metadata, not an enforceable lock.

Create such files only when they materially improve coordination.

Do not clutter simple projects with permanent orchestration artifacts.

---

## 18. Good and Bad Practices

### Good

- Clear task ownership.
- Explicit dependencies.
- Isolated modifications.
- Bounded parallelism.
- Evidence-based completion.
- Conflict checks.
- Safe integration.
- Controlled retries.
- Respect for existing user changes.
- Appropriate failure handling.

### Bad

- Multiple agents blindly editing the same file.
- Parallelising dependent tasks.
- Assuming tasks are finished.
- Repeating non-idempotent operations.
- Ignoring shared resources.
- Creating unnecessary queues.
- Serialising everything without reason.
- Launching excessive workers.
- Overwriting conflicting changes.
- Treating a manifest as a real lock.
- Reporting success before integration verification.

---

## 19. Interaction With Other Skills

### Spoons

Spoons determines whether coordination complexity is proportionate.

The Queue determines how concurrent work is coordinated.

Spoons must not eliminate necessary safety barriers merely for simplicity.

### Parliament

Parliament may evaluate competing orchestration strategies for consequential workflows.

Do not invoke a full deliberation process for routine task ordering.

### Recovery skills

Recovery procedures may handle interrupted execution.

The Queue remains responsible for resource ownership, dependency ordering, and avoiding duplicate concurrent work.

---

## 20. Verification

For coordinated workflows, verify:

- Every required task has a known outcome.
- Dependencies were respected.
- Shared resources were handled safely.
- Conflicts were resolved.
- Integration succeeded.
- Required tests passed.
- No unintended duplicate operations occurred.
- Outstanding work is clearly identified.

When verification is incomplete, report the limitation.

---

## 21. Expected Result

Successful Queue behaviour produces:

- Correct task ordering.
- Safe parallel execution.
- Clear ownership.
- Fewer conflicting edits.
- Reduced duplication.
- Predictable integration.
- Controlled failure recovery.
- Efficient resource utilisation.
- Accurate completion status.

The objective is not to make every agent wait its turn.

The objective is to ensure that independent work proceeds efficiently while dependent or conflicting work remains controlled.

## Final Principle

**A proper queue is not about making everyone wait. It is about making sure nobody gets trampled while the work gets done.**
