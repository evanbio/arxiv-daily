# arXiv Daily

中文 | [English](./README.md)

基于 [zotero-arxiv-daily](https://github.com/TideDra/zotero-arxiv-daily) 的个人论文推荐系统，通过 GitHub Actions 每日推送。

## 配置

### Secrets

```
ZOTERO_ID              # Zotero 用户 ID
ZOTERO_KEY             # Zotero API 密钥
ARXIV_QUERY            # 论文分类，如 cs.AI+cs.CV+cs.LG
SMTP_SERVER            # SMTP 服务器
SMTP_PORT              # SMTP 端口（465）
SENDER                 # 发件邮箱
SENDER_PASSWORD        # 邮箱密码/授权码
```

### Variables

```
REPOSITORY             # TideDra/zotero-arxiv-daily（自动拉取上游代码）
REF                    # main（稳定）或 dev（开发版）
OPENAI_API_KEY         # OpenAI API 密钥
MODEL_NAME             # 模型名称（默认 gpt-4o）
LANGUAGE               # zh-CN
MAX_PAPER_NUM          # 每日推荐数量上限
```

## 说明

采用零 Fork 方案：本仓库仅保留工作流配置，运行时从上游自动拉取最新代码。无需手动同步更新。

## 链接

- 上游项目：https://github.com/TideDra/zotero-arxiv-daily
- Zotero API 设置：https://www.zotero.org/settings/keys
