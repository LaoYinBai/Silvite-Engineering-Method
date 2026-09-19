---
name: silvite-environment-engineering
description: Use when diagnosing, provisioning, recovering, or validating layered Linux development environments where shells, containers, virtual machines, remote sessions, package managers, launchers, configuration files, or generated reports may belong to different lifecycles or execution layers.
---

# Silvite Environment Engineering

## 核心原则

环境工程的完成状态由目标层上的真实能力、冷/新生命周期和可恢复证据决定，不由包已安装、文件存在、当前会话可用或报告写着 PASS 决定。

**REQUIRED BACKGROUND:** 同时使用 `silvite-engineering-method`。它负责通用目标、范围、权限和可逆性；本 Skill 只增加 Linux 与分层开发环境的专用门禁。

## 何时使用

适用于 Linux 主机、容器、VM、WSL、Proot、远程 Shell、桌面会话或类似多层环境中的：

- 开发环境初始化、修复、迁移或重装；
- 启停入口、Shell 配置、PATH、包与命令能力异常；
- “当前可用但重启失效”、warm path 通过而 cold path 失败；
- 备份、恢复、诊断包、基线或验收报告；
- 声称已安装、已加载、可执行、可连接或已恢复，但证据层级不清。

单仓代码修改且不涉及运行环境生命周期时，只使用通用 Skill。多阶段底层架构迁移同时使用 `silvite-architecture-evolution`。

## 环境合同

写入前建立以下最小合同：

```text
Environment Contract
- 当前执行层：
- 目标能力所属层：
- 上游启动者 / 下游依赖：
- HOME、PATH、配置与状态文件的实际归属：
- warm / fresh shell / cold start 中需要验证的状态：
- 允许修改与明确排除的层：
- 回滚与恢复验证：
- 完成证据：
```

无法判断 `HOME`、PATH、进程或配置属于哪一层时，先读取 [topology-and-lifecycle.md](references/topology-and-lifecycle.md)，不得用当前 Shell 的 `~` 代替目标层路径。

## 工作流

### 1. 发现拓扑与资产

先识别执行边界、生命周期和已有入口，再决定是否创建或替换资产：

```text
宿主 / 会话管理层
→ 隔离或来宾环境
→ 桌面或服务会话
→ 应用与工具
```

对每个脚本、alias、rc 文件、socket、进程和状态文件记录其所有者、创建者、消费者及失效时点。入口必须位于目标环境启动前已经存在的上游层；目标环境内部唯一的启动入口不能证明冷启动可用。

### 2. 分离状态与能力

不要把以下状态相互替代：

```text
包可解析 → 包已安装 → 文件存在 → 可执行文件可解析
→ 新会话已加载 → 真实操作成功 → 冷生命周期成功
```

包名不一定是命令名。分别使用包管理器证明安装状态，使用真实二进制名称、解析路径、版本与代表性操作证明能力。详细检查见 [capability-and-state.md](references/capability-and-state.md)。

### 3. 设计最小变化

- 一次修改一个因果边界；记录预期作用、前态、后态和回滚。
- 先验证已有资产能否承担目标能力；“文件存在”不是 proven path。
- 不因缺少无关 SDK、工具或常见目录就补齐环境。
- 当前状态稳定只意味着停止无目标改动，不意味着未执行的 cold、恢复或隐私验收自动通过。

### 4. 验证真实生命周期

验证方式必须匹配声明：

| 声明 | 最低证据 |
|---|---|
| 包已安装 | 目标层包管理器状态 |
| 命令可用 | 目标层解析到的真实路径与版本 |
| 配置已加载 | 新建目标类型的会话后检查生效状态 |
| 功能可用 | 用户实际操作或等价端到端探针 |
| 启动入口持久 | 真正终止上游状态后，从唯一公开入口启动 |
| 停止完成 | 目标进程、socket、锁和状态文件按合同收敛 |
| 可恢复 | 受控样本上完成恢复并验证行为，而非只有备份文件 |

无法执行目标设备、GUI、冷启动或破坏性恢复演练时，报告精确停在 `Unverified`，不得用静态检查或 warm path 补位。

### 5. 验证证据生成器

报告、绿色标记和历史结论只是待验证输入。最终验收必须能从当前工件独立重建。接受结果前检查：

- 运行器是否从头到尾执行并保留退出码；
- 枚举的测试、脚本与当前工件版本是否一致；
- 报告引用的每个文件、测试入口和清单项是否真实存在；
- “新增 N 个”“本阶段 N 个”“总计 N 个”是否按各自集合重新计数，禁止互相替代；
- PASS/WARN/FAIL 计数能否由原始输出重建；
- 路径、版本、SHA256、权限与脚本入口是否指向同一份工件；
- 探针是否断言目标行为，而非只执行了命令或管道末端成功；
- 测试是否可能因交互输入、超时、旧进程或 `set -e` 提前退出；
- 报告是否由本次运行生成，而非手工沿用旧统计。

报告与 artifact 冲突时，以 filesystem、脚本、manifest、hash、入口和可重放结果为准；同时记录冲突本身为验收链 Failure Mode。测试器本身失败时，业务结论保持未知。详见 [evidence-and-recovery.md](references/evidence-and-recovery.md)。

### 6. 建立备份—恢复闭环

备份与恢复是一个能力，不能分别凭叙述验收：

- 备份前明确包含项、排除项、敏感数据边界和递归边界；
- 验证排除规则实际进入归档命令，而非只显示在日志或 manifest；
- 校验和缺失或不匹配时 fail closed，除非用户明确授权例外；
- 解包前检查成员路径和链接目标，恢复到隔离位置预演；
- dry-run 必须解析真实参数且不写入，不以“需要确认”冒充 dry-run；
- 恢复前保护当前目标，恢复后验证功能并保留明确回退点。

诊断包只能声明已检查的敏感面。进程命令行、路径、网络配置和工具输出都可能泄露信息；未经内容审查不得声称“自动脱敏、可以安全分享”。

## 证据状态

```text
Inventoried
→ Located at Correct Layer
→ Statically Valid
→ Resolved in Fresh Session
→ Functionally Verified
→ Cold-Lifecycle Verified
→ Recovery Verified
```

各状态不可跳跃。最终报告列出已达到的最高状态、原始证据、未运行验证与剩余风险。

## 常见错误

| 错误 | 修正 |
|---|---|
| 在当前 Shell 用 `~` 检查另一层文件 | 先证明当前层和目标层，再使用该层可解释的路径 |
| 包存在就宣布功能可用 | 分别验证包、二进制、加载状态和真实操作 |
| `source` 后成功就宣布持久 | 用新会话；涉及启动链时再用真正 cold start |
| 当前已有进程就称启动脚本已验证 | 清理 warm state，从公开入口重放完整生命周期 |
| 看到 PASS 报告就接受 | 核对工件版本、全程输出、退出码、计数和断言 |
| 把“新增 3 个”写成“总共 3 个” | 分别定义全集、增量集与当前阶段集，再从文件系统计数 |
| 验收表引用不存在的文件 | 对全部引用执行存在性、类型、版本与 hash 对应检查 |
| 备份列出排除项就称不含凭据 | 检查归档参数并审计实际成员 |
| 有压缩包就称可恢复 | 在隔离目标完成校验、恢复和功能验证 |
| 诊断脚本使用白名单环境变量就称完全脱敏 | 审查所有采集源和最终文件，只声明已覆盖范围 |

## 停止条件

出现以下任一情况，停止写入并准确报告：目标层仍不明确；必须修改未授权层；没有可恢复基线；校验和失败；归档成员不安全；测试器提前退出；报告与当前工件不一致；冷生命周期或恢复演练无法执行但又是完成条件。
