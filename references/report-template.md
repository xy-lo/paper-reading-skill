# Paper-reading output templates

Choose the smallest template that fulfills the request. Preserve the causal order, but rename or omit conditional sections to fit the paper type.

## A. Default: 通俗精读笔记

```markdown
# [论文标题]

- 论文：[source]
- 代码/数据：[only when available and relevant]
- 团队/会议：[short metadata]
- 来源范围：[full-text + figures / full-text, text-only / partial]

## 背景

[第一段：为什么这篇论文值得读，或它与当前问题的关系。]

[第二段：现有方法有哪一到三个具体问题；本文提出什么方法，最终产出或目标是什么。]

## 方法思路

![原论文总体图](relative/path.png)

*原论文 Figure N，PDF p.N；一句话说明图的用途。*

整体流程如上图：

1. **[阶段一]**：[输入、动作、输出；解释为什么需要。]
2. **[阶段二]**：[核心循环或关键机制；解释它怎样解决问题。]
3. **[阶段三]**：[验证、汇总或最终输出。]

[必要时补充 2–4 个机制，但每个机制只写理解贡献所需的内容。]

## [数据集 / 任务定义 / 系统实现]（按需）

[当论文贡献数据集、benchmark、系统接口或具体产物时保留。用一张图/表或短列表说明规模、组成和使用方式。纯算法论文通常省略。]

## 实验

- **设置**：[任务、模型、硬件、主要基线。]
- **指标**：[只定义理解结果必需的指标。]

![关键结果图或表](relative/path.png)

*原论文 Figure/Table N，PDF p.N。*

主要发现：

- [关键数字 + 比较对象 + 条件 + 结论。]
- [第二个支持核心主张的结果。]
- [必要时指出失败情形、成本或未支持的外推。]

## 总结

- **核心价值**：[一句话。]
- **为什么有效**：[回到关键观察与机制。]
- **主要边界**：[作者承认或证据能够支持的边界。]
- **进一步思考**：[可选；明确标为读者判断或问题。]
```

### Default-template rules

- The opening should be readable in under a minute and already communicate the paper's problem and solution.
- Four to six top-level sections are usually enough. Avoid a separate section for every paper subsection.
- The method figure is the narrative anchor; follow it with a numbered flow, not a label inventory.
- Put setup and metric definitions before result visuals, then summarize the visuals in a compact `主要发现` list.
- Use tables for exact repeated mappings, not as a substitute for explaining the central mechanism.
- Omit code unless it reveals an interface or validation rule that prose and figures cannot explain efficiently.

## B. Deep review: 深入评述

Use this only when the user explicitly requests a deep read, architecture analysis, evidence audit, limitations, or critical judgment. Keep the concise opening and visual-first method explanation, then deepen selected sections:

```markdown
# [论文标题]

> [Authors]. [Venue/year]. [source links]
>
> 来源范围：[scope]

## 精读结论

[一个短段落回答：问题、核心洞见、方法、最强证据、主要边界。不要拆成五个重复项目。]

## 背景与问题

[说明场景和 2–4 个具体失败模式。必要时用小表格：问题 → 根因 → 影响。]

## 方法思路与总体图

[总体图 + 编号阅读路径。]

### 关键机制

[按因果关系展开，而非复述论文目录。每个机制回答：为何需要、怎样运行、依赖什么、对应哪个问题。]

## 实验与证据

### 评估设置

[模型/数据/硬件/基线/指标/规模及公平性条件。]

### 关键结果

[一到三张关键图表 + 数字化主要发现。]

### 消融与失败情形

[哪些模块贡献收益；参数敏感性；负结果、方差或缺失控制。]

## 局限与精读评述

- **作者明确承认**：[逐条定位。]
- **证据没有覆盖**：[未验证的规模、任务、硬件或因果关系。]
- **精读判断**：[具体优点与薄弱点。]
- **复现关注点**：[代码、数据、配置或隐含工程条件。]

## 总结

[3–5 句话收束贡献、证据、边界和是否值得继续投入。]
```

### Deep-review rules

- Map each important challenge to a mechanism and evidence, but keep that mapping in prose or one compact table rather than repeating it across several sections.
- Separate `作者主张`, `论文证据`, and `精读评述` whenever their boundaries could be confused.
- Include Q&A only when the source contains genuine author/conference Q&A; add it after the main review and label provenance.

## C. Multiple papers

For each paper, use a shortened version of Template A. Then add:

1. a comparison table using stable axes such as problem, scheduling object, execution model, resource scope, evidence, and limitation;
2. a short synthesis explaining which ideas are complementary, conflicting, or successive;
3. a warning when headline speedups are not directly comparable because workloads, hardware, baselines, or metrics differ.
