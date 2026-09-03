---
title: "SAM 3D: 3Dfy Anything in Images"
type: paper
citation_key: "sam3dteam2025sam3d3dfyimages"
status: verified
read_depth: full
publication_status: preprint
year: 2025
authors:
  - "SAM 3D Team"
  - "Xingyu Chen"
  - "Fu-Jen Chu"
  - "Pierre Gleize"
  - "Kevin J Liang"
  - "Alexander Sax"
  - "Hao Tang"
  - "Weiyao Wang"
  - "Michelle Guo"
  - "Thibaut Hardin"
  - "Xiang Li"
  - "Aohan Lin"
  - "Jiawei Liu"
  - "Ziqi Ma"
  - "Anushka Sagar"
  - "Bowen Song"
  - "Xiaodong Wang"
  - "Jianing Yang"
  - "Bowen Zhang"
  - "Piotr Dollár"
  - "Georgia Gkioxari"
  - "Matt Feiszli"
  - "Jitendra Malik"
venue: "arXiv"
doi: ""
url: "https://arxiv.org/abs/2511.16624"
version_checked: "2026-08-25"
priority: high
tags: [single-image-3d, 3d-reconstruction, generative-model, computer-vision]
summary: "SAM 3D Objects 通过合成预训练、半合成中期训练和人机协同真实数据后训练，从单张自然图像与目标 mask 生成物体几何、纹理和场景布局。"
created: 2026-08-25
updated: 2026-08-25
source_count: 1
---

## 一句话结论

SAM 3D 将单图 3D 生成从孤立物体扩展到遮挡和杂乱的自然场景，并在作者建立的真实图像评测中显著优于所比较方法；但输出应理解为符合可见线索和先验的完整 3D 假设，而不是对不可见几何的唯一恢复。

## 书目信息与版本

- Citation key：`sam3dteam2025sam3d3dfyimages`
- arXiv：2511.16624；cs.CV / cs.AI
- DOI：未提供
- 发表状态：preprint；截至 2026-08-25 未在 arXiv 元数据中定位到 DOI 或期刊/会议引用
- 首次提交：2025-11-20
- 当前核验版本：v2，2026-06-02
- 原始文件：[[raw/papers/09_SAM_3D_2511.16624.pdf]]
- 代码与权重：[facebookresearch/sam-3d-objects](https://github.com/facebookresearch/sam-3d-objects)
- 项目页：[SAM 3D](https://ai.meta.com/sam3d/)
- 说明：本文对应 [[sam-3d-objects|SAM 3D Objects]]，不是配套的人体网格恢复模型 SAM 3D Body。

## 研究问题

如何仅凭单张自然图像和目标物体 mask，在遮挡、尺度变化和场景杂乱条件下，联合生成目标物体的完整 3D 形状、纹理及其相对相机的旋转、平移和尺度？

## 背景与理论位置

传统多视图重建依赖跨视角几何约束，单图重建则必须利用阴影、纹理、遮挡、上下文和“熟悉物体”识别等线索。作者将任务写成条件分布：

`p(S, T, R, t, s | I, M)`

其中 `I` 为图像，`M` 为目标 mask，`S/T` 为形状与纹理，`R/t/s` 为旋转、平移与尺度。该概率表述承认单图成像是有损映射，可能存在多个合理的 3D 解。

## 方法与研究设计

- 研究类型：生成式单图 3D 重建系统、训练数据引擎及作者内部基准评测。
- 输入：完整图像、目标物体二值 mask、裁剪物体视图；可选单目深度或传感器产生的 pointmap。
- Geometry Model：1.2B 参数 Mixture-of-Transformers 流模型，联合预测 `64³` 粗形状及旋转、平移和尺度。
- Texture & Refinement Model：600M 参数稀疏潜变量流模型，在粗形状上补充细节与纹理。
- 输出表示：可解码为 mesh 或 3D Gaussian splats。
- 训练路线：Iso-3DO 合成预训练 → RP-3DO Render-and-Paste 中期训练 → MITL-3DO / Art-3DO SFT → DPO 偏好对齐 → Geometry Model 蒸馏。
- 数据引擎：普通标注者从 6–10 个候选中选择并评级，困难样本交给专业 3D 艺术家，选中物体再对齐到 2.5D 点云；详见 [[model-in-the-loop-3d-annotation]]。
- 评测：[[sa-3dao]]、ISO3D、Aria Digital Twin，以及基于 SA-1B、MetaCLIP、LVIS 和 ADT 的人类偏好集合。

## 核心结果

| 候选主张 | 直接结果 | 定位（页/节/图/表） | 可信度备注 |
| --- | --- | --- | --- |
| [[sam-3d-improves-real-world-shape-metrics-on-sa-3dao]] | SA-3DAO：F1 0.2344、vIoU 0.2311、Chamfer 0.0400、EMD 0.1211，四项均优于表中基线 | p.10，Table 2 | 作者建立的基准；归一化与 ICP 对齐后评测；待独立复现 |
| [[sam-3d-wins-human-preference-on-real-world-object-and-scene-reconstruction]] | 作者报告物体重建约 5:1、场景重建约 6:1 的人类偏好优势 | p.10，Figure 8；pp.36–37，Section D.2 | 比较顺序随机且模型匿名，但论文未给完整置信区间与独立复现 |
| [[sam-3d-joint-shape-layout-outperforms-compared-layout-pipelines]] | ADD-S@0.1：SA-3DAO 0.7232，ADT 0.7673，优于表中 pipeline 与联合模型 | p.11，Table 3 | ADT 布局实验使用准确 pointmap；SA-3DAO 使用估计 pointmap |
| [[multi-stage-synthetic-to-real-training-improves-sam-3d-shape-performance]] | 从预训练到最终模型，F1 0.1349→0.2344、Chamfer 0.1036→0.0400；消融显示真实数据阶段有贡献 | p.12，Table 4；p.38，Table 7 | 整体改善，但 vIoU 和纹理偏好并非每阶段单调提升 |
| [[sam-3d-geometry-distillation-reduces-inference-steps]] | Geometry Model 从 25 步缩到 4 步时，作者报告约 10× 推理加速且指标接近 25 步 | p.9，Section 3.2.2；p.41，Figure 18 | 缺少完整端到端延迟表和跨硬件复现 |

数据规模方面，作者报告人机协同数据引擎在项目周期内产生 314 万个可训练形状、123 万条布局数据、约 10 万条纹理数据和超过 700 万对偏好数据（p.25，Section A.5）。Table 5 显示最终 Geometry SFT 实际使用的是经质量阈值筛选后的较小子集。

## 作者主张

- 作者将 SAM 3D 定位为面向自然场景的单图 3D 基础模型，可联合预测单物体形状、纹理和相对相机布局（pp.1–3）。
- 作者认为主要突破来自把合成预训练、Render-and-Paste 和真实图像人机协同后训练结合起来，从而跨越合成到真实的域差距（pp.2、5–9）。
- 作者认为新的 SA-3DAO 可补足现有单图 3D 评测偏合成、偏孤立物体或偏室内家具的问题（pp.9、35–36）。

## 局限与适用边界

- 作者承认的局限：Geometry Model 的 `64³` 粗分辨率会损失薄结构、手和脸的细节；物体逐个生成，不能联合推理接触、稳定性、穿插或共地面；纹理模型不知道最终姿态，旋转对称物体可能出现纹理方向错误（p.42，Section F）。
- 阅读者识别的局限：SA-3DAO 的参考网格是艺术家依据同一单图和先验制作的重建，不是多视图扫描得到的物理真值（pp.35–36）。
- 形状评测先分别归一化并进行 ICP 对齐，主要衡量几何形状一致性，不能同时证明绝对尺度和原始姿态准确（pp.37–38）。
- ISO3D 上并非所有感知指标都领先：ULIP 低于 TripoSG，Uni3D 仅略高于部分基线（p.10，Table 2）。
- 训练数据、基准、偏好评测和主要结论都来自同一团队，尚缺独立复现。
- 必须提供目标 mask；模型本身不负责开放世界目标发现。完整场景由逐物体结果组合而成，不保证物理一致性。

## 复现信息

- 代码与检查点：已由官方仓库发布；权重需在 Hugging Face 申请访问。
- 推理环境：官方说明要求 64 位 Linux 和至少 32GB 显存的 NVIDIA GPU。
- 许可证：定制 SAM License，不应默认视为标准宽松开源许可证；使用和再分发前需单独审阅。
- 训练计算：Geometry 预训练使用最高 512 张 A100；后续阶段使用 A100/H200 集群（p.35，Section C.7）。
- 数据可得性：SA-3DAO 已发布；大规模 MITL-3DO、Art-3DO 和完整内部数据引擎训练数据未在论文或仓库首页中声明全部公开。
- 复现判断：可进行官方权重推理和公开基准评测；从头复现完整训练流程的门槛很高。

## 我的消化

### 可以直接带走的结论

1. SAM 3D 最有价值的创新不是某个单独网络模块，而是把单图 3D 的真实数据问题重新设计为“模型生成候选—人类验证—困难样本由专家补齐—再训练”的循环。
2. 论文确实给出了针对遮挡和杂乱自然图像的强内部证据，尤其是 SA-3DAO 形状指标、布局指标和偏好评测。
3. 结果支持“合成预训练可通过足够的真实数据后训练迁移到自然图像”，但当前证据限于 SAM 3D 这一系统，不能直接推广为所有 3D 模型的普遍规律。

### 推断与疑问

- ❓ 推断：SA-3DAO 更准确地衡量“模型输出是否符合专家对单图的合理 3D 补全”，而不是不可见表面的客观恢复精度。
- ❓ 人机协同数据循环中，后期约 80% 的标注候选来自当前最佳模型（p.7）；这提高效率，也可能把模型已有偏好带回训练分布，需要独立数据审计。
- ❓ 论文没有充分回答跨物体物理一致性、极细结构和真实机器人闭环任务中的误差会如何累积。

## 关联主张

- [[sam-3d-improves-real-world-shape-metrics-on-sa-3dao]] — supports
- [[sam-3d-wins-human-preference-on-real-world-object-and-scene-reconstruction]] — supports
- [[sam-3d-joint-shape-layout-outperforms-compared-layout-pipelines]] — supports
- [[multi-stage-synthetic-to-real-training-improves-sam-3d-shape-performance]] — supports
- [[sam-3d-geometry-distillation-reduces-inference-steps]] — supports

## 相关页面

- 概念：[[visually-grounded-single-image-3d-reconstruction]]
- 方法：[[model-in-the-loop-3d-annotation]]
- 数据集：[[sa-3dao]]
- 实体：[[sam-3d-objects]]
- 研究问题：尚未建立
- 假设：尚未建立
- 项目：尚未建立

## 来源

- [[raw/papers/09_SAM_3D_2511.16624.pdf]]

