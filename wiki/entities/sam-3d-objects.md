---
title: "SAM 3D Objects"
type: entity
entity_kind: software
aliases: ["SAM 3D Objects model", "SAM 3D Object"]
tags: [meta, 3d-reconstruction, foundation-model, software]
summary: "Meta 发布的单图物体 3D 重建模型，输入图像与目标 mask，输出几何、纹理及场景布局；它是 SAM 3D 系列中区别于 SAM 3D Body 的对象模型。"
created: 2026-08-25
updated: 2026-08-25
source_count: 2
---

## 简介

SAM 3D Objects 是 Meta Superintelligence Labs 发布的单图 3D 物体重建模型。给定图像和目标物体 mask，它生成完整形状、纹理、旋转、平移和尺度，并可输出 mesh 或 3D Gaussian splats。

“SAM 3D”在产品层面还包括 SAM 3D Body。[[sam3d-team-2025-sam-3d]] 和本页讨论的是 Objects 模型；人体专用的 Body 模型应作为独立实体处理。

## 与当前研究的关系

- 是 [[visually-grounded-single-image-3d-reconstruction]] 的首个入库系统案例。
- 提供了 [[model-in-the-loop-3d-annotation]] 在大规模真实图像 3D 标注中的完整设计。
- 发布了 [[sa-3dao]]，后续可用于比较新的单图 3D 系统。

## 研究路线或关键贡献

- 两阶段生成：1.2B Geometry Model 预测粗形状和布局，600M Texture & Refinement Model 补充几何细节和纹理。
- 训练路线：合成预训练、Render-and-Paste 半合成训练、真实数据 SFT/DPO 和 shortcut 蒸馏。
- 官方仓库称代码和模型权重已发布；权重需要 Hugging Face 访问许可。
- 官方推理要求为 64 位 Linux 和至少 32GB 显存的 NVIDIA GPU。
- 采用定制 SAM License；使用、修改或再分发前需阅读具体条款。

## 相关论文

- [[sam3d-team-2025-sam-3d]]

## 相关页面

- 主张：[[sam-3d-improves-real-world-shape-metrics-on-sa-3dao]]
- 主张：[[sam-3d-wins-human-preference-on-real-world-object-and-scene-reconstruction]]
- 主张：[[sam-3d-joint-shape-layout-outperforms-compared-layout-pipelines]]
- 主张：[[multi-stage-synthetic-to-real-training-improves-sam-3d-shape-performance]]
- 主张：[[sam-3d-geometry-distillation-reduces-inference-steps]]
- 概念：[[visually-grounded-single-image-3d-reconstruction]]
- 方法：[[model-in-the-loop-3d-annotation]]
- 数据集：[[sa-3dao]]

## 来源

- [[sam3d-team-2025-sam-3d]]
- [官方代码仓库](https://github.com/facebookresearch/sam-3d-objects)

