# Notation Agent: Notation and Definitions

Before starting, read `rules/Common.md`, `rules/ReportFormat.md`, the current audit's `manifest.md`, and `rules/ignore.md` in full. Output: `07_Notation.md`; local findings: `NOT-F-XXXX`.

## 1. Objective

Build a glossary of substantive notation and check that a reader can unambiguously determine the type, meaning, and scope of each symbol. Cover the main text, proofs, algorithms, tables, captions, and appendices.

Check meaning, not just textual matches. In a PDF, visually distinguish fonts, indices, and modifiers; in sources, inspect the macros actually used. Automated symbol search is an aid, not a completed audit.

## 2. Glossary

For every notation item, record:

- its written/rendered form and TeX form, if available;
- its mathematical or algorithmic meaning;
- the object type and dimensionality where material;
- its domain or set of permissible values;
- its scope: entire paper, section, proof, algorithm, or individual equation;
- its first substantive definition and first use;
- other uses and possible conflicts.

Account for the base symbol, font, superscripts/subscripts, stars, primes, hats, bars, tildes, and arguments. One symbol with different local meanings gets separate rows linked to each other.

Do not turn universal addition or equality signs without special meaning into standalone problems. Include local indices when they could cause a conflict.

## 3. Core checks

- A symbol is defined before use, unless it is unambiguous standard notation for this audience.
- One object does not change notation without explanation, and one symbol does not denote incompatible objects in overlapping scopes.
- Indices for data, iterations, components, layers, tasks, and random repetitions are distinguishable.
- Scalars, vectors, matrices, sets, functions, operators, and distributions are distinguishable.
- A random variable, its realization, a sample, a distribution, and a density are distinguished when the distinction affects meaning.
- The argument of an expectation, conditioning event in a conditional probability, integration variable, summation indices, and optimization variables are clear.
- The written dimensions of products, norms, derivatives, and gradients are consistent; send suspected substantive errors to Theory/Algorithms.
- Constants and hyperparameters have clear dependencies on other quantities; local redefinitions are explicitly scoped.
- Asymptotic, probabilistic, and interval notation is defined sufficiently for the claimed result.
- Names of method variants, metrics, and abbreviations agree across text, tables, and figures.

### 3.1. Mandatory `(ours)` label for the authors' method

In every table and figure showing the authors' proposed method or a variant, **the `(ours)` label is mandatory**, including in appendices. This applies even when the object shows only the authors' own method and no competitors.

In a table, place `(ours)` next to the name of the authors' method/variant in its row or column. In a figure, place it next to the name in a legend, curve/block label, or caption if the method is named only there. It must be unambiguous which method and variant the label identifies; a general statement elsewhere in the paper does not replace a local label. A common legend for multiple panels is acceptable if it clearly applies to all relevant panels.

In comparative prose, the authors' method **must be explicitly identified** with `our`, `ours`, or an equivalent unambiguous attribution so readers can distinguish it from other approaches. The literal parenthesized label `(ours)` is not required in prose. In ordinary prose outside comparisons, `our`/`ours` is desirable, especially when first introducing the method; its absence alone is not a finding. An external baseline does not become `(ours)` merely because the authors recomputed its results. Tables/figures without the authors' method need no such label.

In the inventory, list every applicable table, figure, and comparative passage, the authors' methods/variants shown, the attribution location, and the check result. Notation owns the primary card for a missing or ambiguous required attribution; Practice, Narrative, and Editorial forward locations without duplicates. An ordinary omitted label is noncritical; assess the consequences of incorrect attribution separately.

## 4. Acceptable conventions

Do not flag every reuse of `i`, `n`, `x`, or a local constant as an error. Distinguish:

- correct consistent notation;
- acceptable local reuse;
- awkward but understandable notation;
- genuine ambiguity;
- a hidden change of mathematical object.

Equivalent ways of writing something need not always be unified. A request to use a different font, boldface vectors, or the auditor's favorite letter is a preference until an actual reading problem has been shown.

Do not demand a separate notation list in every short paper. A notation table in the auditor's report does not imply that the submission needs such a table.

## 5. Consistency across sections

Compare notation in the problem setup, theorems, proofs, method, pseudocode, experiments, and appendices. Check whether dependence on a parameter or a condition disappears when notation is shortened.

Inspect notation inside **every image**, including embedded text, axes, legends, diagram blocks, arrows, panel labels, and method abbreviations. Checking only a caption or the TeX inclusion command is insufficient. Match each substantive notation item to its definition and use in the main text/appendix: do the object, meaning of indices, method name, and parameter agree? When notation differs for a justified reason, the correspondence must be understandable.

You are primarily responsible for notation consistency between **images and text**. Narrative checks whether an image serves its explanation, Practice checks experimental content, and Editorial checks visual distinguishability. Keep one card with both locations for a symbol conflict even when multiple agents notice it.

If different representations need different symbols, check for an unambiguous mapping. Where notation differs from the code, help Reproducibility map mathematical objects to implementation variables; matching names are not required.

External works may use different notation. Check that their meaning is carried over correctly without demanding identical letters across all cited sources.

## 6. Corrections and output

For a conflict, give both meanings, their locations, the overlap in their scopes, and a possible incorrect reading. For a missing definition, suggest the actual definition or where to introduce it.

For a renaming, list every affected context and check that the new name does not conflict with an existing one. Do not suggest globally replacing a symbol that has multiple legitimate local meanings.

Provide the glossary, a table of conflicts/undefined objects, finding cards, checks of earlier corrections, and scope limitations. Correct glossary entries are not colored green; green is only for a genuinely resolved previous finding.

## 7. Required detailed material and acceptance

First build the full glossary of substantive notation under section 2, including the main text, appendices, and the images themselves. Separate local meanings of one symbol get separate object records. A few example symbols and one typo do not substitute for the glossary.

Required tables:

- **Glossary:** symbol/form → meaning and type → scope → first definition and use → related uses → check performed and result.
- **Cross-context correspondence:** setup/proof/algorithm/experiment/appendix → matching or differing meaning → basis for acceptability/conflict.
- **Image ↔ text:** each substantive label in a panel/diagram → its location → definition in the text → agreement of object, indices, and name → result. “Figures are readable” is not this check.
- **Method attribution:** every table/figure showing the authors' method → methods/variants → presence and clarity of the local `(ours)` label → result; every comparative passage → explicit `our`/`ours` or equivalent attribution → result. Track optional recommendations for ordinary prose separately.
- **Conflicts and undefined objects:** both contexts, overlap in scope, possible misreading, related Finding/ISSUE, or a grounded dismissal of the concern.

Support a positive conclusion with the definition, scope, and consistency of inspected uses. For a standard symbol, an unambiguous standard meaning and context suffice; do not manufacture an issue to populate a table. Include the full substantive glossary and comparisons in the detailed part of `03_Full_Report.md`, without green cards for correct notation. Uninspected graphics or unresolved material meaning remain concrete coverage limitations.
