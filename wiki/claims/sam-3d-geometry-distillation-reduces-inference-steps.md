---
title: "SAM 3D Geometry Model 蒸馏可显著减少推理步数"
type: claim
claim_id: "C-2026-005"
claim_kind: empirical
claim_status: supported
confidence: low
scope: "SAM 3D Geometry Model 的 shortcut flow-matching 蒸馏实验"
tags: [sam-3d, distillation, inference-efficiency, flow-matching]
summary: "作者报告 shortcut 蒸馏将 Geometry Model 从 25 步缩减到 4 步时可获得约 10 倍推理加速，质量接近原始多步推理。"
created: 2026-08-25
updated: 2026-08-25
source_count: 1
---

## 主张

对 [[sam-3d-objects]] 的 Geometry Model 使用 shortcut flow-matching 蒸馏后，从 25 步缩减到 4 步可获得作者报告的约 10 倍推理加速，同时 Figure 18 中的形状指标接近 25 步流匹配结果。

## 适用范围

- 对象 / 系统：SAM 3D Geometry Model。
- 条件：论文描述的 shortcut objective、固定 CFG 蒸馏设置和作者测试环境。
- 结果变量：函数评估次数、相对推理加速及 Figure 18 的几何质量曲线。
- 不适用范围：Texture & Refinement Model、端到端场景延迟、显存占用、不同 GPU 或部署框架。

## 证据图谱

| 关系 | 论文 | 定位 | 直接证据或结果 | 可信度与限制 |
| --- | --- | --- | --- | --- |
| supports | [[sam3d-team-2025-sam-3d]] | p.9，Section 3.2.2；pp.32–33，Section C.4；p.41，Section E.8 / Figure 18 | 25→4 步；作者报告 4 步约 10×、1 步约 38×，早期步骤质量明显优于未蒸馏流模型 | 主要以曲线展示；未给完整端到端延迟表、硬件配置和方差 |

## 当前判断

- 证据状态：supported
- 信心：low
- 判断依据：论文明确报告并提供曲线，但只有作者单次系统结果，且“10×”不是整个 SAM 3D pipeline 的加速倍数。

## 矛盾与边界

Texture & Refinement Model 最终发布版本没有采用蒸馏；几何提速不能直接换算为包含图像编码、纹理细化、解码和导出的端到端场景加速。正文“sub-second”也缺少完整硬件和批量条件。

## 待验证问题

- [ ] 在公开权重上按不同 GPU、分辨率和物体数量复现端到端延迟。
- [ ] 分别报告 Geometry、Texture & Refinement、VAE 解码和导出耗时。
- [ ] 比较 4 步蒸馏与 25 步推理在困难薄结构和遮挡样本上的质量差异。

## 相关页面

- 概念：[[visually-grounded-single-image-3d-reconstruction]]
- 实体：[[sam-3d-objects]]
- 论文：[[sam3d-team-2025-sam-3d]]

## 来源

- [[sam3d-team-2025-sam-3d]]

