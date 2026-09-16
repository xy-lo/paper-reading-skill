# paper-reading

面向科研论文阅读的 Codex skill。它默认用通俗、简洁的中文，按照以下因果主线组织内容：

`为什么值得读 → 原来有什么问题 → 方法怎样一步步解决 → 实验说明什么 → 价值与边界`

## 主要特点

- 用少量、有逻辑关系的章节代替逐节复述论文。
- 以论文总览图为方法解释主线，并用编号步骤说明流程。
- 选择关键结果图表，给出实验条件、指标、核心数字和证据边界。
- 区分作者主张、论文证据和读者判断。
- 默认输出通俗精读笔记；仅在用户明确要求时扩展为深入评述。

## 安装

```bash
git clone https://github.com/xy-lo/paper-reading.git ~/.codex/skills/paper-reading
```

重新启动 Codex 或开启新任务后，可通过 `$paper-reading` 调用。

## 目录

- `SKILL.md`：技能入口和完整工作流。
- `agents/openai.yaml`：界面名称和默认提示词。
- `references/report-template.md`：精简笔记与深入评述模板。
- `references/figure-and-evidence-rules.md`：图表选择、视觉核验和证据锚定规则。
- `references/reference-style.md`：写作风格来源与适用边界。

## 适用范围

适用于论文阅读、论文精读、论文解读和论文评述。全文双语翻译、固定 Paper Card、正式审稿报告和幻灯片制作应交给相应的专门技能。
