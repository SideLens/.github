## 这个 PR 做了什么

<!-- 一两句话说清。如果修的是 bug，写清根因而不是现象。 -->

## 为什么

<!-- 关联 issue：Closes #123 -->

## 怎么验证的

SideLens 是延迟敏感的系统，「编译过了」不算验证。请勾选实际跑过的项：

- [ ] `cargo test` 全过
- [ ] `cargo fmt --all` + `cargo clippy --all-targets -- -D warnings` 干净
- [ ] `tools/verify-e2e.ps1 -Quick` 25 项断言全过
- [ ] `tools/verify-cross-platform.ps1` 5 个 target 全过（改了 `#[cfg]` 门控时必须）
- [ ] 改动涉及延迟关键路径，附上 `tools/bench/run-matrix.ps1` 前后对比

### 实测数据（涉及性能时必填）

| 指标 | 改动前 | 改动后 |
| --- | --- | --- |
|  |  |  |

## 改动范围

- [ ] 只动了一个 crate
- [ ] 跨 crate（列出：）
- [ ] 改了协议 / 帧格式（**必须**说明兼容性影响）
- [ ] 改了工具链 / CI / 构建配置

## 检查清单

- [ ] 新增的 `#[cfg(windows)]` 门控有对应的非 Windows 分支或 `compile_error!`
- [ ] 没有把绝对路径写进代码或脚本（一律从 `$PSScriptRoot` / `CARGO_MANIFEST_DIR` 推导）
- [ ] 新增的 `windows` crate feature 确实被源码引用
- [ ] 文档已同步（改了行为就改 `docs/` 对应那篇）
