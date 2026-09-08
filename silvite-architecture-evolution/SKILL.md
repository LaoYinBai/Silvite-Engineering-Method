---
name: silvite-architecture-evolution
description: Use when work requires a multi-stage cross-module architecture migration, underlying subsystem replacement, protocol evolution, cross-platform unification, multi-edition or multi-repository compatibility, release infrastructure migration, or a stable boundary for an explicit future capability.
---

# Silvite Architecture Evolution

## 核心原则

允许真正的大型架构演进，但必须用冻结基线、行为不变量、迁移切片、兼容窗口和分层证据避免大爆炸替换、过度设计与不可验证完成。

**REQUIRED BACKGROUND:** 同时使用 `silvite-engineering-method`。由它负责通用目标、范围、权限、可逆性和证据纪律；本 Skill 只增加架构迁移专用门禁。

## 触发分类

满足任一条件时加载本 Skill：

- 跨模块重构或底层实现替换；
- 协议、传输、状态机或平台适配层演进；
- 多平台统一或共享语义重构；
- 多 edition、多仓库的共享核心迁移；
- 构建、打包、更新或发布基础设施变化；
- 为已有明确场景的未来能力建立兼容边界；
- 需要新旧实现并存、逐步启用、真实升级或分阶段退役。

局部修复、单模块可逆重构或不改变架构边界的维护，只使用 `silvite-engineering-method`。

## 必须执行的阶段

按顺序维护以下清单，不得跳过门禁：

```text
Architecture Evolution Progress:
- [ ] 0. 分类任务并确认范围
- [ ] 1. 冻结 Known-Good 基线
- [ ] 2. 建立现状架构图
- [ ] 3. 定义行为与身份不变量
- [ ] 4. 设计目标边界并审查扩展点
- [ ] 5. 建立迁移台账
- [ ] 6. 按依赖顺序迁移切片
- [ ] 7. 逐切片验证并记录证据状态
- [ ] 8. 通过兼容与发布门禁
- [ ] 9. 退役旧实现或保存可恢复进度点
```

### 0. 分类与范围

写明迁移类型、用户可观察结果、明确排除项、允许变更的模块/仓库/platform/edition、兼容窗口与人工决策点。生成器、格式化器或共享脚本也必须受排除范围约束。

### 1–3. 基线、现状与不变量

跨模块写入前完整读取 [baseline-and-invariants.md](references/baseline-and-invariants.md) 与 [architecture-audit.md](references/architecture-audit.md)。没有可恢复基线，不得开始迁移写入。

验收围绕行为、身份、数据和兼容不变量，不围绕“新架构更整洁”。Discovery、Connecting、认证、传输和业务 Ready 必须拥有不同语义与权限，禁止隐式升级状态或副作用。

### 4. 目标边界

定义职责、状态所有权、生命周期、依赖方向、平台适配、错误传播和 fallback。需要版本、协议或未来能力时读取 [compatibility-and-versioning.md](references/compatibility-and-versioning.md)。

只为明确能力和已知变化轴保留最小扩展槽。当前功能仍保持一条清晰路径；没有能力时核心必须可降级。

### 5–7. 切片迁移与验证

按 [migration-slicing.md](references/migration-slicing.md) 建立台账。默认顺序：

```text
契约与模型
→ 纯逻辑
→ 平台适配
→ 状态机
→ 调用方
→ UI
→ 构建与打包
→ 发布
```

每个切片只允许一个高耦合行为边界写入者。切片必须包含回滚、启用和旧代码删除条件；在验证前不得进入 `Migrated`，在所有调用方和恢复路径验证前不得进入 `Retired`。

### 8. 兼容与发布

跨平台、edition 或仓库时完整读取 [cross-platform-and-editions.md](references/cross-platform-and-editions.md)。目标是行为与契约一致，不是目录、补丁或 Commit 相同。

产生可分发构建或发布时完整读取 [release-evidence-gates.md](references/release-evidence-gates.md)。必须验证实际客户端的版本比较规则；ProductVersion、Build、Commit、Channel、Tag、manifest、Asset 和安装包不得各自独立“看起来正确”。

### 9. 退役或停工

只有满足台账中的删除条件才能移除旧实现。停工时记录当前阶段、已完成与未完成切片、Git 状态、测试状态、最后 Known-Good、下一步唯一入口和未验证风险，使“继续进度”不依赖猜测。

## 关键门禁速查

| 门禁 | 必须回答 | 不通过时 |
|---|---|---|
| 基线 | 能否精确恢复代码、产物、配置和用户状态？ | 停止跨模块写入 |
| 不变量 | 哪些行为、身份、数据和 edition 隔离不得改变？ | 不开始目标设计 |
| 架构 | 谁拥有状态、生命周期、权限和副作用？ | 先补现状图或最小实验 |
| 扩展点 | 是否有明确能力、稳定语义、协商、fallback 和测试？ | 不建立扩展点 |
| 切片 | 是否有单一结果、兼容策略、启用/删除条件和回滚？ | 不迁移该片 |
| 发布身份 | 现有客户端能否识别并安全升级到候选？ | 不发布 |
| 命令行为 | 行为链是否接触凭据、私有接口、二进制或安全产品？ | 使用安全替代或请求明确授权 |
| 完成 | 当前证据实际支持到哪个层级？ | 停留在准确状态 |

## 迁移台账条目

每个切片至少记录：

```text
切片 ID 与目标：
当前入口 / 目标入口：
行为与身份不变量：
修改模块、平台、edition、仓库：
明确排除项：
兼容策略与窗口：
测试与真实环境证据：
回滚点：
启用条件：
旧实现删除条件：
状态：Planned | Implemented | Verified | Migrated | Retired
```

## 分层证据状态

严格区分并按证据推进：

```text
Code Complete
→ Tests Passed
→ Build Produced
→ Artifact Inspected
→ Remote Published
→ Remote Independently Verified
→ Installed
→ Upgrade Verified
→ User Accepted
```

前一状态不蕴含后一状态。缺少目标环境、远端、安装、升级或用户证据时，准确报告停止位置与 `Unverified` 项。

## 并发边界

- 高耦合迁移按依赖顺序串行。
- 同一文件或同一行为边界只允许一个写入者。
- 只把相互独立的只读审计或独立验证并行化。
- 验证者只接收原始任务、必要工件和最小上下文；不提供预期答案或疑似根因。
- 主执行者重新读取完整输出并独立复核结论。

用户或宿主禁止并行执行时，全部串行，并将缺少独立验证如实标记为 `Unverified`。

## 特殊风险路由

- 使用内置 ADB、Git、runtime 或其他随包工具时，完整读取 [hermetic-toolchains.md](references/hermetic-toolchains.md)。
- 命令涉及反射、非公开接口、凭据、下载/生成/执行二进制、签名或安全软件时，执行前完整读取 [command-security-gate.md](references/command-security-gate.md)。
- “只读验证”只描述写入意图，不代表行为低风险。

## 常见错误与红旗

| 错误 | 修正 |
|---|---|
| 一次替换整条链路 | 建立 seam，新旧并存，逐个端到端切片迁移 |
| 机械 cherry-pick 等同同步 | 建立语义矩阵，分仓验证行为和契约 |
| Build 递增等同可更新 | 测试已安装客户端的实际比较谓词 |
| 共享对象直接暴露全部身份 | 用信息暴露矩阵限制每个消费者获得的字段 |
| Discovery 为方便而自动 Connecting | 分离能力、事件、权限与状态所有权 |
| 内置工具失败后静默使用系统版本 | 固定解析路径、版本、环境和缓存边界 |
| 只读脚本接触凭据并下载可执行文件 | 评估组合行为，改用受支持的隔离验证路径 |
| “主要完成”作为恢复入口 | 从进度存档、Git 和测试证据恢复，不猜现场 |

出现以下任一情况立即停止当前写入：基线不可恢复；不变量互相冲突；必须扩大未授权仓库或 edition；需要提取真实凭据；需要关闭安全产品；实际版本比较规则未知；回滚窗口不足；完成状态只能靠叙述推断。

