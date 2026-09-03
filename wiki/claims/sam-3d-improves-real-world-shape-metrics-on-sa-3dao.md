---
title: "SAM 3D 在 SA-3DAO 上提升真实图像单物体形状重建指标"
type: claim
claim_id: "C-2026-001"
claim_kind: empirical
claim_status: supported
confidence: medium
scope: "SA-3DAO 的单图、单物体、归一化并经 ICP 对齐的形状评测"
tags: [sam-3d, single-image-3d, shape-reconstruction, benchmark]
summary: "在作者提出的 SA-3DAO 协议下，SAM 3D 的四项几何指标均优于论文所比较的单图生 3D 基线。"
created: 2026-08-25
updated: 2026-08-25
source_count: 1
---

## 主张

在 [[sa-3dao]] 的作者评测协议下，SAM 3D 在 F1@0.01、vIoU、Chamfer 和 EMD 四项形状指标上均优于论文所比较的单图生 3D 基线。

## 适用范围

- 对象 / 系统：[[sam-3d-objects]] 与 Table 2 中的 Trellis、Hunyuan3D、Direct3D-S2、TripoSG、Hi3DGen。
- 条件：自然图像中的目标物体；预测与艺术家参考网格分别归一化并经 ICP 对齐。
- 结果变量：F1@0.01、体素 IoU、Chamfer Distance、Earth Mover's Distance。
- 不适用范围：绝对尺度、未经对齐的姿态、纹理质量、物理可行性及其他未测试数据分布。

## 证据图谱

| 关系 | 论文 | 定位 | 直接证据或结果 | 可信度与限制 |
| --- | --- | --- | --- | --- |
| supports | [[sam3d-team-2025-sam-3d]] | p.10，Table 2；pp.37–38，Section D.3.1 | SAM 3D：F1 0.2344、vIoU 0.2311、Chamfer 0.0400、EMD 0.1211；对应最佳基线分别为 0.1629、0.1531、0.0844、0.2049 | 1,000 个艺术家网格；作者自建基准；归一化和 ICP 降低了姿态/尺度误差影响 |

## 当前判断

- 证据状态：supported
- 信心：medium
- 判断依据：表中四项指标方向一致且差距较大，但只有作者团队单一来源，尚无独立复现。

## 矛盾与边界

在没有 3D 真值的 ISO3D 上，SAM 3D 并未在所有感知指标上领先：ULIP 为 0.1488，低于 TripoSG 的 0.1529；Uni3D 为 0.3707，仅略高于 Trellis 的 0.3698。因此该主张只覆盖 SA-3DAO 的几何真值协议，不能写成“在所有单图 3D 指标和数据集上全面领先”。

## 待验证问题

- [ ] 在独立维护、非作者构建的真实图像 3D 基准上复现 Table 2 趋势。
- [ ] 使用未归一化、未 ICP 对齐的协议拆分形状、尺度和姿态误差。
- [ ] 审计 SA-3DAO 与训练图像、资产及人工标注流程之间是否存在潜在重叠。

## 相关页面

- 概念：[[visually-grounded-single-image-3d-reconstruction]]
- 方法：[[model-in-the-loop-3d-annotation]]
- 数据集：[[sa-3dao]]
- 实体：[[sam-3d-objects]]
- 论文：[[sam3d-team-2025-sam-3d]]

## 来源

- [[sam3d-team-2025-sam-3d]]

