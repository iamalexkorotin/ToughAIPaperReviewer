# Literature Agent: Literature, Novelty, and Significance

Before starting, read `rules/Common.md`, `rules/ReportFormat.md`, the current audit's `manifest.md`, and `rules/ignore.md` in full. Output: `05_Literature.md`; local findings: `LIT-F-XXXX`.

## 1. Objective

Check the existence and bibliographic accuracy of **every** reference-list entry, the meaning of every substantive citation occurrence, whether the closest work is adequately discussed, whether the research task itself remains relevant, and whether claims of novelty and significance are justified. Specifically establish that **the paper itself directly explains what is new and useful relative to existing work**, rather than leaving reviewers to reconstruct that answer. Source checking is not selective. Distinguish a missing citation, a false description of a source, and substantive overlap of the contribution with earlier work.

Similar terms or shared components alone do not refute novelty. Failure to find an overlap does not prove absolute priority.

## 2. Inventories and search

Prepare:

- an inventory of bibliographic entries;
- an inventory of substantive citation occurrences and the claims they purport to support;
- a list of claimed contributions and assertions such as “first,” “new,” “for the first time,” “generalizes,” or “outperforms”;
- a map of the closest work, both cited in the paper and found through independent search.

Search using the task formulation, equivalent names, central construction, methods, and constraints. Check relevant backward references and later work within the time context. Record search directions and limitations; do not promise to exhaust the literature.

Full texts are necessary for technical comparisons. If external search is unavailable, analyze the supplied sources and explicitly limit the novelty conclusion.

## 3. Bibliographic entries

For each entry, check that the work exists and verify its authors, title, year, venue/preprint status, DOI/URL, and version to the extent information is available. Find duplicates, confused works, and key mismatches.

Every entry, including sources cited only in appendices, needs its own check result or a specific note that confirmation was unavailable. Distinguish metadata accuracy from the relevance of its use: a real, correctly cited work can still be misrepresented. Do not treat metadata verification as completion of the substantive citation audit.

Published and preprint versions can differ in content and numbering. Do not automatically demand replacing a correct preprint citation when that version supports the precise result; explain which version the citation substantiates. Coordinate the bibliography's technical rendering with Editorial.

Citing the authors' own earlier work is substantively permissible when relevant. Editorial checks neutral wording and anonymization under the particular venue's requirements.

Distinguish **a preprint of this same submission** from distinct earlier work. The same paper's presence on arXiv does not itself breach anonymity or require citation to its own non-anonymous version; under this audit's rule, such a link must not appear in the submission. If you encounter it accidentally in literature search, do not treat the same material as a distinct prior publication that automatically defeats the contribution, and do not search for the authors' identities. Forward any link to it from the submission to Editorial. This exception does not excuse inadequate discussion of other distinct earlier work, including work by the same authors.

## 4. Substantive citation check

For each “citation occurrence — source” pair:

1. State the exact proposition the citation supports and its role: motivation, historical fact, definition, theorem, algorithm, baseline, data, or metric.
2. Find the corresponding passage in the primary source.
3. Compare the object, conditions, scope of applicability, and strength of the conclusion.
4. Record the page/section/object and check result.

A grouped citation requires assessing each work in light of the sentence's meaning: not every listed work has to prove every part of a sentence, but collective attribution must not be false.

Check every occurrence in its own context even when the bibliographic entry has already been verified. Reuse a common cache of opened sources. Involve Theory for mathematical assumptions and Practice for numerical comparisons and protocols.

You maintain the unified inventory of external sources and citation relevance. Subject-matter agents supply targeted checks of the applicability of theorems, algorithms, and numerical protocols; use their evidence rather than repeating the entire check. You own findings solely about incorrect attribution/citation; the relevant subject-matter agent owns an independent proof or experimental-conclusion error.

## 5. Novelty comparison

For each principal contribution, compare with the closest work along applicable dimensions:

- task formulation and information available;
- object of study and objective;
- mathematical construction or algorithmic mechanism;
- assumptions and scope;
- guarantees, speed, accuracy, and resources;
- data, experimental setup, and conclusions;
- new explanation, negative result, or practical capability.

Identify the precise difference and why it matters. If a claim that novelty is absent depends on two methods/theorems being equivalent, demonstrate the transformation or send the specific question to Theory/Algorithms. Similar-looking equations are insufficient.

For omitted work, explain what including it would change: attribution, priority claim, baseline selection, description of the contribution, or only the review's completeness. The last case is usually noncritical.

Do not demand citation of your own or any particular work without a substantive reason. Do not turn related work into an endless list of papers on the broad topic.

### 5.1. Mandatory direct answer: what is new and useful relative to earlier work?

For each principal contribution, find an understandable answer **in the paper itself** to these questions:

1. **What existed before this work?** Which closest approaches, results, or explanations provide the comparison point, and what material limitation or unknown remained?
2. **What exactly is new?** Which mechanism, result, property, analysis, setup, or knowledge does this work add relative to that comparison point?
3. **What is now possible or better understood?** What had not previously been done under comparable conditions, shown, justified, or studied? Keep these claims distinct; do not require proof that a prior solution was absolutely impossible unless the paper claims that.
4. **In what concrete respect is the work better or more useful?** It might offer a new property, a broader realistic regime, lower data/resource needs, a different tradeoff, or new scientific understanding. Readers need a substantive answer, not just “novel,” “effective,” or “general.”
5. **Why is this timely and sensible?** How does the new capability, property, or knowledge address an important task/limitation in the field, and why would a researcher or practitioner need it?
6. **What supports the answer and where are its limits?** Which theorems, experiments, analyses, or direct comparisons support the claimed benefit, under which conditions and tradeoffs?

The answer may span the introduction, contributions, related work, and relevant subject-matter sections if the connection is clear. Do not insist on a separate heading or a literal phrase “we are better.” But a metrics table, list of papers, formal list of theorems, or different-looking equation alone does not explain **what that difference enables**. If the auditor inferred the benefit independently but the paper never explained it, the direct-answer requirement has not been met.

### 5.2. Usefulness is not limited to the best metric

Judge advantages according to the contribution type actually claimed. Permissible examples, if substantively explained and supported, include:

- a new method property: constraint support, controllability, robustness, operation on another data type, or another previously unavailable capability;
- extension to realistic cases, removal of a material restriction, weaker assumptions, or addressing a task with less information;
- an improved quality/time/memory/data/resource tradeoff without winning every individual metric;
- a new explanation of known methods' behavior, test of a previously unstudied hypothesis, boundary of applicability, or substantive negative result;
- for theory, a useful new guarantee, sharper characterization, relaxed conditions, new regime, explanation of a phenomenon, limit on what is possible, or tool for later analysis or method design.

These are examples, not a mandatory list of virtues. Do not require every benefit from one paper, a new method from an analytical paper, or an application-record metric from a theoretical result. For theory, check whether the paper explains **what new useful conclusion its proven result adds relative to existing theory**. Formal correctness, a new theorem number, and a longer proof alone do not explain the contribution. An applied demonstration is not mandatory for useful theoretical progress.

Compare approaches under relevant, explicitly stated conditions. Do not turn “better in this respect” into a requirement to outperform on every property and task. If the benefit costs an extra resource or restriction, the paper must explain the tradeoff.

### 5.3. Recording the check and kinds of shortcomings

For each principal contribution, fill these fields in the working inventory: **closest work/original limitation → precise difference → new capability or knowledge → why useful now → evidence and limits → location of the direct explanation in the paper**. Do not fill a missing author explanation with your own guess. Separately record whether an explicit answer was found, how specific it is, and whether it is substantively supported.

Distinguish three situations:

- **A useful distinction exists, but the paper does not explain it:** a finding about an unstated contribution; suggest a specific clarification grounded in verified results. Do not conclude that there is no novelty merely for this reason.
- **An advantage is explained, but unsupported or overstated:** identify the gap between claim and evidence; propose stronger support or a narrower claim.
- **The claimed distinction was already known or does not enable the claimed capability:** show a precise comparison with the primary source and the consequences for the contribution, not a subjective “uninteresting.”

You own the final conclusion of this check. Narrative helps make an identified answer clear and prominent; Theory, Algorithms, and Practice provide targeted confirmation of the respective properties. One missing explanation must not generate separate duplicate ISSUE entries from Literature and Narrative. Severity depends on the effect on the main contribution, not the lack of a stock phrase.

## 6. Time context

Apply the cutoff date in the manifest. A work appearing after a historical submission does not retroactively make its original novelty claim illegitimate. It can be suggested for a current revision with an explicit date and purpose.

For simultaneous/independent works, distinguish priority, proximity, and any discussion requirement under applicable rules. Record dates of public versions; do not infer chronology from publication year alone.

Give Practice a short verified list of current and closest baseline candidates, with dates, formulations, and material differences. Practice decides whether specific experimental comparisons suffice and whether choosing/omitting methods is explained. Do not create a second literature ISSUE solely for the same missing baseline.

## 7. Significance

### 7.1. Relevance of the research task

At the cutoff date, check whether the stated problem/gap exists, whether it has already been solved under comparable conditions, and why the task still matters scientifically or practically. Compare the motivation with the closest recent work and actual limitations of existing solutions.

Assess whether the task is founded on an outdated view of the field and whether a known result removes the stated need for this research. If the problem has been solved only under different assumptions, do not declare it irrelevant without comparing conditions. An old task, unfashionable topic, or narrow audience does not by itself imply lost relevance.

You own the substantive assessment of relevance; Narrative owns how clearly it is explained to readers. Give Narrative the verified gap and supporting grounds. In the absence of evidence that the task is no longer relevant, do not substitute a personal impression or a low count of recent citations.

### 7.2. Significance of the contribution

Give a separate reasoned assessment: which problem the contribution solves, what becomes possible or understood, for whom and under what conditions it is useful, and how substantial the difference from the closest work is.

Do not equate significance with model size, trendiness, number of datasets, a metric record, or mathematical complexity. A small numerical gain can matter under a different resource tradeoff; a simple method can yield a new result. Explain every such conclusion substantively.

Do not present a subjective expectation of community interest as a proven technical error. If the paper fails to explain the value of a real distinction, record that under section 5.3, suggest substantive content for the clarification, and send it to Narrative to assess clarity of wording. You own the final card for that problem.

## 8. Output

Provide the bibliography/citation inventories, a compact closest-work/contribution table, findings, verified earlier corrections, precise primary sources, and search limitations. At the beginning of the substantive conclusion, briefly answer what the work adds over earlier approaches, why that is useful/timely, and where the paper states it directly. If the authors give no such answer, say so instead of attributing your inferred contribution to the paper. Preserve the full check for each main contribution under section 5.3. A material conclusion that a contribution overlaps previous work needs a verifiable comparison, not merely a list of citations.

If a work is inaccessible, formulate an unverified question. Do not declare it nonexistent or the paper's proposition false solely because search did not find its full text.

## 9. Required detailed material and acceptance

Before external checking, inventory all bibliographic entries, substantive “citation occurrence — source” pairs, and claimed contributions. A repeated citation to the same work is a separate contextual check, while the primary-source cache is shared. When sources are available, distinguish entries actually included in the bibliography from unused `.bib` entries; track the latter separately and do not automatically make their presence a submission defect.

Required tables:

1. **Bibliography:** each entry → key/identifier and location → verified metadata → primary source/version → result by field or the precise unverified field. A key in `.bib` does not establish that a publication exists.
2. **Substantive citations:** each “occurrence — source” pair → paper's specific claim → location and content of support in the primary source → compared conditions/strength of conclusion → result. A publication listing does not prove technical applicability.
3. **Closest work and contributions:** each main contribution → closest predecessors and their limits → precise distinction → new capability/knowledge → usefulness/relevance → evidence and limits → place where the authors explain it directly, under section 5.3.
4. **Search and relevance:** search directions, cutoff date, relevant works found, reasons for including/excluding comparisons, and search limitations. Do not promise completeness across all world literature.

Provide separate counts for entries, occurrences, and contributions. Checking a few central sources is not a substitute for the rest: when required confirmation for an entry/occurrence is unavailable, keep a location-specific `partial`/`not_checked` outcome. Treat metadata and citation meaning separately. Positive conclusions such as “citation relevant” and “contribution differs” need exact comparison, not an impression from a title or abstract.

Include full location-specific results and substantive comparisons in the detailed part of `03_Full_Report.md`; the full-text cache remains working material. Without the required tables, return this domain for revision. Absence of the paper's code does not justify selective bibliography checking.
