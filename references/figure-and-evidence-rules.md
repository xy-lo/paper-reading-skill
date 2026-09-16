# Figure and evidence rules

## Figure selection

Select by argumentative value, not visual attractiveness. Priority is:

1. overall architecture, method overview, conceptual model, or mechanism figure;
2. a figure needed to understand the most important internal mechanism;
3. a result or ablation figure that supplies the strongest evidence for the central claim.

Usually one to three figures are enough. Do not dump every figure into the review. A figure is essential when removing it would make the problem-solution chain or evidence judgment materially harder to understand.

For the default concise note, prefer this sequence:

1. one overview/process figure at the start of `方法思路`;
2. one paper-specific artifact figure or table only when it clarifies a dataset, task definition, or system output;
3. one or two related result figures/tables grouped before a compact `主要发现` list.

The visual should carry part of the explanation. Do not include an image merely to decorate a section or reproduce every paper figure.

If the paper has no single overall figure, use the smallest set of original figures that jointly explains the system. Label that choice as an editorial selection, not as the paper's official main architecture.

## Visual inspection

For every embedded or described figure:

- record exact figure/table number, panel letter, caption, section, and PDF page index when available;
- inspect the rendered pixels at readable resolution;
- distinguish figure caption claims from conclusions supported elsewhere;
- use the legend and surrounding paragraph to interpret encodings;
- never infer arrow direction, grouping, color meaning, or numeric values from OCR alone;
- if text is unreadable, crop or render at higher resolution before interpreting it;
- keep crops complete enough to preserve legends, axes, labels, and panel identifiers.

When visual access is unavailable, write `未直接核验图像像素；以下图解仅依据正文/图注` and do not use phrases such as “图中清楚显示” for unverified details.

## Architecture explanation

Explain an architecture/mechanism figure in this order:

1. **Purpose**: the design question the figure answers.
2. **Entry and exit**: inputs, outputs, state, resources, or boundary conditions.
3. **Reading path**: the actual arrow, numbering, or phase order.
4. **Modules**: each important component's job and interface.
5. **Control/data distinction**: separate them when the paper does.
6. **Challenge mapping**: which component addresses which challenge and why.
7. **Claim boundary**: what the diagram specifies but does not empirically establish.

Avoid merely translating labels. The explanation should let a reader mentally execute one end-to-end example.

In the concise style, compress these checks into a short introduction and a numbered flow. Do not create seven visible subsections just because seven analytical questions were checked internally.

## Result figures and tables

Before a result visual, state the minimum setup and metric definitions needed to read it. After the visual:

- lead with the main comparison and exact condition;
- keep the baseline, numerator/denominator, unit, and evaluation scope attached to the number;
- explain what mechanism the result supports;
- state an important boundary when the visual does not establish generality or causality.

When several panels or tables jointly support one conclusion, keep them together and summarize them once. Do not interrupt the reader with repetitive commentary after every panel.

## Evidence anchoring

Use the strongest available locator, for example:

- `[论文 §4.2，Figure 3，PDF p.7]`
- `[论文 Table 2，PDF p.10]`
- `[论文 Eq. (5)，§3.1]`
- `[作者 Q&A，问题 2]`
- `[仅摘要可见]`

`PDF p.N` means the Nth page in the file, not the printed page label. If both matter, name both explicitly. Never assign page 1 to unlocated text.

For numerical comparisons, record the numerator, denominator, unit, evaluation condition, and baseline. Do not rewrite percentage-point changes as percent changes or latency reductions as throughput improvements.

## Provenance labels

Keep these epistemic categories distinct:

- **作者主张**: stated by the paper but not independently verified.
- **论文证据**: directly supported by a figure, table, experiment, proof, or analysis in the paper.
- **作者补充**: conference Q&A, appendix, repository, or author response outside the main paper.
- **精读评述**: the reader's reasoned analysis grounded in identified evidence or gaps.
- **外部核验**: a claim checked against separately cited literature or authoritative records.

Do not upgrade an author claim to external fact merely because it appears in the abstract, introduction, or conclusion.
