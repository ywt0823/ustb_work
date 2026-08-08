---
title: ALG-UB-CEG 草案
type: algorithm
status: drafting
created: 2026-07-29
tags: [自研, 算法, 招聘, 澄清问, 幻觉]
---

# ALG-UB-CEG（草案）

**Uncertainty-aware Belief Clarification with Evidence-Grounded generation**

不确定感知信念澄清 + 证据约束生成。

## 输入

- 对话历史 \(h_t\)，当前用户话轮 \(u_t\)
- 意图空间 \(\mathcal{Z}\)（招聘领域受控意图）
- 可检索证据库 \(\mathcal{E}\)（岗位/流程/政策等，脱敏）
- 代价参数：误答、幻觉、澄清、拒答

## 输出

- 动作 \(a_t \in \{\text{回答}, \text{澄清}, \text{拒答}\}\)
- 自然语言响应（若回答则带证据引用或明确未知）

## 三子算法

1. **BeliefUpdate**：维护 \(b_t(z) = P(z \mid h_t, u_t)\)，输出不确定度 \(u(b_t)\)
2. **RiskSensitiveAct**：最小化期望风险，选择澄清或承诺回答
3. **EvidenceGateDecode**：事实性内容必须绑定证据子集；否则拒答/降级

## LLM API 角色

黑盒：候选意图打分 / 澄清问生成 / 条件生成。  
**不作为**最终决策器。

## 创新表述重心（2026-08-01 按「底层算法」要求升级）

理论归属：**Reject-Option Classification / Selective Prediction 的序贯推广**。

> 将 Chow (1970) 的最优拒答规则推广到「证据约束下的多轮三动作决策」：动作集加入澄清、可行域受证据充分度约束、代价不对称；并证明经典规则是本框架的特例。

详见 [[03-算法/自研算法/算法理论深化方案]]。

对外强调 **Evidence-Gated Risk-Sensitive Decision**，避免被理解为 Belief∥Clarify∥RAG 三件套。

## 待形式化

- [ ] 风险函数 \(R(a, z)\) 与招聘代价表
- [ ] 证据支持度 \(\mathrm{supp}\) 操作化定义
- [ ] 澄清的信息增益 / 共形集缩小近似
- [ ] 与 CICC/UoT/Naive RAG 的可陈述差异（各 3 句话）
- [ ] P1 门控安全性（supp&lt;τ 时最优动作∉无据回答）
- [ ] P2 退化定理（无澄清 + 证据恒充分 ⇒ Chow 规则）
- [ ] P3 单调性；P4 风险–澄清权衡曲线

## 链接

- [[01-论文/方法/方法贡献草案]]
- [[01-论文/开题/开题报告-草案-v1]]
- [[01-论文/开题/创新性评估]]
- [[02-文献/对比表/相关工作对比表-v0]]
