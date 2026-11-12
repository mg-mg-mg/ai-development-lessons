# Hypothetical teaching scenarios

These fictional teaching scenarios illustrate how to reason about evidence, boundaries, uncertainty, and verification. They do not describe actual events. Each scenario includes a practical application for building software.

## Evidence: a delayed delivery

A community garden expects a delivery of compost on Monday. On Tuesday, a volunteer sees no compost at the gate and concludes that the supplier never sent it. The volunteer checks the delivery note and asks the person who received supplies: the note records a Monday delivery, and the recipient says it was placed in a covered shed.

**Lesson.** The empty gate was an observation, not proof that no delivery occurred. Identify what each piece of evidence actually supports, seek a relevant alternative explanation, and distinguish a recorded delivery from direct confirmation of the contents.

**Apply it:** If a service shows no new data, check the relevant logs, storage and delivery path before concluding that the sender failed. Each check supports only what it actually observes.

## Boundaries: a shared workshop plan

A volunteer is asked to correct spelling in a shared workshop plan. While reading it, they notice that the proposed start time conflicts with another activity. Instead of silently changing the schedule, they correct the spelling and flag the conflict to the organizer, who can decide how to resolve it.

**Lesson.** Separate the authorized task from a consequential decision outside its scope. Report an adjacent problem with enough context for its owner to act; do not treat access to a document as permission to change every part of it.

**Apply it:** If an AI assistant finds an unrelated risky configuration while fixing a typo, have it report the finding rather than change the configuration without authorization.

## Uncertainty: a small survey

A neighborhood group asks six attendees whether a Saturday meeting time works for them. Five say yes. The group considers announcing that almost everyone in the neighborhood prefers Saturdays, but recognizes that the respondents were already able to attend that meeting. It reports the count and how the responses were collected, then invites input through another channel before choosing a recurring time.

**Lesson.** A result can accurately describe the people asked without representing everyone affected. State the sample and its limitations, avoid converting a small convenience sample into a population claim, and gather more relevant evidence when the decision needs it.

**Apply it:** A handful of positive usability responses can guide the next question, but does not establish that all users find a feature usable. Record who was asked and how.

## Verification: a readable notice

A museum drafts a large-print notice directing visitors to an accessible entrance. The author checks that the wording names the entrance and that the printed notice is legible from the intended viewing distance. A second person then follows the directions from the proposed notice location; if they cannot find the entrance, the wording or placement needs revision.

**Lesson.** Define the intended outcome before checking it, and verify the artifact in the setting where it will be used. A legible notice alone does not establish that the directions are clear or that the entrance itself is accessible.

**Apply it:** For a changed export, check the generated file and whether a supported consumer can use it. A passing generation test alone does not prove the consumer works.
