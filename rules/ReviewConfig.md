# Parameters for a specific review

This file defines input parameters; it does not require the user to complete a questionnaire. The orchestrator extracts available information from the request and materials and records it in `manifest.md`. Launching separate subagents is mandatory, not an optional parameter: if they cannot be launched, stop the audit under Section 2.1 of `meta_agent.md`. Reasonable assumptions about other parameters do not permit a single-agent mode.

## 1. Parameters and defaults

To set the report language for this review, replace `English` below with your preferred language:

```text
report_language: English
```

An explicit language request in the current review prompt overrides this setting. Otherwise, use this setting; if it is absent, use English. The orchestrator records the resolved language and whether it came from the prompt, this file, or the default in `manifest.md`, then passes it to every subagent. The report and domain analyses use that language. Proposed replacement text for the paper remains in the paper's language unless the user requests otherwise.

| Parameter | What to record | If unspecified |
|---|---|---|
| Paper | Title or working name; list of files | Determine from the materials |
| Target version | Which PDF/source set is being reviewed | Select the version that unambiguously matches the request; clarify a material ambiguity |
| Conference, year, track | Submission target and links to official requirements | General scientific audit calibrated to a leading computer science conference; adapt to the paper's field and do not claim compliance with a specific venue's formal requirements |
| Contribution type | Theory, method, empirical analysis, data/benchmark, application, negative result, position paper, or a combination | Determine provisionally from the paper and label the determination as an assumption |
| Stage | Draft, submission, revision, camera-ready | Preparation for submission; do not apply requirements specific to another stage |
| Anonymity | Which version and files/links are intended for reviewers | For submission, anonymity review is mandatory; the same preprint on arXiv is acceptable, but links from the submission to its non-anonymous version are not. The check does not apply to an explicitly non-anonymous stage |
| Materials | Main PDF, appendices, source files, code, data, configurations, logs | Only what is actually available |
| Previous review | Report, registry, previous paper version, author responses | Initial review; there are no green findings |
| Review mode and comparison baseline | `initial`/`revision`, specific prior reports, and the known coverage of their registries | Without a history, old and new findings cannot be distinguished reliably; state the comparison boundary explicitly |
| Report language | Language of explanations to the user | English; proposed edits are in the paper's language |
| Literature cutoff date | Date as of which prior work is assessed | For a current draft, the audit date; for a historical submission, its known submission date; otherwise state the uncertainty |
| Output directory | A separate directory for the current iteration | `Audit Results/<YYYYMMDD-HHMMSS>/`; add a suffix if it already exists |
| Review scope | Full audit or an explicitly specified subset | All applicable domains, including appendices |
| Reviewers | Actual launch tool, IDs of separate subagents for all eight roles, available slots, and waves | Subagents must be launched; if unavailable, report the reason and stop. The orchestrator does not substitute for a role |
| Completeness and acceptance | Object inventory, required tables, remaining work, revisions, and rechecks of positive findings | Exhaustive review of the agreed scope, without finding quotas or selective shortening |
| Output format | Two short PDFs: overall summary and critical cards; noncritical cards. The complete self-contained report with detailed analyses of all eight domains is only `03_Full_Report.md`, with no PDF build | All three files are mandatory, including empty selections; 60–120 words is a guide for one card, not a limit on an analysis or the report. Select findings by severity while retaining the orange color of new findings |
| Executing the paper's code | Permitted commands, environment, data, and budget | Static review; no training or full reproduction by default |
| Reviewer-side computational checks | Small calculations to test a special case | Brief isolated checks are permitted without paid services, external transmission of data, or modification of source files; they do not replace a proof |
| Resource constraints | Time, GPU/CPU, memory, data downloads | Do not assume unlimited resources or start expensive runs |
| Exclusions | Explicit user decisions and their scope | `rules/ignore.md` has no entries; there are no exclusions |

If the user explicitly limits the substantive scope, record that limit before reviewing and describe the result as a review of that scope rather than of the whole paper. Separate subagents remain mandatory for the substantive checks. Keep all eight role files; for a domain outside the requested scope, its agent records that boundary without falsely claiming that the domain is scientifically inapplicable to the paper itself. Neither the number of available slots nor the absence of code is, by itself, grounds for reducing the requested substantive scope.

## 2. Input formats

- **PDF only:** Conduct a complete substantive review of readable text, formulas, and images; assess reproducibility from the description. Lack of source files does not block the audit.
- **Source files only:** Review the text and resources actually included in the build; building an isolated copy is possible. Without a successful build, do not claim to have checked the actual layout of the submission PDF.
- **PDF and source files:** Establish whether they represent the same version. When reviewing a particular submission, its PDF is authoritative; source files help analyze formulas and locate findings.
- **Any of the above plus code/data:** Add a static review of the implementation; execute it only within the agreed mode and resource budget.

## 3. Clarification without stopping independent work

Clarification is necessary when the paper/version to review cannot be selected, or a particular dependent step cannot be performed, without an answer. While awaiting one, proceed with other unambiguous checks if the subagent-launch requirement has been met. This continuation rule does not apply when subagents are unavailable.

Do not require code, source files, a previous version, or a conference name as a precondition for every audit. Record their absence as a limit on the available review. Assess a missing detail in the paper's own method description separately according to its scientific consequences.

## 4. Formal requirements

If the conference, year, track, and stage are known, Editorial obtains the official instructions for precisely those parameters. Record their URLs, access dates, and applicable provisions in `manifest.md`. Do not carry over page limits or requirements concerning appendices, anonymization, checklists, or mandatory statements from another year or track without verification.

If official requirements are unavailable, retain the completed scientific checks and mark the relevant formal compliance check as unverified. Do not invent a universal page limit for all A* conferences.
