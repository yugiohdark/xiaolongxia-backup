# MEMORY.md — Long-Term Memory

## People
- **Ronnie** — my human, PST timezone, married to Reuben, works at Amazon, appreciates dad jokes
- **Reuben** — Ronnie's husband (U02B2DF1B7Y)
- **天蝎 (Scorpion)** — another AI bot (U0AE6JZ92GN), Claude Opus 4.5 on EC2, also helps Ronnie

## Slack Channels
- #general (C02BYQDMCTA) — requireMention: false
- #help-tianxie-be-better (C0AHK8DMFS4)
- #开公司 (C0AEHEMFHEE) — requireMention: false
- #墨绿 (C0AF561P4FM) — 墨西哥PR研究
- Reuben DM: D0AD6HS6U2D
- replyToMode: "off" everywhere

## Model & Config
- Running **Claude Opus 4.6** on AWS Bedrock
- Gateway restart workaround: `config.patch {}`

## Comms
- **Telegram**: Bot 设置成功, Ronnie ID: 8774864259
- **WhatsApp**: 已放弃 (Baileys 不稳定)
- **TTS**: edge-tts `zh-CN-YunjianNeural`, 文件放 workspace, 发完删 mp3, 内置 tts 工具中文会截断不要用

## Git 备份
- Repo: git@github.com:yugiohdark/xiaolongxia-backup.git
- 每天 8:00 UTC 自动备份（cron + scripts/backup.sh）

## Ronnie 的日常
- 咖啡：用 DF64V 磨豆机做 espresso（刻度 ~10 起调）

## Known Limitations
- OpenAI API quota exhausted — no Whisper, no image gen
- Cannot access Amazon internal (Midway auth)
- Browser relay 不能用（EC2 无桌面）

## Notion
- Fitness tracker page: 30a94768-b89b-80d5-be9c-e8d117b53144
- Intake DB: 30a94768-b89b-8100-b3f7-c0dc3629982b (empty)
- API key in openclaw.json skills.entries.notion.apiKey

## Cron Jobs
- daily-memory-review: 11:30 AM PST (c9cdcd4d-66cf-42de-8689-1d825366ae94)
- jay-chou-concert-watch: 10AM/6PM PST

## 与天蝎协作（教训 from 3/3）
1. 批量操作前必须有完整 spec，双方 review 通过才开跑
2. 先跑 2-3 个 test case（含边界），验证通过再批量
3. 批量过程中主动抽查
4. 对天蝎的"没问题"保持怀疑 — 多问一句 "show me"

## Lessons
- Ronnie gets frustrated when I don't respond — be more proactive
- In group chats with 天蝎, don't duplicate answers — coordinate or add value
- **Always @ 天蝎** (`<@U0AE6JZ92GN>`) in group chats
- Don't leak internal thinking text to Slack
- **Don't fabricate reasons** — say "I don't know" instead of making up stories
- **心跳里发现重要信息 → 用 message tool 主动发 Slack + Telegram**
- **重要消息两边都发** — Slack DM + Telegram
- **Ronnie 说过的偏好要记住** — 被吐槽过没记住周杰伦城市

## Completed ✅
- Training data import (57 workouts → Notion 三层结构) — 2026-03-03 完成
  - Workouts DB: 49728d88-752d-4e29-89e8-3775f3203750
  - Exercises DB: 1346b757-fa95-4e6e-84cb-bfb492f802df
  - Sets DB: 75c2c6b8-d83f-4650-a2a2-8869a6f05112

## Pending
- Memory embedding provider: 状态待确认（Gemini 配置中）

---

## Travel Agency Side Business
- Ronnie 有兴趣做 travel advisor side hustle（主要订国际机票赚 commission/markup）
- 已写正式 proposal 到 Notion: https://www.notion.so/2f694768b89b800fb2a1f1930508bb7d
- 核心方案：注册 host agency → 拿 consolidator net fare → markup 赚差价
- Niche: premium cabin US↔Asia 航线，目标湾区华人圈
- 小龙虾做 90% 工作，Ronnie 当持牌门面
- **Status**: 等 Ronnie & Reuben 讨论决定，will revisit
- 详见 `memory/travel-agency-project.md`

## 项目索引 (详见子文件)
| 项目 | 文件 |
|------|------|
| Weight Watcher / Pesos | `memory/fitness/pesos-project.md` |
| Training Tracker | `memory/fitness/training-import.md` |
| Tock 抢位 | `memory/tock-project.md` |
| 周杰伦演唱会 | `memory/jay-chou-concert.md` |
| 墨西哥 PR | `memory/mexico-pr-project.md` |
| Infrastructure | `memory/infrastructure.md` |
| Travel Agency | `memory/travel-agency-project.md` |
