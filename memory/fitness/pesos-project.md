# Weight Watcher (Pesos) Project

## 概述
帮 Reuben 追踪体重和饮食

## Channels
- #weight-watcher-app-builder — 设计讨论
- #reuben-weight-watcher (C0AGSLLUY2G) — Reuben 日常记录

## Notion
- **页面**: "Pesos" (page ID: 31094768-b89b-80a8-86f9-cab3259a78cd)
- Daily Summary DB: 23a46d2d-8c6d-4a5e-9d51-7ae02b96a260 (data_source: c290bce5-05e3-4942-aab6-fedd134000ff)
- Meals DB: e9465052-5320-48bb-9d00-086f8a8a9b71 (data_source: 9ec508fc-c3f2-4b20-9af3-28b3e7966d31)

## 分工
- **天蝎负责**: 日常交互、Cron 触发、Notion 读写、照片分析
- **小龙虾角色**: Review、QA、协助讨论

## Cron (4个, PST)
- 8AM 平日 / 10AM 周末 — 体重+早餐
- 12:30PM — 午餐
- 7PM — 晚餐
- 10PM — 静默结算

## Edge Cases
- 忘报某餐 → 应该提醒补报（不能省略）
- 两次体重 → 取最后一次

## 状态
- 2026-02-23 数据库搭建完成，Round 2 真人测试中
