---
title: "分阶段的合成到真实训练整体提升 SAM 3D 的真实图像形状性能"
type: claim
claim_id: "C-2026-004"
claim_kind: empirical
claim_status: supported
confidence: medium
scope: "SAM 3D 的 Iso-3DO、RP-3DO、MITL-3DO、Art-3DO、SFT 与 DPO 训练体系"
tags: [sam-3d, post-training, synthetic-data, ablation]
summary: "SAM 3D 的累计实验和消融显示，半合成中期训练及真实数据 SFT/DPO 整体改善 SA-3DAO 形状指标，但并非每项指标单调上升。"
created: 2026-08-25
updated: 2026-08-25
source_count: 1
---

## 主张

在 SAM 3D 的训练体系内，从孤立合成物体预训练，加入 Render-and-Paste 中期训练，再加入人机协同与艺术家真实数据的 SFT/DPO，整体上提升了 [[sa-3dao]] 的形状重建性能，但个别阶段和指标并非单调改善。

## 适用范围

- 对象 / 系统：[[sam-3d-objects]] 的 Geometry Model 与 Texture & Refinement Model。
- 条件：作者的数据配方、训练规模、模型架构和 SA-3DAO/偏好评测。
- 结果变量：F1@0.01、vIoU、Chamfer、EMD 和纹理偏好胜率。
- 不适用范围：其他架构、其他规模、独立训练数据或“任何模型都能从相同配方受益”的普遍结论。

## 证据图谱

| 关系 | 论文 | 定位 | 直接证据或结果 | 可信度与限制 |
| --- | --- | --- | --- | --- |
| supports | [[sam3d-team-2025-sam-3d]] | p.12，Table 4 | 从 Iso-3DO 预训练到最终模型，F1 0.1349→0.2344、Chamfer 0.1036→0.0400、EMD 0.2396→0.1211 | 累计增加多个因素，不能把相邻差异完全归因于单一机制 |
| supports | [[sam3d-team-2025-sam-3d]] | p.38，Table 7 | 去除 MITL-3DO、Art-3DO 或 MITL-DPO 均使一个或多个形状指标下降 | 单系统消融；缺少多随机种子误差条 |
| qualifies | [[sam3d-team-2025-sam-3d]] | p.12，Table 4 | Art-3DO DPO 后 vIoU 0.2337→0.2311；MITL DPO 后纹理胜率 66.9→66.4 | 说明“各阶段所有指标均提升”并不成立 |

## 当前判断

- 证据状态：supported
- 信心：medium
- 判断依据：累计实验与 knockout 消融互相支持整体趋势；但因素耦合、无误差条且只有单一系统。

## 矛盾与边界

论文把数据量、数据质量阈值、模型迭代、训练阶段和偏好优化同时推进。Figure 10 的持续改善是这些变化的合成结果，不能单独证明“数据引擎迭代次数”具有线性因果效应。该主张只保留较弱但有表格支持的“整体提升”。

## 待验证问题

- [ ] 在固定计算量、固定数据量和多个随机种子下隔离各训练阶段的效应。
- [ ] 比较随机扩充真实数据与主动采样困难样本的收益。
- [ ] 检验该训练配方在其他单图 3D 架构上是否成立。

## 相关页面

- 方法：[[model-in-the-loop-3d-annotation]]
- 概念：[[visually-grounded-single-image-3d-reconstruction]]
- 数据集：[[sa-3dao]]
- 实体：[[sam-3d-objects]]
- 论文：[[sam3d-team-2025-sam-3d]]

## 来源

- [[sam3d-team-2025-sam-3d]]

