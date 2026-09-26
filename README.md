<!--
GitHub About:
A reusable Agent-native software engineering method for scoped execution, evidence-based verification, complexity control, and reversible change.

Topics:
ai-agents, agentic-coding, codex, software-engineering, engineering-methodology, developer-tools, agent-skill, vibe-coding
-->

# 🧭 Silvite Engineering Method

> 让 Agent 写得更快之前，先让它知道：**要做什么、哪里不能碰、什么才算完成。**

**Silvite Engineering Method** 是一套面向 AI Coding Agent 的可复用软件工程 Skill 组合：

- `silvite-engineering-method`：通用工程治理，负责目标、范围、权限、可逆性、复杂度和证据。
- `silvite-architecture-evolution`：大型架构演进，负责冻结基线、行为不变量、迁移切片、兼容窗口和发布门禁。
- `silvite-environment-engineering`：Linux 与分层开发环境工程，负责环境拓扑、生命周期、能力状态、冷启动和恢复证据。

它不教 Agent 某一种语言，也不规定某一种架构。

它更关心真实工程里那些很容易被“代码生成速度”掩盖的问题：

- 🎯 任务真正要交付的结果是什么？
- 🧱 修改边界到底在哪里？
- 🔍 现在知道的是事实，还是只是推测？
- 🧩 什么时候应该抽象，什么时候应该保持简单？
- 🛡️ 高风险操作有没有可靠的恢复路径？
- ✅ Agent 说“完成了”，有什么证据？
- 🚦 自动化能力什么时候才有资格真正接管？
- 🗺️ 进入陌生技术栈时，应该先从哪里理解系统？
- 🐧 Host、Guest、Container、VM 或 Shell 的结论是否落在正确层？
- 🧾 绿色报告能否从当前 artifact 和真实执行结果独立重建？
- 🧰 用户还没有收到成果时，Agent 是否先跑去建设工具和基础设施？

它的目标不是让 Agent 变得更谨慎、更啰嗦。

而是让 Agent 在拥有高吞吐执行能力以后，仍然保持：

**边界、判断、证据与可逆性。**

大型重构使用通用 Skill 与架构演进 Skill；分层 Linux / 开发环境任务使用通用 Skill 与环境工程 Skill。互补 Skill 不替代通用治理，也不把所有日常修改升级成重型流程。

---

## ✨ 它是什么

AI 已经可以非常快地：

- 写代码
- 改代码
- 搜索仓库
- 重构模块
- 运行命令
- 分析日志
- 修改配置
- 生成测试
- 跨多个文件完成复杂任务

这大幅降低了软件实现本身的成本。

但一个新的问题也随之出现：

> **Agent 能改多少代码，已经逐渐不再是主要瓶颈。  
> 真正的瓶颈开始变成：它究竟应该改什么。**

一个 Agent 可以在几分钟内修改几十个文件。

但如果目标错了、边界错了、抽象错了，或者验证方式错了，那么更高的执行速度只会让错误扩散得更快。

因此 Silvite Engineering Method 更关注：

```text
目标
 ↓
系统
 ↓
边界
 ↓
失败模式
 ↓
最小闭环
 ↓
执行
 ↓
证据
 ↓
反馈
```

代码只是这条链路中的一部分。

---

## 🤖 关于 Agent-native 软件工程

传统的软件开发流程中，人的实现速度天然限制了改动规模。

一个开发者想进行大规模修改，需要花费大量时间。

这种低吞吐本身，在某种程度上就是一种天然的风险限制。

而 Agent 改变了这件事。

现在，一个人可以把：

```text
需求理解
架构分析
代码实现
测试
重构
日志分析
文档整理
重复操作
```

中的大量执行工作交给 Agent。

于是人的职责开始发生变化。

更重要的工作逐渐变成：

> **定义目标。**

> **划定边界。**

> **判断复杂度是否值得。**

> **决定什么证据足够。**

> **对最终结果负责。**

因此，这套 Skill 的一个基本观点是：

**Agent 是高吞吐执行层，而不是目标、风险与完成状态的最终裁决者。**

---

## 🧠 核心原则

### 🎯 1. 从结果倒推，而不是从代码正推

一个工程任务不应该从：

> “我要改哪几个文件？”

开始。

而应该先回答：

> “用户或系统最终应该观察到什么变化？”

然后倒推：

```text
Outcome
   ↓
Dependencies
   ↓
System boundaries
   ↓
Failure modes
   ↓
Minimal end-to-end slice
   ↓
Implementation
   ↓
Evidence
```

如果连最终结果都无法明确，那么“代码已经写完”没有太大意义。

---

### 🧱 2. 高吞吐能力，不等于更大的权限

Agent 能做到某件事，不意味着它应该做。

默认行为应该包括：

- 🔎 诊断优先只读
- 📏 修改范围与目标保持对应
- 🧹 不顺手清理无关代码
- 🗃️ 不擅自覆盖未知用户改动
- 🔐 权限只提升到当前步骤真正需要的程度
- ↩️ 高风险修改提前建立恢复路径
- ⛔ 边界、风险或权限发生变化时停止重新确认

一句话：

> **能执行，不等于应该执行。**

---

### ✅ 3. 代码写完，不等于工程完成

Agent 最容易产生的一种错觉是：

```text
代码修改完成
=
任务完成
```

但真实工程通常不是这样。

Silvite Engineering Method 将任务状态明确区分为：

| 状态 | 含义 |
|---|---|
| ✅ `Completed` | 请求结果与必要回归已经获得新鲜证据 |
| 🩹 `Mitigated` | 影响已经被控制，但根因或长期方案尚未验证 |
| ⚠️ `Unverified` | 实现已经存在，但关键验证仍然缺失 |
| 🚫 `Blocked` | 缺少权限、环境、信息或安全恢复路径 |

如果测试没有运行，就说明没有运行。

如果目标环境没有验证，就说明没有验证。

如果只是通过重启、重试或降级恢复了服务，就不应该把它描述成：

> “根因已经修复。”

**准确描述系统状态，本身就是工程能力的一部分。**

---

### 🧩 4. 架构的目的，是控制复杂度

抽象不是越多越好。

一个新的接口、层级、框架或通用模块，在加入系统之前应该回答：

1. 当前真实存在什么重复？
2. 当前已经出现了什么变化轴？
3. 这些共同点是语义一致，还是只是长得相似？
4. 抽象以后是否减少了调用方需要理解的内容？
5. 是否让故障更容易局部化？
6. 如果未来需求永远不出现，这个抽象今天仍然值得吗？

如果一个抽象需要：

```text
大量布尔开关
大量类型判断
大量特殊分支
大量尚未使用的扩展点
```

才能维持统一，

那往往意味着真正的边界并不在那里。

有时候：

> **保留少量清晰的重复，比建立错误的统一更便宜。**

通用 Skill 另设 [Direct Execution Before Tooling](SKILL.md)：少量、一次性且低风险的工作默认直接完成。出现工具和治理文件持续增加、正式交付物仍为零时，触发 `ZERO-DELIVERABLE WARNING`，先产出第一个可验收成果。批量高风险操作需要最小必要的预览、自动化和恢复能力。

---

### 🔍 5. 先理解现状，再修改系统

遇到 Bug 时：

```text
现象
≠
根因
```

一个重试解决了现象，不代表问题来自“重试不足”。

一个 sleep 解决了竞态，不代表正确方案就是永久 sleep。

一个重启恢复服务，也不代表故障已经被修复。

更可靠的路径通常是：

```text
观察
 ↓
保全证据
 ↓
建立假设
 ↓
设计最小实验
 ↓
验证 / 反证
 ↓
定位根因所在层
 ↓
最小修复
 ↓
回归验证
```

**Workaround 可以是正确的临时策略。**

但 workaround 不应该通过改名字变成“根因修复”。

---

### ↩️ 6. 可逆性优先于勇气

高权限本身不是问题。

没有边界、没有恢复点地使用高权限才是问题。

对于高风险写操作，推荐：

```text
检查
 ↓
预览
 ↓
执行
 ↓
验证
```

执行前先回答：

- 精确目标是什么？
- 会修改什么？
- 最坏情况下会影响哪里？
- 如何停止？
- 如何恢复？
- 恢复方案真的验证过吗？

> **“有备份”不等于“能够恢复”。**

---

### 🚦 7. 先观察，再自动控制

当一个自动化系统准备替代人工判断或 Known-Good 策略时，不应该因为：

> “离线测试效果不错”

就直接获得完整控制权。

更合理的路径是：

```text
Known-Good baseline
        ↓
Observability
        ↓
Shadow Mode
        ↓
Limited Control
        ↓
Progressive Rollout
        ↓
Continuous Monitoring
        ↓
Fallback
```

先让系统证明：

**它知道发生了什么。**

然后再让它证明：

**它知道应该怎么做。**

最后才逐渐给它真正的控制权。

---

### 🗺️ 8. 陌生技术，先找到它在系统里的位置

遇到一个自己从未使用过的技术时，两个极端都没有必要。

一种是：

> “我不会，先把整套理论学完再开始。”

另一种是：

> “先让 Agent 写，炸了再说。”

更有效的方式是先回答：

- 它解决什么问题？
- 它属于系统哪一层？
- 上游是什么？
- 下游是什么？
- 状态在哪里？
- 数据如何流动？
- 失败会传播到哪里？
- 哪一步具有不可逆风险？
- 最小安全实验是什么？

然后让真实问题暴露知识缺口。

再定向补齐真正需要的理论。

---

## 🔄 默认研发流程

对于非平凡工程任务，这套 Skill 使用七步闭环：

### 1. 🎯 定义结果

明确：

- Outcome
- Evidence
- In Scope
- Out of Scope
- Constraints

---

### 2. 🔍 理解现状

检查：

- 代码
- 状态
- 依赖
- 测试
- 日志
- 版本
- 当前工作树
- 已知问题

并区分：

```text
事实
推断
未知
```

---

### 3. 🗺️ 建立系统图

识别：

- 组件
- 边界
- 依赖方向
- 状态
- 数据流
- 外部条件
- 失败模式
- 故障传播范围

---

### 4. 🧩 找到最小闭环

优先完成一个：

**能够端到端证明方向正确的最小切片。**

而不是先把整个未来架构搭出来。

---

### 5. 🛠️ 受控执行

只修改当前目标真正需要的范围。

如果执行途中发现必须：

- 修改公共接口
- 改变数据语义
- 改变兼容承诺
- 修改生产配置
- 扩大权限
- 修改原本无关模块

就重新评估任务边界。

---

### 6. ✅ 独立验证

根据风险选择合适证据：

- 单元测试
- 集成测试
- 构建
- 静态检查
- 日志
- 实机
- 目标环境
- 可复现实验
- 数据一致性
- 回滚演练

验证强度应该和风险成比例。

---

### 7. 📋 准确报告

最终报告至少应该回答：

- 改了什么？
- 没改什么？
- 验证了什么？
- 哪些验证没有运行？
- 当前状态属于 `Completed / Mitigated / Unverified / Blocked` 中哪一个？
- 还剩什么风险？
- 回退点在哪里？

---

## 🧪 这套 Skill 怎么测试？

Silvite Engineering Method 不把：

> “这几条原则听起来很合理。”

当成有效性的证明。

仓库使用压力场景进行：

```text
Control
Agent without Skill

        VS

Treatment
Agent with Skill
```

关注的不是 Agent 说话像不像某种风格。

而是它的**工程决策有没有真正变化**。

目前测试覆盖包括：

- 🧨 模糊的大规模重构
- 🐛 根因未知的生产故障
- 🌳 脏工作树上的跨模块修改
- 🧹 范围外的顺手重构
- ⏱️ 回滚窗口早于测试结束
- 🏗️ 预测性过度架构
- 🧩 插件故障拖累核心
- 🤖 自动策略准备接管生产
- 🗺️ 首次进入陌生技术栈
- 🌐 开发与生产环境漂移
- 💾 高风险数据迁移
- 🩹 Workaround 被要求包装成最终修复
- 🧰 少量资产任务被工具建设拖走，正式成果长期为零
- 🗂️ 高风险批量变换被误当作应当手工逐项完成

架构演进候选评测另外覆盖：

- 同 ProductVersion 仅增加 Build 导致更新不可发现
- 多仓库、平台和 edition 的语义同步冲突
- 内部 Build/Commit 泄露到普通 UI
- Discovery 隐式触发 Connecting
- 系统工具污染随包密闭工具链
- 凭据复原与二进制下载形成高风险行为链
- 长任务中断后缺少可恢复进度点
- 明确排除的仓库被共享生成器误修改

环境工程候选评测另外覆盖：

- 测试器提前退出但报告保持绿色
- 启动入口错误地位于目标环境内部
- 备份排除列表未进入实际归档操作
- 包名与命令名混淆
- 诊断包脱敏声明超过真实审查范围
- 校验和失败后仍继续恢复
- “新增数量”被错误解释为“总数”
- 报告引用、hash、入口与受测工件不是同一版本

早期 Eval 曾经出现过一个很重要的结果：

**Skill 本身也会犯错。**

某条自动化规则曾被过度泛化到不适用的工程场景。

因此规则被重新收紧。

这也是这个仓库希望长期保持的一种状态：

> **不是证明方法永远正确，而是不断寻找它什么时候会错。**

详细场景与结果：

- [`evals/scenarios.md`](evals/scenarios.md)
- [`evals/results-v0.1.md`](evals/results-v0.1.md)
- [`evals/architecture-evolution-scenarios.md`](evals/architecture-evolution-scenarios.md)
- [`evals/architecture-evolution-results-v0.2.md`](evals/architecture-evolution-results-v0.2.md)
- [`evals/environment-engineering-scenarios.md`](evals/environment-engineering-scenarios.md)
- [`evals/environment-engineering-results-v0.3.md`](evals/environment-engineering-results-v0.3.md)

架构演进和环境工程场景已完成设计；没有运行独立 Agent 的 RED/GREEN 前向测试时，其行为验证状态明确为 `Unverified`。

---

## 🛠️ 安装

先克隆仓库：

例如：

```bash
git clone https://github.com/LaoYinBai/Silvite-Engineering-Method.git
```

再把需要的 Skill 分别放入宿主支持的 Skills 目录。以 `~/.agents/skills` 为例：

```bash
mkdir -p ~/.agents/skills/silvite-engineering-method
cp SKILL.md ~/.agents/skills/silvite-engineering-method/
cp -R references ~/.agents/skills/silvite-engineering-method/
cp -R silvite-architecture-evolution ~/.agents/skills/
cp -R silvite-environment-engineering ~/.agents/skills/
```

如果只需要通用工程治理，安装第一个即可。大型架构迁移或分层环境工程分别安装并同时加载对应的互补 Skill。如果宿主使用其他 Skill 路径，请按对应规则放置。

安装后可以显式调用：

```text
使用 $silvite-engineering-method 处理这次跨模块修改。

先明确目标、修改边界、失败模式、验证方式和回滚路径，
再开始实现。
```

大型架构迁移可以这样调用：

```text
同时使用 $silvite-engineering-method 和 $silvite-architecture-evolution。

先冻结 Known-Good、行为不变量和回滚点，建立迁移台账，
再按依赖顺序逐切片迁移，并分别报告代码、测试、产物、发布和升级状态。
```

Linux / 开发环境工程可以这样调用：

```text
同时使用 $silvite-engineering-method 和 $silvite-environment-engineering。

先识别执行层、配置归属与生命周期，再用当前 artifact、真实入口、
新会话或 cold path 以及恢复演练建立可重建证据。
```

支持自动 Skill Discovery 的 Agent，也可以根据 `SKILL.md` 中的描述自动触发。

---

## 📂 仓库结构

```text
Silvite-Engineering-Method/
│
├── SKILL.md
├── README.md
├── CHANGELOG.md
├── SOURCES.md
├── UPDATE_GUIDE.md
├── PUBLICATION_CHECKLIST.md
│
├── references/
│   ├── engineering-principles.md
│   ├── agent-boundaries.md
│   ├── verification.md
│   ├── complexity-control.md
│   ├── system-thinking.md
│   ├── debugging-and-recovery.md
│   ├── project-driven-learning.md
│   └── anti-patterns.md
│
├── silvite-architecture-evolution/
│   ├── SKILL.md
│   ├── agents/
│   │   └── openai.yaml
│   └── references/
│       ├── baseline-and-invariants.md
│       ├── architecture-audit.md
│       ├── migration-slicing.md
│       ├── compatibility-and-versioning.md
│       ├── cross-platform-and-editions.md
│       ├── release-evidence-gates.md
│       ├── hermetic-toolchains.md
│       └── command-security-gate.md
│
├── silvite-environment-engineering/
│   ├── SKILL.md
│   ├── agents/
│   │   └── openai.yaml
│   └── references/
│       ├── topology-and-lifecycle.md
│       ├── capability-and-state.md
│       └── evidence-and-recovery.md
│
└── evals/
    ├── README.md
    ├── scenarios.md
    ├── results-v0.1.md
    ├── architecture-evolution-scenarios.md
    ├── architecture-evolution-results-v0.2.md
    ├── environment-engineering-scenarios.md
    └── environment-engineering-results-v0.3.md
```

### `SKILL.md`

只保留真正会改变 Agent 决策的核心规则。

### `references/`

存放更完整的：

- 工程原则
- Agent 权限边界
- 验证方法
- 复杂度控制
- 系统思维
- Debug 与恢复
- 项目驱动学习
- 常见反模式

### `silvite-architecture-evolution/`

独立可安装的互补 Skill。核心 `SKILL.md` 只保留阶段与门禁，详细迁移检查表放在一级 `references/`，避免扩写通用 Skill。

### `silvite-environment-engineering/`

独立可安装的互补 Skill。处理分层运行环境、Shell/包能力、冷生命周期、证据生成器与备份恢复，不把单一设备路径或项目脚本写成普遍规则。

### `evals/`

用于验证：

> **这些规则到底有没有真的改变 Agent 的行为。**

---

## 🌱 它如何继续成长

这个仓库不是一次写完以后冻结的方法论。

新的规则应该尽量来自：

**真实失败。**

推荐的更新路径是：

```text
真实问题
   ↓
Agent 做出了不理想的决策
   ↓
记录可观察后果
   ↓
建立 Eval
   ↓
RED
   ↓
修改已有规则
   ↓
GREEN
   ↓
检查是否产生新的副作用
   ↓
Public Safety Review
```

如果一个新认知：

- 只适用于一个项目
- 没有真实失败支持
- 不改变实际工程决策
- 可以被已有原则覆盖

那么它通常没有必要进入核心 Skill。

> **优先修正规则，而不是无限增加规则。**

完整更新流程见：

[`UPDATE_GUIDE.md`](UPDATE_GUIDE.md)

---

## 🔐 Public by Design

这个仓库公开的是：

**工程方法。**

而不是具体项目的内部事实。

公开 Skill 主动排除：

- 🔑 密钥、Token、凭据
- 👤 用户和私人数据
- 🗄️ 私有仓库与私有代码
- 🌐 内部网络与基础设施
- 🧪 未公开技术实现
- 🛣️ 未公开产品路线
- 💰 定价、收入、成本与商业战略
- ⚖️ 内部法律、谈判和治理方案
- 🧩 仅对某个内部项目有意义的实现细节

如果一条经验来自内部项目：

```text
Private Experience
        ↓
Human Declassification
        ↓
Abstraction
        ↓
Public Skill
```

能抽象成通用方法，就公开方法。

不需要公开项目底牌。

详细规则见：

[`PUBLICATION_CHECKLIST.md`](PUBLICATION_CHECKLIST.md)

---

## 🚫 它不是什么

Silvite Engineering Method：

- ❌ 不是万能 Prompt
- ❌ 不是某个项目的开发文档
- ❌ 不是某种语言或框架教程
- ❌ 不是要求所有修改都走重型流程
- ❌ 不是让 Agent 遇到风险就什么都不做
- ❌ 不是“最终的软件工程真理”
- ❌ 不替代领域安全规范和专业判断

一个五分钟就能安全回滚的小修改，没有必要采用生产数据迁移级流程。

而一个只修改三行代码，却可能造成不可逆数据损坏的任务，也不能因为代码量小就被视为低风险。

> **工程风险取决于影响面，而不是代码行数。**

---

## 🧭 当前状态

### `v0.3.1 — Usable, Experimental`

当前版本已经完成：

- ✅ 初始工程方法蒸馏
- ✅ Skill / References 分层
- ✅ 工程压力场景设计
- ✅ 第一轮 RED → GREEN 行为校准
- ✅ 公开安全检查
- ✅ 持续更新机制
- ✅ 通用治理与架构演进职责拆分
- ✅ 大型迁移的基线、不变量、切片和兼容门禁
- ✅ 发布身份、信息暴露、密闭工具链和命令行为安全规则
- ✅ 8 个架构演进压力场景与评分标准
- ✅ 分层环境拓扑、能力状态、可重建验收和备份恢复门禁
- ✅ 8 个环境工程压力场景与评分标准

但它仍然缺少足够多的：

- 🌍 独立真实项目
- 🤖 不同 Agent / 模型
- 🧰 不同技术栈
- 🕒 长期维护样本
- 💥 真实故障与反例
- 🧪 新 Skill 的独立 RED → GREEN 前向测试

因此，在达到 `v1.0` 之前：

**任何规则都应该允许被新的现实证据推翻、拆分或修正。**

如果以后事实证明某条原则是错的，

那就改掉它。

---

## 🌿 最后

这套方法并不是从：

> “怎样设计一套漂亮的软件工程理论？”

开始的。

它更接近于一个不断重复的问题：

> **当 Agent 已经可以替我完成越来越多执行工作以后，我还必须自己负责什么？**

答案逐渐从“写代码”转向：

**目标、系统、边界、复杂度、证据与判断。**

AI 可以让软件生产越来越快。

但速度本身并不会自动带来可靠性。

所以 Silvite Engineering Method 想做的事情其实很简单：

> **让 Agent 放大人的执行能力，而不是放大未经验证的错误。**

---

## 📄 License

MIT License.

See [`LICENSE`](LICENSE).

---

**Silvite Engineering Method**

*答案越来越便宜，判断越来越贵。*
