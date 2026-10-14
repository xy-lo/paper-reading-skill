# Precision deep-read style

This is the canonical style for 论文精读. Its goal is not a shorter summary, a
book review, or a translation. It reconstructs how the paper argues, how the
system executes, and what a researcher should steal or question.

## Core angle

For every section, answer four questions before drafting:

1. **Why is this here?** Which prior limitation, constraint, or challenge does it attack?
2. **What is the mechanism?** What are the input, decision, action, output, and invariant?
3. **Why does the mechanism work?** Name the topology, bandwidth, memory, scheduling, phase, workload, or cost-model property that makes it possible.
4. **What should the reader remember or reuse?** Keep the exact architecture decision, formula, algorithm behavior, headline number, attribution, or reusable sentence pattern.

Never replace a mechanism with a label. “使用 GA 全局优化” is insufficient; say what
the individual encodes, why greedy components become suboptimal, how legality is
preserved, and what the evaluator returns.

## Artifact skeleton

Use the paper's own section numbering. For the second paper in a set, use `2.1`,
`2.2`, and so on. Keep subsection numbering when the paper's structure carries
meaning.

```markdown
# [论文标题]

[Authors / affiliations.] [Venue, year.] [DOI or source.]

整篇逻辑总览：[一两句说清论文类型和核心主张。]

[可选因果链：机会 → 独特约束 → 论点 → Gap → 方案 → 实验证明 → Discussion → Related Works。]

1. [执行型概览第一层：设计/架构探索做什么。]
2. [第二层：资源、内存或运行时调度做什么。]
3. [第三层：全局优化/执行/评估如何收口。]
4. [第四层：实验证明哪个最优设计和端到端收益。]

## [N].1 Abstract

- [中文因果要点。]
- [核心贡献。]
- [结论和关键数字。]

## [N].2 Introduction

1. [作者论证链中的第一个中文判断。]
   - <span style="color:#FF7A00;font-style:italic">“[English source sentence, unchanged.]”</span>
2. [第二个判断。]

## [N].3 Background

### [N].3.1 [paper subsection]

[先用中文解释机制或对比训练/推理、GPU/wafer 的关键差异，再列原文证据。]

...
```

For a systems/DSE paper, include these tail sections when producing the full
writing-oriented template:

```markdown
## [N].x Evaluation

### [N].x.1 Experiment Setup

1. [硬件/die 配置：尺寸、阵列、工艺、频率、算力、SRAM、带宽。]
2. [架构候选：die 数、DRAM、D2D、最优配置。]
3. [Workloads：模型、规模、精度、数据集/trace。]
4. [指标和归一化方式。]

## 可复用图表配置表

## 高频句式模板
```

Omit the two tail sections only when the user asks for a short reading note
rather than the full precision template.

## Section-specific rules

### Abstract

Use three to six bullets, not a translation. Follow the paper's causal order:
workload/resource pressure → platform advantage/limitation → contribution →
headline result. Keep numbers exactly and attach the comparison object.

### Introduction

Preserve the author's argument order. Convert each distinct claim into a short
Chinese judgment, then place the exact English sentence that carries it
underneath. Do not combine challenge, evidence, and contribution into one bullet.
For contributions, preserve the paper's own list order and include stated
insights verbatim in meaning.

### Background

Explain only mechanisms needed later, but explain them operationally. When a
paper contrasts training and serving, old platform and new platform, prefill and
decode, or DP/TP/PP, make the contrast explicit. A useful pattern is:

`共同骨架 → 关键差异 → 平台导致的新约束 → 论文为什么选择/排除某机制`.

### Motivation

Each observation should have three layers:

1. Chinese conclusion in one line;
2. the concrete figure/table evidence and what its panels show;
3. the reason the old system cannot solve it.

Do not state “性能差” without the condition, comparison object, topology, workload,
and number.

### Framework

Start with an overview figure and describe the loop in input → candidate search →
specialized schedulers → execution → evaluator → feedback terms.

Follow the paper's mechanism order, but do not mechanically promote every paper
subsection to a reading-note subsection. Put the framework overview and secondary
components directly under the main framework heading when the user's note uses
that convention; reserve numbered subsections for primary components. For a
WSC-LLM-style note calibrated to the user's WATOS template, the expected shape is:

```markdown
### 2.5 Framework（overview figure）

总览：输入 = ...；离线/在线边界 = ...；核心组件 = ...；Evaluator 输出 = ...

#### 2.5.1 Central Scheduler

1. **Partition Strategy**
   - 算法：...
   - 约束：...
   - 输出：...
2. **Placement Strategy**
   - 洞察：...
   - 公式/例子：...

#### 2.5.2 Execution Scheduler

...
```

For each primary component:

1. First state the remaining problem left by the previous component.
2. Under `方法`, explain the mechanism as numbered executable steps.
3. Preserve constraints, pruning conditions, algorithm complexity, formulas,
   operator choices, placement rules, and output handed to the next stage.
4. Where the paper gives a numeric microexample, include it; it usually reveals
   why the design matters.
5. End with the interface/output only when it is distinct from the mechanism.

Use dense labels instead of prose-heavy subsubsections when the mechanism is
already familiar from a related paper: `洞察`, `算法`, `约束`, `公平性`,
`输出`. Keep formulas, complexity, shapes, queue order, pruning condition, and
numeric microexamples; drop restated background that the reader already needs
only once.

### Cross-paper calibration

When the user supplies an earlier paper note in the same line—for example WATOS
before WSC-LLM—make the comparison explicit at the exact repeated mechanism:

```markdown
- 洞察（与 WATOS 同款）：D2D bandwidth > DRAM bandwidth → 全 wafer DRAM 当作统一内存池。
- 与 WATOS 对照：WATOS 用 γ 惩罚 checkpoint path 与 pipeline path 的共享；WSC-LLM 用 α 惩罚 KV transfer path 的共享。
```

Mark such bridges as reader synthesis unless the later paper itself cites or
compares the earlier mechanism. Do not silently turn a cross-paper inference into
evidence from the current PDF.

### Evaluation

Separate setup, architectural DSE, end-to-end result, attribution, and ablation.
For fair comparisons, record compute, memory capacity, memory bandwidth, topology,
software baseline, workload, and normalization. For a headline gain, always attach
the baseline and metric. After the number, explain the mechanism: utilization,
fewer recomputations, less congestion, better placement, phase-specific TP, etc.

### Discussion and Related Work

For Discussion, list each robustness/generalization axis and the result that
supports it. For Related Work, group by research line and compress each line to
`对象/平台 → 覆盖了什么 → 为什么仍不解决本文问题`. Preserve the paper's first-work
claim only with its exact scope.

## Algorithm, formula, and terminology granularity

For a precision deep read, “explained the algorithm” is not enough. For each
algorithm or formula, preserve the reader's next-level questions:

1. **Objective**: what is being minimized/maximized, and for which unit?
2. **Search space**: exactly what is enumerated; what variables are chosen?
3. **Feasibility constraints**: memory, topology, shape, ordering, capacity.
4. **Black-box helper**: if the algorithm calls a helper such as `test()`,
   state what it returns, what the paper says about its implementation, and
   explicitly flag what remains unspecified.
5. **Microexample**: preserve arithmetic groupings from the paper or user note,
   e.g. `(8α+16)=4×(2+2+2α)` rather than only the simplified form.
6. **Interface/output**: what is handed to the next scheduler or evaluator?

Do not simplify a cost expression if the simplified form hides the physical
meaning. Prefer the decomposition that shows “base hops + shared-link penalty”,
“prefill portion + decode portion”, or “storage cost + recompute cost”.

Add a short **术语与符号表** near the beginning of systems-paper notes. Define
terms needed to parse later mechanisms: phase/instance differences, queue names,
scheduling policies, communication primitives, attention variants, and
paper-specific notation. At first use, also define the term inline when it is
load-bearing. For LLM serving notes, common examples are:

```text
phase vs instance
prefill vs decoding
QP/QD queue
FCFS
chunked prefill
continuous batching
goodput
D2D vs W2W
MHA vs GQA
DRAM Costs
idle/stall
All-Gather vs All-Reduce
Reduce-Scatter
basic TP vs hybrid TP
```

If a paper leaves a critical implementation detail unspecified, add a clearly
labeled `精读追问`, not a silent inference. Example:

```markdown
精读追问：Algorithm 1 的 `test()` 具体如何执行？论文只说明它是单实例模拟器，
用于估计 phase workload 的 goodput；未给出 ASTRA-sim 配置、goodput 定义、
lookup-table 命中逻辑和误差校准细节。
```

Also preserve short but load-bearing source sentences inside method sections,
not only in Abstract/Introduction/Motivation. A shape/topology constraint such as
“instances must be rectangular” or a memory assumption such as “D2D bandwidth >
DRAM bandwidth” often explains the whole mechanism.

## Source sentences and formatting

- Recover exact English sentences from the PDF, not from a prior note, when the
  sentence will be quoted. Preserve hyphenation resolved to normal spelling,
  citation brackets, equations, and any source typo inside a quotation.
- Put a Chinese interpretation first; the English quote is evidence, not the main
  explanation. Do not quote routine transitions.
- In Feishu, format direct source quotes as **italic + orange**. For portable
  Markdown, use:

  ```markdown
  - <span style="color:#FF7A00;font-style:italic">“[source sentence]”</span>
  ```

- Do not apply orange italics to your own interpretation, headings, figure
  captions, or numeric conclusions.
- Bold only load-bearing terms, decisions, numbers, and contrasts. Avoid bolding
  whole sentences.

## Figures

- Crop the original figure from the PDF; do not paste a full page unless panels and
  captions are inseparable.
- Render at 200–300 DPI and preserve panel letters, legends, axes, labels, table
  headers, and enough surrounding whitespace to avoid clipping.
- Place the figure immediately after the Chinese explanation it supports.
- Use this caption pattern:

  ```markdown
  ![原论文 Figure N：短用途](assets/figN.png)

  *原论文 Figure N，PDF p.N：[一句话说明它如何支撑上文。]*
  ```

- Before embedding, inspect the rendered crop. If a legend or axis is unreadable,
  re-render or write that the visual was not fully verified.
- A motivation section usually needs its observed-performance figure; a framework
  section needs its overview and the figure explaining the novel mechanism; an
  evaluation section needs the end-to-end comparison and the utilization/attribution
  figure.

## Calibration against a user reference note

When the user supplies their own note, compare at the subsection level:

1. Are the same claims selected, or did the draft add filler / omit the author's
   key mechanism?
2. Is the granularity the same: component-level decisions, constraints, outputs,
   and numeric microexamples?
3. Does each mechanism explain why it works on the specific platform?
4. Are source sentences attached to the same load-bearing statements?
5. Are figures inserted at the same decision points?
6. Is terminology identical (for example, modelP, activation checkpoint, Mem_pair,
   Sender/Helper, goodput, KV cache, prefill/decoding instance)?

Do not copy unverifiable user-note claims into the PDF-grounded output. If the
user note adds an interpretive bridge not explicit in the paper, either verify it
or mark it as reader analysis. If the draft is broader, narrower, or more formal
than the reference, revise the skill rule, rerun the same section, and compare
again.

Common calibration failures and fixes:

| Failure | Fix |
|---|---|
| Draft follows the PDF table of contents too literally | Promote primary mechanisms, fold overview/evaluator into framework when the reference does so |
| Draft is textbook-like and loses the user's dense judgment | Use `洞察 / 算法 / 约束 / 输出` labels and numeric microexamples |
| Draft omits the user's cross-paper connection | Add a clearly marked `与 WATOS 同款/对照` bridge |
| Draft invents evaluator-level detail the user does not target | Keep secondary components in overview unless they are novel or requested |
| Quotes crowd out mechanism explanation | Put Chinese interpretation first and quote only load-bearing sentences |
| Algorithm explanation stops at loop structure | Preserve objective, feasibility checks, helper behavior, microexample, output interface, and unresolved `test()` details |
| Formula is over-simplified | Keep the decomposition that reveals physical costs and shared-link penalties |
| Reader must already know serving vocabulary | Add a terminology table and define phase/instance, queue, batching, GQA, D2D/W2W, and communication primitives |
| A paper's missing implementation detail is silently filled in | Add a labeled `精读追问` and separate source evidence from inference |

## QA gate

Before delivery, verify:

- section numbers and order match the paper;
- every headline number, formula, algorithm constraint, and component name matches the PDF;
- every quoted sentence exists in the PDF and preserves its claim boundary;
- every embedded image has been visually inspected and cleanly cropped;
- every method mechanism has input/decision/output or a clear reason it works;
- user-reference alignment does not override source evidence;
- the file uses relative image links and keeps assets in a sibling folder.
