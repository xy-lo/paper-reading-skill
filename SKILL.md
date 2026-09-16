---
name: paper-reading
description: >-
  Produce source-grounded Chinese paper-reading notes or deep reviews in plain,
  concise language, organized around background, the problem, method flow,
  figures/tables, experimental findings, and limitations. Use for 论文阅读、论文精读、
  论文解读、论文评述, or requests for a paper's core idea, method, evidence, and
  takeaways. Do not use for full-paper bilingual translation (`nature-reader`), the
  fixed 16-section Paper Card (`nature-paper-card`), formal referee reports
  (`nature-reviewer`), or slide-deck production.
---

# Paper Reading

Turn a paper into a short, logically connected explanation that a technically literate reader can understand without repeatedly consulting the PDF. Default to Chinese when the user writes in Chinese. Preserve canonical English terms on first mention and keep equations, model names, dataset names, metrics, and units faithful to the source.

The default narrative is:

`为什么值得读 → 原来有什么问题 → 方法怎样一步步解决 → 实验说明什么 → 价值与边界`

Prefer a small number of meaningful sections, original figures, and concrete conclusions over an exhaustive section-by-section retelling.

## Default style

Unless the user explicitly asks for a long-form deep review, use the **通俗精读笔记** style:

1. Start with one or two short background paragraphs. Explain why the paper matters and state its main problem and solution in ordinary language.
2. Put the paper's main overview or architecture figure near the start of the method section. Follow it immediately with a numbered reading path that lets the reader mentally execute the method.
3. Explain only the mechanisms needed to understand the contribution. Group them into two to four logically ordered points; do not reproduce the paper's section order mechanically.
4. In the experiment section, first give the minimum setup and metric definitions, then show the most informative result figure or table, and finally state two to four quantitative takeaways.
5. End with a short summary containing the paper's value, main limitation, and one useful question or implication. Separate the paper's claims from the reader's judgment.

Use plain language before terminology. A useful pattern is:

`术语是什么 → 为什么需要它 → 它具体怎么运行 → 它解决了哪个问题`

Avoid ceremonial headings, duplicated summaries, long component inventories, and unexplained acronyms. Use bullets for parallel facts and numbered lists for processes. Use a Markdown table only when it makes repeated mappings or comparisons materially easier to understand.

Read [references/report-template.md](references/report-template.md) before drafting. It contains the concise default template and the deeper variant.

## Depth control

- **Default / 通俗精读笔记**: use `背景 → 方法思路 → 任务/系统产物（按需）→ 实验 → 总结`. Usually four to six top-level sections are enough.
- **Deep review / 深入评述**: when the user explicitly asks for challenges, architecture details, evidence chain, limitations, or critical judgment, deepen the same narrative with challenge-to-mechanism mapping, ablations, assumptions, and reproducibility notes. Do not automatically expand into a fixed ten-section report.
- **Short question**: answer inline with the smallest structure that resolves the question; do not force an artifact or full review.
- **Multiple papers**: explain each paper independently in the same compact structure, then add a comparison table and a short synthesis. Never merge evidence across papers.

## Source boundary

Accept a PDF, DOI, arXiv or publisher URL, pasted text, or an existing source-mapped reading artifact. State the source scope in one short line:

- `full-text + figures`: full text and important visuals were inspected;
- `full-text, text-only`: full text was read but figure pixels were not verified;
- `partial`: only the abstract, excerpts, metadata, or selected figures were available.

Never imply full-paper or visual inspection in a weaker mode. Mark unavailable evidence `材料不足，无法判断`; do not infer unseen results, limitations, or implementation details.

For a PDF, inspect the rendered page for every figure or table used in the output. Text extraction alone is insufficient for claims about arrows, grouping, color, spatial layout, axes, or numeric cells.

## Workflow

1. Identify the paper, accessible source scope, paper type, claimed contribution, and the user's likely reading purpose. Do not ask for a purpose when a useful general explanation is possible.
2. Build an internal evidence inventory before writing: the problem, key observation, method stages, inputs and outputs, one main figure, one or two useful result visuals, evaluation setup, headline results, and limitations.
3. Find the shortest causal explanation: why the old approach fails, what observation unlocks the solution, how the proposed stages respond, and what evidence tests the claim.
4. Select visuals by explanatory value. Read [references/figure-and-evidence-rules.md](references/figure-and-evidence-rules.md) before extracting or explaining figures and tables.
5. Draft with the appropriate depth from [references/report-template.md](references/report-template.md). Introduce a figure before or immediately after it; never leave an unexplained image dump.
6. Run the groundedness checks below before delivery.

## Analytical requirements

- The first screenful should already answer: what problem, what idea, and why it matters.
- State the **core insight** separately from implementation details, but do so in natural prose rather than forcing a ceremonial label when unnecessary.
- Preserve the causal chain `problem → observation → mechanism → evidence → boundary`.
- For the main method figure, explain its purpose, starting point, reading order, major stages, and output. The explanation should be shorter than the figure's surrounding paper text, not a label-by-label translation.
- For a result figure or table, state the comparison condition, baseline, metric, key number, and what conclusion is and is not supported.
- Report only experiments that test central claims. Do not inventory every dataset, baseline, or ablation unless the user requests exhaustive coverage.
- Treat novelty language such as “first” or “state of the art” as an **author claim** unless independently verified.
- Keep **作者主张**, **论文证据**, and **精读评述** distinct. Reader criticism must name the relevant assumption, missing control, unsupported comparison, or deployment boundary.
- Include Q&A only when the source contains real author or conference Q&A; label its provenance and do not invent it.

## Visual and table use

The default visual set is small:

1. one overall method/architecture/process figure;
2. optionally one dataset/task-definition figure or table when the paper contributes a resource;
3. one or two result charts/tables that support the central findings.

Place each visual next to the explanation it supports. Preserve the original figure/table number, panel letter, caption meaning, and PDF page index. When several result panels jointly support one conclusion, group them before a compact `主要发现` list, as in a readable research blog rather than scattering commentary between every panel.

Do not redraw an original figure unless the user explicitly requests a new or editable diagram. When no useful overview figure exists, say so and provide a clearly labeled text-only flow; do not imply it is an original paper figure.

## Output and placement

Return readable Markdown. For a substantial paper, create a `.md` artifact in the user's requested directory or the current project's established `outputs/` or `docs/` area. Keep extracted figures in a sibling asset folder and use relative Markdown links inside the artifact. For a short inline request, respond in conversation without forcing a file.

## Groundedness QA

Before delivery, verify that:

- title, authors, venue/year, model or method names, datasets, baselines, metrics, units, and headline numbers match the source;
- every core factual or numerical claim has a nearby section, figure, table, equation, or page locator when the source permits it;
- every used figure/table was visually inspected, with legends, axes, labels, sample sizes, and relevant footnotes preserved;
- the prose explains a causal story rather than mirroring the table of contents;
- the first explanation is understandable without specialist shorthand, while later detail remains technically accurate;
- limitations distinguish author-stated boundaries from reader analysis;
- cross-paper comparisons do not compare acceleration numbers as though workloads, hardware, baselines, and metrics were identical;
- no unavailable evidence is filled in by guesswork.

## Relationship to adjacent skills

- `nature-reader` owns full-text bilingual translation and source-map creation.
- `nature-paper-card` owns the fixed 16-section Paper Card deliverable.
- `nature-reviewer` owns formal referee-style critique and multi-reviewer reports.
- `nature-paper2ppt` owns slide decks.
- If an existing output from one of these skills is supplied, reuse its verified source anchors and figures without silently changing the requested deliverable.

The default explanatory style and the deeper conference-review style are distilled in [references/reference-style.md](references/reference-style.md). Read it when revising this skill or when the user asks to match one of those references closely.
