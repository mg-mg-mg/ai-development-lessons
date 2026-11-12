# Knowledge and agents

An agent needs a reliable place to find decisions. A chat transcript is not that place. Use a maintained, source-linked wiki for reusable knowledge, and keep each fact with the system that owns it.

## Give each kind of information an owner

- **Source code and contracts** describe the implementation at a specific revision. They do not, by themselves, prove what is running.
- **Issues and pull requests** track work, acceptance criteria, reviews, and one-time decisions. Check their current state before acting.
- **A wiki maintained for people and language-model agents** (sometimes called an llm-wiki) organizes policies, explanations, and reusable findings. It should point back to the evidence, not replace it.
- **Runtime and release evidence** establish what was deployed or observed. A merged change or a passing local test is not proof of a live outcome.

This separation is a recommendation, not a claim that every team needs the same tools. An agent can draft or update a wiki page, but the responsible owner still reviews the claim and its source. A wiki entry does not grant permission for an external action.

This makes the owning record the **single source of truth (SSOT)** for its particular fact, not one document that answers every question. For example, use the release record to establish what was deployed and the code at that revision to understand how it works.

## Make claims traceable

Capture the source and its context before summarizing it. Cite the exact document, revision, and relevant passage when available. Record whether the source is a decision, implementation, test result, review, or observation. Preserve important conditions and disagreement. Separate what a source says from your interpretation and from a proposed policy.

A practical pattern is to keep unchanged copies of sources, link each derived page to them, and maintain a searchable index showing whether each page is current. If a source changes, add a new capture rather than silently rewriting history. Do not put secrets, personal data, or unrestricted transcripts in captures intended for broader access. Limit access to private evidence and publish only a reviewed, safe summary.

For example, a page might say: “The test covers a retry after a specific failure at revision X.” It should not say: “Retries are safe in production.” A test definition is evidence of intended coverage; an execution record is evidence of a particular run; neither alone establishes a production outcome.

## Treat freshness as a question, not a date

A recent edit or a label saying “current” does not prove a claim remains true. Before relying on a page, check its status, cited revision, and the current owner of the underlying behavior. If a source has changed, mark dependent claims stale and inspect the new evidence. Update the page and citations, then mark it current only after review. If the source cannot be checked, say **unknown**. Do not convert an unknown result into a pass. External pages and human reviews may need manual rechecking even when local source checks pass.

Agents should use the wiki to find the evidence, then inspect the relevant source when the decision depends on current behavior. A structural or provenance check can find missing links; it cannot determine whether a citation actually supports a claim.
