# SideLens

把一台设备的**屏幕、麦克风、系统声音**以超低延迟共享给另一台设备。
原生界面、GPU 渲染、开源。

---

## 这是什么

一个自己写协议、自己调编解码、自己接 GPU 的屏幕共享工具。
不用 WebRTC，不用 webview，不用 Electron。

| 实测指标 | 数值 | 条件 |
| --- | --- | --- |
| 端到端可播放延迟 p50 | **19.6 ms** | 720p 60fps，含界面 + GPU 渲染 |
| GPU 渲染单帧 p50 | **437 µs** | 1080p，D3D11 flip-model（GDI 是 7456µs，**17.1x**） |
| 屏幕采集 p50 | **22.7 ms** | 4K DXGI（GDI 60.4ms） |
| Opus 音频带宽 | **45 kbps** | 原始 PCM 768kbps，压 17 倍 |

45,000 行 Rust / 16 个 crate / 1059 个测试 / 5 个平台交叉编译通过。

---

## 仓库

| 仓库 | 说明 |
| --- | --- |
| [sidelens](https://github.com/SideLens/sidelens) | 主仓库（monorepo） |

按 [ADR 0001](https://github.com/SideLens/sidelens/blob/master/docs/adr/0001-monorepo.md)，
核心协议与各平台 UI 暂不拆仓。拆仓触发条件是 UI ≥ 4、core 需要独立发版、
或贡献者出现明显分工。

---

## 快速开始

```bash
git clone https://github.com/SideLens/sidelens.git
cd sidelens
cargo build --release
```

完整用法见 [README](https://github.com/SideLens/sidelens#readme)。

---

## 技术选择

几个可能反直觉的决定，都有实测数据支撑：

- **自己定帧格式**而不是用 WebSocket message 边界 —— 接收端必须能从任意切分的
  字节流重新切出帧，帧头要有 magic + 长度并且能重新同步。
- **GPU 渲染**而不是 GDI —— GDI 有三次全帧拷贝，GPU 合成一步，7456µs → 437µs。
- **原生 Win32 控件**而不是 webview —— 建窗 2.4ms、消息泵 297ns，界面本身只有
  几行状态加一块视频，webview 的数百毫秒启动成本不值得。
- **自适应抖动缓冲**而不是固定 target_ms —— p50 从 20.95ms 降到 13.77ms。

---

## 已知限制

只在 Windows 上运行。5 个 target 编译通过，但 macOS / Linux 没有平台实现。
详见 [blockers.md](https://github.com/SideLens/sidelens/blob/master/docs/blockers.md)。

---

## 许可

Apache-2.0
