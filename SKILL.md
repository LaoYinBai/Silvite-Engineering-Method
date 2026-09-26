---
name: silvite-engineering-method
description: Use when planning or executing non-trivial software work with multiple modules, uncertain failure modes, production impact, elevated permissions, automation, unfamiliar technology, architectural change, or incomplete verification.
---

# Silvite Engineering Method

## 核心原则

把 Agent 当作高吞吐执行层，而不是目标、风险或完成状态的最终裁决者。可靠性来自清晰边界、可逆执行和独立证据，而不是假设 Agent 不犯错。本 Skill 不替代领域安全规范、宿主权限规则或必要的人工授权。

## 研发决策流程

1. **定义结果**：把请求改写成用户可感知、可验证的结果；列出非目标、约束和完成证据。
2. **理解现状**：先查代码、状态、依赖、测试、版本和未提交改动；分开记录事实、推断与未知。
3. **建立系统图**：标出组件、边界、状态、交互、失败模式和影响面；优先定位根因所在层。
4. **选择最小闭环**：设计最小端到端切片、验证方式、停止条件和回滚路径。
5. **受控执行**：只改授权范围；新信息要求扩大范围、权限或风险时，停止并重新确认合同。
6. **独立验证**：运行与改动风险相称的测试、构建、静态检查、日志检查、实机或可复现实验。
7. **准确报告**：区分已完成、已缓解、未验证和受阻；证据不足时写“未验证”，不得推测完成。

复杂任务按 [engineering-principles.md](references/engineering-principles.md) 建立任务合同；陌生系统先读 [system-thinking.md](references/system-thinking.md)。

## Direct Execution Before Tooling

**Do the work before building tooling for the work.** 对一次性、小规模、低风险且可直接完成的任务，默认直接产出用户要的结果。存在重复步骤、可以写脚本或可以抽象成框架，都不是先造工具的理由。本规则约束新建基础设施，不妨碍直接使用现有工具。

开始写新的脚本、CLI、批处理器、pipeline、registry 或辅助框架前，快速比较：直接完成当前交付物的成本，与设计、实现、调试、验证和维护工具的成本；只计算有明确依据的复用。如果直接执行更简单、更快且足够可靠，就直接执行。少量文件修改、视觉资产逐项处理、单次 QA 与格式转换都允许这样做。

只有当前规模已使直接执行明显昂贵、流程确定会反复使用、人工一致性难保证、批量操作风险较高、任务要求可重复审计，或用户明确要求工具时，才优先自动化。此时只建设完成本轮任务所需的最小工具，不为假想需求扩成通用平台。高风险删除、迁移、覆盖和大规模重命名仍须满足预览、验证与恢复门禁。

**ZERO-DELIVERABLE WARNING：** 若脚本、登记表、检查点或 QA 文档持续增加，而本阶段正式交付物仍为零，立即停止工具扩张。重新核对用户等待的成果，选择能产生第一个正式成果的最小步骤并执行；若该步骤确被缺失条件阻断，报告具体阻断证据。辅助基础设施不得计作核心交付物。

发现自己为少量工作搭建批处理框架、为几个视觉状态创建分析管线，或为一次验证编写通用平台时，视为 **Tooling Detour**：返回原始任务。最终验收先看交付物及其质量，再看工具是否有独立价值。

## Agent 权限与边界

- 诊断默认只读，权限只提升到完成当前步骤所需的最小集合。
- 不自行扩大目标、改无关代码、清理用户改动或改变兼容承诺。
- 写入前建立可识别基线。脏工作树必须有不覆盖原改动的隔离或可恢复快照；否则停止写入。
- 高风险动作采用“检查 → 预览 → 执行 → 验证”，并在执行前验证回滚路径。
- 破坏性、生产、凭据、隐私或外部副作用遵循更严格的宿主规则和人工授权。

细则见 [agent-boundaries.md](references/agent-boundaries.md)。

## 验证与完成定义

“代码写完”不是完成。完成证据必须覆盖请求结果、相关回归、构建或产物、目标环境行为以及必要的恢复路径。回滚窗口存在时，从窗口倒推 go/no-go 时点。临时缓解必须有观测、负责人、复查或退出条件；根因未知时不得关闭为“根因已修复”。见 [verification.md](references/verification.md) 与 [debugging-and-recovery.md](references/debugging-and-recovery.md)。

## 复杂度控制

- 架构服务于复杂度控制；抽象必须由已观察到的重复变化、失败模式或隔离需求证明。
- 通用机制下沉，业务语义留在正确层；核心流程不反向依赖可选能力。
- 对会替代人工或 Known-Good 策略的自动控制：先建立 baseline 与可观测性，再用 Shadow Mode 验证，随后有限控制、逐级扩大，并始终保留 fallback。
- 优先最小可逆降级恢复服务，再评估长期结构改造。

详见 [complexity-control.md](references/complexity-control.md)。

## 互补 Skill 路由

当任务涉及多阶段底层替换、协议演进、跨平台统一、多 edition/多仓库兼容或发布迁移时，同时使用 `silvite-architecture-evolution`。本 Skill 继续负责通用工程治理；迁移基线、不变量、切片台账、兼容窗口和发布身份门禁由互补 Skill 负责。

当任务涉及 Linux 开发环境初始化、Host/Guest/Container/VM/WSL/远程会话边界、Shell/PATH/包能力、冷启动、诊断包或备份恢复时，同时使用 `silvite-environment-engineering`。本 Skill 继续负责通用工程治理；环境拓扑、生命周期、能力状态与恢复证据门禁由互补 Skill 负责。

## 常见反模式

- 把“现代化”“重构好”当作验收标准。
- 顺手修改任务外代码，导致范围与证据失去对应关系。
- 为假想未来预建框架，或用大量开关维持错误抽象。
- 用重试、重启、吞异常或补丁掩盖根因并宣布修复。
- 没有日志和状态语义就增加自动控制。
- 以 Agent 的完成声明、历史通过率或局部测试代替当前证据。

完整清单见 [anti-patterns.md](references/anti-patterns.md)。项目暴露知识缺口时，按 [project-driven-learning.md](references/project-driven-learning.md) 定向补齐。
