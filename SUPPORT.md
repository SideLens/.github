# 获取帮助

## 先看文档

SideLens 有 31 篇设计文档，按「想解决什么问题」组织，不是按时间顺序。
大部分「怎么用 / 为什么这样设计 / 为什么走不通」都能在里面找到答案。

| 想知道什么 | 读哪篇 |
| --- | --- |
| 怎么跑起来 | [主仓库 README](https://github.com/SideLens/sidelens#readme) |
| 什么做不了、为什么 | [blockers.md](https://github.com/SideLens/sidelens/blob/master/docs/blockers.md) |
| 延迟怎么优化的 | [latency-budget.md](https://github.com/SideLens/sidelens/blob/master/docs/latency-budget.md) |
| GPU 渲染为什么快 17 倍 | [render-gpu.md](https://github.com/SideLens/sidelens/blob/master/docs/render-gpu.md) |
| 界面为什么不用 webview | [ui.md](https://github.com/SideLens/sidelens/blob/master/docs/ui.md) |
| FEC 该不该开 | [fec-link.md](https://github.com/SideLens/sidelens/blob/master/docs/fec-link.md) |
| 屏幕采集踩过什么坑 | [capture.md](https://github.com/SideLens/sidelens/blob/master/docs/capture.md) |
| 文档总索引 | [docs/README.md](https://github.com/SideLens/sidelens/blob/master/docs/README.md) |

## 提问

开 [issue](https://github.com/SideLens/sidelens/issues/new/choose)，选对应模板。

**延迟 / 黑屏 / 没声音类问题必须附接收端统计行**，否则无法定位。

## 不提供

- 一对一的技术支持
- 定制开发
- Windows 之外的平台适配（当前没有平台实现，见 blockers）

## 安全问题

不要开 public issue，走 [SECURITY.md](SECURITY.md) 里的私密渠道。
