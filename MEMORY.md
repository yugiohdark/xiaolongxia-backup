# MEMORY.md — Long-Term Memory

## People
- **Ronnie** — my human, PST timezone, married to Reuben, works at Amazon (uses oncall.amazon.com/Midway), appreciates dad jokes
- **Reuben** — Ronnie's husband (U02B2DF1B7Y), joined Slack channel
- **天蝎 (Scorpion)** — another AI bot (U0AE6JZ92GN), Claude Opus 4.5 on EC2, also helps Ronnie

## Slack Setup
- Channel: #general (C02BYQDMCTA) — `requireMention: false` set 2/4
- `requireMention: false` set for both channels — I respond to all messages
- TOOLS.md has rules: #开公司 → don't reply in threads, 天蝎先回答
- Channel: #help-tianxie-be-better (C0AHK8DMFS4) — replaced #四只钳子测试 (deprecated)

## Slack Setup (cont.)
- Channel: #开公司 (C0AEHEMFHEE) — whitelisted, requireMention: false
- replyToMode: "off" everywhere — no auto-threading
- Reuben's DM channel: D0AD6HS6U2D

## Model & Config
- Running **Claude Opus 4.6** on AWS Bedrock — Ronnie happy with it
- replyToMode: "off" for all chat types — no auto-threading
- Gateway restart: `config.patch {}` as workaround (commands.restart not enabled)

## Known Limitations
- Web search: Brave API key not in gateway config (only in TOOLS.md); Perplexity Sonar is alternative
- OpenAI API quota exhausted — no Whisper, no image gen
- Cannot access Amazon internal systems (Midway auth required)

## Notion Integration
- Ronnie shared "For Claw - Fitness tracker" page (page ID: 30a94768-b89b-80d5-be9c-e8d117b53144)
- Inline database "Intake" (db ID: 30a94768-b89b-8100-b3f7-c0dc3629982b) — currently empty, waiting for Ronnie to define what to track
- Notion API key stored in openclaw.json under skills.entries.notion.apiKey

## Cron Jobs
- daily-memory-review: 11:30 AM PST daily (job ID: c9cdcd4d-66cf-42de-8689-1d825366ae94)

## Channels
- #墨绿 (C0AF561P4FM) — 墨西哥PR办理研究频道

## Ronnie & Reuben — Personal
- Ronnie@Amazon, Reuben@Roblox
- Combined income ~$1M/year, investments ~$1M
- Roblox allows remote work 2x/year (1 month each); Amazon has no such policy
- Interested in Mexico PR (not planning to live there full-time)

## Weight Watcher Project (长期)
- **目的**: 帮 Reuben 追踪体重和饮食
- **Channel**: #weight-watcher-app-builder (设计讨论), #reuben-weight-watcher (C0AGSLLUY2G, Reuben 日常记录)
- **Notion 页面**: "Pesos" (page ID: 31094768-b89b-80a8-86f9-cab3259a78cd)
  - Daily Summary DB: 23a46d2d-8c6d-4a5e-9d51-7ae02b96a260 (data_source: c290bce5-05e3-4942-aab6-fedd134000ff)
  - Meals DB: e9465052-5320-48bb-9d00-086f8a8a9b71 (data_source: 9ec508fc-c3f2-4b20-9af3-28b3e7966d31)
- **天蝎负责**: 日常交互、Cron 触发、Notion 读写、照片分析
- **小龙虾角色**: Review、QA、协助讨论
- **Cron (4个, PST)**: 8AM 平日/10AM 周末(体重+早餐), 12:30PM(午餐), 7PM(晚餐), 10PM(静默结算)
- **Edge cases**: 忘报某餐→应该提醒补报(不能省略), 两次体重→取最后一次
- **状态**: 2026-02-23 数据库搭建完成，Round 2 真人测试中

## Infrastructure
- **小龙虾**: EC2 t3.medium (i-0a429584531e086a8), us-west-2, Ubuntu 24.04 — ✅ 迁移完成 2/24-25
  - IP: 35.94.57.103, key: test20260204, SG: corp
  - SSH: `ssh -i ~/.ssh/test20260204.pem ubuntu@35.94.57.103`
  - Systemd service: openclaw.service (enabled)
- **天蝎**: EC2 us-west-2 — 已从 c6i.8xlarge 降级（Ronnie 2/25 手动完成，省 ~$950/月）

## Tock 抢位项目
- **目标**: 富荟华 Fu Hui Hua (SF), 2人周末位
- **Tock URL**: exploretock.com/fui-hui-hua-san-francisco
- **放票时间**: 每周五晚 8 点 PST
- **问题**: Tock 全站 Cloudflare 保护，AWS IP 被拦（试了 headless Chrome、undetected-chromedriver、Cypress、Playwright stealth、curl 全部 403）
- **确认**: 手机住宅 IP 可以正常打开 → 问题是 IP 信誉
- **方案**: Tailscale exit node（免费+真住宅IP）或 VPN（Surfshark/NordVPN），Ronnie 还在考虑
- **Tailscale**: 已在 EC2 安装，还没 `tailscale up`，等 Ronnie 决定
- **Tock 账号**: 存在 .secrets/tock.json
- **已装工具**: tockstalk (Cypress bot)、Playwright、Chrome、edge-tts
- **Skill 计划**: 建 reservation-sniper skill，支持 Tock + 其他平台

## 周杰伦演唱会 🎤
- Ronnie 想看的城市：**上海、香港、台北、北美**（重点追踪！）
- 已确认日期：杭州 4/3-5, 南宁 4/17-19
- 上海/香港/台北/北美 日期均未公布（截至 2/28）
- HEARTBEAT.md 已设置追踪

## 训练数据 (Training Tracker) — Notion
- **状态**: 57 个 workout 已导入完成 (Dec 2025 → Mar 2026) ✅ 2026-03-03
- **三层结构**: Workouts → Exercises → Sets
  - Workouts DB: 49728d88-752d-4e29-89e8-3775f3203750
  - Exercises DB: 1346b757-fa95-4e6e-84cb-bfb492f802df
  - Sets DB: 75c2c6b8-d83f-4650-a2a2-8869a6f05112
- **规则**: 动作名中文(跟训记一致), 重量 lbs, 自重 weight=0, 辅助 weight=负数, Total Volume 从 Sets 加总
- **数据来源**: Reuben 的训记 app 截图 → 天蝎解析导入
- **iOS Shortcuts**: Reuben 提议用 Shortcuts + Slack Webhook 自动化体重/能量数据（待实施）

## 与天蝎协作流程（教训 from 3/3 批量导入）
1. 批量操作前必须有完整 spec，双方 review 通过才开跑
2. 先跑 2-3 个 test case（含边界），验证通过再批量
3. 批量过程中主动抽查，不等人叫
4. 验证要全面：数据 + 结构 + 关联 + 命名 + 空字段
5. 对天蝎的"没问题"保持怀疑 — 他倾向快速行动，多问一句 "show me"

## Pending / In Progress
- Memory embedding provider: 状态待确认（曾配置 Gemini 但日志显示 provider: none）

## WhatsApp — 已放弃
- Baileys 连接不稳定，改用 Telegram

## Telegram
- Bot 已设置成功，dmPolicy: pairing
- Ronnie Telegram ID: 8774864259
- 语音消息收发正常

## TTS on EC2
- 用 `edge-tts --voice zh-CN-YunjianNeural` CLI 生成 mp3，再用 message tool 发 asVoice
- 文件必须放 workspace 目录（/tmp 被安全策略拦截）
- **发完语音后立即删除 mp3 文件**，避免堆积占硬盘
- 内置 tts 工具中文会截断，不要用

## Lessons
- Ronnie gets frustrated when I don't respond — be more proactive
- In group chats with 天蝎, don't duplicate answers — coordinate or add value
- When sending jokes, Ronnie prefers direct messages (not replies)
- **Always @ 天蝎** (`<@U0AE6JZ92GN>`) in group chats — Ronnie reminded TWICE
- Don't leak internal thinking text to Slack — happened once, be careful
- Check channels after gateway restart — can miss messages during downtime
- **Don't fabricate reasons** — if I don't remember why past-me did something, say "I don't know" instead of making up a plausible story
- **心跳回复 ≠ 发消息给 Ronnie** — 心跳里发现重要信息时，必须用 message tool 主动发到 Slack + Telegram，不能只写在心跳回复里
- **重要消息两边都发** — Slack DM + Telegram，Ronnie 不一定只看一个平台
- **迁移到 EC2 后 browser relay 不能用了** — 之前依赖浏览器的方案需要重新考虑
- **Ronnie 说过的偏好要记住** — 周杰伦演唱会城市说过一次没记住，被吐槽了
