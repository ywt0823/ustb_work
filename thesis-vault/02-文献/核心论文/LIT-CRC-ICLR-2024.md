---
title: LIT · Conformal Risk Control ICLR 2024
type: literature
status: reviewed
created: 2026-08-08
tags: [B0, 共形, 风险控制, 阈值标定]
sources:
  - https://arxiv.org/abs/2208.02814
  - https://iclr.cc/virtual/2024/poster/19529
pdf: "[[02-文献/核心论文/CRC-ICLR2024.pdf]]"
---

# LIT · Angelopoulos et al. (ICLR 2024) Conformal Risk Control

## 一句话

把共形预测从「覆盖率控制」推广到**任意单调有界损失的期望风险控制**，用校准数据选出保守参数 \(\hat\lambda\)，有限样本、分布无关。

## 问题与方法

- **经典共形**：\(\mathbb{P}(Y\notin C(X))\le\alpha\)  
- **CRC**：对随保守度 \(\lambda\) 非增的损失 \(\ell\)，保证  
  \(\mathbb{E}[\ell(C_{\hat\lambda}(X),Y)]\le\alpha\)  
- **算法**：在校准集上算经验风险 \(\widehat R_n(\lambda)\)，取  
  \(\hat\lambda=\inf\{\lambda:\frac{n}{n+1}\widehat R_n(\lambda)+\frac{B}{n+1}\le\alpha\}\)  
- ** tightness**：连续情形下还有下界，宽松度约 \(O(1/n)\)  
- **扩展**：分布漂移、分位风险、多重/对抗风险等  
- **示例**：控制 FNR、图距离、token-level F1 等

## 实验与结论

CV / NLP 实例表明可用同一程序把「阈值」变成带期望风险保证的量，而不是拍脑袋调参。

## 可复现性

代码：https://github.com/aangelopoulos/conformal-risk ；依赖交换性校准集。

## 与本课题关系

| 用途 | 落点 |
|------|------|
| 标定证据充分度阈值 \(\tau\) | 保证层：幻觉/错误执行风险上界 |
| 标定澄清触发阈值 | 控制过度澄清的期望代价 |
| 分布无关叙事 | 回应导师「阈值别拍脑袋」 |

**注意**：CRC 要求损失对 \(\lambda\) 单调；多轮序贯决策需把损失定义为「在给定门控参数下的回合损失」，并准备校准对话集。

## 可引用金句 / 公式

\[
\mathbb{E}\big[\ell\big(C_{\hat\lambda}(X_{n+1}),Y_{n+1}\big)\big]\le\alpha
\]

\[
\hat\lambda=\inf\Big\{\lambda:\tfrac{n}{n+1}\widehat R_n(\lambda)+\tfrac{B}{n+1}\le\alpha\Big\}
\]

## 精读清单

- [x] 摘要与算法
- [x] 主定理条件（单调、有界）
- [x] 与共形预测关系
- [x] 写入对比表 / 方法保证层
