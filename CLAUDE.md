# 项目文档规范

## 文档体系

```
docs/
  business/
    service-brief.md          # 对外简介，给中间人/引荐人（有泄露风险）
    service-brief.meta.json   # 简介的受众、约束、关联文档
    strategy-internal.md      # 内部战略文档，仅限核心团队与投资人（机密）
  mechanism/
    general_statement.md      # AI 时代社会结构与制度选择（理论愿景）
    alliance_model.md         # 一人公司联盟组织模型（连接理论与实践）
```

### 信息隔离规则

`service-brief.md` 是对外文档，**不得包含**以下内容（详见 `service-brief.meta.json`）：
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
| 产品定位 | 知识资产工程 + 数字员工交付 | 岗位级标准化模块、SaaS 产品 | 知识资产工程是核心价值，数字员工是交付形式 |
| 数字员工角色 | 交付形态 | 产品本身、产品化封装 | 数字员工是交付手段，不是我们卖的产品 |
| 定价模式 | 结果绑定定价 | 订阅制、模块订阅 | 按可验证的业务结果收费 |
| 混合云价值 | 知识资产主权架构 | 数据安全架构 | 架构核心目标是保障知识资产主权 |

### 术语层级

- **知识资产**：核心战略概念，企业知识作为资产类别
- **知识资产工程**：我们交付的服务，将知识结构化
- **知识资产主权**：治理原则，企业保有知识资产的完全控制权
- **结构化知识资产**：工程产出物，AI 可消费的形式

### 允许出现旧术语的场景

在 `strategy-internal.md` 的"SaaS 价值贬值风险"章节中，"SaaS"、"软件模块"、"订阅制"等词汇作为**批判对象**使用（描述我们要避免的定位），这是正确的。除此之外，不应将自身定位为 SaaS 或软件产品。

## 跨文档引用

修改文件名或移动文件时，检查以下引用链：

- `strategy-internal.md` 引用 `service-brief.md`（第3行、第50行）
- `service-brief.meta.json` 引用 `strategy-internal.md` 和 `alliance_model.md`
- `alliance_model.md` 引用 `general_statement.md`（第3行、第7行）
- `general_statement.md` 引用 `alliance_model.md`（第89行）

## 编辑文档前

1. 先读取目标文档及其 `.meta.json`（如存在）
2. 参考本文件的术语一致性表
3. 如修改 `service-brief.md`，确认不泄露内部敏感信息
4. 如修改涉及术语变更，同步更新所有相关文档
