# Team quality beyond the diff

A change can be correct in isolation and still leave a team with unsafe dependencies, an unusable journey, or no evidence that it helped. The practices below are recommendations for closing those gaps, not a claim of measured outcomes. Adapt the depth to the risk and the people affected.

## Own the supply chain

Treat a dependency as code and obligations the team will maintain, not just a convenient import. Before adding one, check whether an existing facility suffices. Assess its maintainer and release health, dependencies it brings in, permissions and network behavior, upgrade path, and known security advisories.

Review licenses for the intended use and distribution, including those indirect dependencies, bundled assets, generated artifacts, and obligations to provide notices or source code. Escalate unclear terms to the responsible legal owner; an automated license label is not legal approval.

Commit the appropriate lockfiles, which record resolved dependency versions, and pin build tools and release artifacts where reproducibility matters. Review dependency and lockfile changes together, including unexpected install scripts and new indirect packages. Use advisory and license scans with documented scope, exceptions, ownership and expiry; arrange regular updates and response to newly disclosed vulnerabilities.

A pin makes an old vulnerable version reproducible too. A failed scan or unavailable advisory database is an unknown, not a clean result. For downloaded artifacts, verify an authenticated publisher signature or independently obtained digest where available. A digest captured from the same untrusted download detects later drift but cannot establish authenticity.

Apply least privilege—granting only the access needed—to continuous integration (CI) as well as runtime. Use read-only defaults and scoped, short-lived credentials. Separate build from deploy authority, and grant publishing or production access only to jobs that need it.

Do not expose secrets or write tokens to untrusted pull-request code, its dependency installation, or artifacts it controls. Isolate privileged workflows and protect their inputs and approval boundaries. Review third-party actions and reusable workflows as dependencies, pin them to immutable revisions where supported, and keep their updates reviewable. A passing workflow demonstrates only its configured checks and permissions, not the safety of every dependency or the live provider configuration.

## Make handoffs useful and bounded

An agent handoff should let the next owner act without reconstructing a long conversation. Include the objective and acceptance criteria, exact scope and ownership, links to the authoritative records and their revisions, current state, decisions and constraints, evidence already collected with its limits, and the next action or explicit blocker.

Name any required authorization separately: receiving context is not permission to merge, publish, access production, or disclose data. Identify the single writer when changes overlap, and say where review findings belong.

Give only the context needed for the task. Prefer a synthetic example and an authorized, narrowly scoped reference over a raw transcript, production payload, or broad credential. Do not put secrets, customer details, or private conversations into prompts, issue bodies, logs, or artifacts merely because an agent might find them useful. Minimize access, retention and audience; check the destination's access and data-handling rules before sharing. Redaction may not prevent re-identification from a combination of details. If essential evidence cannot be shared safely, pass a bounded finding or arrange authorized access rather than inventing details.

For example, a handoff for a form error might give the route, expected and observed states, affected locale, candidate revision, and a sanitized reproduction using invented data. It should distinguish a source inspection from an actual run and state whether the rendered journey was observed. The receiver verifies freshness and reports what changed; a concise handoff is not a substitute for reading the relevant contract.

## Measure before optimizing

Choose a user-relevant scenario and budget before changing code: for example, time to complete a search on a representative device and network, alongside server latency and error rate. Record the workload, data volume, environment, revision, warm or cold state, sample size and variability. Profile the actual bottleneck across client, network, service, database and external calls; distinguish processor, memory, input/output, contention and startup costs. Measure end to end as well as locally, because moving time to another component may not improve the journey.

Compare the same workload before and after, including tail latency (the slower end of request times) and resource or monetary cost where meaningful. Check that a faster result remains correct and accessible, and that caching, batching, or reduced fidelity does not introduce stale data or hide failures. A microbenchmark can explain a hot function but cannot establish user-perceived improvement; a single local timing is especially sensitive to noise. Lab measurements support diagnosis, while appropriately collected field data shows a different population and environment. Keep the distinction, and retain the baseline if the result is inconclusive.

## Verify the real journey, not just the component

Select representative journeys and states from entry to completion: navigation, loading, success, empty, error, recovery and back navigation as applicable. Use the actual route and supported device or browser, with synthetic data where possible. For accessibility, exercise keyboard-only navigation, visible focus, focus order and recovery, semantic names and error announcements; test with the relevant screen reader and zoom or text scaling when appropriate. Automated accessibility checks can catch some structural failures, but a green scan does not certify that someone can complete the task. Include disabled users in research or review when feasible and compensate them; do not claim conformance from a single assistive-technology combination.

For localization, exercise the rendered journey in affected supported locales, not just a translation file. Check meaning and terminology with qualified reviewers, variable substitutions, plural forms, dates and numbers, text expansion, reading direction where applicable, and localized error and recovery paths. Use realistic long strings and small screens without treating invented text as translation approval. A screenshot may reveal clipping but cannot establish spoken labels, keyboard behavior, or translation accuracy. Record what was actually exercised, locale, device and assistive technology, and gaps; an untested locale or platform remains unknown.

For example, on a fictional account form, enter an invalid value with the keyboard, hear or inspect the associated error, correct it, submit, and confirm the resulting screen in a supported locale. A unit test of the validation function and a screenshot of the initial form are useful but do not establish that this complete path works. Follow the evidence and review conventions in [Verification and review](verification-and-review.md) rather than treating a test definition as a test run.

## Measure outcomes without inventing causality

Before rollout, define the intended outcome, the population, a precise numerator and denominator, time window, baseline, data source and owner. Pair a benefit metric with guardrails such as errors, latency, accessibility complaints, support burden, or cost; consider segments that may experience different effects, while avoiding identifying small groups. Collect the minimum data required under the applicable consent, retention and access rules. An event definition is not proof that the event fired or that the analytics pipeline captured it correctly; check instrumentation and missing data separately.

Compare equivalent populations and time periods where possible. A randomized experiment can help isolate an effect when ethical, feasible and correctly implemented. Otherwise use an appropriate comparison group or an interrupted time series: repeated observations before and after a change, analyzed for changes in level or trend. Explicitly qualify the inference. Account for seasonality, traffic mix, releases, campaigns, outages, selection effects and instrumentation changes. Report absolute counts and uncertainty alongside rates, and distinguish a click or server response from a completed user outcome. For small samples or biased measurement, report that the effect is uncertain rather than declaring success or failure. Do not optimize a proxy at the expense of the actual task.
