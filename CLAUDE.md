# 项目文档规范

## 文档体系

```
docs/
  business/
    service-brief-enterprise.md  # 对外简介（中大型企业），面向企业决策者（有泄露风险）
    service-brief-smb.md         # 对外简介（小微企业/一人公司），面向非技术背景创始人（有泄露风险）
    strategy-internal.md         # 内部战略文档，仅限核心团队与投资人（机密）
    meta.json                    # business/ 下所有文档的共享元数据（受众、约束、关联文档）
  mechanism/
    general_statement.md         # AI 时代社会结构与制度选择（理论愿景）
    alliance_model.md            # 一人公司联盟组织模型（连接理论与实践）
    meta.json                    # mechanism/ 下所有文档的共享元数据
  archive/
    case-social-media-ops.md     # 多语言社交媒体运营案例备份（从对外简介移出）
    service-brief-smb-8step-case.md  # SMB 版原始 8 步合作案例备份（精简为 5 阶段前）
    service-brief-enterprise-v1-intermediary.md  # Enterprise 版 v1 归档（面向中间人版本，重构前备份）
    service-brief-smb-v2-pre-restructure.md  # SMB 版 v2 归档（竞争壁垒视角重构前备份）

docs-todo/                       # 审阅建议，镜像 docs/ 目录结构
  business/
    service-brief-enterprise.md  # service-brief-enterprise.md 的待处理审阅建议
    service-brief-smb.md         # service-brief-smb.md 的待处理审阅建议
    strategy-internal.md         # strategy-internal.md 的待处理审阅建议
  mechanism/
    general_statement.md         # general_statement.md 的待处理审阅建议
    alliance_model.md            # alliance_model.md 的待处理审阅建议
```

### docs-todo/ 规则

- `/review-doc` 每次运行后自动更新对应位置的建议文件（完整覆写，反映当前状态）；如所有问题均已解决，则删除该文件
- 路径映射：`docs/X/Y.md` → `docs-todo/X/Y.md`
- `/commit` 审阅时跳过 `docs-todo/` 下的文件

### 元数据规则

每个文档文件夹有一个 `meta.json`，结构为 `shared`（共享约束）+ `files`（per-file 属性）。编辑文档前先读取对应的 `meta.json`。

### 信息隔离规则

`service-brief-enterprise.md` 和 `service-brief-smb.md` 是对外文档，**不得包含**以下内容（详见 `business/meta.json`）：
- 完整商业模式和市场节奏判断（在 strategy-internal.md 中）
- 竞对分析和差异化定位策略（在 strategy-internal.md 中）
- 技术架构细节（在 strategy-internal.md 中）
- 联盟组织模型（在 alliance_model.md 中）
- 定价公式细节（"基础费+效果分成"的具体结构）
- 个人联系方式

## 术语一致性

修改任何文档时，必须遵守以下术语标准：

| 概念 | 正确表述 | 禁止表述 | 说明 |
|------|---------|---------|------|
| 数据安全（升级概念） | 知识资产主权 | 数据安全、数据不出企业边界 | 不只是防泄露，是保护和经营企业核心竞争壁垒 |
| 产品定位 | 知识资产建设 + 数字员工交付 | 岗位级标准化模块、SaaS 产品 | 知识资产建设是核心价值，数字员工是交付形式 |
| 数字员工角色 | 交付形态 | 产品本身、产品化封装 | 数字员工是交付手段，不是我们卖的产品 |
| 定价模式 | 结果绑定定价 | 订阅制、模块订阅 | 按可验证的业务结果收费 |
| 混合云价值 | 知识资产主权架构 | 数据安全架构 | 架构核心目标是保障知识资产主权 |

### 术语层级

- **知识资产**：核心战略概念，企业知识作为资产类别
- **知识资产建设**：持续性过程，通过数字员工嵌入工作流使知识自然积累
- **知识资产主权**：治理原则，企业保有知识资产的完全控制权
- **结构化知识资产**：建设产出物，AI 可消费的形式

### 允许出现旧术语的场景

在 `strategy-internal.md` 的"SaaS 价值贬值风险"章节中，"SaaS"、"软件模块"、"订阅制"等词汇作为**批判对象**使用（描述我们要避免的定位），这是正确的。除此之外，不应将自身定位为 SaaS 或软件产品。

## 跨文档引用

修改文件名或移动文件时，检查以下引用链：

- `strategy-internal.md` 引用 `service-brief-enterprise.md` / `service-brief-smb.md`（第3行、第52行、第139行、第148行、第176行、第184行、第204行、第244行、第274行）
- `business/meta.json` 引用 `strategy-internal.md` 和 `alliance_model.md`
- `mechanism/meta.json` 引用 `service-brief-enterprise.md`、`service-brief-smb.md` 和 `strategy-internal.md`
- `alliance_model.md` 引用 `general_statement.md`（第3行、第7行、资本策略章节）和 `strategy-internal.md`（第81行）
- `general_statement.md` 引用 `alliance_model.md`（第90行）

## 编辑文档前

1. 先读取目标文档所在文件夹的 `meta.json`
2. 参考本文件的术语一致性表
3. 如修改 `service-brief-enterprise.md` 或 `service-brief-smb.md`，确认不泄露内部敏感信息
4. 如修改涉及术语变更，同步更新所有相关文档
5. 重组或精简文档时，有保留价值的内容应迁移到合适的文档（如 `docs/archive/`、内部文档等），而非直接删除
