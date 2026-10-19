<h1 align="center">
Awesome-Text-Editing
</h1>
<p align="center">
<b>An Awesome Collection for Text-in-Image Generation and Editing / 收集和梳理图像中文字生成、替换、擦除与无痕编辑方法</b>
</p>
<p align="center">
  <a href="https://github.com/leeguandong/Awesome-Text-Editing"> <img src="https://img.shields.io/github/stars/leeguandong/Awesome-Text-Editing.svg?style=popout-square" alt="GitHub stars"></a>
  <a href="https://github.com/leeguandong/Awesome-Text-Editing/issues"> <img src="https://img.shields.io/github/issues/leeguandong/Awesome-Text-Editing.svg?style=popout-square" alt="GitHub issues"></a>
  <a href="https://github.com/leeguandong/Awesome-Text-Editing/forks"> <img src="https://img.shields.io/github/forks/leeguandong/Awesome-Text-Editing.svg?style=popout-square" alt="GitHub forks"></a>
  <a href="LICENSE"> <img src="https://img.shields.io/badge/License-Apache--2.0-blue.svg" alt="Apache-2.0 license"></a>
</p>

> A curated list of text-in-image generation and editing methods, covering scene text replacement, text insertion, text removal, multilingual visual text rendering, style-preserving editing, and visual document editing.

> **Last updated / 文献截止 / 链接核验：2026-10-19** · 年份按首次公开时间记录；已确认的会议/期刊另行标注。

本项目旨在收集和梳理 **图像中文字编辑（Text-in-Image Editing / Scene Text Editing）** 相关工作，包括自然场景文字替换、广告海报文字生成、文档图像文字编辑、多语言文字渲染、文字擦除与重绘、OCR / glyph / layout 约束生成，以及对应的数据集与评测基准。

如果本项目能给您带来一点点帮助，麻烦点个⭐️吧～

同时也欢迎大家贡献本项目未收录的论文、开源实现、数据集和 benchmark。提供新的仓库信息请发起 PR，并按照 [CONTRIBUTING.md](CONTRIBUTING.md) 提供论文链接、官方资源、任务类型、语言覆盖、数据集/评测信息等。

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
- [最近更新](#最近更新)
- [1. 代表工作汇总](#1-代表工作汇总)
  - [1.1 论文与项目全景表](#11-论文与项目全景表)
  - [1.2 演化时间线](#12-演化时间线)
- [2. 按任务分类（What to edit）](#2-按任务分类what-to-edit)
  - [2.1 Scene Text Replacement（场景文字替换）](#21-scene-text-replacement场景文字替换)
  - [2.2 Text Addition / Insertion（文字插入）](#22-text-addition--insertion文字插入)
  - [2.3 Text Removal / Erasing（文字擦除）](#23-text-removal--erasing文字擦除)
  - [2.4 Visual Text Rendering（图像文字生成）](#24-visual-text-rendering图像文字生成)
  - [2.5 Multilingual Visual Text（多语言文字生成与编辑）](#25-multilingual-visual-text多语言文字生成与编辑)
  - [2.6 Visual Document Editing（视觉文档与设计图编辑）](#26-visual-document-editing视觉文档与设计图编辑)
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
- [Contributing](#contributing)
- [License](#license)

## 最近更新

- **2026-10-19**：补充 2026-08-08 之后的 PixText、TextVerifier、IDSpect、GlyphAnchor、STEPS、LoGAN、PosterText、InfoVis、UltraText Bench、VTR-Bench 等工作，新增像素级局部修复、IDS 字形结构验证、密集文字与视频文字评测条目。
- **2026-08-08**：补充 JoyType、RepText、EasyText、ControlText、DanceText、TextSculptor 等最新工作，更新文献截止日期和链接核验。
- **2026-07-19**：补充 TextWand、Self-Prompting STE、TextFlow、WeEdit、MiLDEdit、GlyphPrinter、TextPecker 等 2026 年工作，并回补 GlyphMastero、RS-STE、TextMastero、ViTEraser 等代表性方法。
- **2026-07-19**：增加首发年份与 venue/status 口径、训练集/评测集标记，补齐官方代码和项目页；失效资源会显式标为 unavailable，不再保留误导链接。
- **2026-07-19**：新增贡献规范和 Apache-2.0 许可证，移除当前不可用的 Star History 图。

## 1. 代表工作汇总

### 1.1 论文与项目全景表

| 工作 | 首发 | 类型 / 任务 | 核心机制 | 语言 / 脚本 | 数据 / Benchmark | 论文 / Venue | 官方资源 |
|------|------|-------------|----------|-------------|------------------|--------------|----------|
| **EnsNet** | 2018 | method · removal | FCN + local-sensitive GAN | language-agnostic | train/eval: synthetic / ICDAR | [AAAI 2019](https://arxiv.org/abs/1812.00723) | [code/data](https://github.com/HCIILAB/Scene-Text-Removal) |
| **STEFANN** | 2019 | method · replacement | font-adaptive character generation | English | eval: COCO-Text / ICDAR | [CVPR 2020](https://arxiv.org/abs/1903.01192) | [code](https://github.com/prasunroy/stefann) |
| **MTRNet** | 2019 | method · removal | mask-based cGAN | multilingual | eval: ICDAR / MLT / CTW1500 | [ICDAR 2019](https://arxiv.org/abs/1903.04092) | — |
| **SRNet / Editing Text in the Wild** | 2019 | method · replacement | style retention + inpainting | English | train/eval: synthetic / ICDAR | [ACM MM 2019](https://arxiv.org/abs/1908.03047) | [code](https://github.com/youdao-ai/SRNet) |
| **MTRNet++** | 2019 | method · removal | mask refine + coarse/fine inpainting | language-agnostic | eval: Oxford / SCUT | [CVIU 2020](https://arxiv.org/abs/1912.07183) | [code](https://github.com/neouyghur/One-stage-Mask-based-Scene-Text-Eraser) |
| **SwapText** | 2020 | method · replacement / style transfer | source/target text swapping + reconstruction | English | eval: synthetic / real scene text | [CVPR 2020](https://arxiv.org/abs/2003.08152) | — |
| **EraseNet** | 2020 | method · removal | coarse-to-fine erasing + segmentation guidance | language-agnostic | both: SCUT-EnsText | [TIP 2020](https://doi.org/10.1109/TIP.2020.3018859) | [code/data](https://github.com/lcy0604/EraseNet) |
| **Stroke-Based Scene Text Erasing** | 2021 | method · removal | stroke mask prediction + inpainting | language-agnostic | eval: SCUT-Syn / ICDAR / SCUT-EnsText | [TIP 2021](https://arxiv.org/abs/2104.11493) | [code](https://github.com/tzm-tora/Stroke-Based-Scene-Text-Erasing) |
| **PERT** | 2021 | method · removal | progressive region-based erasing | language-agnostic | eval: SCUT-EnsText | [TIP 2023](https://arxiv.org/abs/2106.13029) | [code](https://github.com/wangyuxin87/PERT) |
| **TextStyleBrush** | 2021 | method · style transfer | self-supervised style/content disentanglement | English / handwriting | eval: Imgur5K | [SIGGRAPH 2021](https://arxiv.org/abs/2106.08385) | — |
| **RewriteNet** | 2021 | method · replacement | content/style decomposition | English | train: self-supervised real images | [CVPRW 2022](https://arxiv.org/abs/2107.11041) | unavailable¹ |
| **PSSTRNet** | 2022 | method · removal | progressive segmentation-guided erasing | language-agnostic | eval: SCUT-EnsText / SCUT-Syn | [ICME 2022](https://arxiv.org/abs/2306.07842) | [code](https://github.com/GuangtaoLyu/PSSTRNet) |
| **MOSTEL** | 2022 | method · replacement | stroke guidance + semi-supervised learning | English | both: Tamper-Syn2k / Tamper-Scene | [AAAI 2023](https://arxiv.org/abs/2212.01982) | [code](https://github.com/qqqyd/MOSTEL) |
| **GlyphDraw** | 2023 | method · rendering | glyph + position-conditioned diffusion | Chinese / English | train: custom glyph data | [arXiv](https://arxiv.org/abs/2303.17870) | [project](https://1073521013.github.io/glyph-draw.github.io/) |
| **DiffSTE** | 2023 | method · insertion / replacement | diffusion + dual encoders | English | eval: five datasets | [arXiv](https://arxiv.org/abs/2304.05568) | [code](https://github.com/UCSB-NLP-Chang/DiffSTE) |
| **DiffUTE** | 2023 | method · universal text editing | glyph-conditioned diffusion + background preservation | multilingual | train/eval: synthetic and public STE sets | [NeurIPS 2023](https://arxiv.org/abs/2305.10825) | [code](https://github.com/chenhaoxing/DiffUTE) |
| **TextDiffuser** | 2023 | method · rendering / inpainting | layout planner + diffusion | English | train: MARIO-10M; eval: MARIO-Eval | [NeurIPS 2023](https://arxiv.org/abs/2305.10855) | [code](https://github.com/microsoft/unilm/tree/master/textdiffuser) |
| **GlyphControl** | 2023 | method · rendering | glyph-conditioned ControlNet | English | both: LAION-Glyph | [NeurIPS 2023](https://arxiv.org/abs/2305.18259) | [code](https://github.com/AIGText/GlyphControl-release) |
| **FETNet** | 2023 | method · removal | feature erasing + background transfer | language-agnostic | both: Flickr-ST | [Pattern Recognition](https://arxiv.org/abs/2306.09593) | [code](https://github.com/GuangtaoLyu/FETNet) |
| **ViTEraser** | 2023 | method · removal | ViT encoder-decoder + SegMIM | language-agnostic | train: OCR corpora; eval: SCUT-EnsText | [AAAI 2024](https://arxiv.org/abs/2306.12106) | [code](https://github.com/shannanyinxiang/ViTEraser) |
| **FASTER** | 2023 | method · replacement / rendering | target-mask fusion + cascaded attention | English | eval: real-world STE data | [WACV 2025](https://arxiv.org/abs/2308.02905) | — |
| **DBEST** | 2023 | method · replacement | one-shot style adaptation + recognition guidance | English | eval: COCO-Text / ICDAR | [WACV 2024](https://arxiv.org/abs/2311.00734) | — |
| **AnyText** | 2023 | method · generation / editing | glyph + position + OCR embedding | multilingual | train: AnyWord-3M; eval: AnyText-benchmark | [ICLR 2024](https://arxiv.org/abs/2311.03054) | [code](https://github.com/tyxsspa/AnyText) |
| **TextDiffuser-2** | 2023 | method · rendering / layout | LLM layout planner + diffusion | English | eval: MARIO-Eval | [ECCV 2024](https://arxiv.org/abs/2311.16465) | [code](https://github.com/microsoft/unilm/tree/master/textdiffuser-2) |
| **UDiffText** | 2023 | method · synthesis / editing | character-aware diffusion | English | eval: public rendering sets | [ECCV 2024](https://arxiv.org/abs/2312.04884) | [code](https://github.com/ZYM-PKU/UDiffText) |
| **Brush Your Text** | 2023 | method · scene text synthesis | diffusion + masked text region conditioning | multilingual | eval: public scene-text sets | [AAAI 2024](https://arxiv.org/abs/2312.12232) | [code](https://github.com/ecnuljzhang/brush-your-text) |
| **Glyph-ByT5** | 2024 | method · rendering | customized ByT5 encoder + SDXL | English | eval: design image benchmark | [ECCV 2024](https://arxiv.org/abs/2403.09622) | [code](https://github.com/AIGText/Glyph-ByT5) |
| **LTOS** | 2024 | method · text-object synthesis | adaptive cross-attention fusion | English | both: LTOS dataset | [arXiv](https://arxiv.org/abs/2404.13579) | — |
| **Glyph-ByT5-v2** | 2024 | method · rendering | multilingual ByT5 + preference learning | 10 languages | train: >1M glyph-text + 10M design pairs; eval: 1K prompts | [arXiv](https://arxiv.org/abs/2406.10208) | [code](https://github.com/AIGText/Glyph-ByT5) / [project](https://glyph-byt5-v2.github.io/) |
| **GlyphDraw2** | 2024 | method · poster rendering | LLM + diffusion + triple-cross attention | Chinese / English | train: high-resolution poster/font data | [AAAI 2025](https://arxiv.org/abs/2407.02252) | [code](https://github.com/OPPO-Mente-Lab/GlyphDraw2) |
| **SceneVTG** | 2024 | method · scene text generation | MLLM region/content planning + diffusion | multilingual | train/eval: generated scene-text data | [ECCV 2024](https://arxiv.org/abs/2407.14138) | [code/data](https://github.com/AlibabaResearch/AdvancedLiterateMachinery) |
| **TextHarmony** | 2024 | model · comprehension / generation | Slide-LoRA experts | multilingual | train: DetailedTextCaps-100K | [NeurIPS 2024](https://arxiv.org/abs/2407.16364) | [code](https://github.com/bytedance/TextHarmony) |
| **TextMastero** | 2024 | method · replacement | glyph conditioning + latent style guidance | multilingual / CJK | eval: public STE datasets | [arXiv](https://arxiv.org/abs/2408.10623) | — |
| **TMIM** | 2024 | method · removal | text-aware masked image modeling | language-agnostic | train: detection labels; eval: SCUT-EnsText | [ECCV 2024](https://arxiv.org/abs/2409.13431) | [code](https://github.com/wzx99/TMIM) |
| **JoyType** | 2024 | method · multilingual rendering | font style preservation + canny edge guidance | multilingual | train: JoyType-1M | [arXiv](https://arxiv.org/abs/2409.17524) | [code](https://github.com/jdh-algo/JoyType) |
| **TextCtrl** | 2024 | method · replacement | style-structure guidance + mutual self-attention | English | both: ScenePair | [NeurIPS 2024](https://arxiv.org/abs/2410.10133) | — |
| **DiffSTR** | 2024 | method · removal | ControlNet diffusion + mask refinement | language-agnostic | eval: SCUT-EnsText / SCUT-Syn | [arXiv](https://arxiv.org/abs/2410.21721) | — |
| **AnyText2** | 2024 | method · generation / editing | line-level font and color control | multilingual | eval: multilingual benchmarks | [arXiv](https://arxiv.org/abs/2411.15245) | [code](https://github.com/tyxsspa/AnyText2) |
| **CharGen** | 2024 | method · generation / editing | character-level multimodal encoder + perceptual loss | Chinese / English | eval: AnyText-benchmark / MARIO-Eval | [arXiv](https://arxiv.org/abs/2412.17225) | — |
| **SceneVTG++** | 2025 | method · scene text generation | MLLM planner + controllable local diffusion | multilingual | train/eval: scene-text data | [arXiv](https://arxiv.org/abs/2501.02962) | — |
| **RS-STE** | 2025 | method · replacement | recognition-synergistic parallel decoder | English | train: RS-STE-Dataset; eval: public STE sets | [CVPR 2025](https://arxiv.org/abs/2503.08387) | [code](https://github.com/ZhengyaoFang/RS-STE) |
| **TextInVision** | 2025 | benchmark · visual text generation | text/prompt complexity + VAE diagnosis | multilingual | eval: TextInVision | [arXiv](https://arxiv.org/abs/2503.13730) | — |
| **TextCrafter** | 2025 | method · complex rendering | constrained RL + quotation-guided attention | English | eval: CVTG-2K (2K prompts) / CVTG-Hard (400) | [arXiv](https://arxiv.org/abs/2503.23461) | [code](https://github.com/NJU-PCALab/TextCrafter) |
| **FLUX-Text** | 2025 | method · replacement | FLUX-Fill + lightweight glyph/text embedding | multilingual / Chinese | eval: public STE datasets | [arXiv](https://arxiv.org/abs/2505.03329) | [code](https://github.com/AMAP-ML/FluxText) |
| **GlyphMastero** | 2025 | method · replacement | hierarchical stroke/character glyph encoder | multilingual / Chinese | eval: public STE datasets | [CVPR 2025](https://arxiv.org/abs/2505.04915) | — |
| **FontAdapter** | 2025 | method · font-conditioned generation / editing | reference-glyph curriculum adaptation | cross-lingual | train: synthetic font curricula | [arXiv](https://arxiv.org/abs/2506.05843) | [project](https://fontadapter.github.io/) |
| **Qwen-Image** | 2025 | foundation model · generation / editing | MMDiT + Qwen2.5-VL dual encoding | multilingual / Chinese | eval: multiple generation/editing benchmarks | [technical report](https://arxiv.org/abs/2508.02324) | [code](https://github.com/QwenLM/Qwen-Image) |
| **OTR** | 2025 | dataset · overlay text removal | controllable overlay synthesis + clean ground truth | language-agnostic | both: OTR dataset | [ACM MM 2025](https://arxiv.org/abs/2510.02787) | [data](https://huggingface.co/datasets/cyberagent/OTR) |
| **SceneTextStylizer** | 2025 | method · style transfer | training-free inversion + region control | language-agnostic | eval: style-transfer set | [arXiv](https://arxiv.org/abs/2510.10910) | — |
| **OmniText** | 2025 | method · general text-image manipulation | training-free attention control + latent losses | Latin / alphanumeric | eval: OmniText-Bench | [ICLR 2026](https://arxiv.org/abs/2510.24093) | [code/bench](https://github.com/KAIST-VICLab/OmniText) |
| **STELLAR** | 2025 | method · low-resource replacement | language-adaptive glyph encoder + synthetic-to-real training | multilingual / low-resource | both: STIPLAR; eval: TAS | [AAAI 2026 Workshop](https://arxiv.org/abs/2511.09977) | — |
| **TripleFDS** | 2025 | method · replacement / attribute transfer | content/style/background disentanglement | English / alphanumeric | train: SCB Synthesis (1M images / 125K groups) | [AAAI 2026](https://arxiv.org/abs/2511.13399) | [code](https://github.com/yusenbao01/TripleFDS) |
| **GLASTE** | 2025 | method · replacement | global-local modeling + size-independent style vector | English | eval: public STE datasets | [ICME 2025](https://arxiv.org/abs/2512.03574) | — |
| **ControlText** | 2025 | method · font-controllable rendering | font control without annotations + contrastive learning | multilingual | train: raw images without font labels | [arXiv](https://arxiv.org/abs/2502.10999) | [code](https://github.com/bowen-upenn/controltext) |
| **RepText** | 2025 | method · multilingual rendering | replicating-based font rendering | multilingual | train: user-specified fonts | [arXiv](https://arxiv.org/abs/2504.19724) | [code](https://github.com/Shakker-Labs/RepText) |
| **DanceText** | 2025 | framework · text transformation | training-free layered geometric transformation | multilingual | eval: text transformation benchmarks | [arXiv](https://arxiv.org/abs/2504.14108) | — |
| **EasyText** | 2025 | method · multilingual rendering | DiT + character positioning encoding | 10+ languages | train: 1M synthetic + 20K high-quality | [arXiv](https://arxiv.org/abs/2505.24417) | [code](https://github.com/songyiren725/easytext) |
| **TextEditBench** | 2025 | benchmark · reasoning-aware editing | semantic expectation evaluation | multilingual / mixed-script | eval: 1,196 instances / 12 subtasks | [NeurIPS 2025](https://arxiv.org/abs/2512.16270) | — |
| **UTDesign** | 2025 | framework · graphic design editing / generation | RGBA glyph DiT + MLLM layout planner | Chinese / English | train: SynthGlyph / DesignText; eval: UTDesign-Bench | [SIGGRAPH Asia 2025](https://arxiv.org/abs/2512.20479) | [code/data](https://github.com/ZYM-PKU/UTDesign) |
| **MiLDEdit / MiLDEAgent** | 2026 | framework · multi-layer document editing | RL-trained layer reasoner + image editor | multilingual design docs | eval: MiLDEBench (>20K documents) | [arXiv](https://arxiv.org/abs/2601.04589) | — |
| **UM-Text** | 2026 | model · instruction-based text editing | VLM planner + UM-Encoder + regional loss | Chinese / English | train: UM-DATA-200K; eval: UMT-Benchmark | [AAAI 2026](https://arxiv.org/abs/2601.08321) | — |
| **VDE Bench** | 2026 | benchmark · visual document editing | OCR parsing evaluation | Chinese / English | eval: 942 samples | [arXiv](https://arxiv.org/abs/2602.00122) | [code/data](https://github.com/zion-zion-zion/VDE-Bench) |
| **TextPecker** | 2026 | method · rendering optimization | structural-anomaly reward + RL | Chinese / English | train: TextPecker-1.5M | [CVPR 2026](https://arxiv.org/abs/2602.20903) | [code/data](https://github.com/CIawevy/TextPecker) |
| **InnoAds-Composer** | 2026 | method · e-commerce poster generation | subject + glyph + style tri-conditioning | Chinese | both: e-commerce poster data / benchmark | [CVPR 2026](https://arxiv.org/abs/2603.05898) | — |
| **WeEdit** | 2026 | framework · text-centric image editing | glyph-guided SFT + multi-objective RL | 15 languages | train: 330K pairs; eval: bilingual / multilingual 2K each | [arXiv](https://arxiv.org/abs/2603.11593) | [code/bench](https://github.com/HuiZhang0812/WeEdit) |
| **GlyphPrinter** | 2026 | method · rendering optimization | region-grouped DPO + regional guidance | multilingual | train: GlyphCorrector | [CVPR 2026 Highlight](https://arxiv.org/abs/2603.15616) | [code/data](https://github.com/FudanCVL/GlyphPrinter) / [project](https://henghuiding.com/GlyphPrinter/) |
| **TextFlow** | 2026 | method · replacement | training-free flow steering + attention boost | multilingual | eval: public STE datasets | [CVPR 2026](https://arxiv.org/abs/2603.24571) | [code](https://github.com/lyb18758/TextFlow) |
| **Edit Fidelity Field** | 2026 | method · preservation | OCR-aware continuous fidelity field | language-agnostic | eval: 50 scenes / spillover protocol | [arXiv](https://arxiv.org/abs/2604.17500) | — |
| **POCA** | 2026 | method · rendering alignment | Pareto-optimal multi-reward curriculum | multilingual | train: multi-reward prompt curriculum | [CVPR 2026](https://arxiv.org/abs/2604.24171) | — |
| **MULTITEXTEDIT** | 2026 | benchmark · cross-lingual editing | language/script fidelity scoring | 12 languages | eval: 5 domains / 7 edit types | [arXiv](https://arxiv.org/abs/2605.08163) | — |
| **Qwen-Image-2.0** | 2026 | foundation model · generation / editing | Qwen3-VL + MMDiT joint modeling | multilingual | eval: slides / posters / infographics / comics | [technical report](https://arxiv.org/abs/2605.10730) | — |
| **StyleTextGen** | 2026 | method · style-conditioned generation | dual-branch style encoder + mask guidance | multilingual | eval: StyleText-CE | [CVPR 2026](https://arxiv.org/abs/2605.14708) | — |
| **Self-Prompting STE** | 2026 | method · replacement | self-derived glyph/style prompts + MM-DiT ICL | multilingual / open vocabulary | train: self-supervised + paired refinement | [ICML 2026](https://arxiv.org/abs/2605.15523) | [project](https://hongxiii.github.io/mstedit/) |
| **TextSculptor** | 2026 | framework · generation / editing / benchmark | automated data construction + tailored evaluation | English | train: TextSculpt-Data (3.2M); eval: TextSculpt-Bench | [arXiv](https://arxiv.org/abs/2605.21090) | [code/data](https://github.com/linyiheng123/TextSculptor) |
| **TextWand** | 2026 | method · unified generation / replacement / removal | ORPE + region-adaptive suppression | Chinese / English / symbols | train: TextWand-72K; eval: TextWand-Bench (1.5K) | [arXiv](https://arxiv.org/abs/2606.05730) | — |
| **Mind the Gap** | 2026 | analysis · edit-constraint discovery | 19-type causal dependency diagnostic | multilingual scenes | eval: 461 diagnostic cases | [arXiv](https://arxiv.org/abs/2606.15982) | — |
| **Boogu-Image-0.1** | 2026 | foundation model · generation / editing | unified model family + agentic inference scaling | Chinese / English | train: 208.62M unique images | [technical report](https://arxiv.org/abs/2607.13125) | [code](https://github.com/Boogu-Project/Boogu-Image) |
| **PosterText** | 2026 | framework · poster generation / editing | text-patch atomic operations + curriculum / RL / spatial self-distillation | — | train/eval: patch-level e-commerce poster data / benchmark | [arXiv](https://arxiv.org/abs/2608.16289) | — |
| **GlyphAnchor** | 2026 | method · rendering / editing | position-anchored glyph patch priors + text-aware post-training | — | eval: InfoTextBench | [arXiv](https://arxiv.org/abs/2609.02349) | — |
| **LoGAN** | 2026 | framework · font localization | VLM agent + glyph diffusion + spacing/kerning transfer | 27+ languages | eval: multilingual font / logo datasets | [ECCV 2026](https://arxiv.org/abs/2609.07029) | — |
| **STEPS** | 2026 | method · replacement | contrastive style encoder + glyph and character conditions | — | eval: scene text editing benchmarks | [PAKDD 2026](https://arxiv.org/abs/2609.38636) | — |
| **IDSpect** | 2026 | method · rendering optimization | IDS component/spatial reward for Chinese glyph structure | Chinese | train/eval: IDS recognizer + LongText / GenTextEval | [arXiv](https://arxiv.org/abs/2609.37569) | — |
| **VTR-Bench** | 2026 | benchmark · video text rendering | carrier-aware transcription + prompt-specific visual evaluation | — | eval: 300 prompts / 5 scenarios | [arXiv](https://arxiv.org/abs/2610.01499) | [code](https://github.com/hardenyu21/VTR-Bench) |
| **UltraText Bench** | 2026 | benchmark · dense visual text rendering | bilingual multi-region fidelity / clarity / spatial / scene scoring | Chinese / English | eval: 432 prompts / 24 scene categories | [arXiv](https://arxiv.org/abs/2610.09823) | [code](https://github.com/LINs-lab/UltraText_Bench) |
| **InfoVis** | 2026 | model · slide generation / editing | slide-native continual pretraining + SFT | — | train: 13M + 1.9M records; eval: VisSlideBench | [arXiv](https://arxiv.org/abs/2610.16784) | [code](https://github.com/VectorSpaceLab/InfoVis) |
| **PixText** | 2026 | method · local text refinement | pixel-space grouped generation + four-step MeanFlow | — | eval: Text Refinement Bench | [arXiv](https://arxiv.org/abs/2610.18284) | — |
| **TextVerifier** | 2026 | method · Chinese glyph verification | IDS-conditioned per-character verifier + Flow-GRPO reward | Chinese | train/eval: 12.7M crop-IDS pairs; TEXTRENDERBENCH-ZH | [arXiv](https://arxiv.org/abs/2610.19551) | — |

> **口径说明**：`首发` 指首次公开年份，`论文 / Venue` 仅在官方页面可确认时标注录用 venue；`train` / `eval` / `both` 区分训练资源和评测资源；`—` 表示截至核验日未找到官方公开资源。STR 在本文中专指 **Scene Text Removal**。¹ RewriteNet 论文中的官方仓库已不可访问，因此不再提供失效链接。

### 1.2 演化时间线

```
2018  EnsNet                                      (end-to-end scene text removal)
2019  MTRNet / SRNet / MTRNet++                   (mask-based erasing + word-level replacement)
2020  STEFANN / SwapText / EraseNet               (字符/词级风格保持与端到端擦除)
2021  Stroke Erasing / PERT / TextStyleBrush      (显式笔画、渐进区域擦除与 one-shot 风格迁移)
2022  PSSTRNet / MOSTEL                           (segmentation / stroke guidance + 真实域适配)
2023  GlyphDraw / DiffUTE / DiffSTE               (glyph 条件与 diffusion 进入通用文字编辑)
2023  TextDiffuser / AnyText / UDiffText           (大规模 OCR 数据、多语言与字符级编码)
2024  TextDiffuser-2 / Glyph-ByT5 / TextHarmony   (LLM layout planning + 定制 text encoder)
2024  TextMastero / TextCtrl / AnyText2 / JoyType  (多语言字形、风格结构与属性控制、字体保持)
2024  ViTEraser / TMIM / DiffSTR                   (ViT / masked modeling / diffusion removal)
2025  RS-STE / GlyphMastero / FLUX-Text            (识别协同与复杂字形的高保真替换)
2025  TextCrafter / FontAdapter / Qwen-Image       (复杂多文字、字体适配与强基座模型)
2025  OmniText / TripleFDS / UTDesign              (通用操作、属性解耦与设计图层编辑)
2025  ControlText / RepText / DanceText / EasyText (无标注字体控制、复制式渲染、训练无关变换、DiT 多语言)
2026  UM-Text / MiLDEdit / WeEdit                  (自然语言、多层文档与多语言系统化训练)
2026  TextPecker / GlyphPrinter / POCA             (结构感知 reward / preference optimization)
2026  TextFlow / EFF / Self-Prompting STE          (训练无关编辑、spillover 控制与 in-context editing)
2026  TextSculptor / TextWand                      (大规模 paired data + 统一生成/替换/擦除 benchmark)
2026  Qwen-Image-2.0 / Boogu-Image-0.1             (长文本、双语渲染与统一生成编辑基座)
2026  PosterText / GlyphAnchor / LoGAN                (patch 编辑、位置锚定 glyph 与多语言字体本地化)
2026  STEPS / IDSpect / TextVerifier                  (风格保持与字形部件级验证、结构奖励)
2026  VTR-Bench / UltraText Bench / InfoVis / PixText (视频/密集文字评测、幻灯片编辑与局部像素修复)
```

## 2. 按任务分类（What to edit）

本节从 **"到底要编辑什么"** 的角度切分。一个方法可能同时覆盖多个任务，例如 AnyText 同时覆盖 text generation 和 text editing，TextSculptor 同时覆盖 addition / replacement / removal / hybrid。

### 2.1 Scene Text Replacement（场景文字替换）

**目标**：把图像中已有文字替换成目标文字，同时保持背景、字体、颜色、透视、阴影和局部纹理。

| 方法 | 主要特点 |
|------|----------|
| **STEFANN** | 字符级替换，使用 font adaptive network 保持字体结构，ColorNet 保持颜色 |
| **SRNet / SwapText** | 早期 word-level 替换与文字交换框架，显式处理文字转换、背景补全和风格融合 |
| **RewriteNet** | 通过识别任务诱导 content / style decomposition，并用 self-supervised real-image training 缓解域差 |
| **TextStyleBrush** | one-shot 学习单个文字样例的外观风格，再迁移到新内容 |
| **MOSTEL** | 使用 stroke guidance map 显式告诉模型哪些笔画需要修改 |
| **RS-STE** | 将文字识别与图像编辑放进统一并行 decoder，并用循环自监督适配真实图像 |
| **DiffSTE / DiffUTE / DBEST** | 分别从双编码器、通用 glyph 条件和 one-shot style adaptation 推进 diffusion replacement |
| **TextMastero / TextCtrl** | 用 glyph、latent style 与 style-structure guidance 提升复杂脚本和风格保真 |
| **FLUX-Text / GlyphMastero** | 面向中英文复杂字形，加入轻量 glyph embedding 或层次化笔画/字符编码 |
| **OmniText / TripleFDS** | 覆盖训练无关通用操作，以及 content/style/background 三属性解耦和交换 |
| **STELLAR / GLASTE** | 分别面向低资源多语言的 synthetic-to-real 适配，以及大幅长度变化下的 global-local consistency |
| **TextFlow / Edit Fidelity Field** | 训练无关 flow steering 完成替换，连续 fidelity field 抑制对邻近文字的误改 |
| **Self-Prompting STE** | 从原图直接构造 glyph/style prompt，以 MM-DiT in-context learning 做开放词表编辑 |
| **STEPS** | 用 contrastive style encoder 分离文字风格与内容，提升字体、颜色、方向和背景保持 |
| **GlyphAnchor / PixText** | 分别用位置锚定 glyph prior 和 pixel-space grouped generation 做高保真替换与局部修复 |
| **UM-Text / WeEdit** | 用 VLM 规划和 glyph-guided SFT/RL 支持自然语言、翻译、组合与 reasoning 编辑 |
| **TextSculptor / TextWand** | 用大规模 paired data 和统一模型覆盖 replacement，并提供专用 benchmark |

### 2.2 Text Addition / Insertion（文字插入）

**目标**：在原图中新增文字，模型需要决定位置、尺度、排版、风格和透视。

| 方法 | 主要特点 |
|------|----------|
| **DiffSTE** | 支持插入指定文字，并通过 instruction encoder 控制风格 |
| **TextDiffuser** | 先生成文字布局，再用 diffusion 生成包含文字的图像 |
| **TextDiffuser-2** | 用 LLM 规划关键词和 layout，支持聊天式 layout 修改 |
| **AnyText / AnyText2** | 通过位置、glyph、masked image 等条件实现文字生成和编辑 |
| **OmniText / TextWand** | 在同一框架中支持插入、位置/尺度调整、样式参考及背景保持 |
| **UM-Text / WeEdit** | 由自然语言或多轮指令驱动新增、重排、翻译和组合编辑 |
| **UTDesign** | 先生成透明 RGBA stylized glyph foreground，再合成进海报和广告等设计图 |
| **Qwen-Image / Qwen-Image-2.0** | 面向 posters、slides、infographics 等 text-rich 内容生成和编辑 |
| **InnoAds-Composer** | 同时控制商品主体、glyph 文字和风格，面向电商海报生成 |
| **TextSculptor / TextWand / WeEdit-Bench** | 将 addition 纳入标准训练和评测协议 |
| **PosterText / InfoVis** | 将文字 patch 或 slide 元素作为可操作单元，支持新增、修改和布局编辑 |

### 2.3 Text Removal / Erasing（文字擦除）

**目标**：去掉图像中的文字并恢复背景。这和普通 inpainting 不同，难点在于文字边缘、阴影、遮挡纹理和局部结构。

| 方法 | 主要特点 |
|------|----------|
| **EnsNet** | 端到端 FCN-ResNet + local-sensitive GAN，早期 scene text removal 代表方法 |
| **MTRNet / MTRNet++ / EraseNet** | mask-based cGAN、mask refine 与 coarse-to-fine inpainting，可处理用户指定或自动定位的文字区域 |
| **SRNet** | 显式包含 background inpainting module |
| **Stroke-Based Erasing / PERT** | 用 stroke mask 或 progressive region guidance 限定修改范围，兼顾擦除完整性和背景保持 |
| **PSSTRNet / ViTEraser** | segmentation-guided progressive erasing 与 ViT + SegMIM 两条高效端到端路线 |
| **FETNet** | 在 feature 层做 text feature erasing 和 background feature transferring |
| **TMIM** | 用低成本 text detection label 进行 text-aware masked image modeling 预训练 |
| **DiffSTR** | 将 STR 建模为受控 diffusion inpainting，并强化 mask refinement |
| **OmniText** | 通过 self-attention inversion 进行 training-free removal，并减少文字幻觉 |
| **TextWand** | 以 Region-Adaptive Suppression 做干净擦除，与文字生成/替换共用统一模型 |
| **OTR dataset** | 提供复杂背景、域外 overlay text 与 clean ground truth，用于训练和评估擦除方法 |
| **TextSculptor / TextWand-Bench** | 将 removal 作为独立基本任务，联合评估擦除质量和背景保持 |

### 2.4 Visual Text Rendering（图像文字生成）

**目标**：让 text-to-image 模型把指定文字写对，并自然融入图像或设计场景。

| 方法 | 主要特点 |
|------|----------|
| **GlyphDraw** | glyph + position 条件，重点解决中文等复杂字形结构 |
| **GlyphControl** | 用额外 glyph 条件控制 Stable Diffusion 中的文字内容、位置和大小 |
| **TextDiffuser** | layout transformer + diffusion，配套 MARIO-10M / MARIO-Eval |
| **TextDiffuser-2** | LLM 自动规划 layout，提升布局合理性 |
| **UDiffText** | 轻量 character-level text encoder 替换 CLIP text encoder |
| **Glyph-ByT5** | 定制 ByT5 text encoder，提高设计图文字准确性和长文本渲染能力 |
| **Glyph-ByT5-v2** | 扩展到 10 种语言并提升美学质量 |
| **GlyphDraw2** | LLM + diffusion 自动生成中英文复杂 glyph poster，并支持字体和高分辨率 |
| **JoyType** | 保持字体风格的多语言文字创建，采用 VLM 生成描述和 canny edge 指导 |
| **RepText** | 复制式多语言文字渲染，无需理解语言语义，支持用户指定字体 |
| **ControlText** | 无标注字体可控渲染，通过对比学习实现字体控制 |
| **DanceText** | 训练无关的分层文字几何变换框架，支持复杂变换和前后景融合 |
| **EasyText** | 基于 DiT 的可控多语言文字渲染，支持位置编码插值和曲线文字 |
| **LTOS** | 将 visual text rendering 与 object layout generation 合并为 text-object synthesis |
| **SceneVTG / SceneVTG++** | 用 MLLM 规划自然场景中的合理文字位置和内容，并支持多语言属性控制 |
| **CharGen / GlyphMastero** | 从 character-level multimodal encoding 和层次化 glyph encoding 提升复杂笔画准确性 |
| **TextCrafter** | 以 constrained RL 和 quotation-guided attention 处理多区域、多文字混淆，并提出 CVTG-2K |
| **FontAdapter / StyleTextGen** | 支持参考字体快速适配、跨语言 font transfer 和双语/跨语言风格复刻 |
| **TextPecker / GlyphPrinter / POCA** | 用结构异常 reward、region-grouped DPO 与 Pareto curriculum 改善 glyph accuracy 与美学平衡 |
| **Qwen-Image / Qwen-Image-2.0 / Boogu-Image-0.1** | 基座模型级文字渲染，覆盖长文本、中文、海报、幻灯片和信息图 |
| **GlyphAnchor** | 用与原生位置编码对齐的 glyph patch prior 提升长文本、密集文字和罕见字渲染 |
| **IDSpect / TextVerifier** | 以 IDS 分解和逐字验证识别 OCR 不敏感的错笔画、错部件和空间关系 |
| **AnyText / AnyText2** | 面向开放域 multilingual visual text generation |

### 2.5 Multilingual Visual Text（多语言文字生成与编辑）

**目标**：支持中文、英文以外的脚本与语言，包括变音符、RTL、复杂连写、混合脚本等。

| 方法 / Benchmark | 主要特点 |
|------------------|----------|
| **AnyText** | 首批系统支持 multilingual visual text generation and editing 的 diffusion 工作 |
| **AnyText2** | 在 multilingual 基础上加入字体、颜色等属性控制 |
| **Glyph-ByT5-v2** | 支持 10 种语言的 visual text rendering |
| **JoyType** | 保持字体风格的多语言文字生成，使用 canny edge 辅助 |
| **ControlText** | 无需字体标注的字体可控多语言渲染，基于对比学习 |
| **RepText** | 通过复制机制实现用户指定字体的多语言渲染，无需理解语言本身 |
| **DanceText** | 训练无关的多语言文字几何变换框架，支持旋转、缩放、扭曲 |
| **EasyText** | 基于 DiT 的多语言文字渲染，支持 10+ 种语言和曲线文字 |
| **FLUX-Text** | 以较少训练样本增强 FLUX-Fill 的 multilingual scene text editing，强调中文复杂字形 |
| **SceneVTG++ / StyleTextGen** | 分别关注自然场景中的可控多语言渲染，以及 monolingual / cross-lingual style consistency |
| **FontAdapter** | 通过参考 glyph 支持 unseen font、cross-lingual font transfer 与字体混合 |
| **STELLAR** | 以 language-adaptive glyph encoder、STIPLAR 和 TAS 指标关注 low-resource scripts |
| **WeEdit** | 330K 训练对覆盖 15 种语言，配套中英双语和 15 语 benchmark |
| **UM-Text / UTDesign** | 覆盖中英文自然语言编辑、跨语言翻译与 graphic-design glyph 生成 |
| **Self-Prompting STE / TextWand** | 面向开放词表、多语言复杂字形以及中英/符号的风格保持编辑 |
| **Qwen-Image / Qwen-Image-2.0** | 通过大规模数据和渐进训练强化中英等多语言 text-rich generation/editing |
| **VDE Bench** | 覆盖中英文复杂视觉文档编辑 |
| **MULTITEXTEDIT** | 3,600 个实例、12 种语言、5 个视觉域、7 类编辑操作，专门评估跨语言退化 |

### 2.6 Visual Document Editing（视觉文档与设计图编辑）

**目标**：编辑海报、PPT、论文截图、试卷、报纸、表单等密集文字文档。相比自然场景文字，文档编辑更强调布局、阅读顺序、局部结构和 OCR parsing。

| 方法 / Benchmark | 主要特点 |
|------------------|----------|
| **TextEditBench** | 强调 reasoning-aware text editing，不只看能否写对，还看语义和物理合理性 |
| **VDE Bench** | 942 个中英文 dense-document 样本，并用 OCR parsing 做细粒度评估 |
| **MiLDEdit / MiLDEAgent** | 对海报等多层设计文档做 layer-aware reasoning、目标层定位和协同修改 |
| **UTDesign** | 统一 stylized text editing、conditional generation 与 text-to-design pipeline |
| **UM-Text / WeEdit** | 从自然语言理解、layout planning、翻译、重排和 reasoning 角度编辑 text-rich images |
| **Qwen-Image-2.0** | 面向 slides、posters、infographics、comics 等 text-rich 内容生成和编辑 |
| **InnoAds-Composer** | 面向电商产品海报，联合控制商品主体、文字和设计风格 |
| **PosterText / InfoVis** | 分别面向电商海报 patch 编辑和 slide 原生生成/编辑，补充文本密集设计文档场景 |

### 2.7 任务 × 方法 交叉矩阵

| 任务 \ 方法 | GAN / Translation | Decomposition / Recognition | Stroke / Glyph / Layout | Diffusion / Flow | MLLM / Agent | Data / Benchmark |
|-------------|:-----------------:|:---------------------------:|:-----------------------:|:----------------:|:------------:|:----------------:|
| **Replacement** | STEFANN / SRNet / SwapText | RewriteNet / RS-STE / TripleFDS | MOSTEL / TextCtrl / GlyphMastero | DiffSTE / DiffUTE / FLUX-Text / OmniText / TextFlow / Self-Prompting STE / TextWand | UM-Text / Qwen-Image | ScenePair / TextSculpt / WeEdit / TextWand |
| **Addition** | — | — | GlyphControl / AnyText / UTDesign | DiffSTE / OmniText / TextWand | TextDiffuser-2 / UM-Text / WeEdit / Qwen-Image | TextSculpt / WeEdit-Bench |
| **Removal** | EnsNet / MTRNet / EraseNet | FETNet | Stroke Erasing / PERT / PSSTRNet | DiffSTR / OmniText / TextWand | WeEdit | SCUT-EnsText / TextSculpt / TextWand |
| **Rendering** | — | FontAdapter | GlyphDraw / Glyph-ByT5 / CharGen / GlyphPrinter | TextDiffuser / AnyText / TextCrafter / StyleTextGen | SceneVTG / TextDiffuser-2 / GlyphDraw2 | MARIO-Eval / CVTG-2K / TextInVision |
| **Multilingual** | — | LoGAN / FontAdapter | GlyphDraw / Glyph-ByT5-v2 / GlyphMastero | AnyText / FLUX-Text / StyleTextGen / Self-Prompting STE | UM-Text / WeEdit / Qwen-Image | MULTITEXTEDIT / UMT / WeEdit-Bench |
| **Document / Poster** | — | layer / attribute disentanglement | UTDesign / glyph-layout control | Qwen-Image / Boogu-Image / PosterText | MiLDEAgent / UM-Text / InfoVis / InnoAds | TextEditBench / VDE / MiLDEBench / VisSlideBench |

> **怎么读这张表**：
> - 横向看：同一个任务下有哪些技术路线。
> - 纵向看：同一种方法范式主要覆盖哪些任务。
> - 当前最活跃的区域是 **Diffusion/flow + glyph/OCR/layout conditioning + MLLM planning + benchmark-driven evaluation**。

## 3. 按方法范式详述（How to edit）

### 3.1 GAN / Translation-based Editing

早期 scene text editing 主要依赖 GAN 或 image-to-image translation，把文字区域作为局部图像翻译问题处理。

* **STEFANN**：
  * 论文：[arXiv 1903.01192](https://arxiv.org/abs/1903.01192)
  * 简介：早期字符级场景文字编辑方法。先从源字符生成目标字符，再保持源字符字体和颜色属性，将目标字符贴回原图。

* **SRNet / Editing Text in the Wild**：
  * 论文：[arXiv 1908.03047](https://arxiv.org/abs/1908.03047)
  * 简介：提出 Style Retention Network，将任务拆成文字转换、背景补全、融合三部分，是 word-level scene text editing 的代表性早期工作。

* **EnsNet**：
  * 论文：[arXiv 1812.00723](https://arxiv.org/abs/1812.00723)
  * 简介：scene text removal 早期代表。使用端到端 FCN-ResNet-18 与 local-sensitive GAN，把文字区域替换成自然背景。

* **MTRNet / MTRNet++**：
  * 论文：[MTRNet](https://arxiv.org/abs/1903.04092) / [MTRNet++](https://arxiv.org/abs/1912.07183)
  * 简介：mask-based text eraser。MTRNet++ 加入 mask-refine、coarse inpainting、fine inpainting 和 attention blocks，可支持有 mask 或无外部 mask 的文字擦除。

* **SwapText / EraseNet**：
  * 论文：[SwapText](https://arxiv.org/abs/2003.08152) / [EraseNet](https://doi.org/10.1109/TIP.2020.3018859)
  * 简介：SwapText 将 scene text replacement 建模为 source/target text swapping；EraseNet 则以 segmentation guidance 和 coarse-to-fine decoder 端到端擦除文字。

### 3.2 Decomposition / Stroke / Style Guidance

这类方法显式或隐式地把文字内容、字体风格、背景、笔画结构拆开，核心目标是减少"改字但丢风格"的问题。

* **TextStyleBrush**：
  * 论文：[arXiv 2106.08385](https://arxiv.org/abs/2106.08385)
  * 简介：从单个文字样例中抽取 appearance representation，并迁移到新内容上。它不完全等同于 scene text editing，但对 style-preserving text replacement 很关键。

* **RewriteNet**：
  * 论文：[arXiv 2107.11041](https://arxiv.org/abs/2107.11041)
  * 简介：通过 scene text recognition 引导模型区分 content 和 style，并使用 self-supervised training 利用真实未标注图像。论文给出的官方代码链接截至 2026-07-19 已失效。

* **MOSTEL**：
  * 地址：https://github.com/qqqyd/MOSTEL ![](https://img.shields.io/github/stars/qqqyd/MOSTEL.svg)
  * 论文：[arXiv 2212.01982](https://arxiv.org/abs/2212.01982)
  * 简介：将修改目标下沉到 stroke level，用 stroke guidance map 显式约束编辑区域，同时用半监督混合学习缓解 synthetic-to-real domain gap。

* **TextCtrl**：
  * 论文：[arXiv 2410.10133](https://arxiv.org/abs/2410.10133)
  * 简介：提出 style-structure guidance，将文字风格与 glyph 结构作为先验注入 diffusion-based editing，并引入 ScenePair 作为真实配对评测集。

* **FETNet**：
  * 地址：https://github.com/GuangtaoLyu/FETNet ![](https://img.shields.io/github/stars/GuangtaoLyu/FETNet.svg)
  * 论文：[arXiv 2306.09593](https://arxiv.org/abs/2306.09593)
  * 简介：面向 scene text removal。提出 Feature Erasing Module 和 Feature Transferring Module，在 encoder feature 层擦除文字信息并迁移背景特征。

* **Stroke-Based Erasing / PERT**：
  * 论文：[Stroke-Based](https://arxiv.org/abs/2104.11493) / [PERT](https://arxiv.org/abs/2106.13029)
  * 简介：前者缩小到 stroke-level hole 再补背景，后者用 progressive region modification 平衡 background integrity 与 erasure exhaustivity。

* **RS-STE / TripleFDS**：
  * 论文：[RS-STE](https://arxiv.org/abs/2503.08387) / [TripleFDS](https://arxiv.org/abs/2511.13399)
  * 简介：RS-STE 让 recognition 与 editing 在并行 decoder 中协同；TripleFDS 显式拆分 content、style、background，并支持风格替换与背景迁移。

* **STELLAR / GLASTE**：
  * 论文：[STELLAR](https://arxiv.org/abs/2511.09977) / [GLASTE](https://arxiv.org/abs/2512.03574)
  * 简介：STELLAR 用 language-adaptive glyph encoder、STIPLAR 和 TAS 支持低资源脚本；GLASTE 用 global-local features 和尺寸无关 style vector 处理长短差异明显的替换。

### 3.3 Diffusion-based Text Editing

Diffusion 让 text-in-image editing 从局部替换走向开放域图像编辑，但也带来新的挑战：文字容易写错，非编辑区域容易漂移。

* **DiffSTE**：
  * 地址：https://github.com/UCSB-NLP-Chang/DiffSTE ![](https://img.shields.io/github/stars/UCSB-NLP-Chang/DiffSTE.svg)
  * 论文：[arXiv 2304.05568](https://arxiv.org/abs/2304.05568)
  * 简介：双编码器设计：character encoder 提升文字可读性，instruction encoder 控制风格，支持文字插入和编辑。

* **DiffUTE**：
  * 地址：https://github.com/chenhaoxing/DiffUTE
  * 论文：[NeurIPS 2023](https://arxiv.org/abs/2305.10825)
  * 简介：把 glyph condition 和背景保持统一到 diffusion editing 中，支持 insertion、replacement 等通用文字编辑操作。

* **TextDiffuser**：
  * 地址：https://github.com/microsoft/unilm/tree/master/textdiffuser
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

* **DiffSTR**：
  * 论文：[arXiv 2410.21721](https://arxiv.org/abs/2410.21721)
  * 简介：把 scene text removal 建模成 ControlNet diffusion inpainting，并用 mask pretraining 和 segmentation-based mask refinement 提升边界与纹理一致性。

* **FLUX-Text**：
  * 地址：https://github.com/AMAP-ML/FluxText
  * 论文：[arXiv 2505.03329](https://arxiv.org/abs/2505.03329)
  * 简介：基于 FLUX-Fill 的 multilingual scene text editing baseline。通过轻量 glyph 和 text embedding module 增强复杂字形理解，用较少训练样本取得强编辑效果。

* **Qwen-Image**：
  * 地址：https://github.com/QwenLM/Qwen-Image ![](https://img.shields.io/github/stars/QwenLM/Qwen-Image.svg)
  * 论文：[arXiv 2508.02324](https://arxiv.org/abs/2508.02324)
  * 简介：图像生成基座模型，但对本方向很重要：技术报告明确强调复杂文字渲染和精确图像编辑，尤其在中文等 logographic language 上做了专门数据和训练设计。

* **Qwen-Image-2.0**：
  * 论文：[arXiv 2605.10730](https://arxiv.org/abs/2605.10730)
  * 简介：统一高保真生成和精确编辑，面向 ultra-long text rendering、multilingual typography、slides、posters、infographics、comics 等 text-rich 内容。

* **OmniText**：
  * 地址：https://github.com/KAIST-VICLab/OmniText
  * 论文：[ICLR 2026](https://arxiv.org/abs/2510.24093)
  * 简介：基于 TextDiffuser-2 做 training-free attention inversion/redistribution 与 latent optimization，统一 removal、insertion、style editing、repositioning 和 rescaling。

* **TextFlow / Edit Fidelity Field**：
  * 论文：[TextFlow](https://arxiv.org/abs/2603.24571) / [EFF](https://arxiv.org/abs/2604.17500)
  * 简介：TextFlow 用 flow manifold steering 与 attention boost 做 training-free replacement；EFF 用 OCR-aware continuous field 将目标区、邻近文字和背景分级保护，量化并降低 edit spillover。

* **Self-Prompting STE**：
  * 项目：https://hongxiii.github.io/mstedit/
  * 论文：[ICML 2026](https://arxiv.org/abs/2605.15523)
  * 简介：直接从源图构造 glyph/style prompts，以 MM-DiT in-context learning 实现开放词表和多语言风格保持编辑。

* **TextWand**：
  * 论文：[arXiv 2606.05730](https://arxiv.org/abs/2606.05730)
  * 简介：把 rendering 与 erasure 作为两个原子能力统一建模；ORPE 控制像素级 layout/参考风格，RAS 负责干净擦除，并配套 TextWand-Bench。

* **UM-Text / WeEdit**：
  * 论文：[UM-Text](https://arxiv.org/abs/2601.08321) / [WeEdit](https://arxiv.org/abs/2603.11593)
  * 简介：UM-Text 用 VLM 自动规划 content/layout 和组合条件；WeEdit 以 330K 多语言样本做 glyph-guided SFT 与 multi-objective RL，覆盖八类 text-centric edits。

* **STEPS**：
  * 论文：[PAKDD 2026](https://arxiv.org/abs/2609.38636)
  * 简介：使用独立的 contrastive style encoder 提取与文字内容解耦的视觉风格，并与字符编码和 rendered glyph 条件联合完成场景文字替换。

* **PixText**：
  * 论文：[arXiv 2610.18284](https://arxiv.org/abs/2610.18284)
  * 简介：将局部文字修复建模为 pixel-space grouped image generation，只生成目标区域并保留未编辑内容；MeanFlow 版本支持四步推理。

### 3.4 Glyph / OCR / Layout Guided Rendering

这类方法的共同点是承认普通文本编码器不足以精确控制字形，因此引入 glyph、OCR、character encoder 或 layout planner。

* **GlyphDraw**：
  * 项目：https://1073521013.github.io/glyph-draw.github.io/
  * 论文：[arXiv 2303.17870](https://arxiv.org/abs/2303.17870)
  * 简介：为复杂字形结构提供 glyph 和 position 条件，重点解决中文等复杂字符在 text-to-image 模型中的准确渲染。

* **GlyphControl**：
  * 地址：https://github.com/AIGText/GlyphControl-release
  * 论文：[arXiv 2305.18259](https://arxiv.org/abs/2305.18259)
  * 简介：在 off-the-shelf Stable Diffusion 上加入 glyph conditional control，使用户可以控制文字内容、位置和大小，并构建 LAION-Glyph 训练 benchmark。

* **TextDiffuser-2**：
  * 地址：https://github.com/microsoft/unilm/tree/master/textdiffuser-2
  * 论文：[arXiv 2311.16465](https://arxiv.org/abs/2311.16465)
  * 简介：用大语言模型规划文字内容和 layout，再将 layout 编码进 diffusion 模型，支持聊天式布局调整。

* **Glyph-ByT5**：
  * 地址：https://github.com/AIGText/Glyph-ByT5
  * 论文：[arXiv 2403.09622](https://arxiv.org/abs/2403.09622)
  * 简介：定制 character-aware ByT5 text encoder，并与 SDXL 结合，让设计图和长文本渲染的 spelling accuracy 大幅提升。

* **Glyph-ByT5-v2**：
  * 论文：[arXiv 2406.10208](https://arxiv.org/abs/2406.10208)
  * 简介：扩展到 10 种语言，并结合偏好学习提升美学质量，是 multilingual visual text rendering 的强基线。

* **GlyphDraw2**：
  * 地址：https://github.com/OPPO-Mente-Lab/GlyphDraw2 ![](https://img.shields.io/github/stars/OPPO-Mente-Lab/GlyphDraw2.svg)
  * 论文：[arXiv 2407.02252](https://arxiv.org/abs/2407.02252)
  * 简介：自动复杂 glyph poster 生成框架。结合 LLM、SDXL、triple-cross attention，支持中英文海报文字、字体控制和高分辨率输出。

* **LTOS**：
  * 论文：[arXiv 2404.13579](https://arxiv.org/abs/2404.13579)
  * 简介：将 visual text rendering 与 object layout generation 合并为 layout-controllable text-object synthesis，面向 emoji / poster 等图文组合场景。

* **TextCrafter**：
  * 地址：https://github.com/NJU-PCALab/TextCrafter
  * 论文：[arXiv 2503.23461](https://arxiv.org/abs/2503.23461)
  * 简介：以 bottleneck-aware constrained RL 与 quotation-guided attention 缓解多文字 insulation 和 token 混淆，并提出 CVTG-2K / CVTG-Hard。

* **InnoAds-Composer**：
  * 论文：[arXiv 2603.05898](https://arxiv.org/abs/2603.05898)
  * 简介：电商产品海报生成框架，单阶段联合控制 subject、glyph 和 style，并为中文文字渲染设计 Text Feature Enhancement Module。

* **SceneVTG / SceneVTG++**：
  * 论文：[SceneVTG](https://arxiv.org/abs/2407.14138) / [SceneVTG++](https://arxiv.org/abs/2501.02962)
  * 简介：使用 MLLM 推荐自然场景中合理的 text region/content，再以 conditional diffusion 完成真实、多语言且属性可控的渲染。

* **CharGen / GlyphMastero**：
  * 论文：[CharGen](https://arxiv.org/abs/2412.17225) / [GlyphMastero](https://arxiv.org/abs/2505.04915)
  * 简介：分别以 character-level multimodal encoder 和 stroke/character/line hierarchical glyph encoder 提升复杂字形的结构准确性。

* **FontAdapter / StyleTextGen**：
  * 论文：[FontAdapter](https://arxiv.org/abs/2506.05843) / [StyleTextGen](https://arxiv.org/abs/2605.14708)
  * 简介：前者从 reference glyph 在数秒内适配 unseen font；后者用双分支 style encoder 和 mask guidance 做多语言、跨语言风格复刻。

* **TextPecker / GlyphPrinter / POCA**：
  * 论文：[TextPecker](https://arxiv.org/abs/2602.20903) / [GlyphPrinter](https://arxiv.org/abs/2603.15616) / [POCA](https://arxiv.org/abs/2604.24171)
  * 简介：代表 2026 年 post-training 路线：结构异常感知 reward、region-grouped DPO，以及在文字准确、美学和指令遵循间求 Pareto-optimal curriculum。

* **GlyphAnchor**：
  * 论文：[arXiv 2609.02349](https://arxiv.org/abs/2609.02349)
  * 简介：将轻量 glyph patch 与目标图的原生位置编码锚定，兼容 text-to-image 和 image-editing DiT，并配套 InfoTextBench 评测长文本、密集排版和罕见字。

* **IDSpect / TextVerifier**：
  * 论文：[IDSpect](https://arxiv.org/abs/2609.37569) / [TextVerifier](https://arxiv.org/abs/2610.19551)
  * 简介：把汉字拆成 IDS 部件和空间关系，用结构级 reward 或逐字 verifier 发现 OCR 和通用 VLM 容易漏掉的错笔画、错部件与布局错误。

### 3.5 Attribute and Multilingual Control

当文字已经能写对之后，下一步是可控：字体、颜色、行级属性、多语言脚本、甚至文档排版。

* **AnyText2**：
  * 地址：https://github.com/tyxsspa/AnyText2 ![](https://img.shields.io/github/stars/tyxsspa/AnyText2.svg)
  * 论文：[arXiv 2411.15245](https://arxiv.org/abs/2411.15245)
  * 简介：在 AnyText 基础上增加字体和颜色属性控制，可对每行文字设置定制属性，面向更实用的海报、广告、商品图编辑。

* **MULTITEXTEDIT**：
  * 论文：[arXiv 2605.08163](https://arxiv.org/abs/2605.08163)
  * 简介：不是模型，而是跨语言 benchmark。覆盖 12 种语言、5 个视觉域、7 类编辑操作，并提出 language fidelity scoring，专门揭示不同脚本上的退化。

* **SceneTextStylizer**：
  * 论文：[arXiv 2510.10910](https://arxiv.org/abs/2510.10910)
  * 简介：training-free scene text style transfer。通过 diffusion inversion、自注意力 feature injection、region control 和 Fourier style enhancement，只改文字区域风格并保持可读性。

* **UTDesign**：
  * 地址：https://github.com/ZYM-PKU/UTDesign
  * 论文：[SIGGRAPH Asia 2025](https://arxiv.org/abs/2512.20479)
  * 简介：用 DiT 生成透明 RGBA stylized glyph foreground，统一中英文 text editing、conditional generation 和完整 text-to-design pipeline。

* **MiLDEdit / MiLDEAgent**：
  * 论文：[arXiv 2601.04589](https://arxiv.org/abs/2601.04589)
  * 简介：面向多层海报和设计文档，以 RL-trained multimodal reasoner 识别目标图层，再协调 image editor 执行局部修改。

* **LoGAN**：
  * 论文：[ECCV 2026](https://arxiv.org/abs/2609.07029)
  * 简介：VLM agent 协调 glyph diffusion、字体风格微调、spacing/kerning transfer 和纹理扩展，从少量字形样例完成 27+ 语言的字体本地化。

* **PosterText / InfoVis**：
  * 论文：[PosterText](https://arxiv.org/abs/2608.16289) / [InfoVis](https://arxiv.org/abs/2610.16784)
  * 简介：PosterText 把文字 patch 作为海报生成、添加、删除和修改的原子单位；InfoVis 面向 slide 原生数据，统一生成、编辑、布局和文本渲染。

### 3.6 Benchmark-first Frameworks

最近的趋势是：单个模型结果已经不足以说明问题，领域更需要标准数据、任务划分和评测协议。

* **TextEditBench**：
  * 论文：[arXiv 2512.16270](https://arxiv.org/abs/2512.16270)
  * 简介：1,196 个 multilingual / mixed-script 标注实例，覆盖 14 个主题、6 类任务和 12 个子任务；强调 reasoning-aware editing beyond rendering。

* **VDE Bench**：
  * 地址：https://github.com/zion-zion-zion/VDE-Bench
  * 论文：[arXiv 2602.00122](https://arxiv.org/abs/2602.00122)
  * 简介：942 个中英文样本，覆盖论文、海报、幻灯片、试卷、报纸等 dense text document，并使用 OCR parsing 做细粒度评估。

* **TextSculptor**：
  * 地址：https://github.com/linyiheng123/TextSculptor ![](https://img.shields.io/github/stars/linyiheng123/TextSculptor.svg)
  * 论文：[arXiv 2605.21090](https://arxiv.org/abs/2605.21090)
  * 简介：系统化的数据构造和评测框架。构造 TextSculpt-Data（3.2M 样本），并发布 TextSculpt-Bench，覆盖 addition / replacement / removal / hybrid editing 四类任务。

* **WeEdit / TextWand**：
  * 论文：[WeEdit](https://arxiv.org/abs/2603.11593) / [TextWand](https://arxiv.org/abs/2606.05730)
  * 简介：WeEdit 提供中英与 15 语两个 2K benchmark；TextWand-Bench 含 1,500 个样本，在 generation、replacement、removal 三类任务上各 500 个。

* **GlyphAnchor / UltraText Bench**：
  * 论文：[GlyphAnchor](https://arxiv.org/abs/2609.02349) / [UltraText Bench](https://arxiv.org/abs/2610.09823)
  * 简介：前者将 glyph prior 与位置锚定结合，后者用中英双语、4–12 个文字区域和三级难度评估 dense visual text 的 fidelity、clarity、spatial quality 与 scene quality。

* **VTR-Bench / InfoVis**：
  * 论文：[VTR-Bench](https://arxiv.org/abs/2610.01499) / [InfoVis](https://arxiv.org/abs/2610.16784)
  * 简介：VTR-Bench 将文字保真纳入视频生成评测；InfoVis 发布 VisSlideBench，覆盖 slide 生成和编辑的多维自动评测并与人工评分对齐。

* **MULTITEXTEDIT / Mind the Gap**：
  * 论文：[MULTITEXTEDIT](https://arxiv.org/abs/2605.08163) / [Mind the Gap](https://arxiv.org/abs/2606.15982)
  * 简介：前者以 3,600 个实例测量 12 种语言的 script fidelity；后者用 461 个案例和 19 类依赖诊断模型能否发现局部改字触发的二级一致性约束。

* **TextInVision**：
  * 论文：[arXiv 2503.13730](https://arxiv.org/abs/2503.13730)
  * 简介：联合控制 text complexity 与 prompt complexity，系统诊断 visual text generation，并分析 VAE 在小字和密集文字上的瓶颈。

* **ImgEdit / EditInspector**：
  * 论文：[ImgEdit](https://arxiv.org/abs/2505.20275) / [EditInspector](https://arxiv.org/abs/2506.09988)
  * 简介：不是 text-in-image 专用 benchmark，但对通用图像编辑模型评估很有参考价值。可作为评估 text editing 模型 instruction adherence、artifact、detail preservation 的外部补充。

## 4. 数据集与 Benchmark

### 4.1 数据集

| 数据集 | 年份 | 来源 | 规模 / 标注 | 用途 |
|--------|------|------|-------------|------|
| **SCUT-Syn** | 2018 | EnsNet | 8K train / 800 test synthetic pairs | scene text removal training / evaluation |
| **SCUT-EnsText** | 2020 | EraseNet | real-world paired text / clean-background images | real-world scene text removal |
| **Imgur5K** | 2021 | TextStyleBrush | handwritten word images | one-shot text style transfer |
| **Tamper-Syn2k / Tamper-Scene** | 2022 | MOSTEL | synthetic + real scene text editing pairs | stroke-level editing training / evaluation |
| **MARIO-10M** | 2023 | TextDiffuser | 10M image-text pairs，含 OCR recognition / detection / character-level segmentation | text rendering training |
| **AnyWord-3M** | 2023 | AnyText | 3M multilingual image-text pairs，含 OCR 标注 | multilingual generation / editing |
| **LAION-Glyph** | 2023 | GlyphControl | glyph-conditioned visual text data | glyph-controlled text rendering |
| **Flickr-ST** | 2023 | FETNet | scene text removal / segmentation annotations | text removal and segmentation |
| **ScenePair** | 2024 | TextCtrl | real-world paired scene text editing dataset | real-world STE comparison |
| **DetailedTextCaps-100K** | 2024 | TextHarmony | 100K detailed visual-text captions | comprehension + generation training |
| **LTOS dataset** | 2024 | LTOS | layout-aware text-object labels | poster / emoji-style text-object synthesis |
| **RS-STE-Dataset** | 2025 | RS-STE | paired synthetic data + unpaired real-data recipe | recognition-synergistic editing |
| **OTR** | 2025 | OTR | out-of-domain overlay text + clean GT / complex backgrounds | text removal training / evaluation |
| **STIPLAR** | 2025 | STELLAR | low-resource languages + real-world pairs | multilingual STE / TAS evaluation |
| **SCB Synthesis** | 2025 | TripleFDS | 1M images / 125K SCB Groups | content/style/background disentanglement |
| **SynthGlyph / DesignText** | 2025 | UTDesign | ≈28.8M character instances / 115.5K design images | bilingual stylized design editing / generation |
| **UM-DATA-200K** | 2026 | UM-Text | 200K poster / product images | context-aware bilingual editing |
| **TextPecker-1.5M** | 2026 | TextPecker | 1.5M character-level structural-anomaly samples | VTR reward training / evaluation |
| **WeEdit Dataset** | 2026 | WeEdit | 330K pairs，7 operations，15 languages | text-centric SFT / RL training |
| **TextSculpt-Data** | 2026 | TextSculptor | 3.2M samples，1.2M OCR-verified T2I + 2M paired editing | scene text generation / editing |
| **TextWand-72K** | 2026 | TextWand | 72K Chinese/English/symbol samples，>300 fonts | unified generation / replacement / removal |
| **PosterText data** | 2026 | PosterText | large-scale e-commerce poster data with text-patch annotations | unified poster generation / patch editing |

> ScenePair 等资源同时承担训练/评测用途；这里按“数据来源”收录，下面的 Benchmark 表再描述其评测协议。下载入口：[SCUT-Syn](https://github.com/HCIILAB/Scene-Text-Removal)、[SCUT-EnsText](https://github.com/HCIILAB/SCUT-EnsText)、[RS-STE-Dataset](https://huggingface.co/datasets/Nineve/RS-STE-Dataset)、[OTR](https://huggingface.co/datasets/cyberagent/OTR)、[TextPecker-1.5M](https://huggingface.co/datasets/CIawevy/TextPecker-1.5M)、[TextSculpt-Data](https://huggingface.co/datasets/dafbgd/TextSculpt-Data)。

### 4.2 Benchmark

| Benchmark | 年份 | 关注点 | 语言 | 链接 |
|-----------|------|--------|------|------|
| **MARIO-Eval** | 2023 | visual text rendering quality | English | [TextDiffuser](https://arxiv.org/abs/2305.10855) |
| **AnyText-benchmark** | 2023 | multilingual text generation / editing | Multilingual | [AnyText](https://arxiv.org/abs/2311.03054) |
| **ScenePair** | 2024 | real-world paired scene text editing | English | [TextCtrl](https://arxiv.org/abs/2410.10133) |
| **CVTG-2K / CVTG-Hard** | 2025 | complex multi-text rendering，2K prompts + 400 hard samples | English / Chinese | [TextCrafter](https://github.com/NJU-PCALab/TextCrafter) |
| **TextInVision** | 2025 | text complexity × prompt complexity / VAE failure diagnosis | multilingual | [paper](https://arxiv.org/abs/2503.13730) |
| **OmniText-Bench** | 2025 | insert / edit / remove / reposition / rescale with style refs | Latin / alphanumeric | [code/bench](https://github.com/KAIST-VICLab/OmniText) |
| **UTDesign-Bench** | 2025 | stylized text edit / conditional generation，1K cases | Chinese / English | [code/data](https://github.com/ZYM-PKU/UTDesign) |
| **TextEditBench** | 2025 | reasoning-aware editing，1,196 instances / 12 subtasks | multilingual / mixed-script | [paper](https://arxiv.org/abs/2512.16270) |
| **MiLDEBench / MiLDEEval** | 2026 | multi-layer design-document editing，>20K documents | design documents | [paper](https://arxiv.org/abs/2601.04589) |
| **UMT-Benchmark** | 2026 | context-aware / multi-turn visual text editing | Chinese / English | [UM-Text](https://arxiv.org/abs/2601.08321) |
| **VDE Bench** | 2026 | visual document editing / OCR parsing，942 samples | Chinese / English | [code/data](https://github.com/zion-zion-zion/VDE-Bench) |
| **TIQA / ANTIQA** | 2026 | no-reference human-aligned typography quality，120K crops + 1.5K images | multilingual | [paper](https://arxiv.org/abs/2603.07119) / [code/data](https://github.com/koltsov-cmc/antiqa) |
| **WeEdit Bilingual / Multilingual** | 2026 | 8 edit categories，2K cases each | Chinese / English + 15 languages | [benchmark](https://huggingface.co/datasets/HuiZhang0812/WeEdit_benchmark) |
| **StyleText-CE** | 2026 | monolingual / cross-lingual text-style consistency | multilingual | [StyleTextGen](https://arxiv.org/abs/2605.14708) |
| **MULTITEXTEDIT** | 2026 | 3,600 edits，5 domains / 7 operations / script fidelity | 12 languages | [paper](https://arxiv.org/abs/2605.08163) |
| **TextSculpt-Bench** | 2026 | addition / replacement / removal / hybrid editing | English | [code/data](https://github.com/linyiheng123/TextSculptor) |
| **TextWand-Bench** | 2026 | generation / replacement / removal，500 each | Chinese / English / symbols | [paper](https://arxiv.org/abs/2606.05730) |
| **Constraint-discovery diagnostic** | 2026 | 461 cases / 19 secondary-constraint types | multilingual scenes | [Mind the Gap](https://arxiv.org/abs/2606.15982) |
| **InfoTextBench** | 2026 | long, dense and rare-character rendering in generation/editing | — | [GlyphAnchor](https://arxiv.org/abs/2609.02349) |
| **Text Refinement Bench** | 2026 | local text correction and image preservation | — | [PixText](https://arxiv.org/abs/2610.18284) |
| **TEXTRENDERBENCH-ZH** | 2026 | per-character Chinese rendering correctness / 7,358 annotations | Chinese | [TextVerifier](https://arxiv.org/abs/2610.19551) |
| **VisSlideBench** | 2026 | slide generation and editing / 11 multidimensional metrics | — | [InfoVis](https://arxiv.org/abs/2610.16784) |
| **UltraText Bench** | 2026 | dense multi-region visual text / 432 prompts | Chinese / English | [paper](https://arxiv.org/abs/2610.09823) / [code](https://github.com/LINs-lab/UltraText_Bench) |
| **VTR-Bench** | 2026 | video visual text rendering / 300 prompts and 5 scenarios | — | [paper](https://arxiv.org/abs/2610.01499) / [code](https://github.com/hardenyu21/VTR-Bench) |

### 4.3 常用评测指标

| 类别 | 指标 | 含义 |
|------|------|------|
| 文字正确性 | **OCR exact match / OCR accuracy** | 编辑后文字是否能被 OCR 正确识别 |
| 文字正确性 | **CER / WER** | 字符错误率 / 词错误率 |
| 脚本保真 | **Language / Script Fidelity** | 是否保留变音符、RTL 顺序、连写形态、混合脚本 |
| 风格一致性 | **Style similarity** | 字体、颜色、stroke、阴影、透视是否与原图一致 |
| 风格一致性 | **TAS / reference-style similarity** | 分别衡量 font、color、background 或参考 glyph 风格是否保持 |
| 背景保持 | **LPIPS / PSNR / SSIM on non-edit region** | 非编辑区域是否漂移 |
| 局部保护 | **Edit spillover rate / per-region preservation** | 编辑目标文字时，邻近非目标文字是否被误改 |
| 语义一致性 | **Semantic Expectation / VLM judgment** | 编辑结果是否符合上下文和物理常识 |
| 指令遵循 | **IA / TA / VQ / BP** | instruction adherence、text accuracy、visual quality、background preservation 的组合评估 |
| 字形结构 | **Structural-anomaly score** | 检测错笔画、扭曲、模糊、错位等 OCR 可能忽略的结构错误 |
| 文档结构 | **OCR parsing / reading order** | dense document 中布局和阅读顺序是否保持 |
| 人类偏好 | **Human preference** | 综合文字正确、视觉自然、编辑保真 |

## 5. 开源工具与项目

这里只列官方公开实现、数据或评测代码；完整论文列表以上方全景表为准。

| 项目 | 主要用途 | 官方资源 |
|------|----------|----------|
| **AnyText / AnyText2** | multilingual generation/editing + font/color control | [AnyText](https://github.com/tyxsspa/AnyText) / [AnyText2](https://github.com/tyxsspa/AnyText2) |
| **Boogu-Image-0.1** | bilingual unified generation / editing foundation model | [Boogu-Project/Boogu-Image](https://github.com/Boogu-Project/Boogu-Image) |
| **DiffSTE / DiffUTE** | diffusion insertion / replacement | [DiffSTE](https://github.com/UCSB-NLP-Chang/DiffSTE) / [DiffUTE](https://github.com/chenhaoxing/DiffUTE) |
| **FETNet / PSSTRNet** | feature- and segmentation-guided text removal | [FETNet](https://github.com/GuangtaoLyu/FETNet) / [PSSTRNet](https://github.com/GuangtaoLyu/PSSTRNet) |
| **FLUX-Text** | multilingual FLUX-Fill scene text editing | [AMAP-ML/FluxText](https://github.com/AMAP-ML/FluxText) |
| **Glyph-ByT5 / v2** | accurate multilingual visual text rendering | [AIGText/Glyph-ByT5](https://github.com/AIGText/Glyph-ByT5) |
| **GlyphControl / GlyphDraw2** | glyph-controlled rendering / complex poster generation | [GlyphControl](https://github.com/AIGText/GlyphControl-release) / [GlyphDraw2](https://github.com/OPPO-Mente-Lab/GlyphDraw2) |
| **GlyphPrinter / TextPecker** | preference/reward-based glyph post-training | [GlyphPrinter](https://github.com/FudanCVL/GlyphPrinter) / [TextPecker](https://github.com/CIawevy/TextPecker) |
| **MOSTEL / RS-STE / TripleFDS** | stroke, recognition, and attribute-disentangled replacement | [MOSTEL](https://github.com/qqqyd/MOSTEL) / [RS-STE](https://github.com/ZhengyaoFang/RS-STE) / [TripleFDS](https://github.com/yusenbao01/TripleFDS) |
| **OmniText** | training-free general text-image manipulation + benchmark | [KAIST-VICLab/OmniText](https://github.com/KAIST-VICLab/OmniText) |
| **PERT / ViTEraser** | progressive region / ViT-based text removal | [PERT](https://github.com/wangyuxin87/PERT) / [ViTEraser](https://github.com/shannanyinxiang/ViTEraser) |
| **Qwen-Image** | text-rich generation and precise image editing | [QwenLM/Qwen-Image](https://github.com/QwenLM/Qwen-Image) |
| **SceneVTG / TextHarmony** | scene text planning, comprehension and generation | [SceneVTG](https://github.com/AlibabaResearch/AdvancedLiterateMachinery) / [TextHarmony](https://github.com/bytedance/TextHarmony) |
| **SRNet / EnsNet / EraseNet** | classic replacement / removal baselines | [SRNet](https://github.com/youdao-ai/SRNet) / [EnsNet](https://github.com/HCIILAB/Scene-Text-Removal) / [EraseNet](https://github.com/lcy0604/EraseNet) |
| **TextCrafter** | complex multi-text rendering and CVTG evaluation | [NJU-PCALab/TextCrafter](https://github.com/NJU-PCALab/TextCrafter) |
| **TextDiffuser / TextDiffuser-2** | layout-guided rendering and LLM layout planning | [TextDiffuser](https://github.com/microsoft/unilm/tree/master/textdiffuser) / [TextDiffuser-2](https://github.com/microsoft/unilm/tree/master/textdiffuser-2) |
| **TextFlow** | training-free flow-based scene text editing | [lyb18758/TextFlow](https://github.com/lyb18758/TextFlow) |
| **TextSculptor** | training data, four-task benchmark and evaluation | [linyiheng123/TextSculptor](https://github.com/linyiheng123/TextSculptor) |
| **TMIM** | text-aware masked image modeling for removal | [wzx99/TMIM](https://github.com/wzx99/TMIM) |
| **UDiffText / UTDesign** | character-aware synthesis / bilingual graphic-design editing | [UDiffText](https://github.com/ZYM-PKU/UDiffText) / [UTDesign](https://github.com/ZYM-PKU/UTDesign) |
| **VDE Bench / WeEdit** | document/text-centric editing datasets and evaluation | [VDE-Bench](https://github.com/zion-zion-zion/VDE-Bench) / [WeEdit](https://github.com/HuiZhang0812/WeEdit) |
| **InfoVis / UltraText / VTR-Bench** | slide, dense visual text and video text evaluation | [InfoVis](https://github.com/VectorSpaceLab/InfoVis) / [UltraText Bench](https://github.com/LINs-lab/UltraText_Bench) / [VTR-Bench](https://github.com/hardenyu21/VTR-Bench) |

## 6. 相关方向

* **Text-to-Image Generation with Accurate Typography**：关注模型能否在从零生成图像时写对字。
* **Scene Text Removal / Text Erasing**：更偏向 inpainting，但和 text editing 强相关。
* **OCR-guided Image Editing**：用 OCR detection / recognition / parsing 引导图像编辑。
* **Visual Document Understanding and Editing**：从文档理解、版面分析进入文档图像编辑。
* **Multilingual Visual Generation**：关注非英文脚本、多语言、跨语言退化。
* **Layered Image / Design Decomposition**：[Qwen-Image-Layered](https://github.com/QwenLM/Qwen-Image-Layered) 提供 RGB-to-RGBA 图层分解；[CreatiParser](https://arxiv.org/abs/2604.19632) 将 raster design 解析为可编辑的文字、背景和贴纸图层。两者都更偏通用设计可编辑性，而非 text-specific 方法。
* **General Image Editing Evaluation**：[ImgEdit](https://arxiv.org/abs/2505.20275) 与 [EditInspector](https://arxiv.org/abs/2506.09988) 可补充 instruction adherence、artifact 和 detail preservation 评估。
* **Structured Graphic Design**：[StructuredEdit](https://arxiv.org/abs/2607.04612) 与 [PosterHarness](https://arxiv.org/abs/2607.03006) 分别研究参数化 typography/layout 编辑和 scientific-poster generation audit，属于邻近方向。
* **Benchmark and Evaluation**：从 OCR accuracy 走向 OCR + structural anomaly + VLM + human preference 的组合评测。

## Contributing

欢迎提交论文、官方实现、数据集、benchmark 或已失效链接修复。请先阅读 [CONTRIBUTING.md](CONTRIBUTING.md)，并在 PR 中给出可核验来源；未正式录用的工作会明确标为 arXiv / preprint，不把计划投稿写成已录用 venue。

## License

[Apache License 2.0](LICENSE)
