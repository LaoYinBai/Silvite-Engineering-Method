# Release Evidence Gates

## 发布身份门禁

任何可分发构建或发布前逐项验证：

- ProductVersion 符合产品顺序和通道策略；
- Build 按项目规则全局单调且未被其他平台/通道占用；
- Commit 是构建所用源码，工作树状态已记录；
- Channel、edition、platform 与目标分发位置匹配；
- stable、beta、rc 的排序和跨通道升级符合实际客户端逻辑；
- 包名/application ID、签名身份、UpgradeCode 或平台等价身份保持兼容；
- 用户数据、配置、缓存和凭据引用在升级后保留或按合同迁移；
- Tag、manifest、Asset、文件名、内部包属性、哈希和签名指向同一身份；
- 明确排除的仓库、平台和发布文件保持零修改；
- 回滚产物、权限、时间窗口和恢复验证仍然可用。

构建成功后再发现身份矛盾说明门禁太晚。候选身份必须在昂贵构建前预演，并在产物生成后重新读取验证。

## 升级矩阵

至少覆盖：最低支持正式版→候选、当前正式版→候选、最近 beta/rc→正式版、同 ProductVersion 不同 Build、跨平台独立升级、各 edition、失败中断后重试以及回滚后再次升级。

使用真实更新器或等价契约测试验证“能发现、能下载、能校验、能安装、能启动、数据仍有效”。其中任一环节未验证，不得报告 Upgrade Verified。

## 九层证据状态

| 状态 | 最低新鲜证据 |
|---|---|
| Code Complete | 目标 diff 已实现并完成范围检查 |
| Tests Passed | 指定测试与相关回归完整输出、退出码和失败数 |
| Build Produced | 目标平台/edition 构建退出码与产物路径 |
| Artifact Inspected | 包内版本、Build、Commit、Channel、签名、哈希、文件内容 |
| Remote Published | 上传操作成功且远端对象存在 |
| Remote Independently Verified | 通过受支持的独立路径重新读取远端 manifest、元数据、哈希或签名 |
| Installed | 目标设备/环境完成安装并启动 |
| Upgrade Verified | 规定旧版本真实发现并升级，数据/身份/核心行为通过 |
| User Accepted | 用户或指定验收者按标准明确接受 |

状态只能单向按证据推进；失败、回退或证据过期时回降到实际支持的层级。

## 远端验证

优先使用公开/受支持 API、正常客户端路径、签名 manifest、哈希和响应头验证。验证者不得通过复原真实凭据、调用非公开接口或规避终端安全来追求“独立”。无法安全访问时报告 Remote Published 但 Remote Independently Verified 未完成。

## Go/No-Go

从回滚窗口结束点倒推恢复与验证耗时。最晚决策点前未取得继续所需证据则 No-Go 或回滚；历史成功率和局部测试不能延长真实回滚能力。

