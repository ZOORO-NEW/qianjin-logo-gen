---
name: qianjin-logo-gen
agent_created: true
slug: qianjin-logo-gen
displayName: 专业Logo生成引擎
summary: "WorkBuddy 专业 Logo/标识/图标生成引擎：把图像模型切到专为设计生的模型（硅基流动 SiliconFlow 国内直连免费、豆包 Seedream、通义万相、Recraft 原生产 SVG、OpenAI gpt-image-1、Ideogram），并将「三层锁定」提示词框架（genre 风格锚定 / style 形态约束 / no-text 应用约束）固化为参数，默认追加扁平矢量、禁用渐变3D等专业约束。密钥仅从环境变量读取，绝不落代码。"
description: 用「Logo 专用」图像模型在 WorkBuddy 里生成专业级 Logo/标识/图标。支持硅基流动 SiliconFlow（国内直连、OpenAI 兼容、模型多、用户已有券可免费）、豆包 Seedream、通义万相、Recraft（原生产 SVG 矢量）、OpenAI gpt-image-1、Ideogram。把前进公众号「三层锁定」提示词框架固化成参数（genre 风格锚定 / style 形态约束 / no-text 应用约束），默认追加扁平矢量、禁用渐变3D等专业约束。当用户想在 WorkBuddy 做 Logo、品牌标识、公众号头像、图标，或抱怨通用模型（如 Agnes）做不出好 Logo 时使用。密钥仅从环境变量读取，绝不落代码。
version: 1.0.0
category: 设计创作
platforms: [workbuddy, claude-code, cursor, windsurf, codex, linux, macos, windows]
author: qianjin
tags:
  - logo
  - brand-design
  - visual-design
  - ai-image
  - siliconflow
license: MIT
disable: false
---

# qianjin-logo-gen · WorkBuddy 专业 Logo 生成

通用生图模型（如 Agnes Image 2.1 Flash）是为「高信息密度、复杂场景」优化的，做 Logo 反而别扭。本技能把图像引擎切到**专为设计生的模型**，并把「三层锁定」框架做成参数，让 WorkBuddy 稳定出专业 Logo。

## 为什么通用模型做不出 Logo（根因）

- Logo 要「极简、扁平、矢量干净、字要准」，而通用模型强项是「密、繁、写实」。
- Logo 是 AI 出图最难的活：要同时满足矢量级干净 + 字母精准 + 品牌味，通用模型给的常是「好看的装饰画」。
- 提示词不能跨模型平移：豆包自带中文设计语感能接住「负空间/禁用渐变」，Agnes 会把中文翻英文再生成，约束被稀释。

## 模型怎么选（含国内直连）

| 模型 | 鉴权 env | 国内直连 | 最适合 | 免费 / 低价 |
|------|----------|----------|--------|-------------|
| **硅基流动 SiliconFlow** | `SILICONFLOW_API_KEY` | ✅ 是 | 聚合 Flux / Kolors / SDXL，模型多、Kolors 中文强 | 你已有券≈免费；¥0.01-0.1/张 |
| **豆包 Seedream** | `ARK_API_KEY` | ✅ 是 | 中文设计语感好（你已验证 App 出图） | 免费 50-200 次 |
| **通义万相** | `DASHSCOPE_API_KEY` | ✅ 是 | 中文提示词最佳 | 新户约 50-100 张免费 |
| **Recraft** | `RECRAFT_API_KEY` | ⚠️ 波动 | Logo/图标/矢量，原生产 SVG | 每天 30 积分（免信用卡） |
| **OpenAI gpt-image-1** | `OPENAI_API_KEY` | ❌ 需代理 | 通用强、文字稳、可透明底 | 按量付费 |
| **Ideogram V2** | `IDEOGRAM_API_KEY` | ❌ 需代理 | 纯文字字标（wordmark）最强 | 每天 10 张免费 |

**推荐**：境内优先 **硅基流动**（你已有 key + 券，等于免费；做中文/国风 Logo 用 `Kwai-Kolors/Kolors` 更懂中文，要约束收敛用 `Qwen/Qwen-Image`）。想要「真·SVG 矢量」再上 Recraft（国内访问波动、免费档产出公开无商业授权）。纯文字店名标用 Ideogram（需代理）。

⚠️ **实测踩坑（2026-08-21）**：`black-forest-labs/FLUX.1-dev` 在部分账号返回 `Model disabled`（需付费/单独开通），先用 `GET /v1/models` 核实可用列表。`Qwen/Qwen-Image` 是硅基流动免费档里**指令遵循最强**的，最适合「单色/禁渐变/几何」这类硬约束 brief，实测优于 Kolors（Kolors 会忽略英文负面约束、出 3D/渐变）。

硅基流动上值得用的生图模型（用 `--model` 指定，先 `GET /v1/models` 核实在你账号是否可用）：
- `Qwen/Qwen-Image`：**指令遵循最强**，单色/几何/禁渐变类硬约束 brief 首选（实测可用）
- `Kwai-Kolors/Kolors`：快手可图，中文理解强，国风友好，约 ¥0.01-0.02/张（但易忽略负面约束）
- `black-forest-labs/FLUX.1-dev`：高质量通用约束强，但部分账号 `Model disabled`
- `black-forest-labs/FLUX.1-schnell`：快速、开源免费档
- `black-forest-labs/FLUX.1-Kontext-dev`：图像编辑（改图）
- `stabilityai/stable-diffusion-xl-base-1.0` / `SD3.5`：经典 SD，可控
- `Z-Image-Turbo` / `Z-Image`：阿里通义，约 ¥0.10/张，出图快
- `Qwen/Qwen-Image-Edit` / `baidu/ERNIE-Image-Turbo`：编辑/备选

## 快速开始

1. 去对应官网拿 API key，设为环境变量（**不要写进任何文件/代码**）：
   - Windows PowerShell：`$env:RECRAFT_API_KEY="你的key"`
   - Bash/Linux：`export RECRAFT_API_KEY="你的key"`
   - Recraft：登录 recraft.ai → 用户菜单 → API → Generate Token
   - OpenAI：platform.openai.com → API keys
   - Ideogram：ideogram.ai → Settings → API
2. 用受管 Python 跑脚本（纯标准库，无需 pip）：

```bash
"C:/Users/ZQJ/.workbuddy/binaries/python/envs/default/Scripts/python.exe" \
  "C:/Users/ZQJ/.workbuddy/skills/qianjin-logo-gen/scripts/logo_gen.py" \
  --provider recraft \
  --brief "一家做 AI 工具的初创公司 App 图标，字母 Q 与向上箭头结合" \
  --genre swiss \
  --no-text \
  --num 3 \
  --out "C:/Users/ZQJ/WorkBuddy/2026-06-04-22-58-34/每日文章/logo_output"
```

3. 出图后人工挑一张，再细化或单独加文字。

### 国内直连：硅基流动 SiliconFlow（你已有 key + 券，等于免费）

```bash
# 1) 设好环境变量（只放内存，不落文件）
$env:SILICONFLOW_API_KEY="你的硅基流动key"

# 2) 跑（默认 FLUX.1-dev 高质量；中文/国风换 Kolors）
"C:/Users/ZQJ/.workbuddy/binaries/python/envs/default/Scripts/python.exe" `
  "C:/Users/ZQJ/.workbuddy/skills/qianjin-logo-gen/scripts/logo_gen.py" `
  --provider siliconflow `
  --model "Kwai-Kolors/Kolors" `
  --brief "一家 AI 工具初创公司的 App 图标，字母 Q 与向上箭头结合，国风" `
  --genre guofeng --no-text --num 3 `
  --out "C:/Users/ZQJ/WorkBuddy/2026-06-04-22-58-34/每日文章/logo_output"
```

## 参数说明（对应三层锁定框架）

- `--brief`：你的需求（必填）。可用中文，脚本会自动补专业约束。
- `--genre`：**第一层 风格锚定**。预设 `swiss`(瑞士国际主义) / `bauhaus`(包豪斯几何) / `muji`(无印风) / `badge`(复古徽章) / `memphis`(孟菲斯) / `guofeng`(国风)；也可直接写任意流派名。
- `--style`：**第二层 形态约束**。补图形类型、构图、母题等，如「圆形印章构图，桂花与碗形负空间结合」。
- `--no-text`：**第三层 应用约束（符号优先）**。生成纯图形标、不带字，绕开 90% 的文字翻车；文字后续用矢量软件或 Ideogram 单独加。
- `--vector`：Recraft 专属，请求 SVG 矢量输出（默认 PNG 预览）。
- `--transparent`：OpenAI 专属，出透明底。
- `--num`：一次出几个候选（推荐 3-4，人工挑）。
- `--size` / `--aspect`：尺寸。
- `--model`：硅基流动模型 ID（仅 `siliconflow` 用），如 `Kwai-Kolors/Kolors`（中文强）/ `FLUX.1-schnell` / `SDXL`。默认 `black-forest-labs/FLUX.1-dev`。

## 默认追加的专业约束（每次自动带上）

`flat vector logo, minimal, solid color, clean geometric, professional brand mark, no gradient, no 3D, no photorealism, no drop shadow, high contrast, balanced composition`

即文章里说的「禁用渐变、禁用 3D、禁用写实阴影」自动化进提示词，和你手写三层锁定等价。

## 工作流建议（比一锤子生成稳）

1. 用 `--no-text` 先出 3-4 个纯符号方案。
2. 挑一个记忆点最强的。
3. 若需文字：用 Ideogram（`--provider ideogram`，Magic Prompt 已默认 OFF）单独出带字标，或进 Figma/Inkscape 手动加。
4. Recraft `--vector` 出的 SVG 可直接无限缩放、改色。

## 重要提醒

- API key 只放环境变量，脚本绝不打印、绝不落盘。
- Recraft 免费档产出归 Recraft 所有、公开、无商业授权；客户/商用项目请升级付费档。
- 图像 URL 有时效，脚本已自动下载到本地 `--out` 目录。
