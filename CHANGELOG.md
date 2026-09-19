# Changelog

版本遵循阶段性规则：`v0.x` 表示方法仍在快速变化；`v1.0` 需要经过多个真实项目、长期维护和反例检验后再确定。

## [0.3.0] - 2026-09-19

### Added

- 新增互补 Skill `silvite-environment-engineering`，用于分层 Linux 开发环境的拓扑、生命周期、能力状态、冷启动和恢复验收。
- 增加测试器自证、包名与命令名分离、备份—恢复闭环、诊断包隐私边界和 fail-closed 校验门禁。
- 增加 8 个由真实现场工件失败抽象而来的环境工程压力场景。

### Changed

- 在通用 Skill 中增加环境工程最小路由，避免把平台细节继续堆入通用治理。
- 更新 README 的三 Skill 职责、安装、目录、评测与状态说明。

### Validation

- 对交接包执行成员安全检查、SHA256 复核、文件/案例/测试计数、Shell 语法检查和测试器重放。
- 复现测试器首条 PASS 后退出，确认历史绿色报告与当前工件不一致；独立复核 Case/Test 数量、文件引用、hash 与入口；静态确认备份排除、恢复校验和包/命令检查缺陷。
- 因用户要求串行执行且禁止子 Agent，环境 Skill 的独立 RED/GREEN 前向测试未运行，行为状态保持 `Unverified`。

### Safety

- 未收录设备路径、用户名、产品版本或项目脚本作为普遍规则。
- 舍弃互相冲突的案例、占位测试和缺少原始执行证据的 Cold Start/Stop 成功结论。
- 未同步任何 Codex 或 Agent 实际 Skill 目录。

## [0.2.0] - 2026-09-08

### Added

- 新增互补 Skill `silvite-architecture-evolution`，用于多阶段底层替换、协议演进、跨平台/edition/仓库迁移和发布基础设施变化。
- 增加 Known-Good 基线、行为与身份不变量、现状架构审计、迁移台账、兼容窗口、扩展点准入和旧实现退役门禁。
- 增加 ProductVersion/Build/Commit/Channel 联合发布身份、信息暴露矩阵、密闭工具链和命令行为安全规则。
- 增加九层交付证据状态以及 8 个架构演进压力场景。

### Changed

- 在通用 `silvite-engineering-method` 中增加最小路由，保持通用治理与大型架构迁移职责分离。
- 更新 README 的双 Skill 安装、使用、目录与评测说明。
- 将公开仓库地址统一为 `LaoYinBai/Silvite-Engineering-Method`；不重写既有提交作者历史。

### Validation

- 新 Skill 通过 `skill-creator` 结构校验，核心文件与一级引用关系通过本地检查。
- 架构演进场景已建立，但因本轮明确采用单会话串行执行，未运行独立 Agent 的 RED/GREEN 前向测试；行为状态保持 `Unverified`。

### Safety

- 将项目使用经验去名称、去仓库服务和去私有实现后抽象为通用规则。
- 明确拒绝凭据复原、非公开接口调用、二进制下载与安全产品规避组成的危险验证链。

## [0.1.0] - 2026-08-29

### Added

- 建立目标、现状、系统图、最小闭环、受控执行、独立验证和准确报告的决策流程。
- 建立 Agent 最小权限、范围合同、脏工作树保护和高风险回滚边界。
- 建立 evidence-based completion、Known-Good baseline、observability、Shadow Mode、渐进控制和 fallback 规则。
- 增加复杂度预算、最小必要抽象、依赖方向和故障局部化指导。
- 增加项目驱动学习、陌生领域建模、根因分析与临时缓解生命周期。
- 增加公开压力场景、更新协议和公开安全检查表。

### Validation

- 使用 12 个基础工程压力场景检查跨项目判断；脱敏结果见 `evals/results-v0.1.md`。
- 使用无选项强压力场景识别脏工作树恢复点和临时 workaround 退出机制的真实缺口。
- 根据失败结果补充对应规则，而非复制项目案例。

### Safety

- 排除个人经历、产品专有细节、商业推演和公开性不确定的实现信息。
- 采用仓库维护者已选择的 MIT License。
