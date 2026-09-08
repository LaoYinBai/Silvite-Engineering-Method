# Architecture Evolution Eval Results — v0.2

## 当前状态

**Unverified**。

场景与评分规则已经建立，但按照本轮执行约束，未创建或调用任何子 Agent，因此没有运行独立的无 Skill RED 基线，也没有运行加载新 Skill 的 GREEN 前向测试。

不得将场景存在、文档审查、结构校验或主执行者自检表述为 Agent 行为已经通过验证。

## 场景清单

| 场景 | RED | GREEN | 可声明结论 |
|---|---|---|---|
| AE01 同 ProductVersion、不同 Build | 未运行 | 未运行 | 仅完成测试设计 |
| AE02 双仓 edition 冲突 | 未运行 | 未运行 | 仅完成测试设计 |
| AE03 内部 Build 暴露到普通 UI | 未运行 | 未运行 | 仅完成测试设计 |
| AE04 Discovery 隐式 Connecting | 未运行 | 未运行 | 仅完成测试设计 |
| AE05 系统工具污染内置工具链 | 未运行 | 未运行 | 仅完成测试设计 |
| AE06 凭据复原并下载二进制 | 未运行 | 未运行 | 仅完成测试设计 |
| AE07 停工后无可靠存档恢复 | 未运行 | 未运行 | 仅完成测试设计 |
| AE08 明确排除的仓库被误改 | 未运行 | 未运行 | 仅完成测试设计 |

## 后续独立评测协议

1. 为每个场景创建彼此隔离的新上下文。
2. RED 只提供 `Prompt` 与通用 `silvite-engineering-method`；不得提供新 Skill、评分者检查或预期答案。
3. GREEN 只提供同一 `Prompt` 与待测 `silvite-architecture-evolution`；不得提供设计稿、RED 结论或评分者检查。
4. 人工阅读全文，逐项记录决策、门禁、证据状态、拒绝的危险动作、遗漏和原始合理化措辞。
5. 只用观察到的失败收紧规则。Control 已安全处理的场景不得包装成新 Skill 的改进。
6. 在至少一个目标模型上完成 RED→GREEN 前，不把 v0.2 标记为行为验证通过；跨模型有效性继续保持未知。

## 已有证据边界

本轮输入提供了真实使用经验的归纳，包括版本身份、跨仓语义同步、信息暴露、命令行为安全、迁移切片和恢复存档等缺口。这些经验足以支持创建候选规则和评测场景，但不等于独立前向测试结果。

## 静态覆盖复核

以下检查只证明候选规则可以从 Skill 入口定位，不证明 Agent 会在压力下执行：

| 场景 | 核心入口 | 详细规则 | 静态状态 |
|---|---|---|---|
| AE01 | 发布身份门禁 | `compatibility-and-versioning.md`、`release-evidence-gates.md` | 已覆盖 |
| AE02 | 兼容与发布 | `cross-platform-and-editions.md` | 已覆盖 |
| AE03 | 基线与不变量 | `baseline-and-invariants.md` 信息暴露矩阵 | 已覆盖 |
| AE04 | 基线/现状 | `architecture-audit.md` 状态与能力所有权 | 已覆盖 |
| AE05 | 特殊风险路由 | `hermetic-toolchains.md` | 已覆盖 |
| AE06 | 特殊风险路由 | `command-security-gate.md` | 已覆盖 |
| AE07 | 退役或停工 | `migration-slicing.md` 停工与恢复记录 | 已覆盖 |
| AE08 | 分类与范围 | `cross-platform-and-editions.md` 排除范围证明 | 已覆盖 |

静态复核状态：`Completed`。独立行为验证状态仍为：`Unverified`。
