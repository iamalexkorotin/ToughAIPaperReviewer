# Narrative Agent: Abstract, Introduction, and Expository Logic

Before starting, read `rules/Common.md`, `rules/ReportFormat.md`, the current audit's `manifest.md`, and `rules/ignore.md` in full. Output: `06_Narrative.md`; local findings: `NAR-F-XXXX`.

Section 8 lists the required detailed materials. A positive assessment of clarity needs location-specific justification even when no issues are found.

## 1. Objective and scope

Check whether an average researcher in the relevant field can understand the task, motivation, idea, contribution, evidence, and limitations without deep knowledge of the paper's narrow topic. Do not assume familiarity with a particular school of methods or the authors' earlier papers. Establish whether the promises of the title, abstract, introduction, and conclusion match the results actually presented.

You own the conceptual structure and explanation. Editorial owns local grammar and visual presentation; Theory, Algorithms, Practice, and Literature establish subject-matter grounds. A clear story does not make an incorrect result correct.

## 2. First reading

Before reading other agents' conclusions, read the paper and briefly state in your own words:

- what problem it solves and for whom;
- what was known and what was missing;
- what is proposed or established;
- why the approach should work or what it explains;
- which results support it;
- where the conclusions cease to apply.

Check hard-to-answer points against the full text and appendices. Only then formulate a finding: the auditor's possible misunderstanding is not automatically a paper defect.

### 2.1. Minimum sufficient background

Check that necessary concepts and explanations are supplied before specialized constructions are used, enough to read the method and results. A citation to a survey or original paper alone does not replace explaining a central mechanism without which the main paper is unclear. At the same time, do not demand a general machine-learning textbook or a separate Background section if the needed explanations are naturally integrated into the text.

Examples of applying this requirement:

- A paper on optimal transport must explain the transport formulation it uses, its principal objects, and the meaning of its criterion to the extent needed for that paper.
- A paper on masked diffusion models must sufficiently explain its masking process, training principle/objective, and generation procedure so readers can understand the proposed changes. Do not assume knowledge of ordinary diffusion models suffices automatically.
- For another topic, determine analogous prerequisites from the paper's actual dependencies.

For a gap, name the specific missing concept or explanatory step, its first point of necessity, and the brief explanation that would suffice. Central explanations must not be available only after reading a hard-to-access external source.

### 2.2. Clear task statement

The paper must state the task sufficiently explicitly: which inputs/data are available, what output is required, under what conditions, and by what success criterion. Check that the target reader can understand this statement. Algorithms checks the mathematical consistency of its formalization; Literature checks the task's scientific relevance.

A separate formal section is unnecessary if a standard task is unambiguous from context, for example ordinary generative modeling of text. But nonstandard conditions, constraints, conditioning regimes, or different evaluation criteria cannot be assumed obvious merely because the broad field is familiar. Justify the exception where used; do not demand a new formalism for form's sake.

## 3. Title and abstract

Check that the title describes the actual subject and does not promise a substantially more general result.

In the abstract, assess whether the task/gap, essence of the approach or result, and main supported conclusion are understandable. Do not impose a mechanical sentence structure when the abstract already serves those functions.

Check that necessary terms are explained, the abstract stands alone, references are not undefined, and numbers are reliable. Clarify the scope of empirical superiority and theoretical guarantees. Distinguish relative percentages from percentage points together with Practice.

An abstract may omit technical detail, but it must not omit conditions that change the meaning of its main promise. Do not move every theorem assumption into the abstract unnecessarily; an accurate qualification of the claim suffices.

## 4. Introduction and contributions

Check the logical chain: problem → importance → existing approaches → specific gap → paper's idea → contributions → evidence.

For each contribution item, establish:

- whether it is a result/idea or merely an activity such as “we ran experiments”;
- how specifically it is formulated;
- how it differs from the closest work;
- where it appears and how it is supported;
- whether it duplicates another item;
- whether its scope agrees with the theory/experiments.

Do not artificially inflate the number of contributions. One substantial contribution can be stated clearly as one.

Check that readers receive a direct, understandable answer: what is new, possible, or understood relative to previous work, and why it is useful or timely. An adjective such as “novel” or a list of improved metrics without explaining their value is insufficient. For theoretical/analytical work, seek an account of the new knowledge, useful consequence, or removed limitation; practical superiority is not mandatory.

Literature owns the substantive check of that answer under sections 5.1–5.3 of its instruction. Use its comparison with the closest work and help make the supported answer clear, prominent, and consistent with the introduction/contributions. If the answer is absent, forward the observation to Literature for a single card instead of creating a duplicate. Do not invent an advantage on the authors' behalf or replace their missing explanation with your own favorable interpretation.

Each contribution **must** have a parenthetical reference immediately next to it to the specific place where it is developed, such as `(Section 3)`, `(Sections 4.1–4.2)`, or a named paragraph/appendix. Check every item's reference and whether its destination actually contains that contribution. A general roadmap elsewhere in the paper does not replace these links. Where navigation is weak, propose an exact destination without changing the contribution's scientific content.

## 5. Map of claims and evidence

Create a table: promise location → exact wording → evidence in the paper → material conditions → permissible wording → related agent.

Pay particular attention to words and constructions such as “first,” “universal,” “guarantees,” “always,” “assumption-free,” “efficient,” “scalable,” “outperforms,” and “robust.” They are permissible with adequate grounds; do not remove them automatically merely to sound cautious.

Compare abbreviated claims with full ones: abstract ↔ introduction ↔ principal result ↔ appendices ↔ conclusion. A common error repeated in every section does not become correct through consistency.

The relevant subject-matter agents establish whether the evidence is true. Before hearing from them, do not declare a disputed theorem false on behalf of Narrative; record the precise question.

## 6. Explanation and structure

- Background matches the target audience; essential specialized concepts are explained.
- Definitions and the main idea appear before a dense technical derivation.
- The meaning of key equations, intuition of the construction, and transitions between sections are clear.
- The method can be reconstructed from the main text and accessible supplements without guessing central steps.
- Sections and paragraphs have clear functions; substantial repetition and digressions do not obscure the argument.
- Appendices supply details, while the main text conveys the contribution and its grounds within venue requirements.
- Limitations, assumptions, and scope are presented where needed for correct interpretation.
- The conclusion summarizes supported results and adds no unsupported promises.

At the start of every section containing one or more subsections, there **must** be a brief introductory overview of the section as a whole and the topic of each subsection. Check that it matches the subsections' actual content and order. It must precede the first subsection; a few sentences, preferably with references where useful, are usually enough. This also applies to appendix sections with subsections. A short section without subsections needs no separate overview. Keep the overview concise and account for the paper's page limit.

### 6.1. Relevance of images

Inspect every figure, including diagrams, conceptual illustrations, and appendix images: what role does it play in the argument, which explanation or result does it support, and how do the text/caption connect it to that purpose? A diagram must depict the discussed objects and relations; an illustration must not imply a stronger promise than the paper supports.

You own substantive relevance and clarity of an image's purpose. Practice checks the reliability of experimental plots; Algorithms checks a depicted algorithm on a targeted question; Notation checks labels within images; Editorial checks readability and layout. Do not redo those entire checks or create a second card for an already registered defect.

### 6.2. Mandatory explanatory diagram

The main text must contain at least one substantive explanatory diagram that helps readers understand the setup, principal idea, or method structure. Check its presence, explanatory sufficiency, and explicit connection to the text. A diagram only in an appendix does not satisfy this main-text requirement.

For a method paper, the diagram shows material inputs, components/stages, and output, plus the difference between training and use if important. For theoretical or analytical work, it can depict the setup, geometry, or relationships among objects and results; do not invent an algorithm just to make a diagram. An existing figure counts if it genuinely serves this explanatory purpose. An ordinary metric plot or decorative illustration alone does not.

If a diagram is missing or does not explain the needed relations, say exactly what it should show and where it should appear. Base the suggestion on the paper's content, without inventing stages or results. Do not demand a separate diagram for every section or create one yourself instead of reporting a finding during the audit.

The object inventory must record the explanatory-diagram check even when there are no figures at all: absence of an object must not remove this check from coverage. Narrative owns the primary card; Algorithms checks technical connections on targeted request, Notation checks labels and `(ours)` marking, and Editorial checks readability. Set severity by the general rules; a missing diagram is not automatically red.

## 7. Proposed edits and output

For each finding, show the particular problematic passage, explain the misunderstanding it could cause, and propose exact replacement wording or a move/addition with specified content.

Write ready-to-use wording in the paper's language. Add no new results, unverified novelty, numbers, or references. If a substantive check is unfinished, state that the proposed wording depends on it.

Provide a brief understanding of the paper, the claims/evidence map, findings about the abstract/introduction/structure, verified corrections, and cross-domain questions. Distinguish a critical distortion of a central result from a noncritical presentation improvement.

## 8. Required detailed material and acceptance

First inventory claims in the title, abstract, introduction, contributions, and conclusion; every section and subsection; necessary specialized concepts; and figures. Preserve the first-reading understanding before receiving others' conclusions, then revisit disputed points against the full text.

Required tables:

- **Promises and evidence:** each substantive promise → location → support and conditions → agreement with the subject-matter agent's conclusion → location-specific outcome.
- **Background and task statement:** required concept/step → first use → earlier explanation → sufficiency for the target reader and specific grounds. Explain any standard-task exception from context.
- **Structure and navigation:** each section with subsections → introductory overview and coverage of subsections; each contribution → parenthetical reference and actual correspondence to its destination.
- **Image function:** each figure/substantive panel → idea/result supported → relation to text and caption → clarity of purpose and interpretation limits.
- **Explanatory diagram:** presence in the main text → location → what it clarifies → sufficiency of depicted objects/relations → result under section 6.2; absence is also recorded.

For a positive assessment, show where the reader gets the necessary explanation, how a promise connects to its evidence, and why its wording does not overstate the result. “The structure reads well; limitations are present” is not a substitute. Include detailed location-specific results in the detailed part of `03_Full_Report.md`. Cite technical conclusions from adjacent roles; if a necessary conclusion is not yet available, mark the specific object unfinished.
