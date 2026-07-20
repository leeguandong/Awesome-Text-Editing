# Contributing to Awesome-Text-Editing

感谢你帮助维护这份列表。我们欢迎补充论文、官方实现、项目页、模型、数据集、benchmark、评测协议，以及修复失效或错误信息。

## 收录范围

优先收录与以下任务直接相关、且有可核验公开来源的工作：

- scene text replacement、addition / insertion、removal / erasing；
- visual text rendering、style / font / color control；
- multilingual、cross-script、RTL 或复杂字形生成与编辑；
- text-rich visual document / graphic design editing；
- 面向上述任务的数据集、benchmark 和评测指标。

纯 OCR、普通图像编辑、字体设计工具或通用文档编辑器通常不进入主表；若能为本方向提供直接方法或评测参考，可放入“相关方向”。

## 提交前检查

1. 搜索 README，确认没有同名论文、旧版本或重复项目。
2. 优先提供论文、作者项目页、官方仓库、官方数据/模型页面；第三方复现必须显式标注为 unofficial。
3. 确认所有链接可以访问，且论文标题、arXiv ID、venue、年份和代码归属一致。
4. 年份使用首次公开年份；只有在论文、OpenReview、会议页面或作者官方页面明确确认时才填写 venue。
5. 不确定的信息使用 `—`，不要根据仓库名、搜索摘要或计划投稿信息推断。

## 新条目所需信息

请尽量提供：

- 工作名称与完整论文标题；
- 首次公开年份，以及已确认的 venue / status；
- 任务类型和核心机制的一句话说明；
- 支持的语言或脚本；
- 训练数据、评测数据及其规模；
- paper / project / code / model / dataset / benchmark 链接；
- 为什么该工作与 text-in-image generation/editing 直接相关。

主表格式：

```markdown
| **Method** | 2026 | method · replacement | concise mechanism | multilingual | train: Dataset; eval: Benchmark | [Venue](paper-url) | [code](official-url) |
```

`train`、`eval`、`both` 分别表示训练资源、评测资源和兼具两种用途的资源。官方资源尚未发布时填写 `—`；不要链接空仓库或论文里已经失效的地址。

## Pull request 建议

- 一个 PR 聚焦一组相关更新，标题简洁明确。
- 同步更新主表、对应任务索引、数据集/benchmark 表和开源项目表；避免只在一个位置添加名称。
- 按首次公开年份排序，同一年尽量按 arXiv / 发布时间排序。
- 描述保持客观，避免 “best”“first”“state of the art” 等不可持续宣传语，除非它本身是必要且有上下文的论文结论。
- 不提交论文 PDF、模型权重或数据文件，只提交公开来源链接。

发现失效链接或事实错误时，可以直接提交小型修复 PR，并附上核验日期和替代来源。
