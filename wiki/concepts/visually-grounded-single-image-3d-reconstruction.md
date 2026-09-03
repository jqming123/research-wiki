---
title: "视觉落地的单图 3D 重建"
type: concept
aliases: ["visually grounded single-image 3D reconstruction", "自然图像单图 3D 重建"]
tags: [single-image-3d, 3d-reconstruction, computer-vision]
summary: "从自然图像中的目标像素、场景上下文和物体先验推断完整 3D 形状、纹理及布局，同时承认不可见部分存在多解。"
created: 2026-08-25
updated: 2026-08-25
source_count: 1
---

## 定义

视觉落地的单图 3D 重建，是给定自然图像 `I` 和目标物体 mask `M`，估计物体完整形状 `S`、纹理 `T` 以及相对相机布局 `(R, t, s)` 的任务。[[sam3d-team-2025-sam-3d]] 将其建模为条件分布 `p(S,T,R,t,s | I,M)`，强调模型需要同时利用目标局部像素、完整场景上下文、遮挡线索和物体识别先验。

“视觉落地”意味着输出要与输入图像里的具体对象相符，而不仅是生成同类别的任意 3D 资产。

## 不同来源的定义差异

| 来源 | 定义 / 用法 | 差异与影响 |
| --- | --- | --- |
| [[sam3d-team-2025-sam-3d]] | 联合预测目标物体的完整形状、纹理、旋转、平移与尺度 | 同时覆盖资产生成和场景布局；依赖目标 mask，可选 pointmap |

## 核心机制或理论位置

- 单张图像只呈现可见表面，完整 3D 反演不是唯一确定问题。
- 阴影、纹理梯度、遮挡边界和透视提供局部几何线索。
- 物体识别与场景上下文为不可见部分、尺度和典型结构提供先验。
- 生成模型描述多个可能解，比单一确定性回归更符合任务的不确定性。

## 边界与易混淆概念

- 与孤立物体 image-to-3D 资产生成不同：后者通常针对居中、无遮挡物体，不一定预测场景尺度和姿态。
- 与多视图重建不同：单图缺少跨视角几何约束，更依赖学习到的先验。
- 与 2.5D 深度估计不同：深度图只描述可见表面，完整 3D 重建还要补全背面与被遮挡结构。
- 与传统 6D pose estimation 不同：后者常假设已知 CAD 模型，此处需要同时生成形状和姿态。
- 生成的不可见部分是合理假设，不应自动称为物理真值。

## 如何测量或操作化

- 形状：F1、体素 IoU、Chamfer、EMD；需记录是否归一化和 ICP 对齐。
- 布局：3D IoU、旋转误差、ADD-S；需记录 pointmap 来源。
- 纹理与整体质量：人类偏好、图像—3D 感知相似度。
- 实际应用还应增加碰撞、物理稳定性、端到端延迟和下游任务成功率。

## 相关主张

- [[sam-3d-improves-real-world-shape-metrics-on-sa-3dao]]
- [[sam-3d-wins-human-preference-on-real-world-object-and-scene-reconstruction]]
- [[sam-3d-joint-shape-layout-outperforms-compared-layout-pipelines]]
- [[multi-stage-synthetic-to-real-training-improves-sam-3d-shape-performance]]

## 相关页面

- 论文：[[sam3d-team-2025-sam-3d]]
- 方法：[[model-in-the-loop-3d-annotation]]
- 数据集：[[sa-3dao]]
- 实体：[[sam-3d-objects]]

## 来源

- [[sam3d-team-2025-sam-3d]]
