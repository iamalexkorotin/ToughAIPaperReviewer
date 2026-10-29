# Unified format for findings and the final report

This file is mandatory for the orchestrator and every subagent. The deliverables are two coordinated short PDFs and one complete, self-contained Markdown report. Use the four-color scheme, concise finding cards, the “Tough Reviewer” block, detailed analyses, the object registry, and the acceptance log with rechecks of positive findings.

## 1. Primary deliverables

The user receives **exactly three final files for one audit: two PDFs and one MD file**:

1. `01_Summary_Critical.pdf` — an overall summary, a “Tough Reviewer” block of at most five points, counts for all eight domains, material limitations, and concise cards for open critical findings.
2. `02_Noncritical.pdf` — concise cards for open noncritical findings in the same domains and a brief summary of this selection only.
3. `03_Full_Report.md` — a complete, self-contained Markdown report: the same overall summary and “Tough Reviewer” block, all current findings and questions, verified fixes and history, and mandatory detailed analyses of all eight domains, including grounds for positive conclusions. Part I contains the summary/cards; Part II contains the complete domain checks. This is the whole report, not merely what remains after the first two files. Do not create a PDF version of the full report.

The first two PDFs are selections from the shared material; detailed grounds appear in the full MD. Each short card contains a brief verifiable argument and a precise reference to its section/ISSUE in `03_Full_Report.md`. References within the full report point to locations in that same file. Separate domain Markdown files do not substitute for detailed analyses inside the full MD. A clickable PDF-to-MD link is desirable, but the filename and a readable locator are mandatory. See Section 8.0 for selection rules.

Write human-readable prose, headings, count labels, and card labels in the report language resolved under `rules/ReviewConfig.md` (English by default). Literal English headings and templates below name required sections and meanings; translate them consistently when another report language is selected. Keep the same language and wording in matching parts of all three deliverables. Use explicit language-independent anchors for translated headings that serve as link targets. Preserve file names, ISSUE IDs, stable anchors, JSON keys, and machine-readable enum values exactly.

Keep an editable report source and machine-readable registries. The material and checks determine the length: there is no minimum number of findings/pages and no overall page limit. Concise cards do not limit the number of justified findings or the depth of the audit. Correct objects appear in domain registries without a green marker and do not increase finding counts.

If mandatory subagents cannot be launched, Section 2.1 of `meta_agent.md` applies: report the stop, preserve materials already obtained, create none of the three final files, and do not replace the audit with a partial single-agent review.

## 2. Output files

In a separate directory for the current audit:

```text
01_Summary_Critical.pdf
01_Summary_Critical.md
02_Noncritical.pdf
02_Noncritical.md
03_Full_Report.md
manifest.md
issues.json
objects.json
coverage.md
acceptance.md
decisions.md
01_Theory.md
02_Algorithms.md
03_Practice.md
04_Reproducibility.md
05_Literature.md
06_Narrative.md
07_Notation.md
08_Editorial.md
work/<domain>/...
```

All eight domain files belong directly in the current run's directory, not in a neighboring iteration or a parent directory. Each subagent stores its object registry and detailed supporting material in `work/<domain>/`; the orchestrator assembles the unified `objects.json`. Build both PDFs, their Markdown sources, and the full MD from one `issues.json`, one `objects.json`, and accepted domain analyses, without independently rewriting conclusions by hand. List the files and the results of their assembly/checks in the manifest.

Always create all eight domain reports: an inapplicable domain needs a justified statement of inapplicability. The `work` directory contains detailed registries, primary notes, review materials, temporary builds, and logs. The two short PDFs and full MD are mandatory even if one selection is empty: state that no findings of the corresponding severity were identified within the checked scope and describe the review boundaries. This does not establish that unexamined parts are error-free. Do not create an additional full PDF. A prior report may be used as input to a later audit when its provenance and scope are recorded.

## 3. Severity, state, novelty, and confidence are separate fields

### 3.1. Severity

- `critical`: The problem materially changes a central result, the correctness of the method, the reliability of the main conclusions, a claim about the principal contribution, or confirmed submission eligibility. The relevant claim must be fixed, justified, or narrowed.
- `noncritical`: A local inaccuracy, missing explanation, presentation problem, or optional improvement that does not undermine the paper's core argument.

Justify severity by consequences. Do not assign it because of a sharp tone, the size of the fix, a deviation from a preferred style alone, or speculation about a reviewer's reaction. A small sign error can be critical; many typos do not make each typo critical.

For an anonymous submission, a confirmed disclosure of the authors through submitted code, leftover working comments/annotations, or other related artifacts accessible to reviewers is **always critical**, even if it consists of a single line containing a personal path or surname. Sections 2.1.1 and 4.2 of `agents/Editorial.md` define the scope and contextual checks; do not downgrade such a disclosure to a cosmetic finding. Keep the usual states and colors: a confirmed open disclosure is red; one first found in a revision audit is orange with an explicit critical-severity label. In both cases it belongs in the critical selection and full report. Assess ordinary editorial leftovers that do not disclose authorship as noncritical under Editorial Section 4.2. An unconfirmed match remains a question, not a proven leak.

### 3.2. Finding states

| Value | Meaning |
|---|---|
| `open` | An evidence-backed finding remains relevant |
| `resolved` | A previous finding has actually been fixed and the fix verified |
| `unverified` | A specific question or suspicion exists, but evidence is insufficient to establish a finding |
| `accepted` | The user explicitly accepted a limitation or excluded a requirement; this is not a fix |
| `dismissed` | A previous finding was erroneous, inapplicable, or reasonably withdrawn without a change to the paper |
| `merged` | A historical record was merged into another ID, with a link to the primary ID retained |

A partially fixed finding remains `open`: list the corrected and remaining parts. If the problem recurs, reuse its ID and `open` state, and add a `reopened` event to its history.

### 3.3. Confidence

- `confirmed`: direct verifiable evidence supports the precisely stated problem;
- `supported`: the conclusion is reasoned but involves an interpretation that is described explicitly;
- `uncertain`: confirmation is insufficient; the state must be `unverified`.

An open `critical` finding requires `confirmed` regardless of color. The confirmed fact may be a gap in a proof rather than proof that a result is false; word the finding to match what has actually been established. If a potentially serious error remains unconfirmed, put it among the questions requiring verification and state its possible consequences. Marking a new question orange does not turn it into a confirmed error.

### 3.4. Novelty relative to an earlier review

`is_new_this_run` means the finding was first added in the current revision audit. Assign `true` only when all of these hold: `review_mode: revision`, a known baseline of earlier findings, no equivalent finding in the available history, and a `first_seen_run` equal to the current run_id. Check duplicates and history before assigning it.

This marks the novelty of the comment, not a claim that the underlying defect arose only after the revision. A pre-existing defect noticed for the first time is also a new comment. A reopened problem, change of severity, rewording, transfer to another domain, or confirmation of an earlier question retains its old ID and is not new.

In an initial audit the value is `false`: findings receive the normal red/yellow categories and none are orange. In the following iteration, a formerly orange finding is no longer new. If history is unknown for the relevant area, use `null`, state the limitation explicitly, and do not invent an orange status or a zero count of new findings.

### 3.5. Colors and assignment order

| Condition | Color and label in PDF; textual category in MD |
|---|---|
| `resolved` + verified fix of a previous finding | 🟢 RESOLVED |
| `open` or `unverified` + `is_new_this_run: true` | 🟠 NEW; also say “critical,” “noncritical,” or “requires verification” |
| `open` + `critical` + `confirmed`, if the orange rule does not apply | 🔴 CRITICAL |
| `open` + `noncritical`, if the orange rule does not apply | 🟡 NONCRITICAL |
| Other states | No color category; questions or decision history |

In a revision audit, a new finding is always orange even if it is critical. Do not add a second red or yellow marker to its card: state severity in words. Label new unverified questions “NEW · requires verification” and place them in the questions section, apart from established errors.

Orange applies only in the report for the iteration when the finding was first registered. At the next review, an open confirmed finding becomes red/yellow according to severity; a verified fix becomes green. A dismissed, accepted, or merged finding receives the corresponding uncolored status.

For a resolved finding, keep its previous severity as historical data. Green encodes the state of a verified fix, not low severity. An initial audit without earlier findings has no green cards. “Checked; no issue found” describes coverage, not a green finding. An author's statement that something was fixed does not replace actual verification.

Use all four colors together with text labels so that both PDFs remain understandable in grayscale and the full MD works in any Markdown viewer. In MD, always write the category in words; color or emoji may supplement, but not replace it. If PDF fonts do not display emoji, draw a colored marker and ordinary text label.

## 4. Numbering and duplicates

Subagents use local IDs: `TH-F-0001`, `ALG-F-0001`, `EXP-F-0001`, `REP-F-0001`, `LIT-F-0001`, `NAR-F-0001`, `NOT-F-0001`, `ED-F-0001`.

The orchestrator assigns global IDs `ISSUE-0001`, `ISSUE-0002`, and so on. Once a report has been issued, an ID does not change when its color, section, wording, or state changes. Assign new findings numbers above the historical maximum, including dismissed records. Do not mix one paper's history with another's.

If several agents describe the same cause, object, and consequence, merge their reports into one finding with all supporting grounds. Assign one primary domain and references to the others. Within each final file, place a full card in one section; a brief cross-reference is allowed elsewhere. A card selected for a short PDF must also appear in the full MD, without acquiring another ID. Count unique global IDs, not the total number of cards across files.

Different errors at the same location are not necessarily duplicates. A missing assumption and a mistaken label on a formula, for example, may require different fixes. Compare the specific grounds before merging uncertain cases.

When merging previously published IDs, retain the secondary IDs as historical `merged` records with `duplicate_of` pointing to the primary ID. Do not reuse their numbers.

## 5. Full record and concise user-facing card

### 5.1. What to keep in the registry

For every finding, retain the following in the registry and domain materials:

1. **ID, color, short title, and novelty flag.**
2. **Domain, state, severity, and confidence.**
3. **Location:** precise locator in the current version, plus the previous locator in a revision review.
4. **Source excerpt or object:** enough brief context to identify it.
5. **Problem:** exactly what is wrong, missing, or obstructs understanding.
6. **Evidence:** a derivation, counterexample, comparison, verified source, or execution result. State every material assumption.
7. **Impact:** which claims, results, or decisions are affected and why that severity was chosen.
8. **Proposed fix, if known:** a specific action, ready-to-use wording, or necessary further check. Do not invent a solution merely to fill a field.
9. **Closure criterion:** what a new version must show for the problem to count as fixed.
10. **History:** first iteration, earlier states, author response, and result of checking that response, where applicable.

For `resolved`, always state what was wrong, what changed, where the change is visible, and why it fixes the original problem. Also check dependent conclusions if the fix affected them.

For `unverified`, state what data are missing, which interpretations have already been checked, and how the question can be resolved. An unconfirmed question does not count as an established error even when marked orange.

### 5.2. Concise card in the PDFs

One card represents one finding. As a guide, use 60–120 words and generally no more than half a page at a readable font size. Simple cards may be much shorter; several cards should fit comfortably on a page. Do not inflate cards with every technical field, long quotations, or a full history.

This guide applies only to cards. It does not limit detailed proofs, checks, domain tables, the number of findings, or the full MD. Direct readers to the detailed analysis with precise references instead of shrinking the font or removing evidence.

A status-bearing heading, brief locator, core issue, short evidence/impact statement, and a possible action are enough. For a green card, use “previously → changed → how verified” instead of repeating the long original error. For a new finding, explicitly put “New” (or its translation in the selected report language) in the heading and state its severity or need for verification in words.

Put a complex derivation, counterexample, or detailed comparison in a numbered appendix of `03_Full_Report.md`. Keep the key verifiable argument and a reference to the details on the card. In short PDFs, provide the full file's name, section, and ISSUE/object; a clickable link is desirable, but a readable locator is mandatory. In MD, use stable headings or explicit anchors for precise links. Do not hide a material assumption to shorten a card or split one problem across IDs merely to reduce card size.

### Concise card template

```text
ISSUE-XXXX — [title] | [color category; severity in words]
Where: [page / section / object]
Issue: [1–2 sentences]
Evidence and impact: [brief argument; link to details if needed]
Possible action: [if known, 1–2 sentences]
If resolved: [what changed and where it was verified, instead of the full history]
```

The template is not an actual finding. Do not leave placeholders in a finished report.

## 6. Locators and evidence

- PDF: filename, one-based file page number, printed page number if different, section, object, and a short excerpt.
- Source file: path, one-based line numbers, label, and the checked document version.
- Code: commit or version hash, path, function, and lines; if executed, a reference to the log and configuration.
- External paper: title, authors/year as needed, direct URL/DOI, version, page/section/formula/theorem, and access date.
- Computational check: conditions, inputs, procedure, and observed result sufficient to repeat it.

Relative paths in the registry are acceptable if the material root is specified. A PDF reader must understand a locator without access to the agent's internal state. Do not use opaque search-tool identifiers in place of ordinary references.

## 7. Structure of a domain report

1. Domain name, pinned paper identifier, instruction source from the manifest, actual subagent ID, available-material mode, and task boundaries.
2. Brief conclusion: what was checked and the main problems, if any; which positive conclusions were established and within what limits.
3. Complete object registry with locations, results, and grounds; counts by type and an explanation of how the inventory was reconciled with the document.
4. A mapping of every mandatory point in the domain instruction to objects and review locations, or a justified statement of inapplicability.
5. All required domain tables and detailed object analyses, including positive results. An “object — checked” table without the content of the check does not satisfy this point.
6. Findings table with local IDs, concise cards, and full grounds linked to objects.
7. Review of this domain's prior findings.
8. Unverified questions, limitations, remaining actions, and inapplicable points with reasons.
9. Cross-domain questions, answers from related agents, and external sources used.
10. Links to working materials and a history of revisions requested during acceptance.

Do not reduce mandatory tables and analyses to a summary. They may live in linked working files as the single source of truth, but they must also be included in the domain report and the detailed portion of `03_Full_Report.md` during assembly. There is no need to maintain several independent manual copies of the same analysis. Raw logs, full source-paper caches, and machine-generated intermediate results may remain outside the full MD; conclusions, key calculations, and sufficient verifiable grounds must remain inside the full report.

## 8. Contents of the two PDFs and structure of the full MD report

### 8.0. Selection, common version, and counts

| Material from the shared registry | PDF: summary and critical | PDF: noncritical | Full MD |
|---|---|---|---|
| `state: open`, `severity: critical`, `confidence: confirmed` | Every card | No cards | The same cards and detailed grounds |
| `state: open`, `severity: noncritical` | Overall counts/links only, if needed | Every card | The same cards and detailed grounds |
| `state: unverified`, any/unknown severity | Material risks and limitations, explicitly marked “requires verification,” with a link | Do not present as an established noncritical finding | Separate questions section, cards, and grounds |
| `resolved` | Count in overall summary | No cards | Green cards for fixes verified in this iteration; older fixes in a historical index |
| `accepted`, `dismissed`, `merged` | Counts/material limitations under Section 8.1 | No cards | History and grounds for decisions, without a false green marker |
| Complete checks, positive grounds, object registries | Links to full report | Links to full report | All eight detailed appendices |

Select findings for short PDFs by **state and severity, not color**. A new critical finding in a revision audit appears orange in the first PDF; a new noncritical finding appears orange in the second. Color, state, ID, severity, card content, and grounds must match the full report; only the navigation link may differ. An orange question does not become an established error and stays in the full report's questions section.

The overall summary in Section 8.1 and the “Tough Reviewer” block must be identical in the first PDF and full MD and describe **the entire audit**, including yellow, green, and orange records. In the second PDF, label the summary “Open Noncritical Findings” (or its translation in the selected report language): its domain counts cover only that selection, and new findings are included in its total. Do not add counts from different files. Count only the primary ID for `merged` records.

Use the same paper, version, run_id, date, and `audit_status` in all three documents. For a partial audit, write “Partial audit” (or its translation in the selected report language) on the first page of each PDF and at the beginning of the MD, with a brief statement of limitations; detailed remaining work belongs in the full report. An empty selection does not remove those limitations. Put critical cards by domain after the overall summary in the first PDF, and noncritical cards in the second. Put green cards and the full history in the MD.

The full MD must be readable on its own, without the first two PDFs or access to working Markdown/JSON files. Sections 8.1–8.4 define its structure. The first PDF uses its summary and critical cards; the second uses its noncritical cards. Preserve every mandatory detailed table and evidence-based analysis regardless of the size of the short files. Raw logs, source caches, and large intermediate arrays remain separate technical files.

### “Tough Reviewer” in the summary

In `01_Summary_Critical.pdf` and `03_Full_Report.md`, place the identical **“Tough Reviewer”** block immediately after the eight-domain summary table and its brief count legend. Use that heading in English, or one consistent translation in the selected report language, followed by no more than five identical brief points about vulnerabilities that a reviewer determined to reject the paper would press. If `audit_status: partial`, explicitly write “Partial audit” (or its translation in the selected report language) on the PDF's first page and at the beginning of the MD. The orchestrator itself creates this block after its synthesis under Section 9.1 of `meta_agent.md`. Do not repeat it in the second PDF.

Each point is usually one or two short sentences and cites grounds or a related ISSUE. Clearly label a possible nitpick that is not an established error as a potential reviewer argument. Do not repeat full cards here. Use fewer than five points if fewer are justified; if none are justified, one honest sentence is enough.

This is a separate short summary block, **not a ninth findings domain**. It receives no independent IDs, colors, counts, or cards and adds no rows to `issues.json`. Its references lead to registered findings or specific evidence in the paper. Check and register any genuinely new independent finding in the appropriate domain before using it in this block. The block does not change the four-color scheme or counts.

### 8.1. Summary by domain

Start with brief paper details, the pinned input identifier, date, audit completeness, and material limitations. Then place a summary table for all eight domains and its brief count legend, followed immediately by the “Tough Reviewer” block. Do not insert a long process description or narrative paper synopsis between them.

| Domain | Unclosed | New 🟠 | Closed total | Of those, resolved 🟢 |
|---|---|---|---|---|
| [domain] | [count] | [count/n/a] | [count] | [count] |
| Total | [count] | [count/n/a] | [count] | [count] |

Include a brief legend for the counts:

- **Unclosed:** unique records in `open` or `unverified` state. Separately state how many of these are unverified questions so they are not mistaken for confirmed errors.
- **New:** the subset of unclosed records with `is_new_this_run: true`, shown orange in the current revision audit. Do not add them to the unclosed count again. If the history cannot be matched, show “n/a” for the affected domain instead of inventing zero.
- **Closed total:** unique records in `resolved`, `accepted`, or `dismissed` state. Here, “closed” means closed in the review workflow, not necessarily fixed in the paper.
- **Of those, resolved:** the `resolved` subset of closed records; only these may be green. Accepted limitations and dismissed mistaken findings are not fixes.
- `merged` adds no findings; count only the primary ID. Count each ID in one primary domain even if it involves several agents.

The counts describe the currently known registry, including retained older fixes. Separately and briefly state how many fixes were verified in this run, how many problems were reopened, and how many were closed without a fix by author decision or withdrawal of a mistaken finding. If a finding's primary domain changed, record the transfer rather than creating a new record.

After the “Tough Reviewer” block, give a short list of highest-priority problems with IDs and links to their cards, plus material review limitations. All open critical findings must appear here, including **new orange critical findings**, not only red ones. Brief scientific context is acceptable if it helps explain findings; do not bloat the summary.

For inapplicable domains, keep a row with zeros for the known registry and an explanation of inapplicability; inapplicability in the new version does not automatically close earlier findings. The table must fit at a normal readable font size. Put further detail in prose rather than dozens of narrow columns.

### 8.2. Full report, Part I: cards by domain

After the summary and navigation, use these sections:

1. Theory and proofs.
2. Method and algorithms.
3. Experiments and validity of conclusions.
4. Reproducibility and code.
5. Literature, novelty, and significance.
6. Abstract, introduction, and narrative structure.
7. Notation and definitions.
8. Language, presentation, and submission requirements.

At the start of each section, briefly describe its scope and counts. Then provide concise cards: first open findings ordered by impact, with a clear orange marker for new ones, followed by resolved findings. Do not place a new critical finding below all yellow findings solely because it is orange. Put new unverified questions in the questions section, linked from their domain. Explicitly explain an inapplicable domain or one with no findings. Each ID has one card, with only a link in related domains.

### 8.3. Full report, Part II: mandatory detailed checks

After the cards, questions, and brief history, add eight numbered domain appendices in the same order. Include every domain: give a specific reason if one is inapplicable; if a check is partial, describe what was completed and what remains. Having no findings does not justify omitting a detailed appendix.

Each appendix must contain:

1. Boundaries, inventory completeness, and coverage counts.
2. A complete registry of domain objects with locators, states, and object-specific results. Describe correct objects neutrally, without green cards.
3. Detailed checks and required tables from the role's instruction: every result/proof, substantive procedure step, experiment and comparison, source and citation occurrence, significant notation item, and other objects belonging to that role. A page list or general positive verdict does not replace these checks.
4. Key calculations, checked conditions, exact locations in primary sources, comparisons, and grounds for negative as well as positive conclusions. There is no need to reproduce the full paper or an external source verbatim.
5. Links to ISSUE IDs and short cards, results of checking prior fixes, remaining unchecked steps, and the limits of each conclusion.

Carry substantive analyses from accepted domain reports into the full MD without losing material steps or conditions. One complete account of a shared ground is enough if all relevant objects link to it precisely. Mechanical records, raw execution logs, and large unprocessed arrays may stay in working materials; the data needed to verify a conclusion and the result of the analysis must appear in the full MD.

Preserve navigation from “card → detailed analysis” and “object → check result.” In MD, use stable headings/anchors and test internal links. In the PDFs, give the MD filename, appendix/section number, and ISSUE or object_id; add clickable links when supported. Do not leave the detailed portion only in separate domain files. The short portion remains easy to browse, and the detailed portion must support verification of its arguments.

### 8.4. Limitations, history, and sources

- Questions not yet confirmed or resolved.
- Coverage limitations and reproducibility levels actually achieved.
- History of author decisions and dismissed and merged findings; earlier resolved records may appear in a concise historical index with IDs retained.
- A list of primary sources used, with precise locations when cited in an analysis.
- A brief acceptance result and recheck of positive conclusions; the full record remains in `acceptance.md`.

Briefly present questions and material limitations immediately after the cards; technical history and the source list may go at the end of the detailed portion. The detailed analyses required by Section 8.3 cannot be replaced by this closing section.

Every current open finding and every fix first verified in this iteration must have a concise card. Retain older verified fixes in the registry and in a brief historical index within the relevant domain; do not count them as newly verified fixes again. If a revision reveals a regression, reopen the card under its old ID without an orange novelty flag.

## 9. `issues.json` registry

This file must be valid UTF-8 JSON, not pseudocode. Root fields:

- `instruction_source`: the same instruction-set location and commit or file hashes recorded in the manifest;
- `audit_status`: `complete` or `partial` for an issued report; record a technical stop as `blocked_subagents` in the manifest without creating a fictitious registry;
- `objects_file`: relative path `objects.json`;
- `acceptance_file`: relative path `acceptance.md`;
- `run_id`: current audit identifier;
- `review_mode`: `initial` or `revision`;
- `paper_id`: stable working name for the paper;
- `paper_version`: version/hash/reference to the fixed manifest;
- `previous_run_ids`: array of known earlier iterations;
- `comparison_scope`: earlier reports used and completeness of history matching by domain;
- `issues`: array of records.

Fields in each record:

| Field | Content |
|---|---|
| `id` | Global `ISSUE-XXXX` |
| `local_ids` | Array of originating local finding IDs, such as `TH-F-0001`; executor IDs are recorded in the manifest and `objects.json` |
| `domain` | `Theory`, `Algorithms`, `Practice`, `Reproducibility`, `Literature`, `Narrative`, `Notation`, or `Editorial` |
| `related_domains` | Array of other affected domains |
| `title` | Short title |
| `state` | One of the states in Section 3 |
| `severity` | `critical`, `noncritical`, or `null` if not yet determined |
| `confidence` | `confirmed`, `supported`, or `uncertain` |
| `is_new_this_run` | `true`, `false`, or `null` if history is unknown, under Section 3.4 |
| `color` | `red`, `yellow`, `green`, `orange`, or `null` under Section 3.5 |
| `locations` | Array of objects with `artifact`, `version`, `locator`, `quote`; an unavailable quote may be `null` |
| `problem` | Precisely stated problem |
| `evidence` | Array of objects with `description`, `source`, `locator`, `version`; inapplicable source fields are `null` |
| `impact` | Consequences and severity rationale |
| `recommendation` | Justified proposed action, or `null` if the remedy is not yet known |
| `closure_criterion` | Condition for closing the finding |
| `verification_required` | What remains to be checked, or `null` |
| `first_seen_run` | First known iteration |
| `last_checked_run` | Last actual check, not merely a copied record |
| `previous_ids` | Earlier identifiers when importing an external report |
| `duplicate_of` | Primary ID for `merged`; otherwise `null` |
| `resolution` | For `resolved`, an object with `previous_problem`, `change`, `current_evidence`, `verified_in_run`; otherwise `null` |
| `history` | Array of events with `run_id`, `date`, `event`, `from_state`, `to_state`, `reason` |

All fields are mandatory. Use `null` or an empty array for unknown or inapplicable values; do not invent information. An `open` record cannot have `severity: null`. A `resolved` record requires confirmation, a prior finding, and `confidence: confirmed`. An orange record requires `review_mode: revision`, `is_new_this_run: true`, `first_seen_run` equal to the current run_id, and no equivalent entry in the comparison baseline. An unverified orange question retains `state: unverified` and `confidence: uncertain`.

When importing a previous report or registry, preserve existing IDs, history, and actual states. Add missing fields only where supported by evidence, and derive this iteration's color under the current rules. Importing previous findings does not make an old finding new; the “Tough Reviewer” block adds no findings. Do not attribute an object check to an earlier report if it did not perform one: new registries describe checks actually performed in the current run. Do not invent an earlier date or run_id; identify the imported source by its real filename and link.

The orchestrator validates JSON syntax, unique IDs, allowed values, consistency of colors with states and novelty, merged-ID references, grounds for green cards, and agreement between each domain's counts and the three final files within their respective counting scopes. Verify that every new unclosed finding in a revision audit is orange, new critical findings are visible in the summary, and reopened old findings did not receive new IDs. The registry and full Markdown provide the basis for a later review; a prior full PDF is also acceptable as the only available report. If only one short PDF is available, account for incomplete history; import matching IDs from multiple PDFs only once.

## 10. Object registry, coverage, acceptance, and decisions

### 10.1. `objects.json`: complete object registry

This is a registry of checks, not another error list. Root fields are `instruction_source` (matching the manifest and `issues.json`), `run_id`, `paper_version`, `scope` (agreed review scope and level of computational checks), `inventory_complete` (Boolean; the inventory has been reconciled with the materials), and `objects` (an array of records). Keep independent counts and the reconciliation method by role/type in `coverage.md` and `acceptance.md`.

Each record has mandatory fields:

| Field | Content |
|---|---|
| `object_id` | ID unique to this run, such as `TH-OBJ-0001`; role prefixes match local findings |
| `domain`, `type`, `title` | Strings identifying the primary responsible domain from `issues.json`, the type, and the object's precise name/content |
| `locations` | Object locators in the format of the `locations` field in `issues.json` |
| `required_checks` | Array of concrete checks from the domain instruction |
| `performed_checks` | Array describing each actual check and its object-specific result; details linked from `evidence` |
| `coverage_status` | `checked`, `partial`, `not_checked`, or `not_applicable` |
| `verdict` | `no_issue_found`, `issue_found`, `unresolved`, or `not_applicable` |
| `evidence` | Array of grounds with `description`, `artifact`, `locator`; link to the precise detailed analysis/calculation and, where needed, primary source |
| `limitations` | Array of `remaining_check`, `reason`, `next_action` records; empty if nothing remains |
| `related_object_ids` | Dependencies and domain relationships, without recreating another role's check |
| `local_finding_ids`, `issue_ids` | Associated findings; empty arrays are allowed when none exist |
| `reviewed_by` | Array of actual subagent IDs that performed the check; reconcile with the manifest |

Before inventory completion, records may have `not_checked` status; keep them in the registry until checked or justified as inapplicable. `checked` requires every relevant object check to have been performed and meaningful nonempty evidence. `no_issue_found` is permitted only with `checked` and means no problem was identified in the stated scope, not proof of error-free work. `issue_found` is also permitted with `partial` when a defect is confirmed but other steps remain. `unresolved` means an incomplete check or unresolved question and is incompatible with `checked`. `not_applicable` in either field requires a specific explanation in `evidence`.

The same passage may contain different domain objects, such as a proof and the spelling of a symbol. They have different checks and responsible roles; link them through `related_object_ids` instead of duplicating one check across roles. Do not present the object count as the number of findings or unique paper passages. In a revision audit, old `object_id` values may be matched by meaning, but historical ID stability is mandatory primarily for ISSUE IDs; carrying forward an old `checked` result without a current check is prohibited.

The orchestrator checks JSON validity, unique `object_id` values, allowed status/verdict combinations, mandatory grounds for `checked`, inter-object links, existence of related ISSUE IDs, and real reviewer identities. Empty evidence or a nonexistent file fails validation. These technical checks do not replace substantive acceptance.

### 10.2. `coverage.md`: completeness reconciliation

For each role and object type, state the agreed scope; inventory method; expected and registered counts; counts of `checked`, `partial`, `not_checked`, and `not_applicable`; remaining applicable checks; and links to the full registry and detailed analyses. For each type, `N = checked + partial + not_checked + not_applicable`; remaining work equals `partial + not_checked`. If inventory completeness is unknown, say so explicitly: arithmetic agreement does not establish completeness.

List every unfinished object and its specific limitation, not merely a general statement for the role. Do not sum total rows again. Derive finding counts in the summary separately from `issues.json`. Never give `checked` an automatic green marker.

### 10.3. `acceptance.md`: orchestrator acceptance

Record actual subagent availability and launches with a reference to the manifest. For each role, record its result against Section 7.1 of `meta_agent.md`, `return_for_revision`/`accepted_complete`/`accepted_partial` state, missing objects, revision requests, and the result of re-acceptance. A separate table of positive conclusions contains `object_id`, original verdict, initial location, actual independent recheck, result, and limits. Record the final reconciliation of the two PDFs and full MD with the PDFs' Markdown sources: selected ID sets, agreement of cards/textual statuses and overall summaries, absence of double counting, both parts of the full report, navigation, substantive and structural checks of the MD, and visual checks of each PDF.

The final `audit_status` agrees between manifest and report: `in_progress` until completion; `complete` when Section 10 of `meta_agent.md` is satisfied; `partial` for specific remaining limitations; `blocked_subagents` for a mandatory stop. Audit completeness is not the same as submission readiness and does not depend on the number of open findings.

### 10.4. `decisions.md`: decisions and history

The decision log records explicit user decisions, withdrawal of mistaken findings, merging of duplicates, and resolution of disagreements. Do not hide a previously reported critical error from history merely because the reviewer later had to withdraw it.

## 11. Quality checks for two PDFs and the full MD

For the two PDFs, use a readable font covering the selected report language and any quoted source text, sufficiently large body text, clear heading hierarchy, page numbers, a table of contents/bookmarks, and clickable links where supported. Tables must break across pages without clipping; long URLs and formulas must stay within margins. Save the full MD as UTF-8 with readable headings, tables, formulas, and precise links. Do not build its PDF version even for checking.

Colored fills or markers must be accompanied by the words “Critical,” “Noncritical,” “Resolved,” and “New,” or clear equivalents in the selected report language. For an orange card, additionally state its severity or unverified status in words. Do not depend on PDF font support for colored emoji. Formulas must be legible as formulas; do not leave broken LaTeX markup for the user.

After final assembly:

1. Open both PDFs and the full MD. Verify that each is readable and contains its required sections, an empty selection is explicitly explained, and no file is omitted.
2. Render and visually inspect every page of **the two PDFs only**, especially cards, tables, and section transitions. Check for clipping, overlaps, missing-glyph boxes, or dropped lines. After fixing a layout problem, recheck changed and adjacent pages.
3. Check PDF cards for ease of reading: heading, locator, and issue should be immediately visible, with detailed analysis directed to `03_Full_Report.md`. Verify actual color fills/markers; words alone with identical styling on every card do not satisfy PDF color coding.
4. Check the full MD as a text document: valid readable UTF-8, headings and both parts, all eight detailed appendices, mandatory domain tables, substantive grounds for positive and negative conclusions, questions, fixes, and history. Reconcile against accepted domain reports and `coverage.md` to ensure no necessary analyses were lost; use `objects.json` to verify an object-specific result for every object. Checking only for headings does not replace substantive acceptance.
5. Check Markdown syntax where it affects meaning: tables, formula and code blocks, escaping, links, and stable anchors. Verify every internal target and file link, automatically or at its precise location; check readable MD locators in the PDFs. Do not render the full MD into PDF or perform a page-by-page visual inspection of it; use completed domain acceptance, registry reconciliation, and targeted checks of disputed or changed material.
6. Reconcile IDs, textual states/color categories, severity, card content, and history with the shared registry across all three final files. Check both PDF selections under Section 8.0, identical overall summaries and “Tough Reviewer” blocks in the first PDF and full MD, separate counts in the second PDF, and no double counting. New orange findings must appear in the appropriate short PDF according to severity.
7. Reconcile `audit_status`, accepted roles, unchecked objects remaining, and the presence of all files in the current run directory. Save the results of checking both PDFs and the full MD in `acceptance.md`.

If either PDF cannot be generated or visually inspected, or if the full MD cannot be substantively and structurally checked, preserve available sources and completed files, identify the unfinished file/stage precisely, and do not claim the set is complete. The full MD requires no PDF rendering. The mandatory stop without subagents still applies.
