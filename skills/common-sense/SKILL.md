---
name: common-sense
description: >-
  Make straightforward, convention-led changes in the application. Use when
  implementing, reviewing, or fixing screens, components, headers, microcopy,
  settings, interactions, or everyday application logic. Reuse existing owners
  and existing design system patterns, keep user-facing text useful, and avoid
  speculative complexity while finishing the requested behaviour.
---

# Common sense

Make the application easy to use and easy to maintain. Prefer the familiar existing pattern that solves the actual task. Spend effort on behaviour the user can feel, such as a clear action, reliable recovery, a preserved draft, or one fewer interruption.

## Start with the actual job

1. State the desired outcome in one sentence. Identify the normal entry point, the user action or event, and what the user should see or be able to do afterwards.
2. Read the repository's `AGENTS.md` and the relevant product and design contracts. Inspect the closest existing surface, its callers, and its failure handling. For production UI, use the current design system and follow the repository's motion guidance. Keep this skill alongside those rules.
3. Find the existing owner for each piece of work. Reuse its component, state, action, and verification paths where they fit. Check repository requirements and use upstream research to resolve API or design questions that matter to the change.
4. Use the smallest complete implementation. Cover the states the feature can actually reach. Choose routine details using the surrounding code. Ask when a material product choice, required information, or authorization remains unresolved after inspection.

## Follow the convention that already works

| Decision | Default |
| --- | --- |
| Add a setting | Put it in the owning settings section and reuse a matching existing row. Use the existing settings entry and search behaviour. |
| Add an action | Place it where the need arises. Keep the primary action visible and follow the surface's existing overflow pattern for secondary actions. |
| Add a screen or sheet | Use its closest neighbour for the title, spacing, dismissal, scrolling, and navigation. Respect system insets and text scaling. |
| Add a loading or result state | Render the real state from the owning flow. Reuse the existing loading, empty, error, or completion pattern where it applies. |
| Add a component | Check the existing components, tokens, icons, and motion first. Add a primitive only when the required interaction is missing and belongs in the shared library. |
| Add application logic | Keep it in the existing feature, repository, or controller. Keep the UI layer focused on displaying state and dispatching events. |
| Change an existing pattern | Follow an explicit requirement or fix a demonstrated usability, accessibility, or correctness problem. Make the change at the narrowest appropriate owner. |

Use the current written contract and intentional tests to distinguish convention from a stale implementation. Preserve existing callers, saved data, permissions, and behaviour outside the requested change. Keep the change local where possible. Extract a helper when it removes meaningful duplication or names a real invariant. Give a new dependency, abstraction, or persistent state a concrete job.

## Make every line of UI copy earn its place

- Give each header one clear title. On a settings section, use its familiar noun, such as **Notifications** or **Voice**. On a task card, name the task. Keep the established header height and hierarchy.
- Add a subtitle only when it supplies information needed to choose, proceed, or recover. A second line that explains what the title already says can go. Skip decorative eyebrows, redundant section labels, repeated brand names, taglines, and filler in routine screens.
- Give controls plain, specific labels. Use **Save draft**, **Retry**, or **Open settings** when that is what the control does. Use the same term for the same feature across screens. Keep identifiers, model routing, internal state names, and diagnostic text in their proper surfaces.
- Put help next to the choice it changes. Keep essential details about permissions, costs, irreversible actions, or recovery where the user will see them before acting. Preserve accessibility names, labels, and error announcements even when visible text is shorter.
- Read the whole screen as a person would. For each line, ask what decision or understanding would be lost if it disappeared. If the answer is "none", remove the line. Apply the same check to badges, dividers, icons, and controls.
- Give failure copy a cause when known and a useful next step when available. Keep the draft or input intact. Let normal success be quiet unless confirmation or an outcome is useful.

| Surface | Cluttered | Use instead |
| --- | --- | --- |
| Settings header | **Manage your notification preferences** / "Control how the app sends you notifications." | **Notifications** |
| Row with an obvious label | **Play sound** / "Turn this on to play a sound." | **Play sound** |
| Control whose effect matters | **Background updates** | **Background updates** / "The app can check tasks while it is closed." Use this only if the option actually grants that behaviour. |
| Permission needed | "The capability is unavailable due to an authorization issue." | "Allow microphone access to use voice." Show the existing permission action. |
| Recoverable upload failure | "An error occurred while processing your request." | "The upload stopped. Your draft is saved." Offer **Retry** if it is supported. |
| Approval sheet | **Confirmation required** / "Are you sure you want to continue?" | **Send this draft to Alex?** Show the relevant draft or recipient and label the action **Send**. |

## Keep routine work quiet

- Route through the permissions and approvals that already own the action. Continue safe, authorized work when possible. Ask only for a decision, missing information, or confirmation the current action actually requires.
- Use inline status for useful progress. Group ordinary updates. Escalate through the application's existing attention surfaces when something needs action, a time-sensitive result matters, or an important failure would otherwise go unnoticed.
- Let the displayed result follow evidence. **Draft saved**, **Waiting for approval**, and **Sent** describe different facts. Choose the state the system can establish. Keep retry and cancellation consistent with the underlying operation.
- Make an interaction feel responsive with the application's existing press, entrance, or state transition patterns. Let passive text and icons move with their parent. Use extra motion when it explains where something went or what changed. Keep the reduced-motion path complete.

## Choose the simple implementation

| Use | Avoid |
| --- | --- |
| One owner and one source of truth | Mirroring a setting or task state in multiple layers |
| The existing event or callback | Adding polling, a new observer, or a model call for information already available |
| A direct branch for a small, real distinction | A framework, generic strategy, or configuration switch for hypothetical variants |
| The existing route, state, and action with a targeted change | A parallel implementation that bypasses normal callers, approvals, or recovery |
| A meaningful comment about a constraint or invariant | A comment that narrates the next line or repeats the function name |
| A narrowly scoped fix with the affected flow finished | A drive-by redesign, rename, formatting pass, or unrelated refactor |
| Honest handling of applicable loading, failure, and retry states | An optimistic success label without evidence, or speculative UI for states the flow cannot reach |

When two approaches are viable, choose the one with fewer concepts, fewer state owners, and clearer failure behaviour. Keep necessary complexity where it belongs. If a simpler-looking patch duplicates a permission check, drops a draft, or breaks retry, it is incomplete.

## Verify before delivery

- Review the diff against the requested outcome. Check that each new string, control, state, dependency, and abstraction does a job.
- Test through the real entry point. Check the normal path and the relevant failure, retry, cancellation, or existing-data case. Add the narrowest regression test required by the repository or needed to catch the specific bug.
- For UI work, inspect the whole rendered screen and the affected element. Check hierarchy, alignment, text scaling, accessibility, and applicable light, dark, and reduced-motion states. Run the repository's required UI audit and verify the actual interaction where possible.
- Report the behaviour changed, the checks run, and any verification gaps. Keep completion notes as plain and specific as the UI.
