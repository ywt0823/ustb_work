---
title: LIT · Franc et al. JMLR 2023 拒答最优策略
type: literature
status: reviewed
created: 2026-08-08
tags: [B0, 拒答, proper uncertainty, 黑盒]
sources:
  - https://jmlr.org/papers/v24/21-0048.html
  - https://jmlr.org/papers/volume24/21-0048/21-0048.pdf
pdf: "[[02-文献/核心论文/Franc-2023-RejectOption.pdf]]"
---

# LIT · Franc, Průša & Voráček (JMLR 2023) Optimal Strategies for Reject Option Classifiers

## 一句话

证明代价型 / 有界改进 / 有界弃权三种拒答模型导出**同一最优策略**：Bayes 分类器 + 随机化 Bayes 选择函数；并给出黑盒模型上学习 **proper uncertainty score** 的算法与一致性。

## 问题与方法

三种模型：

1. **Cost-based（Chow）**：显式拒答代价 \(\varepsilon\)，最小化期望损失  
2. **Bounded-improvement**：选择性风险 ≤ 目标时最大化覆盖率  
3. **Bounded-abstention**：覆盖率 ≥ 目标时最小化选择性风险  

**核心定理**：三者最优解均为 Bayes 分类器 + randomized Bayes selection：

- \(r^*(x)<\) 阈值 → 接受预测  
- \(r^*(x)>\) 阈值 → 拒答  
- 相等 → 以概率 \(\tau\) 接受  

**Proper uncertainty score**：保持条件风险诱导排序的标量不确定度，足以构造上述选择函数。

**学习算法（黑盒可用）**：

1. 对分类损失做回归，估计不确定度  
2. 最小化 SELE 损失（逼近 AuRC，可优化）  
并证明 Fisher 一致性。

## 实验与结论

在分类、序数回归、结构化输出等任务上，SELE 学习的不确定度优于常见基线，并与专用 SOTA 相当；RC 曲线 / AuRC 是有界弃权模型的质量刻画。

## 可复现性

JMLR 公开 PDF；算法描述完整，依赖校准集估计不确定度。

## 与本课题关系

| 直接可用 | 本课题扩展点 |
|----------|--------------|
| 统一「风险阈值拒答」理论语言 | 动作集加入 **CLARIFY**（改变后续信念） |
| 黑盒 proper uncertainty 学习思路 | LLM API 输出不能直接当后验，需学/校准不确定度 |
| RC / AuRC 评测 | 开题主图用风险–覆盖 / 风险–澄清权衡 |
| 三种模型等价视角 | 招聘业务可用代价型（不对称 \(C\)）陈述 |

**警示**：Franc 仍是**单步**选择性分类，不含多轮澄清与证据门控。

## 可引用金句 / 公式

> Despite different formulations, the three rejection models lead to the same prediction strategy: the Bayes classifier endowed with a randomized Bayes selection function.

\[
c_B(x)=\begin{cases}1 & r^*(x)<\varepsilon\\ \tau & r^*(x)=\varepsilon\\ 0 & r^*(x)>\varepsilon\end{cases}
\]

## 精读清单

- [x] 摘要与引言
- [x] 三种模型与最优策略
- [x] proper uncertainty / SELE
- [x] 写入对比表
