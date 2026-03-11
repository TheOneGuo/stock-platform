# SECRETS_INDEX.md - 密钥索引

> ⚠️ 本文件只记录"有什么密钥、存在哪里、怎么取"，不含任何明文密钥值。
> 明文密钥存储在 macOS Keychain，重装前务必导出备份。

---

## Turso 数据库

| 项目 | 内容 |
|------|------|
| 用途 | financial_brain 金融新闻监控数据库 |
| URL | `libsql://macmini-m4-theoneguo.aws-ap-northeast-1.turso.io` |
| Token存储 | macOS Keychain |
| Keychain账户名 | `turso_financial_brain` |
| Keychain服务名 | `financial_brain` |
| 取出命令 | `security find-generic-password -a "turso_financial_brain" -s "financial_brain" -w` |
| 首次建立 | 2026-03-11 |
| 轮换记录 | — |

---

## 取回流程（重装后）

```bash
# 取 Turso Token
security find-generic-password -a "turso_financial_brain" -s "financial_brain" -w

# 重新存入（轮换后）
security add-generic-password -a "turso_financial_brain" -s "financial_brain" -w "新TOKEN" -U
```

## Keychain 备份（重装前必做）

```bash
# 导出所有 Keychain（需要密码）
security export -k ~/Library/Keychains/login.keychain-db -t all -f pkcs12 -o ~/keychain_backup.p12
```

---

_新增密钥时，在此文件追加一条记录。_
