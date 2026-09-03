# Research Wiki 内容目录

> 由 Agent 维护。每次正式 Ingest 后更新；查询时先读此文件定位相关页面。

## 研究问题（wiki/questions/）

| 页面 | 状态 | 优先级 | 一句话摘要 |
| --- | --- | --- | --- |

## 假设（wiki/hypotheses/）

| 页面 | 状态 | 关联问题 | 一句话摘要 |
| --- | --- | --- | --- |

## 科研主张（wiki/claims/）

| 页面 | 证据状态 | 来源数 | 一句话摘要 |
| --- | --- | ---: | --- |
| [[sam-3d-improves-real-world-shape-metrics-on-sa-3dao]] | 支持（单来源，待独立复现） | 1 | SAM 3D 在 SA-3DAO 的四项对齐后形状指标上优于论文所比较基线。 |
| [[sam-3d-wins-human-preference-on-real-world-object-and-scene-reconstruction]] | 支持（单来源，待独立复现） | 1 | 作者报告物体和场景重建约 5:1 与 6:1 的人类偏好优势。 |
| [[sam-3d-joint-shape-layout-outperforms-compared-layout-pipelines]] | 支持（单来源，条件限定） | 1 | SAM 3D 在 SA-3DAO 与 ADT 的布局指标上优于表中比较方法。 |
| [[multi-stage-synthetic-to-real-training-improves-sam-3d-shape-performance]] | 支持（单系统消融） | 1 | 合成到真实的分阶段训练整体改善形状性能，但并非每项指标单调提升。 |
| [[sam-3d-geometry-distillation-reduces-inference-steps]] | 初步支持（低信心） | 1 | Geometry Model 的 4 步 shortcut 推理被报告为约 10 倍加速且接近 25 步质量。 |

## 跨文献综合（wiki/synthesis/）

| 页面 | 范围 | 来源数 | 一句话摘要 |
| --- | --- | ---: | --- |

## 论文卡片（wiki/papers/）

| 页面 | 年份 | 阅读状态 | 优先级 | 一句话摘要 |
| --- | ---: | --- | --- | --- |
| [[sam3d-team-2025-sam-3d]] | 2025 | verified / full | high | 通过分阶段训练和人机协同数据引擎，从单张自然图像重建物体形状、纹理与布局。 |

## 概念（wiki/concepts/）

| 页面 | 来源数 | 一句话摘要 |
| --- | ---: | --- |
| [[visually-grounded-single-image-3d-reconstruction]] | 1 | 从自然图像的目标像素、上下文和先验推断完整 3D 形状、纹理与布局。 |

## 方法（wiki/methods/）

| 页面 | 来源数 | 一句话摘要 |
| --- | ---: | --- |
| [[model-in-the-loop-3d-annotation]] | 1 | 用模型候选、人类验证、专家补难例和偏好训练扩展真实图像 3D 标注。 |

## 数据集（wiki/datasets/）

| 页面 | 领域 | 来源数 | 一句话摘要 |
| --- | --- | ---: | --- |
| [[sa-3dao]] | 真实图像单图 3D 重建 | 1 | 由专业艺术家根据自然场景单图制作并对齐的 1,000 个无纹理参考网格。 |

## 实体（wiki/entities/）

| 页面 | 类型 | 来源数 | 一句话摘要 |
| --- | --- | ---: | --- |
| [[sam-3d-objects]] | software | 2 | Meta 的单图物体 3D 重建模型，区别于人体专用的 SAM 3D Body。 |

## 检索记录（wiki/searches/）

| 页面 | 检索日期 | 状态 | 一句话摘要 |
| --- | --- | --- | --- |

## 项目（wiki/projects/）

| 页面 | 状态 | 一句话摘要 |
| --- | --- | --- |

## 查询归档（wiki/queries/）

| 页面 | 日期 | 一句话摘要 |
| --- | --- | --- |
