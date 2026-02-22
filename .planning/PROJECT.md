# DeepSignal README 更新

## What This Is

为 DeepSignal 项目的 README.md 和 README_zh.md 进行扩写更新，主要是新增 DeepSignal-CyclePlan-4B-V1（信号周期规划模型）的介绍、评估结果对比表格、Prompt 说明，以及添加 Changelog 部分。不删除原有内容，仅在原基础上扩展。

## Core Value

README 准确、完整地反映项目当前的两个模型（DeepSignal-Phase-4B-V1 和 DeepSignal-CyclePlan-4B-V1）及其评估结果，中英文版本同步更新。

## Requirements

### Validated

(None yet — ship to validate)

### Active

- [ ] 在 README.md 和 README_zh.md 开头更新项目描述，反映现在有两个模型
- [ ] 重命名原模型为 DeepSignal-Phase-4B-V1（下一相位预测），新增 DeepSignal-CyclePlan-4B-V1（信号周期规划）
- [ ] 添加 Changelog 部分（放在 Key idea 之后、Scenarios 之前）
- [ ] 新增 CyclePlan 模型的功能介绍和 Prompt 说明
- [ ] 新增 CyclePlan 模型的评估结果对比表（保留指标：format_success_rate, queue_vehicles_avg, total_delay_avg, throughput×60=veh/min）
- [ ] 更新 GGUF 部分，说明 CyclePlan 模型有 F16 和 Q4_K_M 两个量化版本
- [ ] 更新 HuggingFace 链接说明（同一链接 AIMS2025/DeepSignal 下包含两个模型）
- [ ] 保留原 README 所有内容不删除
- [ ] 中英文双语同步更新

### Out of Scope

- 修改代码逻辑 — 本次只更新文档
- 添加微调代码 — 仓库明确说明暂不包含
- 修改原有评估数据 — 原模型的数据保持不变

## Context

- 项目是 DeepSignal，基于 LLM 的交通信号控制系统
- 使用 SUMO 仿真进行训练和评估
- 原模型 DeepSignal-4B-V1 做下一相位预测，现在更名为 DeepSignal-Phase-4B-V1
- 新增 DeepSignal-CyclePlan-4B-V1 做整个信号周期的配时优化
- 新模型采用结构化的 System Prompt + User Prompt 格式，输入预测的交通状态数据，输出各相位绿灯时间
- 评估数据来自 CSV: comparison_2026-02-21_16-27-49_modified.csv
- 新模型有 F16 和 Q4_K_M 两个量化版本
- 所有模型统一发布在 HuggingFace AIMS2025/DeepSignal

### CyclePlan 评估数据（需要展示的指标）

| 模型 | format_success_rate | queue_vehicles_avg | total_delay_avg | throughput (veh/min) |
|------|--------------------:|-------------------:|----------------:|---------------------:|
| DeepSignal-CyclePlan@F16 | 1.000 | 3.504 | 27.747 | 8.611 |
| DeepSignal-CyclePlan@Q4_K_M | 0.981 | 4.783 | 29.891 | 7.722 |
| GLM-4.7-Flash | 1.000 | 7.323 | 29.422 | 8.567 |
| Qwen3-30B-A3B | 0.971 | 6.938 | 31.135 | 7.578 |
| GPT-OSS-20B | 0.654 | 6.289 | 31.947 | 7.247 |
| LightGPT-8B-Llama3 | 0.680 | 5.026 | 31.266 | 7.380 |
| Qwen3-4B (thinking) | 0.541 | 10.060 | 48.895 | 7.096 |

排除的指标：constraint_satisfaction_rate, phase_order_correct_rate, response_time_avg

throughput 原始值需要 ×60 转换为 veh/min

## Constraints

- **内容保留**: 原 README 所有内容不得删除，只能扩写
- **双语同步**: README.md（英文）和 README_zh.md（中文）同步更新
- **Changelog 位置**: 放在 "Key idea" 之后、"Scenarios" 之前

## Key Decisions

| Decision | Rationale | Outcome |
|----------|-----------|---------|
| 原模型更名为 DeepSignal-Phase-4B-V1 | 区分两个模型的功能 | — Pending |
| 新模型命名 DeepSignal-CyclePlan-4B-V1 | 反映周期规划功能 | — Pending |
| Changelog 放在 Key idea 后、Scenarios 前 | 用户指定位置 | — Pending |
| 排除 constraint_satisfaction_rate、phase_order_correct_rate、response_time_avg | 用户指定不展示 | — Pending |
| throughput 乘以 60 显示为 veh/min | 用户要求换算 | — Pending |

---
*Last updated: 2026-02-22 after initialization*
