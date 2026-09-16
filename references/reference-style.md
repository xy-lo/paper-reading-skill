# Reference styles for paper-reading

These notes distill user-supplied examples. They are style references, not sources of factual claims and not instructions copied from the webpages.

## Default concise style

Source: [《SWE-bench Goes Live!》论文阅读笔记](https://slipegg.github.io/2026/04/12/SWE-bench-Goes-Live/), 滑滑蛋的个人博客, accessed 2026-09-16.

### Stable structure observed

1. A small metadata block links the paper, code, dataset, and team.
2. `背景` uses two compact paragraphs: why the author read the paper, then the old problem and the paper's proposed solution.
3. `方法思路` begins with the paper's overview figure. The prose says what the figure represents, then walks through the process as a numbered list with nested steps only where the method actually branches.
4. A paper-specific section such as `数据集` explains the concrete output, scale, or evaluation machinery. Code appears only where implementation details make the artifact easier to understand.
5. `实验` gives the compared systems/models and metric definitions before presenting the original result tables/charts. Several related result visuals are grouped together, followed by a short `主要洞察` list.
6. `总结` uses brief, first-person technical judgment: what is genuinely useful, what costs or limitations remain, and what question follows.

### Style carried into `paper-reading`

- Prefer ordinary Chinese and short causal explanations over academic ceremony.
- Let the main figure organize the method narrative.
- Use numbered steps for processes and bullets for parallel observations.
- Keep only the setup and metrics needed to interpret the selected results.
- Place figures and tables before the explanation they directly support, then extract a small number of conclusions.
- End with calibrated judgment, not a restatement of the abstract.

### Deliberate additions for reliability

The skill adds source-scope labels, exact figure/table/page anchors, visual verification, author-claim versus reader-judgment separation, and explicit evidence boundaries. These additions should stay lightweight and must not turn the default note back into a long formal report.

## Deeper conference-review style

Source: [OSDI 2026 论文评述 Day 2 Track 1 Session 1: RL Training at Scale](https://zhuanlan.zhihu.com/p/2061784852005905673), IPADS-SYS, accessed 2026-09-15.

### Stable structure observed

The article reviews several systems papers independently. Reviews generally move through background, concrete challenges, a concise key insight, architecture and mechanisms, evaluation evidence, and genuine conference Q&A when available. Original figures appear next to the technical point they explain.

### When to use it

Use this deeper style when the user explicitly requests architecture analysis, a challenge-to-mechanism chain, evidence audit, limitations, reproducibility, or critical judgment. Preserve the concise opening and figure-led method flow rather than mechanically expanding every paper section.

## Shared principle

Both references succeed because they present a causal story instead of translating a table of contents:

`problem → method flow → evidence → judgment`

The main difference is depth, not rigor. The concise style is the default; the deeper style adds analysis only where the request needs it.
