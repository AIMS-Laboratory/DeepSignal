# DeepSignal README 更新

## What This Is

为 DeepSignal 项目的 README.md 和 README_zh.md 完成全量扩写更新，新增了 DeepSignal-CyclePlan-4B-V1（信号周期规划模型）的功能介绍、评估对比表格、Prompt 说明、GGUF 推理示例，并添加了 Changelog 部分。原有内容完整保留，中英文双语同步更新。

## Core Value

README 准确、完整地反映项目当前的两个模型（DeepSignal-Phase-4B-V1 和 DeepSignal-CyclePlan-4B-V1）及其评估结果，中英文版本同步更新。

## Requirements

### Validated

- ✓ 在 README.md 和 README_zh.md 开头更新项目描述，反映现在有两个模型 — v1.0
- ✓ 重命名原模型为 DeepSignal-Phase-4B-V1，新增 DeepSignal-CyclePlan-4B-V1 — v1.0
- ✓ 添加 Changelog 部分（放在 Key idea 之后、Scenarios 之前） — v1.0
- ✓ 新增 CyclePlan 模型的功能介绍和 Prompt 说明 — v1.0
- ✓ 新增 CyclePlan 模型的评估结果对比表（4 项指标，throughput 已换算） — v1.0
- ✓ 更新 GGUF 部分，说明 CyclePlan 模型有 F16 和 Q4_K_M 两个量化版本 — v1.0
- ✓ 更新 HuggingFace 链接说明 — v1.0
- ✓ 保留原 README 所有内容不删除 — v1.0
- ✓ 中英文双语同步更新 — v1.0

### Active

（无 — v1.0 已完成全部需求）

### Out of Scope

- 修改代码逻辑 — 本次只更新文档
- 添加微调代码 — 仓库明确说明暂不包含
- 修改原有评估数据 — 原模型的数据保持不变

## Context

已完成 v1.0，README.md 和 README_zh.md 均已全量更新。
- 技术栈：Markdown 文档
- 修改文件：README.md, README_zh.md（+280 行，-14 行）
- 两个模型均已完整文档化：DeepSignal-Phase-4B-V1（相位预测）和 DeepSignal-CyclePlan-4B-V1（周期规划）
- 所有模型统一发布在 HuggingFace AIMS2025/DeepSignal

## Constraints

- **内容保留**: 原 README 所有内容不得删除，只能扩写 ✓ 已满足
- **双语同步**: README.md（英文）和 README_zh.md（中文）同步更新 ✓ 已满足
- **Changelog 位置**: 放在 "Key idea" 之后、"Scenarios" 之前 ✓ 已满足

## Key Decisions

| Decision | Rationale | Outcome |
|----------|-----------|---------|
| 原模型更名为 DeepSignal-Phase-4B-V1 | 区分两个模型的功能 | ✓ Good |
| 新模型命名 DeepSignal-CyclePlan-4B-V1 | 反映周期规划功能 | ✓ Good |
| Changelog 放在 Key idea 后、Scenarios 前 | 用户指定位置 | ✓ Good |
| 排除 constraint_satisfaction_rate 等 3 个指标 | 用户指定不展示 | ✓ Good |
| throughput 乘以 60 显示为 veh/min | 用户要求换算 | ✓ Good |
| CyclePlan Prompt 在英文 README 用英文 | 语言匹配规则 | ✓ Good |
| GGUF 章节用子标题区分模型 | 提高文档清晰度 | ✓ Good |

---
*Last updated: 2026-02-23 after v1.0 milestone*
