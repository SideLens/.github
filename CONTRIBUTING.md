# 贡献指南

## 提 issue 之前

先看这两篇，很多问题已经写在里面：

- [blockers.md](https://github.com/SideLens/sidelens/blob/master/docs/blockers.md) —— 什么做不了、为什么
- [progress.md](https://github.com/SideLens/sidelens/blob/master/docs/progress.md) —— 每一轮做了什么、实测数字

如果是「画面黑屏 / 没声音 / 延迟异常」，**请附接收端统计行**。没有这一行基本无法定位：

```text
UDP 统计 frames=1024 net_ms="0.13/65.44/81.84" playable_ms="15.65/24.43"
  jitter=1 target_ms="10.0" nack_sent=316 healed=152 dropped=229
  loss="0.079" fec_reds=18 fec_recovered=11 fec_redundant=11
  video_decoded=888 render_frames=888 render_failed=0 render_mode="gpu-window"
```

## 参数配对（最常见的误报来源）

配错不会报错，只会得到「看起来像 bug」的静默失败：

| 发送端 | 接收端 | 配错的后果 |
| --- | --- | --- |
| `--h264` | `SIDELENS_H264_DECODE=1` | 不开：`video_decoded=0` 但不报错 |
| 不给 `--h264` | 却开了解码 | `video_decode_failed` 飙升 |
| `--audio --opus` | `SIDELENS_OPUS=1` | 不开：`audio_decode_failed` 飙升 |
| `--psk X` | `SIDELENS_PSK=X` | **`decrypt_failed=0` 但两路解码全废** |

## 开发环境

```bash
# Rust 侧：标准 cargo，无额外要求
cargo build --release
cargo test

# JS 侧：用 Vite+（vp），不要用 npm / pnpm / yarn
vp install
vp test run
```

Windows 上 Rust 工具链路径在脚本里通过环境变量 `RUSTUP_HOME` / `CARGO_HOME` 读取，
不写死绝对路径。

## 提交前必跑

```powershell
cargo fmt --all
cargo clippy --all-targets -- -D warnings
cargo test

.\tools\verify-e2e.ps1 -Quick        # 25 项断言，约 1 分钟

# 改了 #[cfg] 门控时必须跑
.\tools\verify-cross-platform.ps1    # 5 个 target，产物自动清理
```

**「编译过了」不算验证。** 这个项目是延迟敏感的系统，行为正确性靠断言保证，
性能靠 `tools/bench/run-matrix.ps1` 的前后对比保证。

## 代码约定

### 路径

不要写死绝对路径。脚本从 `$PSScriptRoot` 推导仓库根，Rust 用 `CARGO_MANIFEST_DIR`。

### 跨平台门控

新增 `#[cfg(windows)]` 时必须同时处理非 Windows 分支，否则 `verify-cross-platform.ps1`
会在 `cargo check --target <非本机>` 时暴露 `E0425` / `E0433`。

### windows crate feature

加 feature 前先 `grep` 确认源码真的用到了那个命名空间。`windows` crate 的体积随
feature 数线性增长 —— 开 15 个 feature 时单个 rlib 就有 105 MB。

注意有些 feature 是**前置依赖**，源码里看不到直接引用但不能删。例如
`Win32_Security`：`CreateFileW` / `CreateNamedPipeW` / `CreateEventW` /
`CreateFileMappingW` 都依赖它，删了 `sidelens-ipc` 直接 `E0432`。

### 文档

改了行为就改 `docs/` 里对应那篇。文档按「想解决什么问题」组织，不按时间顺序。

## 分支与提交

- 从 `master` 切分支，PR 合回 `master`
- 提交信息用中文，写清「为什么改」而不只是「改了什么」
- 涉及性能改动的 PR 必须附 `run-matrix` 前后对比数据

## 许可

贡献的代码默认按 [Apache-2.0](https://github.com/SideLens/sidelens/blob/master/LICENSE) 授权。
