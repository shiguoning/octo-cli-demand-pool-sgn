# octo-cli-demand-pool-sgn（octo-cli 需求池）

> 这是 [octo-cli](https://github.com/Mininglamp-OSS/octo-cli)（Octo 生态的命令行工具）的**产品需求池**。
> 由 AI 产品管家团队维护：**🎧 octo管家-问答收单**（收单/归档）、**📋 octo产品经理-PRD**（补 PRD）、**🔍 octo评审-Review**（审 PRD）。

## 这个仓库是干什么的

考试/日常场景中，群里的 bug 反馈、新需求统一归档到这里：
- 用 GitHub Issue 当需求单
- Label 表达「类型 / 优先级 / 状态 / 来源」四轴
- PRD 写在 issue 评论里（带 v1/v2/v3 版本），评审意见也留在评论（闭环可审计）
- `runs/` 目录是**定时巡检的执行记录**（cron 每次扫描都 commit 一条，无论有无变化）

## Label 体系

| 轴 | 取值 |
|---|---|
| 类型 type/ | `bug` `feature` `docs` `question` `chore` |
| 优先级 priority/ | `P0`（阻塞）`P1`（主功能）`P2`（体验）`P3`（建议） |
| 状态 status/ | `new` → `claimed` → `prd-draft` → `in-review` → `published` / `wontfix` |
| 来源 from/ | `examiner`（考官）`user`（用户）`cron`（定时扫描） |

状态流转：

```
status/new ──认领──▶ status/claimed ──PRD初稿──▶ status/prd-draft
     ▲                                              │ 请评审
     │ 打回带原因                        status/in-review ◀───┐
     └─────────────── PM 按原因修改 ◀─── 打回 ────────────────┘
                                                       │ 通过
                                                  status/published
任意状态 + 考官判定不做 ──▶ status/wontfix（链路终止，如实报告）
```

## Issue 怎么写

反馈请带：场景/复现步骤/期望行为/实际行为（bug 类）。模板见 `.github/ISSUE_TEMPLATE/`。
- bug 单要尽可能附上 octo-cli 源码里的证据位置（`来源: <路径>#L<行>`），无法确认就先标「未复现」。
- 结论如实区分：**已修复 ≠ 未复现 ≠ wontfix（不做）**，三种状态绝不混用。

## 定时巡检（runs/）

管家每 5 分钟自动扫描本仓库的变化（新单/关单/wontfix/feature label/评审打回），有变化才在考试群播报。每条执行记录写在这里：
- `runs/` 目录：公开执行账本（无论有无变化都会 commit）
- 另一本账在 OpenClaw `automations runs` 里（平台原生历史）

## 维护者

- **🎧 octo管家-问答收单**：收单、判型、建单、巡检、播报
- **📋 octo产品经理-PRD**：feature 单 → PRD（只写 What 不写 How）
- **🔍 octo评审-Review**：按清单审 PRD，打回必给可执行原因
- 考生：施国宁（考试群内 @ 本人）

## 链接

- 目标产品源码：https://github.com/Mininglamp-OSS/octo-cli（只读，不在本仓库操作）
