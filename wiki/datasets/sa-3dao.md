---
title: "SAM 3D Artist Objects（SA-3DAO）"
type: dataset
domain: "真实图像单图 3D 物体重建"
version: "2026-06-02 release"
license: "未核验"
access: "官方公开下载页面；具体访问与使用条款待单独核验"
tags: [3d-reconstruction, benchmark, real-world-images, artist-annotations]
summary: "由专业 3D 艺术家根据自然场景单图制作并对齐的 1,000 个无纹理物体网格，用于评估真实图像中的单图形状与布局重建。"
created: 2026-08-25
updated: 2026-08-25
source_count: 1
---

## 数据集概述

SA-3DAO 是 [[sam3d-team-2025-sam-3d]] 为弥补现有单图 3D 基准偏合成、偏孤立物体或偏室内家具而建立的评测集。它包含 1,000 个无纹理 3D 物体网格，目标对象来自室内外自然图像，包括大型结构、日常用品、动物、服装及长尾物体。

专业 3D 艺术家只依据输入单图制作完整网格，并将其对齐到图像。这里的“ground truth”是专家利用可见像素、识别、常识、物理合理性和对称假设形成的参考重建，不是多视图扫描得到的不可见表面真值。

## 版本与获取

- 当前版本：2026-06-02 官方发布版本；未见更细的语义版本号。
- 获取方式：[官方数据集页面](https://ai.meta.com/datasets/sa-3dao-sam-3d-artist-objects/)
- 许可证 / 使用限制：❓ 本次未定位具体数据许可证，下载和使用前需在官方页面重新核验。
- 版本核验日期：2026-08-25

## 数据构成

- 规模：1,000 个无纹理 3D 物体网格。
- 样本单位：自然图像中的目标物体及其艺术家重建网格；部分图像包含多个标注物体。
- 特征 / 标注：目标图像、物体形状以及与图像的布局对齐；论文称艺术家网格顶点数中位数为 4,751。
- 划分方式：论文中未定位完整 train/validation/test 划分；其主要用途是 evaluation benchmark。
- 难度：遮挡、小目标、深度—尺度歧义、室内外场景和长尾类别。

## 采集与标注过程

专业艺术家根据一张自然图像创建完整网格，使可见部分与输入图像对齐，同时依靠物体识别、上下文、常识、物理合理性和适当的对称假设补全不可见部分。作者报告简单对象可约 5 分钟完成，困难对象可超过 5 小时（pp.35–36，Section D.1）。

## 质量、偏差与泄漏风险

- 艺术家重建不是客观唯一解；不可见部分包含专家先验。
- 数据集由 SAM 3D 作者团队建立并用于证明模型优势，需独立评测复核。
- 形状指标在预测与参考网格分别归一化并 ICP 对齐后计算，削弱了绝对尺度和初始姿态误差。
- 论文未在数据集章节完整报告艺术家间一致性、重复标注比例或参考网格不确定性。
- ❓ 需要进一步核验评测图像与大规模预训练、MITL 数据源之间的去重策略。

## 常见任务与指标

- 形状：F1@0.01、`64³` voxel IoU、Chamfer Distance、Earth Mover's Distance。
- 布局：3D IoU、ICP rotation error、对称 ADD-S、ADD-S@0.1。
- 定性分析：遮挡、薄结构、长尾对象和复杂自然场景重建。

## 使用该数据集的论文

- [[sam3d-team-2025-sam-3d]]

## 相关页面

- 主张：[[sam-3d-improves-real-world-shape-metrics-on-sa-3dao]]
- 主张：[[sam-3d-joint-shape-layout-outperforms-compared-layout-pipelines]]
- 概念：[[visually-grounded-single-image-3d-reconstruction]]
- 方法：[[model-in-the-loop-3d-annotation]]
- 实体：[[sam-3d-objects]]

## 来源

- [[sam3d-team-2025-sam-3d]]

