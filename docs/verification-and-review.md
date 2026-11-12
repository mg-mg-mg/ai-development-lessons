# Verification and review

Mechanical checks and independent judgment answer different questions. Both are needed: a passing check does not establish product intent, and a persuasive review does not prove that a command ran or that a service is running the reviewed code. The workflow here is recommended practice, not a claim that every project has the same gates.

**Start here:** identify the changed behavior and consumers, choose checks that exercise them, and ask someone other than the author to review the proposed revision. Record what ran and what remains unverified before merging.

## Put mechanical gates at the boundaries

Automate repeatable checks at commit, merge and deploy boundaries where appropriate. The repository and the risk determine the checks: formatting or static analysis, targeted tests, checks that generated files match their source contracts, security checks, and build or integration checks are examples. A local hook (a check triggered by a developer's Git operation) gives fast feedback but may be absent or bypassed; it cannot replace required integration checks. Do not run a costly full suite for every edit simply because it exists.

Before merge, select checks for the changed behavior and affected consumers. Include relevant failure and boundary cases, and widen coverage when the affected surface is unknown or risk warrants it. Required failures, missing results and interrupted runs are not passes. Resolve findings before the full required check set, then tie approval to the exact candidate revision and its combination with the current base branch.

At deploy, require the appropriate approval, verify the artifact or revision is the approved one, and check the resulting service using a safe, authorized observation. A successful build or merge does not prove deployment; a deployment command's success alone does not prove the desired behavior. Record what remains unobserved.

## Use independent review for judgment

Have a reviewer separate from the author inspect the exact proposed head (the latest revision in the pull request) and its context, including the issue contract, diff (the proposed changes), relevant callers and verification evidence. An independent AI reviewer can assess whether the change solves the problem, introduces risks, misses edge cases, exposes data or merely makes tests pass. It should explain material findings and their evidence, not just emit an approval marker. Independence means a genuinely separate review, not a different label on the author's own result.

The author addresses findings; the reviewer assesses the changed head before a mergeable verdict. A changed head needs review of that head. If the base branch moves, check the current combination; base movement alone does not necessarily invalidate review of an unchanged head. Human decisions and authorization still apply where required. AI can also help investigate, implement and plan checks; its role is not limited to PR review.

## Record evidence, not confidence

For each check, record the candidate revision, command or check identity, relevant environment and inputs, start and end times, elapsed time, exit status and outcome. For parallel checks, record each check and the group as a whole. Record failures and interruptions as well as passes, and explain any claim that a failure is unrelated. Keep enough output to inspect the result without exposing credentials or personal data. A test definition, a planned command, or a screenshot of a success message without provenance is not proof of execution.

Reuse earlier results only when they are completed and inspectable and the relevant inputs are demonstrably equivalent. Preserve the original execution identity and state any gaps. Changes to source, dependencies, toolchain, fixtures, environment or external state can invalidate reuse. Independently review the candidate and independently observe the changed path where required; author evidence alone is not independent proof.

## Real and synthetic evidence

Label the origin and limits of each piece of evidence:

- **Synthetic fixtures** use invented inputs. They can demonstrate a tested code path under those inputs, including hard-to-create boundary cases. They do not establish that production users experienced the same behavior or that a realistic output is semantically correct.
- **Real observations** show something that actually occurred in a named, authorized environment and time window. They still have a scope: one observation does not prove every case, and a local run is not production evidence. Redact or summarize sensitive information before sharing.
- **Static inspection** can support a statement about source at a specified revision. It does not prove a test passed, a feature was deployed, or a user saw the result.

For example, a fictional export test can demonstrate that missing and zero values serialize differently. A separate consumer compatibility check supports the contract across that consumer. Neither establishes a live deployment; that requires separate release and observation evidence. Do not invent an incident, a test pass or a production outcome to make an example convincing.
