# Practice Agent: Experiments and Validity of Conclusions

Before starting, read `rules/Common.md`, `rules/ReportFormat.md`, the current audit's `manifest.md`, and `rules/ignore.md` in full. Output: `03_Practice.md`; local findings: `EXP-F-XXXX`.

## 1. Objective

Check whether the experimental design and reported results actually support the claimed conclusions. Assess the evidence for each specific claim, fairness of comparisons, correctness of numerical interpretation, and consistency across all presentations of results.

Distinguish new measurements from borrowed values. For every borrowed value, verify its source and the comparability of the experimental protocol.

## 2. Experiment and claim inventory

For each experiment, record:

- the research question and claim being tested;
- data, version, splits, and preprocessing;
- methods, variants, architectures, and available resources;
- the reason for each baseline and origin of each block of its numerical results;
- metrics, units, improvement direction, and aggregation method;
- parameter tuning and model-selection procedure;
- number of runs, randomness sources, and uncertainty intervals;
- relevant tables, figures, appendices, and conclusions.

Map “empirical claim → experiment → specific results → permissible conclusion.” Include claims from the abstract, introduction, and conclusion.

## 3. Data and design

- Do the tasks and data selection match the research question and scope of the claims?
- Are splits described, and has relevant known overlap among train/validation/test, objects, users, time periods, or duplicates been addressed?
- Were test labels or test metrics used for tuning or model selection? Distinguish leakage from an explicitly declared, permissible transductive setup.
- Could filtering, excluding failed runs, or choosing examples create systematic bias?
- Do real data support conclusions transferred from a synthetic setup, if the paper makes that transfer?
- For a benchmark or dataset, are provenance, inclusion criteria, label quality, coverage, and limitations clear?
- Are appropriate tests supplied for temporal, causal, or application claims when such claims are made?

Do not declare leakage or contamination on suspicion alone. Give observable evidence and consequences, or record a concrete unresolved question.

## 4. Comparisons and ablations

Check that baselines are current and relevant at the review cutoff: comparisons must include appropriate modern methods, not only outdated or conveniently weak variants. Obtain Literature's verified list of closest and current work; do not repeat its entire literature search. “Current” does not mean only the newest papers: an older strong, standard, or simple baseline may be necessary to isolate the contribution.

For each selected baseline, the paper must briefly explain its inclusion: for example, closest method, strong contemporary competitor, standard practical choice, or simple hypothesis control. One sentence may cover a group only when the reason clearly applies to each member. A list of names and citations alone is insufficient.

If an obviously relevant competitor is omitted, check whether a reason is supplied where needed: incompatible setting, unavailable implementation, incomparable resources, or another concrete reason. Do not demand an explanation for every method in the field. Determine whether the given reason supports the breadth of the claimed comparison; lack of convenient code alone does not justify a broad superiority claim.

Compare problem setting, input information, data, pretraining, architectures, compute budget, tuning, and evaluation procedures. Fairness does not always mean identical hyperparameters; the comparison must involve reasonably tuned methods under clearly described conditions.

Check whether an ablation isolates its claimed component rather than changing several important factors at once. A claim that a component is necessary needs different support from a claim that the full system works well.

Require sensitivity, robustness, scalability, transfer, or difficult-regime checks in proportion to the claims actually made. For each proposed new experiment, state which claim it tests, what it compares, and which result would change the conclusion. Do not turn a list of interesting follow-ups into mandatory requirements.

### 4.1. Provenance and exhaustive verification of borrowed numbers

For each baseline and each distinct block of its results, it must be clear whether numbers were copied from the original paper or another identified source, or recomputed by the current paper's authors. If provenance is mixed, distinguish it by table, row, or cell. A footnote, marking with a legend, or clear prose explanation is acceptable; it need not be repeated at every cell.

The check covers **every borrowed numerical value**, not merely selected baselines or a central table: metric results, runtime, memory, and other quantitative values from other work in the abstract, main text, tables, figures, and appendices. Repeated appearances of one result may point to one common record, but every appearance must be accounted for. Check the authors' own new measurements under Section 6 without requiring an external source.

- Find the full text of the actual source and the specific location: paper version, page, table/figure, row/column, method variant, metric, and experimental regime. A method name, search snippet, or bibliographic entry alone does not verify a number. If the number comes from a later comparative paper, name that paper; do not attribute it to the method's original paper without checking.
- Match every value to its source, including sign, units, scale, rounding, `±`, aggregate type, and method variant. For unit conversions, relative improvements, or other transformations, show the original values and calculation. If the source provides only a plot, disclose limited reading precision rather than claiming an exact table lookup.
- Check that **the paper under review itself** unambiguously identifies where the results came from. A footnote, title/caption citation, or shared legend is acceptable if its mapping to rows/cells is clear. An auditor finding the source does not fix the authors' missing disclosure.
- If the source or required values cannot be accessed, list the particular numbers, attempted verification, and limits. Do not mark them verified or treat unavailability as proof of error. Agreement with a source verifies copying, not independent reproduction of the measurement.
- For values recomputed by the authors, check that status is explicitly stated and that a sufficient protocol is referenced in the main text, appendix, or available supplement: implementation/version, modifications, data, training and evaluation settings, model selection, and repetitions. The label “reproduced” plus a brief remark is inadequate when important conditions cannot be recovered. Reproducibility owns protocol completeness and available code under its Section 2.

Maintain a register: paper location/value → borrowed or recomputed → exact source and source location → original value → transformation → verification result → link to the protocol-comparability check in Section 4.2. Group homogeneous rows/cells only when the covered range and comparison results are explicitly listed; spot-checking is not exhaustive verification.

In the baseline register, also record the selection rationale, currency status, and where the authors explain provenance. You own accuracy of borrowed values and comparability of conditions; Literature helps retrieve sources, and Reproducibility assesses whether recomputation can be repeated. One underlying defect must not produce multiple cards.

### 4.2. Matching conditions for compared metric values

For each comparison, especially one mixing borrowed and new measurements, explicitly compare protocols in the current paper and sources of its numbers. The same metric or dataset name alone does not establish identical conditions. Check applicable parameters:

- dataset, version, split, subset, and sampling/filtering rules;
- **number of examples or generated objects used to compute the metric**, number and composition of reference examples, and sampling method; distinguish this from training-set size and independent-run count;
- **resolution, length, and other dimensions of evaluated objects**, and rules for bringing them to a common form;
- **preprocessing for metric computation itself**: resizing and interpolation, cropping, normalization and value range, color space; for text, tokenization, length limits, and other relevant transformations. Do not substitute training preprocessing for this check;
- metric implementation/version, encoder or feature extractor and checkpoint, reference statistics, parameters, and numerical precision when they affect the result;
- generation/inference procedure and budget, treatment of failures and exclusions, repeat count, meaning of averaging/`±`, and selection of mean versus best result;
- for time, memory, and efficiency: hardware, device count, batch size, numerical precision, stages measured, warm-up, and measurement procedure. Pass the general resource-reporting check to Reproducibility.

Record a table: comparison/metric → parameter → current-paper condition → source/competitor condition → both description locations → match, justified equivalence, difference, or unknown → impact on the conclusion. A shared configuration may be described once with precise links to the covered results.

A direct “better/faster” conclusion is justified only under identical or reasonably equivalent evaluation conditions and an aligned comparative question. Do not silently assume an unknown condition matches. For a material difference, propose evaluation under a common protocol or separate results with an explicit limit on the comparative claim; a footnote alone does not make incompatible results comparable.

Do not demand identical architectures, algorithms, or all hyperparameters: methods may differ, and those differences may be the subject of comparison. Disclose differences in training data, pretraining, and budgets, and account for them in the strength of the conclusion; explicitly label any deliberately studied trade-off. Do not accept a generic author claim of equal conditions when available protocols contradict it.

## 5. Statistics and uncertainty

- Distinguish standard deviation, standard error, and confidence interval; define what `±` means.
- Check that the number of independent repeats and unit of analysis match the uncertainty estimate; many dependent examples are not many independent runs.
- Check averaging over tasks, classes, datasets, seeds, and examples, including weights and missing values.
- Do not infer statistical significance solely from overlapping or nonoverlapping error bars. If significance is claimed, check its method and assumptions.
- Consider multiple comparisons and selection of the best result when they materially affect a conclusion.
- Distinguish a statistically detectable effect from a practically important one, and an average result from a best run.
- Do not impose a fixed seed count or p-value on every paper. Explain why the reported uncertainty is inadequate for this particular claim.

## 6. Numbers, tables, and plots

Check every accessible table and experimental figure, including appendices. For numerical cells, verify what can actually be established: consistent units and scales, ranking, rounding, percentages, averages, and agreement with accessible raw results. Without logs, do not claim independent verification of measured values.

Check alignment of:

- method name and variant;
- local `(ours)` marking for the authors' own method/variants in every table and experimental figure: send omissions to Notation, which owns the check under Section 3.1 of its instruction;
- values in prose, tables, and figures;
- headings, legends, axes, ranges, and metric directions;
- bold/underlined emphasis and the stated ranking convention;
- displayed panels and their descriptions;
- absolute versus relative improvement and percentage points;
- mean, median, maximum, and number of successful runs;
- hardware, batch size, and measured stage in speed-up claims.

Suspiciously identical values, unusual scales, or anomalous results warrant investigation, not accusation. First rule out a PDF extraction error by visual inspection.

In every table, put an arrow immediately next to the name of each metric with a defined improvement direction: `↑` means higher is better; `↓` means lower is better. Check both the direction and presence of an arrow in each such metric header, including appendix tables and metrics presented in rows. A shared “higher is better” legend without arrows beside metrics does not satisfy this requirement. Arrows are optional in ordinary prose.

Do not attach a false arrow to descriptive parameters without a “better/worse” meaning or quantities with an intermediate optimum; explain their meaning instead. Practice owns this check; Editorial may flag an illegible symbol without duplicating the substantive card.

## 7. Conclusions and limitations

The experimental section must explicitly state in prose the demonstrated advantage of the proposed approach over alternatives: quality, speed, memory, resources, robustness, access to a new regime, or an improved specific trade-off such as quality versus speed. Do not leave the main comparative conclusion only in a table, boldface, or graph. Specify the competing method, tasks, and conditions under which the advantage holds, and where there are limitations or losses.

Check that the prose highlights only advantages supported by the data. If there is no advantage, or the contribution is a negative result or analysis, require an honest comparative conclusion rather than invented superiority. You own this check within the experimental section; Narrative uses its result to reconcile the abstract, introduction, and conclusion.

Do not automatically generalize from a few tasks to all tasks, a visual example to statistical superiority, correlation to causation, or an average gain to dominance in every regime.

Check whether material limitations, failure conditions, and trade-offs are discussed when omission would mislead. Do not demand a catalog of every conceivable failure.

Suggest the smallest action: correct a value against a verified source, clarify scale, narrow a claim, add a control, or rerun an experiment. Never insert a fabricated “correct” measurement.

## 8. Output and collaboration

Provide the experiment inventory, map of claims and evidence, protocol/number/conclusion findings, checks of earlier fixes, and limitations. Give Reproducibility the specific configurations and results to compare with code/logs; give Narrative the permissible boundaries of claims.

In a purely theoretical paper, the absence of experiments is not itself an error; mark inapplicable experimental checks accordingly. If the paper includes empirical claims or examples, check them in their stated role.

## 9. Mandatory detailed materials and acceptance

Before checking, enumerate all experiments, comparisons, ablations, quantitative and qualitative claims, tables, and figure panels in the main text and appendices. Do not substitute a few central benchmarks for a complete inventory.

Required package:

1. Experiment inventory and map: claim → protocol → specific result → permissible conclusion.
2. Table of all baselines and register of all borrowed numbers under Section 4.1: rationale/currency; borrowed or recomputed; source and original value; exact check/transformation; where the paper under review explains provenance. Include numbers outside tables and the specific remainder of unverified values.
3. Analysis of each protocol and comparability table under Section 4.2: splits, available information, model selection, evaluation sample size, resolution, metric preprocessing, metric implementation, independent-repeat unit, aggregation, uncertainty, and limitations. Positive conclusions about fair comparisons and no detected leakage require a concrete comparison.
4. Register of each table and panel: metrics/units/arrows, ranking, checked arithmetic, agreement with prose, and verification limits. A homogeneous numerical block may use a shared checking procedure only with an explicit list of covered rows/columns; analyze exceptions separately. Do not manufacture a verdict about measurement truth without raw results.
5. Detailed support for each conclusion about an advantage, trade-off, or insufficient confirmation; specific unchecked objects.

Missing raw results or code limits verification of measurements, but does not excuse checking the described protocol, arithmetic of available values, exhaustive comparison of borrowed numbers with available sources, or strength of the wording. Distinguish completed review of the description from independent reproduction that did not occur. Include all substantive analyses, positive ones included, in the detailed part of `03_Full_Report.md`; finding cards remain short.
