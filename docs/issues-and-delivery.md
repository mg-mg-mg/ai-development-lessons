# Issues and delivery

An issue is a small contract for an outcome, not just an instruction to an AI. A useful contract lets an implementer work independently and lets a reviewer decide whether the work is actually done. The practices below are recommendations; the example is illustrative, not a record of an incident or a completed change.

**Start here:** inspect the current behavior, write the desired observable outcome and its boundaries, then name the checks and review needed to show it works. Use the example below as a starting point, not a mandatory template.

## Write a contract before starting

First inspect current behavior and existing issues or pull requests. State what is observed, how it was observed, and what is still an inference. Avoid turning a suspected cause into a fact. If the behavior may already have changed, check the current code and evidence before creating or closing work.

Include:

- **Problem and context:** who or what is affected, the current behavior, and why it matters. Give a safe reproduction or an explicit statement that reproduction is not yet known.
- **Desired behavior and scope:** what should change, what should remain unchanged, affected surfaces and consumers, and explicit non-goals. Name important constraints such as compatibility, privacy, or data preservation.
- **Acceptance criteria:** observable, testable outcomes, including relevant negative and boundary cases. Specify what evidence would distinguish completion from a plausible implementation. Do not make a test name or a checklist tick stand in for the behavior it is meant to prove.
- **Dependencies and decisions:** link actual prerequisites in the tracking system; separate them from unresolved product or policy decisions. Record a recommendation when a decision is needed. A subtask describes part of an outcome, not automatically a prerequisite.
- **Verification and release needs:** identify likely checks and affected consumers, any independent review needed, and whether deployment or later observation is part of completion. Keep the final evidence with the work, not just in a chat.

Split work when parts have genuinely independent outcomes and ownership. Do not split so finely that no issue owns the end-to-end result. Assign one writer to shared files or a branch; coordinate overlap rather than allowing concurrent edits to race.

## An illustrative issue

**Title:** Preserve an unavailable value in account export

**Current behavior:** In a fictional export flow, a missing optional measurement is serialized as `0`. A reader cannot distinguish “not available” from a real zero. This is a constructed example, not a claim about a real product.

**Desired behavior:** Export a missing measurement as `null`; keep an actual zero as `0`. Preserve the rest of the export format. Do not change how the measurement is calculated or fill historical missing values.

**Acceptance criteria:**

1. Given a record with no measurement, the exported field is `null`; given a measured zero, it is `0`.
2. A nonzero value and unrelated fields retain their existing representation. Export does not invent a measurement or discard the record.
3. The owning automated test covers missing, zero and nonzero values. Affected consumers are identified and checked for the nullable contract, or a compatible rollout is agreed before merge.
4. The pull request (PR) records the candidate revision, checks and results, and an independent review. If release is required, completion additionally needs evidence of the approved version deployed and the expected behavior observed in an appropriate safe environment.

This example deliberately leaves implementation and test commands to the repository that owns the export. A passing serializer test alone would not prove that every consumer accepts `null`, nor that a deployed service contains the change.

## Carry the work through its lifecycle

1. **Admit:** confirm scope, dependencies, ownership and any needed decision. Continue unrelated eligible work while a decision is pending.
2. **Implement:** work against a known revision, preserve existing work, and update all affected callers and contracts. Record discoveries that change the acceptance criteria rather than silently narrowing them.
3. **Review and verify:** open a PR with its issue and evidence. Address independent review findings, then verify the exact candidate revision and its combination with the current base branch. A new PR head (the latest revision proposed by the PR) needs review of the new head. See [Verification and review](verification-and-review.md).
4. **Integrate:** use the repository's required automated checks and reviewed integration path. Resolve failures and unknowns instead of treating an interrupted check as a pass. Reconcile an uncertain merge outcome before retrying.
5. **Release and close:** merge is not deployment. When the issue requires release, deploy only the approved revision through the authorized path and verify the actual result. If a later observation is required, record its signal, window and responsible checker; leave that criterion open until evidence exists. Close only when the issue's applicable criteria are met, and clean up owned resources safely.
