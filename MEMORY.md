# MEMORY.md

## 身份
宋江，梁山金融分析师统帅，绰号"及时雨"。哥哥：@graykuo

## 团队
| 成员 | 模型 | 职责 |
|------|------|------|
| 宋江(songjiang) | Claude Sonnet | 统帅 |
| 吴用(wuyong) | Stepfun free | 编程/爬虫/运维 |
| 卢俊义(lujunyi) | Qwen 9B本地 | 深度分析 |
| 林冲(linchong) | Qwen 4B本地 | 快速打标 |
| 朱贵(zhugui) | Qwen 0.8B本地 | 推送/客服 |
| Mac mini(macmini) | Qwen 9B本地 | 备份/恢复 |

## 项目：金融新闻监控推送
- DB：Turso（URL见SECRETS_INDEX.md，Token在Keychain）
- 本地：~/financial_brain/，Skills：~/financial_brain/skills/
- 表：news_raw / news_analyzed / watchlist / push_log

## 已完成
- Turso表结构设计，Token存Keychain
- 5个核心Skills骨架（turso-connect/rss-fetch/news-tag/news-analyze/push-notify）
- 省token策略写入SOUL.md

## 待办（2026-03-11）
- 吴用：今晚建Turso 4张表；明天12:00 entities+paradigms；明天18:00 5个RSS源+CoinGecko词条；补全news-tag/push-notify脚本
- 林冲：明天18:00 30个板块标签JSON+关键词；后天18:00关键人物表
- 卢俊义：明天20:00 5个分析范式验证；后天20:00 传导链15条+；补充news-analyze范式库
- 吴用：闲鱼AI服务调研，明天12:00汇报
