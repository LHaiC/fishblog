---
title: "RC Net 时延预测：CNN + ODE Solver"
date: 2026-01-21T16:10:33+08:00
description: "用神经网络学习物理世界的衰减因子。"
topics: ["EDA", "Timing", "Machine-Learning"]
---

# 核心提案

**目标**：在 Optimization Loop 中替代昂贵的 SPICE 仿真，提供比 Elmore Delay 更准的梯度。

**方法论**：
1.  **学习目标**：预测衰减因子 $\kappa = \frac{Delay_{real}}{Delay_{elmore}}$，而非绝对时延。
2.  **模型架构**：
    - **CNN/GNN**：提取 RC 树拓扑特征。
    - **Neural ODE**：建模电荷在 RC 网络中的连续流动过程。
3.  **应用场景**：指导 Router 绕线或 Sizer 调整门级尺寸。

> **可行性分析 (Review)**
>
> RC 电路本质就是微分方程，神经网络拟合其系数比直接拟合结果更符合物理直觉 (Physics-Informed ML)。
>
> 这种方法在布局布线阶段的优化可能有用，但在 Signoff 阶段精度可能不够。
