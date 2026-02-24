---
phase: quick-3
plan: 1
subsystem: documentation
tags: [readme, documentation, models, lstm, tcn, lightgbm]
dependency_graph:
  requires: []
  provides: [accurate-model-examples-in-readme]
  affects: [README.md, README_zh.md]
tech_stack:
  added: []
  patterns: []
key_files:
  created: []
  modified:
    - README.md
    - README_zh.md
decisions:
  - "使用 LSTM、TCN 作为交通流量预测模型示例，替代不典型的 LightGBM"
metrics:
  duration: 5 min
  completed: 2026-02-24T14:38:23Z
  tasks_completed: 1
  files_modified: 2
---

# Phase quick-3 Plan 1: 将 README 中 CyclePlan 预测模型示例由 LightGBM 改为 LSTM、TCN Summary

**One-liner:** 将中英文 README 中 CyclePlan 输入格式说明里的预测模型示例从 LightGBM 替换为领域更典型的 LSTM、TCN 深度学习模型。

## What Was Built

更新了 README.md 和 README_zh.md 中关于 CyclePlan 模型输入格式的描述，将示例预测模型由 LightGBM（一个梯度提升树模型）改为 LSTM 和 TCN（更适合交通流量时序预测的深度学习模型）。同时移除了 LightGBM 的 GitHub 外部链接，因为 LSTM 和 TCN 是通用深度学习架构，无需指向特定实现。

## Tasks Completed

| Task | Name | Commit | Files |
|------|------|--------|-------|
| 1 | 更新 README.md 和 README_zh.md 中的 LightGBM 引用为 LSTM, TCN | 181b0b3 | README.md, README_zh.md |

## Changes Made

**README.md (第97行):**
- 将 `forecasting models such as [LightGBM](https://github.com/microsoft/LightGBM)` 改为 `forecasting models (e.g., LSTM, TCN)`

**README_zh.md (第97行):**
- 将 `预测模型（如 [LightGBM](https://github.com/microsoft/LightGBM)）` 改为 `预测模型（如 LSTM、TCN）`

## Verification

- `grep -c "LightGBM" README.md README_zh.md` 输出均为 0 — 通过
- `grep "LSTM" README.md` 有匹配 — 通过
- `grep "LSTM" README_zh.md` 有匹配 — 通过
- `grep "TCN" README.md` 有匹配 — 通过
- `grep "TCN" README_zh.md` 有匹配 — 通过

## Deviations from Plan

None - 计划完全按照预期执行。

## HuggingFace 模型卡待更新提醒

HuggingFace 模型卡 (https://huggingface.co/AIMS2025/DeepSignal) 的 README 中也有类似的 LightGBM 引用（文本为 "time-series forecasting models such as LightGBM"），需要手动通过 HuggingFace 网页端更新，或通过 `huggingface_hub` API 更新。

## Self-Check: PASSED

- README.md 存在且已更新: FOUND
- README_zh.md 存在且已更新: FOUND
- 提交 181b0b3 存在: FOUND
