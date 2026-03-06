# Tock 抢位项目

## 目标
富荟华 Fu Hui Hua (SF), 2人周末位

## 信息
- **Tock URL**: exploretock.com/fui-hui-hua-san-francisco
- **放票时间**: 每周五晚 8 点 PST
- **Tock 账号**: 存在 .secrets/tock.json

## 问题
- Tock 全站 Cloudflare 保护，AWS IP 被拦
- 试过: headless Chrome、undetected-chromedriver、Cypress、Playwright stealth、curl — 全部 403
- 手机住宅 IP 可以正常打开 → 问题是 IP 信誉

## 方案
- Tailscale exit node（免费+真住宅IP）或 VPN（Surfshark/NordVPN）
- Tailscale 已在 EC2 安装，还没 `tailscale up`，等 Ronnie 决定

## 已装工具
- tockstalk (Cypress bot)、Playwright、Chrome、edge-tts

## Skill 计划
- 建 reservation-sniper skill，支持 Tock + 其他平台
