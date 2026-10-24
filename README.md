<h1 align="center">Professional Raster Compositor</h1>

<p align="center">
  <b>An open-source, native image editor — layers, masks, adjustment layers, layer styles, type, vectors, brushes and real PSD files, written entirely in Rust.</b><br>
  A fork of <a href="https://github.com/storytold/photocraft">PhotoCraft</a> by the ArtCraft team (MIT OR Apache-2.0),
  rebranded and maintained here as an independent project.
</p>

<p align="center">
  <img alt="100% Rust" src="https://img.shields.io/badge/100%25-Rust-b7410e?style=flat-square&logo=rust">
  <img alt="Windows · macOS · Linux" src="https://img.shields.io/badge/Windows%20%C2%B7%20macOS%20%C2%B7%20Linux-native-2f7bf5?style=flat-square">
  <img alt="License: MIT OR Apache-2.0" src="https://img.shields.io/badge/license-MIT%20%2F%20Apache--2.0-3a3a3a?style=flat-square">
</p>

## 简介（中文）

Professional Raster Compositor（简称 PRC）是一个开源、原生（无 Electron/WebView）的专业栅格图像合成器，
基于 [PhotoCraft](https://github.com/storytold/photocraft) 项目的 fork。PhotoCraft 是一个用纯 Rust 从零实现的
Photoshop 风格图像编辑器，本仓库在其基础上改名并独立维护。

主要能力：

- **图层体系**：图层组、剪贴蒙版、像素/矢量蒙版、填充图层、调整图层、智能对象与智能滤镜、27 种 Photoshop 混合模式
- **调整**：16 种调整图层（曲线、色阶、色相/饱和度、黑白、颜色查找……），全部非破坏性
- **图层样式**：投影、内/外发光、斜面浮雕、描边、颜色/渐变/图案叠加
- **选区与蒙版**：选框、套索、魔棒、快速选择、对象选择、选择主体（本地 AI 推理，无云端）
- **矢量**：钢笔工具、形状图层、路径面板、布尔运算
- **文字**：画布上直接编辑的点文本/段落文本，完整字符与段落控制
- **滤镜**：67 个工具，实时预览；大半径高斯模糊多核并行
- **文件格式**：PSD/PSB 读写（307/309 psd-tools 测试文件渲染一致）、分层 TIFF、OpenRaster、XCF/KRA/PDN 读取、PNG/JPEG/WebP/EXR 等
- **色彩管理**：纯 Rust 实现的 ICC，RGB/灰度/CMYK/Lab，8/16/32 位
- **Agent 就绪**：500+ 命令均可通过 CLI、JSON 控制通道或 MCP server 驱动

## Build from source

Prerequisites: [Rust](https://rustup.rs) 1.95+ (on Windows: the MSVC toolchain and Visual Studio C++ Build Tools).

```sh
git clone https://github.com/ryxc355/professional-raster-compositor
cd professional-raster-compositor
cargo run --release -p photocraft            # the desktop app
cargo build --release -p photocraft-cli      # the headless CLI (target/release/prc-cli)
```

Optional: clone [craft-fonts](https://github.com/storytold/craft-fonts) next to this repository and build with
`CRAFT_FONTS_DIR="$PWD/../craft-fonts" cargo build` to embed Japanese fonts; without it the app falls back to system CJK fonts.

The command-line tool opens, edits and saves documents without a window:

```sh
prc-cli run photo.psd \
  --cmd filter.sharpen.smartSharpen     --params '{"amount":80}' \
  --cmd layer.newAdjustmentLayer.curves --params '{"points":[[0,0],[64,48],[192,212],[255,255]]}' \
  --out photo-final.png
prc-cli mcp   # drive the engine from an AI agent over MCP
```

## Status

This is the upstream project's early alpha, rebranded. Most of Photoshop's feature surface exists in some
form, but it is not yet a daily-driver professional replacement; expect rough edges. Upstream docs in
[`docs/`](docs/) and [`book/`](book/) and `AGENTS.md` still refer to the project by its original name.

## Relationship to upstream and to Adobe

- Upstream: [storytold/photocraft](https://github.com/storytold/photocraft) — clean-room reimplementation from
  public specs; no Adobe code, shaders or assets. Thank you, ArtCraft team and contributors.
- Per the upstream license terms, the ArtCraft name, wordmark and logos (trademarks of the ArtCraft Team) are
  **not** covered by the open license and must be removed in forks; they have been removed here, and this
  project is not affiliated with or endorsed by the ArtCraft Team or Adobe Inc.
- License: MIT OR Apache-2.0. Copyright of the original code: ArtCraft Team and the PhotoCraft contributors —
  see [NOTICE](NOTICE), [LICENSE-MIT](LICENSE-MIT), [LICENSE-APACHE](LICENSE-APACHE) and [ATTRIBUTION.md](ATTRIBUTION.md).
