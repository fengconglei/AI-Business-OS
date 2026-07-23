# GPT Internal Test Plan
# Business Diagnosis Engine

## 一、测试目标

本文件用于指导 Business Diagnosis Engine 的 GPT Builder 内测。

目标不是立刻对外发布 GPT，而是验证 GPT 是否能稳定完成以下任务：

1. 正确读取客户信息
2. 输出六大模块评分
3. 判断诊断置信度
4. 识别核心瓶颈
5. 推荐正确产品包
6. 输出30天行动计划
7. 避免推荐不适合客户阶段的方案

---

## 二、测试前提

内测前必须确认以下文件已存在：

- gpt-builder-prompt.md
- scoring-rules.md
- report-template.md
- packages/starter-growth-loop.md
- packages/product-system-rebuild.md
- packages/delivery-retention-optimization.md
- cases/case-001-family-education.md
- cases/case-002-content-strong-product-weak.md
- cases/case-003-sales-strong-delivery-weak.md

---

## 三、测试案例

### Case-001

客户类型：

获客弱、成交弱。

预期推荐：

AI知识IP增长闭环搭建包。

通过标准：

GPT 不应优先推荐产品体系重构包或交付复购优化包。

---

### Case-002

客户类型：

内容强，但产品体系弱。

预期推荐：

产品体系重构与高客单承接设计包。

通过标准：

GPT 必须识别该客户不是内容获客问题，不应优先推荐 AI内容工作流或增长闭环包。

---

### Case-003

客户类型：

成交强，但交付复购弱。

预期推荐：

交付复购优化包。

通过标准：

GPT 必须识别该客户不是获客问题，也不是成交问题，不应继续建议扩大成交。

---

## 四、测试流程

每个案例按以下步骤测试：

1. 将 gpt-builder-prompt.md 内容复制到 GPT Builder Instructions。
2. 将对应 case 文件内容作为客户输入。
3. 让 GPT 生成完整商业体检报告。
4. 检查输出是否符合 report-template.md V1.3 结构。
5. 检查推荐产品包是否正确。
6. 记录问题。
7. 如果 GPT 输出错误，回写到 prompt.md 或 scoring-rules.md。

---

## 五、输出检查清单

每份 GPT 输出必须包含：

- 综合评分
- 当前业务阶段
- 信息完整度
- 诊断置信度
- 六大模块评分表
- 核心瓶颈
- 推荐产品包
- 30天行动计划
- 下一步邀约
- 禁止承诺固定收入结果

---

## 六、失败标准

以下情况视为测试失败：

1. 推荐错误产品包
2. 把所有客户都推荐同一个方案
3. 忽略信息不足
4. 承诺收入结果
5. 只输出方向性建议，没有行动指标
6. 推荐网站、SaaS、复杂Agent等非当前阶段方案
7. 没有区分获客、产品、成交、交付等不同瓶颈

---

## 七、测试记录方式

每次 GPT 内测后，应新增 Review 文件：

outputs/gpt-test-output-case-xxx.md

reviews/gpt-test-review-case-xxx.md

不要覆盖已有人工测试输出。

---

## 八、当前判断

当前 Business Diagnosis Engine 可以进入内部 GPT 测试阶段。

但仍不建议直接对客户开放。

必须先使用 Case-001、Case-002、Case-003 完成至少一轮 GPT 输出测试。
