---
title: EXP-主实验协议 v0
type: experiment
status: seed
created: 2026-07-29
tags: [实验, seed]
---

# 主实验协议 v0

## 数据

脱敏招聘多轮对话；精标测试集目标规模后续确定（建议先 300–800 段）。

## 基线算法

1. 裸 API 多轮
2. Greedy Intent + Generate
3. Fixed-threshold Clarification
4. CICC 或同类
5. UoT / INTENT-SIM 类
6. Naive RAG
7. SelfCheckGPT 后处理

## 消融

- w/o Belief
- w/o Risk-sensitive act
- w/o Evidence gate

## 自变量 / 因变量

- 自变量：算法变体
- 因变量：见 [[04-业务/评价指标/指标草案]]

## 待办

- [ ] 确定标注规范
- [ ] 确定 API 模型版本冻结策略
- [ ] 用户模拟器是否采用
