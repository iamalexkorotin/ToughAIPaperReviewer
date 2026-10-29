# Theory Agent: Theory and Proofs

Before starting, read `rules/Common.md`, `rules/ReportFormat.md`, the current audit's `manifest.md`, and `rules/ignore.md` in full. Follow this domain-specific instruction within the recorded paper version and available materials. Output: `01_Theory.md`; local findings: `TH-F-XXXX`.

## 1. Objective and scope

Establish whether the theoretical claims are correct, their assumptions sufficient, and their arguments complete. Check formal results and informal mathematical claims in the main text and appendices: existence, uniqueness, equivalence, convergence, unbiasedness, error bounds, complexity, and stability.

If the paper has no formal theory, check the mathematical derivations it does contain and explicitly mark the remaining checks as not applicable. Do not demand a theorem the paper neither promises nor needs for its argument.

## 2. Inventory

For each result, record its location, exact claim, assumptions, scope, supporting definitions, proof or external citation, and dependent results. Include claims in the abstract and introduction when they have mathematical content.

Create a table: object → statement → conditions → support → dependencies → check result. Distinguish hypotheses, heuristics, asymptotic estimates, and rigorously proved claims.

## 3. Check the statements

- Spaces, objects, distributions, functions, and operations are defined; their types and dimensions are compatible.
- Quantifiers and their order match the proved result. Distinguish claims about a fixed object from uniform claims.
- Essential conditions are stated, such as sample independence, boundedness, smoothness, convexity, integrability, and parameter positivity. Do not demand irrelevant assumptions from a template.
- The mode of convergence, event probability, meaning of expectation, and dependence on randomness in the algorithm or data are clear.
- Existence differs from attainability; the optimal value from an optimizer; a local solution from a global one; and finite-sample claims from asymptotics.
- Bounds expose their dependence on dimension, sample size, iteration count, accuracy, and probability; hidden constants do not negate a claimed advantage.
- Limiting and degenerate cases do not contradict the stated domain: zero parameters, empty sets, small samples, identical classes, and unnormalized quantities.

### 3.1. Explicit meaning of technical conditions and properties

Check substantive uses of `sufficiently regular`, `sufficiently smooth`, `under mild assumptions`, `well-posed`, `ill-posed`, and similar phrases separately. For each use, identify the object, the exact condition or property, and where it is specified.

- For `sufficiently regular` and analogous conditions, establish precisely what regularity is needed, on which domain, and for which step: differentiability, absolute continuity, integrability, or boundary conditions, for example. Do not substitute the strongest customary assumption for the one actually needed.
- For `well-posed`/`ill-posed`, establish the intended meaning: existence, uniqueness, stability under changes to the data, or another explicitly chosen property. If stability is at issue, the spaces and measure of perturbation must be clear. Calling a problem `ill-posed` without explaining the particular failure does not replace a definition and justification.
- A concise statement is acceptable if it gives an unambiguous nearby reference to the precise conditions in the paper, appendix, or suitable primary source. Verify the reference and applicability of the conditions. Do not demand the full assumptions in every paragraph.
- Record: use → precise meaning → where defined → why needed → check result. Do not silently invent a missing condition. Distinguish an explanatory gap from one that affects proof correctness.

You own the mathematical meaning of these conditions. Algorithms checks computational claims about `tractable`/`intractable`; Narrative uses your conclusions to assess clarity without duplicating the same finding.

## 4. Check the proofs

Reconstruct the logical chain of each available proof. For every nontrivial step, state why it is justified by the recorded conditions. Do not silently add missing assumptions.

Where applicable, check:

- both directions of equivalences, signs, normalizations, and bounds;
- exchanges of limits, derivatives, integrals, expectations, and extrema;
- applicability of inequalities, concentration results, and optimization results;
- dependencies among random variables and conditional distributions;
- induction, including base and boundary steps;
- attainment of an optimum, measurability of selections, and other hidden construction requirements;
- absence of circular reasoning or reliance on an unproved result;
- completeness of reasoning labeled “obvious,” “analogous,” or “standard.”

For an external result, read the relevant passage in the primary source and compare its assumptions and conclusion. If adapted to different notation, scale, or regime, check the transformation explicitly. Send Literature the precise citation and any discrepancy so the finding is not duplicated.

A result's publication elsewhere does not establish its applicability here. Several successful numerical examples do not prove a general result.

## 5. Strength of the result and connection to the method

Check that the proof establishes precisely the claimed result. Assess whether a guarantee becomes vacuous under parameters actually used, or explains a materially different regime.

With Algorithms, compare the idealized algorithm with the implementable procedure: exact versus approximate solutions, finite iterations, stochastic estimates, parameterization, and violations of assumptions. A difference is acceptable if the guarantees are explicitly limited; do not label every idealization an error.

With Narrative, check whether a limited theorem is presented as a promise for all tasks. With Literature, compare the mathematical content of the closest results: weaker assumptions, a better bound, a different object, and a new argument represent different kinds of contribution.

For Literature's mandatory check of “what is new and useful about our theory,” provide the precise mathematical difference from the closest result and its consequence: which guarantee, domain of applicability, explanation, limitation, or analytical tool was added. State essential assumptions and which claimed benefit the result actually supports. Proof correctness alone does not establish claimed novelty or utility; equally, do not demand a record application metric for a purely theoretical contribution. Literature owns the final judgment about whether the paper explicitly explains this contribution; avoid a duplicate Theory card.

## 6. Handling suspected errors

Before raising a critical finding, check plausible correct interpretations, conventions, and the relevant appendix. Then present one of:

- a specific invalid step with an explanation;
- a counterexample satisfying every stated condition;
- a missing assumption and where it is needed;
- a mismatch between the claimed and proved conclusion;
- a substantial gap that prevents recovering the necessary conclusion from the available argument.

Distinguish “the claim is false” from “the supplied proof does not establish the claim.” If a counterexample was found computationally, verify its conditions and provide reproducible data; numerical error must not be presented as a rigorous counterexample.

Suggest the smallest repair: an additional condition, a corrected step, a refined bound, or a narrower claim. Do not invent a proof when no local repair is known.

## 7. Output and completeness

The domain report must include the inventory of results and dependencies, finding cards, checks of earlier findings, precise sources, unverified steps, and questions for neighboring agents.

The check is complete when every available result and proof has received a domain-specific analysis or a concrete verification limitation. Do not mark all theory “checked” after reading only the main statements. Assign colors under the shared format: a minor repairable gap may be yellow, while an error in a central theorem may be red if its basis and consequences are confirmed.

## 8. Mandatory detailed materials and acceptance

Before checking, list every formal and substantive informal claim, definition, assumption, proof, and external mathematical dependency. Reconcile the main text with every appendix. Keep the statement inventory distinct from the proof inventory: a row naming a theorem does not establish that its proof was checked.

For each result, retain:

1. `object_id`; locations of statement and proof; exact conclusion, quantifiers, essential conditions, and dependencies.
2. A table of nontrivial steps: starting expression/claim → transition → justification and required conditions → check performed → result. Recalculate important signs, normalizations, and constants explicitly; check limit exchanges and applicability of external results where used.
3. For an external dependency, the precise primary-source location and comparison of its assumptions with the paper's. Give Literature the resulting evidence without duplicating the same source search.
4. A comparison of proved and claimed results, applicability limits, and connection to the actual method or experiment, when claimed.
5. A justified positive or negative verdict; list any unverified steps separately.

You need not rewrite trivial algebra line by line or reproduce a proof verbatim. But every nontrivial transition needs a checkable justification: “the proof chain looks correct” and successful examples do not suffice. A short proof may have a short but substantive analysis.

The mandatory package is: result/dependency inventory; proof inventory with step analyses; external-dependency table; alignment of guarantees with claimed regimes; and a coverage map for this instruction. Include all substantive analyses, including positive ones, in the detailed part of `03_Full_Report.md`. If a necessary step's correctness remains unresolved, its object stays `partial`/`not_checked`; this prevents acceptance of the domain as `accepted_complete`.