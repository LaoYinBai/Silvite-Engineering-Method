---
name: silvite-environment-engineering
description: Use when diagnosing, provisioning, cleaning up, isolating, relocating, decommissioning, recovering, or validating layered or host-isolated development environments across Linux, Windows, or macOS where shells, containers, virtual machines, remote sessions, PATH, package/runtime managers, launchers, configuration files, or generated reports may belong to different lifecycles or execution layers.
---

# Silvite Environment Engineering

## 核心原则

环境工程的完成状态由目标层上的真实能力、冷/新生命周期和可恢复证据决定，不由包已安装、文件存在、当前会话可用或报告写着 PASS 决定。

**REQUIRED BACKGROUND:** 同时使用 `silvite-engineering-method`。它负责通用目标、范围、权限、回滚和证据纪律；本 Skill 只增加分层与宿主机/隔离环境治理的专用门禁。

## 何时使用

适用于跨平台宿主机（Linux、Windows、macOS）、容器、VM、WSL、Proot、远程/桌面会话及多运行时管理器中的：

- 环境初始化、整理、隔离、迁移、重装或彻底退场；
- 启停入口、Shell 配置、`PATH` 污染/空壳劫持、多包管理器混装冲突与命令能力异常；
- “当前可用但重启失效”、warm path 通过而 cold path 失败；
- 备份恢复、诊断包脱敏边界或工件/报告验收。

## 环境合同

写入前建立最小合同（无法判断 `HOME`、`PATH` 或进程所属层时先读 [topology-and-lifecycle.md](references/topology-and-lifecycle.md)，不得用当前 Shell 的 `~` 代替目标层路径）：

```text
Environment Contract
- 当前执行层 / 目标能力所属层：
- 上游启动者 / 下游依赖与活跃消费者：
- HOME、PATH、配置与持久化面归属：
- warm / fresh shell / cold start 需验证的状态：
- 允许修改与明确排除的层：
- 回滚与恢复验证 / 完成证据：
```

## 工作流

### 1. 盘点拓扑、消费者与底座边界

先只读盘点并向用户对齐方案，再决定创建、替换或清理。入口必须位于目标环境启动前已经存在的上游层；目标环境内部唯一的启动入口不能证明冷启动可用。

- **宿主机底座极简**：全局 `PATH` 与管理器 `base` 只留全机刚需底座；业务依赖收敛到独立隔离环境；禁止子环境动态库、`bin`/`Scripts` 或捆绑私有子链留在全局 `PATH`；修正 OS 空壳（stub）与重复条目抢占。
- **消费者与硬链接审计**：删除或清理前扫描后台进程、服务、配置引用与跨环境硬链接，保护仍有活跃消费者的运行时；清缓存前用 `--dry-run` 区分纯缓存与硬链接共享包。

### 2. 分离状态与能力

不相互替代：`包可解析 → 包已安装 → 文件存在 → 可执行文件可解析 → 新会话已加载 → 真实操作成功 → 冷生命周期成功`。包名不一定是命令名，分别用包管理器、解析路径、版本与代表性操作证明。详见 [capability-and-state.md](references/capability-and-state.md)。

### 3. 受控变更、隔离迁移与退场

一次修改一个因果边界，先验证已有资产能否承担目标能力，不补齐无关工具。整理与迁移细则见 [runtime-isolation-and-relocation.md](references/runtime-isolation-and-relocation.md)：

- **禁止直接剪切与“旧路径幽灵存活”门禁**：含绝对路径绑定（启动器/wrapper、shebang、`pyvenv.cfg`、元数据、Shell init）的环境严禁直接移动目录。必须按“备份前态 → 重定位默认配置 → 新位置克隆/重建 → 扫描并重绑入口内残余旧前缀与过期前缀 → 验证新环境独立可用 → 删旧并复验”执行；未完成旧前缀零残留审计前禁止删旧。
- **混装清理与防误装护栏**：在混用过主/二级包管理器的环境批量卸载后，立即执行主管理器自检与二级依赖校验，补回被覆盖拆掉的共享底座依赖；全局防误装护栏须通过环境级作用域放行合法隔离环境。
- **全持久化面退场**：彻底卸载须清零包管记录、磁盘目录、环境变量、Shell Profile、OS 注册表/启动项/计划任务/后台服务，并在新会话验证 `NOT_FOUND`。

### 4. 验证真实生命周期

| 声明 | 最低证据 |
|---|---|
| 包已安装 / 命令可用 | 目标层包管理器状态 / 解析到的真实路径与版本 |
| 配置已加载 / 功能可用 | 新建目标类型会话核对生效状态 / 等价端到端探针 |
| 启动入口持久 / 停止完成 | 终止上游状态后从唯一公开入口启动 / 进程与锁按合同收敛 |
| 可恢复 | 受控样本上完成恢复并验证行为，而非只有备份文件 |

涉及 `PATH`、环境变量或激活配置变更时，必须剥离当前进程继承的激活变量、从持久化存储重载配置，并在用户全部常用壳层（如 PowerShell + CMD，或 bash + zsh）冷启验证首命中解析顺序、默认环境状态、子环境切换与真实执行。无法执行冷启动或恢复演练时，准确停在 `Unverified`。

### 5. 验证证据生成器

报告与绿色标记只是待验证输入，最终验收须能从当前工件独立重建：检查运行器全程执行与退出码（防交互取消、`set -e` 或旧进程提前退出）、枚举集合与当前版本一致、分别计算全集/增量集/阶段集、所有引用文件存在且路径/SHA256/入口指向同一工件、探针断言实际行为。冲突时以工件与可重放结果为准。详见 [evidence-and-recovery.md](references/evidence-and-recovery.md)。

### 6. 建立备份—恢复闭环与隐私边界

备份前冻结包含/排除/敏感/递归边界，验证排除参数真实进入归档命令；校验和缺失或不匹配时 fail closed；解包前检查成员路径与链接目标并先在隔离位置预演；dry-run 须真实解析参数且不写入；恢复前保护当前目标并保留回退点。诊断包仅声明已人工审查的敏感面，禁止用白名单环境变量宣称自动脱敏。

## 证据状态

```text
Inventoried → Located at Correct Layer → Statically Valid → Resolved in Fresh Session → Functionally Verified → Cold-Lifecycle Verified → Recovery Verified
```

各状态不可跳跃。最终报告列出已达到的最高状态、原始证据、未运行验证与剩余风险。

## 核心反模式（示例）

| 错误 | 修正 |
|---|---|
| 在当前 Shell 用 `~` 检查另一层，或用包名代替命令解析 | 先证明当前层与目标层，再分别验证包状态、真实路径与功能 |
| 旧环境未删前测新克隆通过就直接删旧 | 先清零克隆体入口/wrapper/shebang 的旧前缀引用，删旧后再冷启复验 |
| 混装环境只跑二级卸载就宣布纯净 | 立即做主管理器自检与依赖校验，补回被拆掉的共享底座包 |
| 仅凭 `source`、当前热会话、包 hash 或“新增数”宣布持久/全部通过 | 剥离继承态做多壳层冷启，并从当前 artifact 重新计数与重放 |

## 停止条件

出现以下任一情况，停止写入并准确报告：目标层不明确；必须修改未授权层或提权受阻（停止该层写入、保留前态备份并可交付带断言的审阅脚本，严禁绕过）；没有可恢复基线；未清零活跃消费者或克隆体旧前缀引用；校验和或归档成员检查失败；测试器提前退出或报告与工件冲突；冷生命周期或恢复演练不可执行但属完成条件。
