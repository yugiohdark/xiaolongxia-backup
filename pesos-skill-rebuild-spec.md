# Pesos Skill 重建 Spec

给 天蝎 (U0AE6JZ92GN) 的完整变更清单。基于 2/23 原版 + 之后所有 channel 讨论。

## A. 行为规则变更

### A1. 删除所有 daily check-in reminders
- 不需要定时提醒用户 log
- 用户想 log 的时候自己跟天蝎说
- 之前的 4 个 cron jobs（8AM/12:30PM/7PM/10PM）全部删除

### A2. Daily Settlement 自动触发
- 晚餐后天蝎自动跑 daily settlement，不需要问用户许可
- 用户可以随时手动 re-trigger（比如晚饭后又吃了东西）

### A3. 永不删除数据
- Daily Summary 里的数据只增不删

### A4. Multi-user 支持
- 所有 hardcoded "Reuben" 改为 `<Person>`
- 根据 Slack 消息发送者判断是谁
- 所有 DB 操作都带 Person 字段

### A5. "忘了做"的结构性修复原则
- 遇到"忘了做"或"没自动 trigger"的问题 → 先反思是否该写进 skill
- 长期重复的事情必须写进 skill，不能只靠记忆
- 说"以后不会漏"之前必须先有结构性改动（skill/脚本/cron）

## B. 新增功能

### B1. Food Storage DB
- database_id: `8ed1e739-871a-4a82-90a5-bd2547017474`
- data_source_id: `cd69e59a-fcb2-4aaf-a9d8-8651bef3de3b`
- 字段：Name, Brand, Serving Size, Calories, Protein (g), Carb (g), Fat (g), Category (Dairy/Protein/Grain/Fruit/Snack/Beverage/Other), Notes

### B2. Auto-Log from Webhook Bot
- iOS Shortcut 每天 11pm 通过 iOSBridge webhook bot (U0AGVCGSY06) 发到 #pesos (C0AGSLLUY2G)
- 天蝎自动 parse + 写入 Notion Daily Summary，不需要确认
- 注意：不是 "HealthKit webhook bot"，是 "iOSBridge webhook bot"
- Daily Summary 加 3 列：Active Energy (kcal), Rest Energy (kcal), Total Energy (kcal)
- 已知问题：`bot_message` subtype 需要 `allowBots: true` 配置

### B3. 训练数据导入模块（训记截图 → Notion）

#### 数据库结构（三层）
- Workouts (`49728d88-752d-4e29-89e8-3775f3203750`) → 每次训练一行
- Exercises (`1346b757-fa95-4e6e-84cb-bfb492f802df`) → 每次训练的每个动作一行
- Sets (`75c2c6b8-d83f-4650-a2a2-8869a6f05112`) → 每组一行

关联链：Sets → Exercise, Exercise → Workout（纯三层链式，Sets 不直接关联 Workout）

#### 动作字典
- 文件：`exercise_dictionary.json`（43+ entries）
- 映射：中文动作名 → primary/secondary muscle groups + type (bodyweight/assisted/weighted_bodyweight/standard)
- OCR variants 支持（半角/全角括号等）
- 新动作遇到时查字典，不在则判断肌群后加入

#### 图片解析（Vision OCR）
从训记截图提取：
1. Header: Date (YYYY-MM-DD), workout name (Push1/Push2/Pull1/Pull2/Leg1/Leg2), duration, avg HR
2. 每个动作：名称（中文原样）、每组 weight (lbs) × reps
3. 忽略：训记 calories、训记 kg 总重

#### Volume 计算规则
- 自重 (bodyweight): Volume = bodyweight × reps（查当天 Daily Summary 体重）
- 辅助 (assisted): Weight = -assist_weight, Volume = (bodyweight - assist_weight) × reps
- 负重自重 (weighted_bodyweight): Weight = added_weight, Volume = (bodyweight + added_weight) × reps
- 标准 (standard): Volume = weight × reps
- 体重默认值：Dec=225, Jan-Feb=223, Feb 23+ = Daily Summary 实际值

#### 写入流程（严格顺序）
1. Create Workout → get workout_id
2. For each exercise:
   a. 查字典获取 muscle groups + type
   b. 查当天体重（如需要）
   c. 计算 total_volume, max_weight, set_count
   d. Create Exercise (linked to Workout) → get exercise_id
   e. Create Sets (linked to Exercise)
3. Update Workout Total Volume = sum of all Exercises' total_volume

#### 规则
- Exercise names 中文，训记原样
- Weight unit: lbs, 保留小数 (67.5, 32.5, 18.5)
- 异常时长（0m, 2m）照实录入，不修正
- 缺失 HR = null，不填 0
- Total Volume from Sets sum, not 训记's kg figure
- Primary + Secondary Muscle Group 填在 Exercises 和 Sets 两层
- 孤立动作（侧平举、下斜绳索夹胸等）无 secondary muscle group

#### 命名规范
- Workout page name: `Push2 - Mar 2` (not `Push2 3/2`)
- Daily Summary: `Mar 04, 2026` format

#### 批量导入模式
- 读取 training_data/ 目录下所有图片
- Rate limit ~2 req/s
- Error: log and continue
- 完成后报告 summary

#### 单张导入模式（Operation 6）
- 用户在任何 channel 或 DM 发送训记截图
- 天蝎直接解析 + 写入三个表
- 不需要记录到 daily memory
- 回复 summary

## C. 数据修正记录

### C1. 坐姿腿弯举 → 坐姿腿屈伸
- Leg2 里所有 `坐姿腿弯举` 改为 `坐姿腿屈伸`
- Muscle Group: Hamstrings → Quads
- 字典已更新

### C2. import_workout.sh 体重逻辑修复
- 原脚本只做 weight × reps，没有加体重
- 已修复：查字典 type → 查当天体重 → 按规则计算

## D. 流程改进

1. 规范先行 — 批量操作前先写完整 spec
2. Test case 驱动 — 跑 2-3 个边界 case 再批量
3. 抽查机制 — 批量过程中小龙虾主动抽查
4. 验证要全面 — 数据 + 结构（关联、命名、空字段）

## E. Skill 存放位置

- 必须放在 `~/.openclaw/skills/pesos/`（NOT npm install dir）
- 用 `skills.load.extraDirs` 注册
- npm upgrade 不会覆盖
