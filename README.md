# paper-reading-skill

面向科研论文阅读的 Codex skill。它包含两种模式：

- **通俗精读**：默认用短因果主线组织内容。
- **Precision deep read / 论文精读**：当用户明确要求论文精读、源文锚定的全文笔记，或要求对齐已有精读笔记时使用；保留论文节号、机制颗粒度、PDF 原图裁剪和橙斜体原文。

默认通俗模式的因果主线是：

`为什么值得读 → 原来有什么问题 → 方法怎样一步步解决 → 实验说明什么 → 价值与边界`

## 主要特点

- 用少量、有逻辑关系的章节代替逐节复述论文。
- 以论文总览图为方法解释主线，并用编号步骤说明流程。
- 选择关键结果图表，给出实验条件、指标、核心数字和证据边界。
- 区分作者主张、论文证据和读者判断。
- 默认输出通俗精读笔记；明确要求时进入论文精读或深入评述模式。

## 安装

```bash
git clone https://github.com/xy-lo/paper-reading-skill.git ~/.codex/skills/paper-reading
```

重新启动 Codex 或开启新任务后，可通过 `$paper-reading` 调用。

## 目录

- `SKILL.md`：技能入口和完整工作流。
- `agents/openai.yaml`：界面名称和默认提示词。
- `references/report-template.md`：精简笔记与深入评述模板。
- `references/precision-reading-style.md`：论文精读模板、原文引用、原图裁剪和用户笔记校准规则。
- `references/figure-and-evidence-rules.md`：图表选择、视觉核验和证据锚定规则。
- `references/reference-style.md`：写作风格来源与适用边界。

## 适用范围

适用于论文阅读、论文精读、论文解读和论文评述。全文双语翻译、固定 Paper Card、正式审稿报告和幻灯片制作应交给相应的专门技能。
