# Explicit exclusions and author decisions

There are no exclusions by default.

An entry may be added by the user, or by the orchestrator based on an explicit decision already obtained from the user. A subagent must not create an exclusion independently or interpret a lack of response as agreement.

## Entry format

- Decision ID and date.
- Paper and version, or an explicitly stated scope covering future versions.
- Related `ISSUE-XXXX`, if one exists.
- Exact content of the author's decision.
- Circumstances that should not be filed again as findings.
- Related checks that remain in force.
- Conditions for reconsideration: new evidence, a changed context, or circumstances outside the agreement's scope.

## Application

An accepted limitation does not become a fix and does not receive a green status. If it concerns an existing finding, set that finding's state to `accepted` and record the decision in its history. An exclusion is not evidence of scientific correctness; briefly describe any material accepted limitation in the relevant section of the final report.

Do not refile an excluded finding under a new ID. If you find a substantively different problem, explain the difference. If new material undermines the basis for an earlier exclusion, notify the orchestrator with a reference to the decision; do not silently overturn the author's decision.
