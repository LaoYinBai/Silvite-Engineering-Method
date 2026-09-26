# Publication Checklist

状态定义：

- **SAFE**：逐文件检查后未发现需要隐藏或确认的内容。
- **REVIEW NEEDED**：公开性无法由现有信息判断，必须由维护者确认；存在此状态时不得发布。
- **REMOVED**：已从公开内容删除，仅记录类别，不复述敏感事实。

## v0.3.1 文件状态

| 文件或目录 | 状态 | 说明 |
|---|---|---|
| 名称 `silvite-engineering-method` | SAFE | 维护者在公开仓库规格中明确指定的名称。 |
| `SKILL.md` | SAFE | 仅包含跨项目工程规则、宿主边界声明和公开路由。 |
| `README.md` | SAFE | 无个人、项目或商业事实；未宣称普适最佳。 |
| `CHANGELOG.md` | SAFE | 只记录方法、Eval 和安全变化。 |
| `SOURCES.md` | SAFE | 不披露原材料标题、数量、路径或具体内容，只记录抽象来源类型和准入规则。 |
| `UPDATE_GUIDE.md` | SAFE | 只包含更新流程和脱敏模板。 |
| `references/` | SAFE | 使用通用系统示例，不含项目专有实现。 |
| `evals/` | SAFE | 场景均为合成、匿名、跨项目压力测试；结果只保留脱敏聚合。 |
| `silvite-architecture-evolution/SKILL.md` | SAFE | 只包含通用架构迁移阶段、门禁、状态和公开路由。 |
| `silvite-architecture-evolution/agents/openai.yaml` | SAFE | 只包含名称、简述和默认调用提示。 |
| `silvite-architecture-evolution/references/` | SAFE | 使用通用版本、平台、edition、工具链和安全边界，不含项目专有参数。 |
| `evals/architecture-evolution-*` | SAFE | 合成压力场景不含真实仓库、服务、凭据或内部项目名称；未运行结果明确标记 Unverified。 |
| `silvite-environment-engineering/` | SAFE | 只包含通用环境拓扑、生命周期、能力状态、证据和恢复门禁；未保留设备或账户路径。 |
| `evals/environment-engineering-*` | SAFE | 场景由现场失败去实例化生成；不含真实设备、产品、用户或私有文件名，结果标记 Unverified。 |
| `docs/superpowers/` | SAFE | 设计与实施计划只记录公开方法、文件结构、验证和发布步骤。 |
| License | SAFE | 远端仓库维护者已选择并提交 MIT License；公开内容保持一致。 |

## 敏感类别检查

| 检查项 | 状态 |
|---|---|
| 个人身份、私人生活、关系或联系人 | SAFE |
| API Key、Token、密码、Cookie、密钥或证书 | SAFE |
| 私有路径、私有仓库或未公开代码 | SAFE |
| 内部服务器、IP、端口或基础设施拓扑 | SAFE |
| 用户数据或隐私数据 | SAFE |
| 未公开合作方或内部人员信息 | SAFE |
| 未发布功能、产品路线图或协议实现细节 | SAFE |
| 具体商业战略、定价、收入、成本或现金流 | SAFE |
| 公司主体、股权、法律、谈判或竞争方案 | SAFE |
| 可能增加攻击面的实现细节 | SAFE |
| 只对某个内部项目有意义的事实 | SAFE |
| 架构迁移中的真实仓库、服务或产品名称 | SAFE |
| 凭据复原方法、真实 Token 或私有接口细节 | SAFE |
| 真实设备路径、账户目录、工具版本或诊断内容 | SAFE |

## 主动排除记录

| 类别 | 状态 | 处理 |
|---|---|---|
| 个人经历、教育和职业判断 | REMOVED | 只保留直接改变工程决策的抽象。 |
| 项目名称、时间线和专有功能 | REMOVED | 改写为通用客户端、插件、网络或跨平台系统。 |
| 具体协议字段、链路组合和实现参数 | REMOVED | 只保留分层、版本、边界和复杂度原则。 |
| 公司、商业、组织和治理推演 | REMOVED | 不进入公开工程 Skill。 |
| 现场设备、Host/Guest 绝对路径与特定脚本名 | REMOVED | 只保留环境所有权、生命周期和入口归属规则。 |
| 未经原始日志复现的成功结论与冲突案例 | REMOVED | 不进入 Skill；仅将可机器验证的失败抽象为 Eval。 |

## REVIEW NEEDED

当前没有 REVIEW NEEDED 项目。若后续更新出现任何不确定项，必须在此列出并暂停发布。
