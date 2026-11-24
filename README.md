# SideLens/.github

这个仓库不是代码，是 **SideLens 组织的社区健康文件与组织主页**。
GitHub 会自动从这里继承默认的社区文件。

## 这里有什么

| 路径 | 作用 | 如何生效 |
| --- | --- | --- |
| `profile/README.md` | 组织主页 https://github.com/SideLens 显示的内容 | 自动 |
| `CONTRIBUTING.md` | 贡献指南 | 组织下**没有**自带 CONTRIBUTING 的仓库自动继承 |
| `SECURITY.md` | 安全策略与漏洞报告渠道 | 同上 |
| `CODE_OF_CONDUCT.md` | 行为准则 | 同上 |
| `SUPPORT.md` | 获取帮助的入口 | 同上 |
| `LICENSE` | Apache-2.0 全文 | **不自动继承**，仅作组织统一许可的参照 |
| `.github/ISSUE_TEMPLATE/` | issue 模板 | 同上（仓库级模板优先） |
| `.github/PULL_REQUEST_TEMPLATE.md` | PR 模板 | 同上 |

## 不生效的部分

GitHub 的继承机制只覆盖少数几类文件，以下几点容易误解：

- **`LICENSE` 不会被继承。** 每个仓库必须自带 LICENSE 文件，
  GitHub 才会在仓库页面显示许可标识。本仓库的 LICENSE 只是组织统一口径的参照。
- **`FUNDING.yml` 组织级不传播。** 要支持赞助需在每个仓库单独配置。
  （本仓库因此没有放 FUNDING.yml。）
- **`workflows/` 不会被继承。** CI 必须放在各自的仓库里。

## 当前生效范围

组织下目前只有 [sidelens](https://github.com/SideLens/sidelens) 一个代码仓库。
它已经自带 README 与 docs/，社区文件从本仓库继承。

## 修改

这些文件都是普通 Markdown / YAML，直接提 PR 即可。

内容原则：**写这个项目真实的情况，不要套模板**。比如 SECURITY.md 里写清了
「不做身份认证、不做前向保密轮换、不做 DoS 防护」是有意取舍而非漏洞 ——
这类说明比通用模板有用得多。
