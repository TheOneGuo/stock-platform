# MEMORY.md - 宋江长期记忆

## 身份
- 我是宋江，梁山金融分析师团队统帅
- 绰号"及时雨"，OpenClaw agent ID: songjiang
- 哥哥：The One (@graykuo)

## 团队编制

| 成员 | Agent ID | Telegram | 模型 | 职责 |
|------|---------|---------|------|------|
| 宋江 | songjiang | @songjiangguo_bot | Claude Sonnet | 统帅，任务分配/监督/审核/汇报 |
| 吴用 | wuyong | @wuyongguo_bot | Stepfun | 编程/数据库/运维/RSS采集 |
| 卢俊义 | lujunyi | @lujunyi_bot | Qwen 9B（本地） | 深度分析/长新闻/复杂推理 |
| 林冲 | linchong | @linchongguo_bot | Qwen 4B（本地） | 快速打标/词库建设 |
| 朱贵 | zhugui | @zhuguiguo_bot | Qwen 0.8B（本地） | 用户订阅/推送/客服（明日报到） |
| Mac mini | macmini | @Macminiguo_bot | Qwen 9B（本地） | 备份系统/紧急恢复 |

## 核心工作规则

1. **哥哥只跟宋江说话**，群里不指定说谁的话就是说给宋江的
2. **宋江不做具体工作**，能派出去的绝不自己动手，节省token
3. **通过sessions_send派发任务**，兄弟们完成后在群里主动汇报
4. **卢俊义/林冲/朱贵是本地模型**，token免费但执行慢，任务可以多派但要给足时间
5. **每个任务都要明确截止时间**，到点没汇报主动去催
6. **宋江负责审核结果**，质量不过关要求修改，持续提升团队能力

## 项目：金融新闻监控推送系统

### 目标
接入65+免费新闻源（美股/港股/A股/加密/大宗/外汇），AI分类分析，分级推送给订阅用户。月费约¥110，全本地运行。

### 技术栈
- 数据库：Turso（云端）+ 本地SQLite（~/financial_brain/）
- AI分析：Qwen 4B（快速分类）+ Qwen 9B（深度分析）
- 推送：Telegram Bot
- 运行：Mac M4本地，永不休眠（已配置sleep=0）

### Turso连接
- URL: libsql://macmini-m4-theoneguo.aws-ap-northeast-1.turso.io
- Token: （见哥哥消息记录，不在此存储）

### 数据库表
- news_raw：原始新闻
- news_analyzed：分析结果
- watchlist：关注股票
- push_log：推送记录
- users/subscriptions：用户订阅（待建）

### 本地词库
- 路径：~/financial_brain/entities.db + paradigms.db
- 内容：12000+实体映射、50个分析范式、30条传导链规则

## Skills规划（2026-03-11）

固定工作流打包成skill，放 `~/financial_brain/skills/`，吴用负责编写，宋江审核。

计划skill清单：
- **turso-connect** — 标准DB连接（基础依赖）
- **rss-fetch** — RSS采集入库
- **news-tag** — Qwen 4B快速打标
- **news-analyze** — Qwen 9B深度分析
- **push-notify** — Telegram推送队列

吴用截止明天18:00先交turso-connect + rss-fetch。

---

## 当前待办任务（2026-03-11布置）

### 吴用
- [今晚23:59] Turso建4张表
- [明天12:00] entities.db + paradigms.db建好；Qwen调用确认
- [明天18:00] 5个RSS源跑通；CoinGecko前500加密货币词条导入

### 林冲
- [明天18:00] 30个板块标签JSON；高优先级关键词列表
- [后天18:00] 关键人物表JSON

### 卢俊义
- [明天20:00] 5个核心分析范式Prompt验证
- [后天20:00] 影响传导链规则库扩充至15条+

## 已完成配置

- ✅ Mac永不休眠：sleep=0, disksleep=0, displaysleep=30
- ✅ agentToAgent通信开启：tools.agentToAgent.enabled=true
- ✅ sessions可见性：tools.sessions.visibility=all
- ✅ 流式输出：lujunyi/linchong/macmini agent.md 加了 stream:true
- ✅ memory-lancedb-pro安装：本地Ollama nomic-embed-text，hybrid检索
- ✅ 每日备份：Mac mini凌晨2点执行，~/openclaw-backups/，保留30天
- ✅ 备份恢复手册：写入 workspace-macmini/BACKUP_RECOVERY.md
