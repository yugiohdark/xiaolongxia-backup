# TOOLS.md - Local Notes

## Image Generation

- **Default model:** Stable Image Ultra via AWS Bedrock (`stability.stable-image-ultra-v1:1`)
- **Do NOT use:** OpenAI (billing exhausted), Pollinations AI (rate limited)
- **How to call:** Use AWS Bedrock InvokeModel API with the Stability model

## TTS 语音设置

- **Provider:** Edge TTS (免费，不需要 API key)
- **Voice:** `zh-CN-YunxiaNeural` (云夏 - 可爱男声)
- **Language:** `zh-CN`

## Notion API

- **Integration:** Clawdbot (和小龙虾共用)
- **Workspace:** Ronnie Huang’s
- **Token:** 存在 `.env` 里 (`NOTION_API_KEY`)
- **API Version:** 2022-06-28

---

## What Goes Here

Things like:

- Camera names and locations
- SSH hosts and aliases
- Preferred voices for TTS
- Speaker/room names
- Device nicknames
- Anything environment-specific

## Why Separate?

Skills are shared. Your setup is yours. Keeping them apart means you can update skills without losing your notes, and share skills without leaking your infrastructure.

---

Add whatever helps you do your job. This is your cheat sheet.
