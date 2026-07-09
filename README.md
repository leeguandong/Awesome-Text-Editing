<h1 align="center">
Awesome-Text-Editing
</h1>
<p align="center">
<b>An Awesome Collection for Text-in-Image Generation and Editing / 收集和梳理图像中文字生成、替换、擦除与无痕编辑方法</b>
</p>
<p align="center">
  <a href="https://github.com/leeguandong/Awesome-Text-Editing/stargazers"> <img src="https://img.shields.io/github/stars/leeguandong/Awesome-Text-Editing.svg?style=popout-square" alt="GitHub stars"></a>
  <a href="https://github.com/leeguandong/Awesome-Text-Editing/issues"> <img src="https://img.shields.io/github/issues/leeguandong/Awesome-Text-Editing.svg?style=popout-square" alt="GitHub issues"></a>
  <a href="https://github.com/leeguandong/Awesome-Text-Editing/forks"> <img src="https://img.shields.io/github/forks/leeguandong/Awesome-Text-Editing.svg?style=popout-square" alt="GitHub forks"></a>
</p>

> A curated list of text-in-image generation and editing methods, covering scene text replacement, text insertion, text removal, multilingual visual text rendering, style-preserving editing, and visual document editing.

本项目旨在收集和梳理 **图像中文字编辑（Text-in-Image Editing / Scene Text Editing）** 相关工作，包括自然场景文字替换、广告海报文字生成、文档图像文字编辑、多语言文字渲染、文字擦除与重绘、OCR / glyph / layout 约束生成，以及对应的数据集与评测基准。

如果本项目能给您带来一点点帮助，麻烦点个⭐️吧～

同时也欢迎大家贡献本项目未收录的论文、开源实现、数据集和 benchmark。提供新的仓库信息请发起 PR，并按照本项目格式提供论文链接、代码链接、任务类型、语言覆盖、数据集/评测信息等。

## About

**Why this repo / 为什么做这个仓库**

图像中文字编辑是当前生成式视觉模型里最难但也最实用的能力之一：模型不仅要把文字写对，还要让字体、颜色、透视、背景纹理、局部光照、文档结构都保持自然。过去这个方向经历了几条明显的演化路线：

- 从 **GAN / image-to-image translation** 的局部文字替换，走向基于 diffusion 的开放域编辑。
- 从只处理英文单词，走向 **中文、多语言、复杂脚本、RTL、混合脚本**。
- 从只追求 OCR 正确，走向同时关注 **style consistency、background preservation、semantic consistency、document layout**。
- 从孤立方法论文，走向 **数据构造 + benchmark + 自动评测协议** 的系统化阶段。

但目前相关工作分散在 scene text editing、text rendering、image editing、document editing、multilingual generation 等多个社区里，分类口径也不统一。这个仓库试图把它们放到同一个视角下：

- **以任务为主轴**：replacement / addition / removal / rendering / document editing / multilingual editing。
- **以方法为辅轴**：GAN、decomposition、glyph/OCR/layout guidance、diffusion、MLLM、benchmark-first。
- **同时收录论文、代码、数据集、benchmark 和评测指标**，方便做 baseline 选择和后续研究定位。

**Scope / 收录边界**

✅ 收录：图像中文字生成、替换、插入、移除、局部重绘、字体/颜色/风格保持、多语言文字渲染、视觉文档文字编辑、OCR/glyph/layout 约束生成、文本编辑 benchmark 和数据集。

❌ 暂不收录：纯 OCR 识别、纯文字检测、普通图像编辑、纯排版工具、传统 PDF/HTML 文本编辑器、与图像文字无关的富文本编辑器。

**Maintainer**

由 [@leeguandong](https://github.com/leeguandong) 维护，欢迎 issue / PR。如果你在做 text-in-image editing 相关工作希望被收录，请提供：论文链接、代码仓库、目标任务、语言覆盖、是否有数据集/benchmark、核心简介。

## 目录

- [About](#about)
- [1. 方法汇总](#1-方法汇总)
  - [1.1 方法全景表](#11-方法全景表)
  - [1.2 演化时间线](#12-演化时间线)
- [2. 按任务分类（What to edit）](#2-按任务分类what-to-edit)
  - [2.1 Scene Text Replacement（场景文字替换）](#21-scene-text-replacement场景文字替换)
  - [2.2 Text Addition / Insertion（文字插入）](#22-text-addition--insertion文字插入)
  - [2.3 Text Removal / Erasing（文字擦除）](#23-text-removal--erasing文字擦除)
  - [2.4 Visual Text Rendering（图像文字生成）](#24-visual-text-rendering图像文字生成)
  - [2.5 Multilingual Text Editing（多语言文字编辑）](#25-multilingual-text-editing多语言文字编辑)
  - [2.6 Visual Document Editing（视觉文档编辑）](#26-visual-document-editing视觉文档编辑)
  - [2.7 任务 × 方法 交叉矩阵](#27-任务--方法-交叉矩阵)
- [3. 按方法范式详述（How to edit）](#3-按方法范式详述how-to-edit)
  - [3.1 GAN / Translation-based Editing](#31-gan--translation-based-editing)
  - [3.2 Decomposition / Stroke / Style Guidance](#32-decomposition--stroke--style-guidance)
  - [3.3 Diffusion-based Text Editing](#33-diffusion-based-text-editing)
  - [3.4 Glyph / OCR / Layout Guided Rendering](#34-glyph--ocr--layout-guided-rendering)
  - [3.5 Attribute and Multilingual Control](#35-attribute-and-multilingual-control)
  - [3.6 Benchmark-first Frameworks](#36-benchmark-first-frameworks)
- [4. 数据集与 Benchmark](#4-数据集与-benchmark)
  - [4.1 数据集](#41-数据集)
  - [4.2 Benchmark](#42-benchmark)
  - [4.3 常用评测指标](#43-常用评测指标)
- [5. 开源工具与项目](#5-开源工具与项目)
- [6. 相关方向](#6-相关方向)
- [Star History](#star-history)
- [License](#license)

## 1. 方法汇总

### 1.1 方法全景表

| 方法 | 年份 | 任务 | 范式 | 语言 | 数据 / Benchmark | arXiv | 代码 |
|------|------|------|------|------|------------------|-------|------|
| **STEFANN** | 2019 | character-level scene text editing | font adaptive generation | English | COCO-Text / ICDAR | [1903.01192](https://arxiv.org/abs/1903.01192) | - |
| **SRNet / Editing Text in the Wild** | 2019 | word-level replacement | style retention + inpainting | English | synthetic / ICDAR | [1908.03047](https://arxiv.org/abs/1908.03047) | - |
| **RewriteNet** | 2021 | style-preserving replacement | content-style decomposition | English | self-supervised real images | [2107.11041](https://arxiv.org/abs/2107.11041) | [clovaai/rewritenet](https://github.com/clovaai/rewritenet) |
| **MOSTEL** | 2022 | stroke-level scene text editing | stroke guidance + semi-supervised | English | Tamper-Syn2k / Tamper-Scene | [2212.01982](https://arxiv.org/abs/2212.01982) | [qqqyd/MOSTEL](https://github.com/qqqyd/MOSTEL) |
| **GlyphDraw** | 2023 | visual text rendering | glyph + position conditioned diffusion | Chinese / general | custom glyph data | [2303.17870](https://arxiv.org/abs/2303.17870) | [project](https://1073521013.github.io/glyph-draw.github.io/) |
| **DiffSTE** | 2023 | editing + insertion | diffusion + dual encoders | English | five datasets | [2304.05568](https://arxiv.org/abs/2304.05568) | [UCSB-NLP-Chang/DiffSTE](https://github.com/UCSB-NLP-Chang/DiffSTE) |
| **TextDiffuser** | 2023 | text rendering + inpainting | layout planning + diffusion | English | MARIO-10M / MARIO-Eval | [2305.10855](https://arxiv.org/abs/2305.10855) | [aka.ms/textdiffuser](https://aka.ms/textdiffuser) |
| **AnyText** | 2023 | multilingual generation + editing | glyph / OCR embedding diffusion | Multilingual | AnyWord-3M / AnyText-benchmark | [2311.03054](https://arxiv.org/abs/2311.03054) | [tyxsspa/AnyText](https://github.com/tyxsspa/AnyText) |
| **TextDiffuser-2** | 2023 | text rendering + layout planning | LLM planner + diffusion | English | - | [2311.16465](https://arxiv.org/abs/2311.16465) | [aka.ms/textdiffuser-2](https://aka.ms/textdiffuser-2) |
| **UDiffText** | 2023 | visual text synthesis + editing | character-aware diffusion | English | - | [2312.04884](https://arxiv.org/abs/2312.04884) | [ZYM-PKU/UDiffText](https://github.com/ZYM-PKU/UDiffText) |
| **Glyph-ByT5** | 2024 | accurate visual text rendering | customized ByT5 text encoder + SDXL | English | design image benchmark | [2403.09622](https://arxiv.org/abs/2403.09622) | - |
| **Glyph-ByT5-v2** | 2024 | multilingual visual text rendering | multilingual ByT5 + preference learning | 10 languages | multilingual paragraph benchmark | [2406.10208](https://arxiv.org/abs/2406.10208) | - |
| **TextCtrl** | 2024 | scene text editing | style-structure guidance + mutual self-attention | English | ScenePair | [2410.10133](https://arxiv.org/abs/2410.10133) | - |
| **AnyText2** | 2024 | attribute-controllable generation + editing | font / color control diffusion | Multilingual | - | [2411.15245](https://arxiv.org/abs/2411.15245) | [tyxsspa/AnyText2](https://github.com/tyxsspa/AnyText2) |
| **TextEditBench** | 2025 | reasoning-aware text editing benchmark | semantic expectation evaluation | English | TextEditBench | [2512.16270](https://arxiv.org/abs/2512.16270) | - |
| **VDE Bench** | 2026 | visual document editing benchmark | OCR parsing evaluation | English / Chinese | VDE Bench | [2602.00122](https://arxiv.org/abs/2602.00122) | - |
| **MULTITEXTEDIT** | 2026 | cross-lingual text-in-image editing benchmark | language fidelity scoring | 12 languages | MULTITEXTEDIT | [2605.08163](https://arxiv.org/abs/2605.08163) | - |
| **TextSculptor** | 2026 | scene text editing + benchmark | data construction + evaluation | English | TextSculpt-Data / TextSculpt-Bench | [2605.21090](https://arxiv.org/abs/2605.21090) | [linyiheng123/TextSculptor](https://github.com/linyiheng123/TextSculptor) |

> 备注：会议/期刊信息仍在持续补全。为了避免误标，未确认 venue 的条目暂以年份 + arXiv 为准。

### 1.2 演化时间线

```
2019  STEFANN / SRNet                         (早期字符级、词级场景文字编辑)
2021  RewriteNet                              (内容-风格隐式解耦)
2022  MOSTEL                                  (stroke-level guidance + 半监督真实图适配)
2023  GlyphDraw / DiffSTE                     (glyph 条件生成 / diffusion 进入 scene text editing)
2023  TextDiffuser / AnyText / UDiffText      (大规模 OCR 数据 + 多语言 + 字符级编码)
2023  TextDiffuser-2                          (LLM layout planning)
2024  Glyph-ByT5 / Glyph-ByT5-v2              (定制 text encoder，长文本和多语言渲染)
2024  TextCtrl / AnyText2                     (style-structure guidance / 字体颜色属性控制)
2025  TextEditBench                           (reasoning-aware text editing evaluation)
2026  VDE Bench / MULTITEXTEDIT               (视觉文档编辑 / 跨语言脚本保真)
2026  TextSculptor                            (大规模 paired editing data + 四任务 benchmark)
```

## 2. 按任务分类（What to edit）

本节从 **"到底要编辑什么"** 的角度切分。一个方法可能同时覆盖多个任务，例如 AnyText 同时覆盖 text generation 和 text editing，TextSculptor 同时覆盖 addition / replacement / removal / hybrid。

### 2.1 Scene Text Replacement（场景文字替换）

**目标**：把图像中已有文字替换成目标文字，同时保持背景、字体、颜色、透视、阴影和局部纹理。

| 方法 | 主要特点 |
|------|----------|
| **STEFANN** | 字符级替换，使用 font adaptive network 保持字体结构，ColorNet 保持颜色 |
| **SRNet** | word-level 替换，拆成 text conversion、background inpainting、fusion 三个模块 |
| **RewriteNet** | 通过识别任务诱导 content / style decomposition，并用 self-supervised real-image training 缓解域差 |
| **MOSTEL** | 使用 stroke guidance map 显式告诉模型哪些笔画需要修改 |
| **DiffSTE** | 使用 character encoder 增强文字正确性，instruction encoder 控制风格 |
| **TextCtrl** | style-structure guidance + glyph-adaptive mutual self-attention，强调 style fidelity |
| **TextSculptor** | 把 replacement 作为四大基本任务之一，用 paired editing data 训练和评测 |

### 2.2 Text Addition / Insertion（文字插入）

**目标**：在原图中新增文字，模型需要决定位置、尺度、排版、风格和透视。

| 方法 | 主要特点 |
|------|----------|
| **DiffSTE** | 支持插入指定文字，并通过 instruction encoder 控制风格 |
| **TextDiffuser** | 先生成文字布局，再用 diffusion 生成包含文字的图像 |
| **TextDiffuser-2** | 用 LLM 规划关键词和 layout，支持聊天式 layout 修改 |
| **AnyText / AnyText2** | 通过位置、glyph、masked image 等条件实现文字生成和编辑 |
| **TextSculptor** | 将 text addition 纳入标准 benchmark 任务 |

### 2.3 Text Removal / Erasing（文字擦除）

**目标**：去掉图像中的文字并恢复背景。这和普通 inpainting 不同，难点在于文字边缘、阴影、遮挡纹理和局部结构。

| 方法 | 主要特点 |
|------|----------|
| **SRNet** | 显式包含 background inpainting module |
| **TextDiffuser** | 支持 text inpainting / reconstruction 设定 |
| **AnyText** | masked image 条件可用于文字区域重绘 |
| **TextSculptor** | 将 text removal 作为独立基本任务评测 |

### 2.4 Visual Text Rendering（图像文字生成）

**目标**：让 text-to-image 模型把指定文字写对，并自然融入图像或设计场景。

| 方法 | 主要特点 |
|------|----------|
| **GlyphDraw** | glyph + position 条件，重点解决中文等复杂字形结构 |
| **TextDiffuser** | layout transformer + diffusion，配套 MARIO-10M / MARIO-Eval |
| **TextDiffuser-2** | LLM 自动规划 layout，提升布局合理性 |
| **UDiffText** | 轻量 character-level text encoder 替换 CLIP text encoder |
| **Glyph-ByT5** | 定制 ByT5 text encoder，提高设计图文字准确性和长文本渲染能力 |
| **Glyph-ByT5-v2** | 扩展到 10 种语言并提升美学质量 |
| **AnyText / AnyText2** | 面向开放域 multilingual visual text generation |

### 2.5 Multilingual Text Editing（多语言文字编辑）

**目标**：支持中文、英文以外的脚本与语言，包括变音符、RTL、复杂连写、混合脚本等。

| 方法 / Benchmark | 主要特点 |
|------------------|----------|
| **AnyText** | 首批系统支持 multilingual visual text generation and editing 的 diffusion 工作 |
| **AnyText2** | 在 multilingual 基础上加入字体、颜色等属性控制 |
| **Glyph-ByT5-v2** | 支持 10 种语言的 visual text rendering |
| **VDE Bench** | 覆盖中英文复杂视觉文档编辑 |
| **MULTITEXTEDIT** | 12 种语言、5 个视觉域、7 类编辑操作，专门评估跨语言退化 |

### 2.6 Visual Document Editing（视觉文档编辑）

**目标**：编辑海报、PPT、论文截图、试卷、报纸、表单等密集文字文档。相比自然场景文字，文档编辑更强调布局、阅读顺序、局部结构和 OCR parsing。

| 方法 / Benchmark | 主要特点 |
|------------------|----------|
| **TextEditBench** | 强调 reasoning-aware text editing，不只看能否写对，还看语义和物理合理性 |
| **VDE Bench** | 面向视觉文档修改，覆盖中英文 dense document 场景 |
| **MULTITEXTEDIT** | 从跨语言角度评估 text-in-image editing 的脚本保真 |
| **TextSculptor** | 提供标准化 addition / replacement / removal / hybrid editing benchmark |

### 2.7 任务 × 方法 交叉矩阵

| 任务 \ 方法 | GAN / Translation | Decomposition | Stroke / Glyph | Diffusion | LLM / MLLM Planning | Benchmark-first |
|-------------|:-----------------:|:-------------:|:--------------:|:---------:|:-------------------:|:---------------:|
| **Replacement** | STEFANN / SRNet | RewriteNet | MOSTEL / TextCtrl | DiffSTE / AnyText / AnyText2 | - | TextSculptor |
| **Addition** | - | - | AnyText | TextDiffuser / DiffSTE / AnyText | TextDiffuser-2 | TextSculptor |
| **Removal** | SRNet | - | - | TextDiffuser / AnyText | - | TextSculptor |
| **Rendering** | - | - | GlyphDraw / Glyph-ByT5 | TextDiffuser / UDiffText / AnyText | TextDiffuser-2 | MARIO-Eval |
| **Multilingual** | - | - | GlyphDraw / Glyph-ByT5-v2 | AnyText / AnyText2 | - | VDE Bench / MULTITEXTEDIT |
| **Document Editing** | - | - | OCR / layout guided | general image editors + text-aware models | reasoning-aware editing | TextEditBench / VDE Bench |

> **怎么读这张表**：
> - 横向看：同一个任务下有哪些技术路线。
> - 纵向看：同一种方法范式主要覆盖哪些任务。
> - 当前最活跃的区域是 **Diffusion + glyph/OCR/layout conditioning + benchmark-first evaluation**。

## 3. 按方法范式详述（How to edit）

### 3.1 GAN / Translation-based Editing

早期 scene text editing 主要依赖 GAN 或 image-to-image translation，把文字区域作为局部图像翻译问题处理。

* **STEFANN**：
  * 论文：[arXiv 1903.01192](https://arxiv.org/abs/1903.01192)
  * 简介：早期字符级场景文字编辑方法。先从源字符生成目标字符，再保持源字符字体和颜色属性，将目标字符贴回原图。

* **SRNet / Editing Text in the Wild**：
  * 论文：[arXiv 1908.03047](https://arxiv.org/abs/1908.03047)
  * 简介：提出 Style Retention Network，将任务拆成文字转换、背景补全、融合三部分，是 word-level scene text editing 的代表性早期工作。

### 3.2 Decomposition / Stroke / Style Guidance

这类方法显式或隐式地把文字内容、字体风格、背景、笔画结构拆开，核心目标是减少"改字但丢风格"的问题。

* **RewriteNet**：
  * 地址：https://github.com/clovaai/rewritenet ![](https://img.shields.io/github/stars/clovaai/rewritenet.svg)
  * 论文：[arXiv 2107.11041](https://arxiv.org/abs/2107.11041)
  * 简介：通过 scene text recognition 引导模型区分 content 和 style，并使用 self-supervised training 利用真实未标注图像。

* **MOSTEL**：
  * 地址：https://github.com/qqqyd/MOSTEL ![](https://img.shields.io/github/stars/qqqyd/MOSTEL.svg)
  * 论文：[arXiv 2212.01982](https://arxiv.org/abs/2212.01982)
  * 简介：将修改目标下沉到 stroke level，用 stroke guidance map 显式约束编辑区域，同时用半监督混合学习缓解 synthetic-to-real domain gap。

* **TextCtrl**：
  * 论文：[arXiv 2410.10133](https://arxiv.org/abs/2410.10133)
  * 简介：提出 style-structure guidance，将文字风格与 glyph 结构作为先验注入 diffusion-based editing，并引入 ScenePair 作为真实配对评测集。

### 3.3 Diffusion-based Text Editing

Diffusion 让 text-in-image editing 从局部替换走向开放域图像编辑，但也带来新的挑战：文字容易写错，非编辑区域容易漂移。

* **DiffSTE**：
  * 地址：https://github.com/UCSB-NLP-Chang/DiffSTE ![](https://img.shields.io/github/stars/UCSB-NLP-Chang/DiffSTE.svg)
  * 论文：[arXiv 2304.05568](https://arxiv.org/abs/2304.05568)
  * 简介：双编码器设计：character encoder 提升文字可读性，instruction encoder 控制风格，支持文字插入和编辑。

* **TextDiffuser**：
  * 地址：https://aka.ms/textdiffuser
  * 论文：[arXiv 2305.10855](https://arxiv.org/abs/2305.10855)
  * 简介：先生成关键词布局，再让 diffusion 根据 layout 生成文字图像。贡献 MARIO-10M 和 MARIO-Eval，是视觉文字生成的重要基线。

* **AnyText**：
  * 地址：https://github.com/tyxsspa/AnyText ![](https://img.shields.io/github/stars/tyxsspa/AnyText.svg)
  * 论文：[arXiv 2311.03054](https://arxiv.org/abs/2311.03054)
  * 简介：多语言视觉文字生成与编辑模型。使用 glyph、position、masked image、OCR embedding 等条件，让文字更准确地融入背景。

* **UDiffText**：
  * 地址：https://github.com/ZYM-PKU/UDiffText ![](https://img.shields.io/github/stars/ZYM-PKU/UDiffText.svg)
  * 论文：[arXiv 2312.04884](https://arxiv.org/abs/2312.04884)
  * 简介：用 lightweight character-level text encoder 替换原 CLIP encoder，并结合 local attention control，提高任意图像中文字合成质量。

### 3.4 Glyph / OCR / Layout Guided Rendering

这类方法的共同点是承认普通文本编码器不足以精确控制字形，因此引入 glyph、OCR、character encoder 或 layout planner。

* **GlyphDraw**：
  * 项目：https://1073521013.github.io/glyph-draw.github.io/
  * 论文：[arXiv 2303.17870](https://arxiv.org/abs/2303.17870)
  * 简介：为复杂字形结构提供 glyph 和 position 条件，重点解决中文等复杂字符在 text-to-image 模型中的准确渲染。

* **TextDiffuser-2**：
  * 地址：https://aka.ms/textdiffuser-2
  * 论文：[arXiv 2311.16465](https://arxiv.org/abs/2311.16465)
  * 简介：用大语言模型规划文字内容和 layout，再将 layout 编码进 diffusion 模型，支持聊天式布局调整。

* **Glyph-ByT5**：
  * 论文：[arXiv 2403.09622](https://arxiv.org/abs/2403.09622)
  * 简介：定制 character-aware ByT5 text encoder，并与 SDXL 结合，让设计图和长文本渲染的 spelling accuracy 大幅提升。

* **Glyph-ByT5-v2**：
  * 论文：[arXiv 2406.10208](https://arxiv.org/abs/2406.10208)
  * 简介：扩展到 10 种语言，并结合偏好学习提升美学质量，是 multilingual visual text rendering 的强基线。

### 3.5 Attribute and Multilingual Control

当文字已经能写对之后，下一步是可控：字体、颜色、行级属性、多语言脚本、甚至文档排版。

* **AnyText2**：
  * 地址：https://github.com/tyxsspa/AnyText2 ![](https://img.shields.io/github/stars/tyxsspa/AnyText2.svg)
  * 论文：[arXiv 2411.15245](https://arxiv.org/abs/2411.15245)
  * 简介：在 AnyText 基础上增加字体和颜色属性控制，可对每行文字设置定制属性，面向更实用的海报、广告、商品图编辑。

* **MULTITEXTEDIT**：
  * 论文：[arXiv 2605.08163](https://arxiv.org/abs/2605.08163)
  * 简介：不是模型，而是跨语言 benchmark。覆盖 12 种语言、5 个视觉域、7 类编辑操作，并提出 language fidelity scoring，专门揭示不同脚本上的退化。

### 3.6 Benchmark-first Frameworks

最近的趋势是：单个模型结果已经不足以说明问题，领域更需要标准数据、任务划分和评测协议。

* **TextEditBench**：
  * 论文：[arXiv 2512.16270](https://arxiv.org/abs/2512.16270)
  * 简介：强调 reasoning-aware text editing beyond rendering。评估模型是否能在编辑文字时保持语义、物理和上下文合理性。

* **VDE Bench**：
  * 论文：[arXiv 2602.00122](https://arxiv.org/abs/2602.00122)
  * 简介：面向视觉文档编辑，覆盖论文、海报、幻灯片、试卷、报纸等 dense text document，并使用 OCR parsing 做细粒度评估。

* **TextSculptor**：
  * 地址：https://github.com/linyiheng123/TextSculptor ![](https://img.shields.io/github/stars/linyiheng123/TextSculptor.svg)
  * 论文：[arXiv 2605.21090](https://arxiv.org/abs/2605.21090)
  * 简介：系统化的数据构造和评测框架。构造 TextSculpt-Data（3.2M 样本），并发布 TextSculpt-Bench，覆盖 addition / replacement / removal / hybrid editing 四类任务。

## 4. 数据集与 Benchmark

### 4.1 数据集

| 数据集 | 年份 | 来源 | 规模 / 标注 | 用途 |
|--------|------|------|-------------|------|
| **MARIO-10M** | 2023 | TextDiffuser | 10M image-text pairs，含 OCR recognition / detection / character-level segmentation | text rendering training |
| **AnyWord-3M** | 2023 | AnyText | 3M multilingual image-text pairs，含 OCR 标注 | multilingual generation / editing |
| **Tamper-Syn2k / Tamper-Scene** | 2022 | MOSTEL | synthetic + real scene text editing pairs | stroke-level editing evaluation |
| **ScenePair** | 2024 | TextCtrl | real-world paired scene text editing dataset | real-world STE comparison |
| **TextSculpt-Data** | 2026 | TextSculptor | 3.2M samples，1.2M OCR-verified T2I + 2M paired editing | scene text editing training |

### 4.2 Benchmark

| Benchmark | 年份 | 关注点 | 语言 | 链接 |
|-----------|------|--------|------|------|
| **MARIO-Eval** | 2023 | visual text rendering quality | English | [TextDiffuser](https://arxiv.org/abs/2305.10855) |
| **AnyText-benchmark** | 2023 | multilingual text generation / editing | Multilingual | [AnyText](https://arxiv.org/abs/2311.03054) |
| **ScenePair** | 2024 | real-world paired scene text editing | English | [TextCtrl](https://arxiv.org/abs/2410.10133) |
| **TextEditBench** | 2025 | reasoning-aware text editing | English | [paper](https://arxiv.org/abs/2512.16270) |
| **VDE Bench** | 2026 | visual document editing / OCR parsing | English / Chinese | [paper](https://arxiv.org/abs/2602.00122) |
| **MULTITEXTEDIT** | 2026 | cross-lingual degradation / script fidelity | 12 languages | [paper](https://arxiv.org/abs/2605.08163) |
| **TextSculpt-Bench** | 2026 | addition / replacement / removal / hybrid editing | English | [TextSculptor](https://github.com/linyiheng123/TextSculptor) |

### 4.3 常用评测指标

| 类别 | 指标 | 含义 |
|------|------|------|
| 文字正确性 | **OCR exact match / OCR accuracy** | 编辑后文字是否能被 OCR 正确识别 |
| 文字正确性 | **CER / WER** | 字符错误率 / 词错误率 |
| 脚本保真 | **Language / Script Fidelity** | 是否保留变音符、RTL 顺序、连写形态、混合脚本 |
| 风格一致性 | **Style similarity** | 字体、颜色、stroke、阴影、透视是否与原图一致 |
| 背景保持 | **LPIPS / PSNR / SSIM on non-edit region** | 非编辑区域是否漂移 |
| 语义一致性 | **Semantic Expectation / VLM judgment** | 编辑结果是否符合上下文和物理常识 |
| 文档结构 | **OCR parsing / reading order** | dense document 中布局和阅读顺序是否保持 |
| 人类偏好 | **Human preference** | 综合文字正确、视觉自然、编辑保真 |

## 5. 开源工具与项目

| 项目 | 说明 |
|------|------|
| **AnyText** | 多语言文字生成与编辑 baseline：[tyxsspa/AnyText](https://github.com/tyxsspa/AnyText) |
| **AnyText2** | 字体/颜色属性可控的文字生成与编辑：[tyxsspa/AnyText2](https://github.com/tyxsspa/AnyText2) |
| **DiffSTE** | diffusion-based scene text editing：[UCSB-NLP-Chang/DiffSTE](https://github.com/UCSB-NLP-Chang/DiffSTE) |
| **MOSTEL** | stroke-level scene text editing：[qqqyd/MOSTEL](https://github.com/qqqyd/MOSTEL) |
| **RewriteNet** | content-style decomposition baseline：[clovaai/rewritenet](https://github.com/clovaai/rewritenet) |
| **TextDiffuser** | layout-guided text rendering：[aka.ms/textdiffuser](https://aka.ms/textdiffuser) |
| **TextSculptor** | data construction + benchmark framework：[linyiheng123/TextSculptor](https://github.com/linyiheng123/TextSculptor) |

## 6. 相关方向

* **Text-to-Image Generation with Accurate Typography**：关注模型能否在从零生成图像时写对字。
* **Scene Text Removal / Text Erasing**：更偏向 inpainting，但和 text editing 强相关。
* **OCR-guided Image Editing**：用 OCR detection / recognition / parsing 引导图像编辑。
* **Visual Document Understanding and Editing**：从文档理解、版面分析进入文档图像编辑。
* **Multilingual Visual Generation**：关注非英文脚本、多语言、跨语言退化。
* **Benchmark and Evaluation**：从 OCR accuracy 走向 OCR + VLM + human preference 的组合评测。

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=leeguandong/Awesome-Text-Editing&type=Date)](https://star-history.com/#leeguandong/Awesome-Text-Editing&Date)

## License

Apache License 2.0
