# arXiv Daily

中文 | [English](./README.md)

基于 [zotero-arxiv-daily](https://github.com/TideDra/zotero-arxiv-daily) 的个人论文推荐系统，通过 GitHub Actions 每日推送。

## 工作原理

该系统根据您的 Zotero 文献库自动推荐相关的 arXiv 论文：

1. **数据采集**：获取您的 Zotero 文献库和指定分类下昨日发布的 arXiv 论文
2. **相关性评分**：计算 arXiv 论文与您文献库的嵌入向量相似度
3. **AI 摘要生成**：使用 LLM（本地或 API）生成论文 TL;DR 摘要
4. **邮件推送**：每天 22:00 UTC 将排序后的论文及摘要发送到您的邮箱

**工作流执行方式**：
- 通过 GitHub Actions 每日自动触发（cron: `0 22 * * *`）
- 支持在 GitHub Actions UI 手动触发（workflow_dispatch）
- 运行在免费的 GitHub 托管运行器上（ubuntu-latest）
- 使用 `uv` 实现快速的 Python 依赖管理

## 核心特性

- **零成本**：通过 GitHub Actions 免费部署
- **AI 驱动**：自动生成 TL;DR 摘要，快速审阅论文
- **智能排序**：根据研究兴趣对论文进行相关性排序
- **灵活的 LLM**：支持本地模型（免费但较慢）或 API 模型（更快但收费）
- **模式过滤**：类似 gitignore 的规则来排除不需要的论文
- **作者单位显示**：显示作者所属机构信息（如果有）

## 配置

### 必需的 Secrets

在 `Settings > Secrets and variables > Actions > Repository secrets` 中配置：

```
ZOTERO_ID              # 您的 Zotero 用户 ID（在 https://www.zotero.org/settings/keys 查找）
ZOTERO_KEY             # Zotero API 密钥（在 https://www.zotero.org/settings/keys 创建）
ARXIV_QUERY            # 论文分类，如 cs.AI+cs.CV+cs.LG
SMTP_SERVER            # SMTP 服务器地址（如 smtp.gmail.com）
SMTP_PORT              # SMTP 端口（SSL 通常为 465）
SENDER                 # 发件邮箱地址
SENDER_PASSWORD        # 邮箱密码或应用专用密码
RECEIVER               # 收件邮箱地址（可与 SENDER 相同）
```

### 可选的 Secrets（LLM API 模式）

```
USE_LLM_API            # 设置为 "true" 以使用 API 而不是本地模型
OPENAI_API_KEY         # OpenAI API 密钥（或兼容服务）
OPENAI_API_BASE        # 自定义 API 基础 URL（可选）
MODEL_NAME             # 模型名称（默认：gpt-4o）
MAX_PAPER_NUM          # 每日推荐数量上限（可选）
```

### 可选的 Variables

在 `Settings > Secrets and variables > Actions > Repository variables` 中配置：

```
REPOSITORY             # TideDra/zotero-arxiv-daily（自动拉取上游代码）
REF                    # main（稳定版）或 dev（开发版分支）
LANGUAGE               # 摘要语言：zh-CN（中文）或 en-US（英文）
ZOTERO_IGNORE          # 类 gitignore 模式来排除论文
SEND_EMPTY             # 设置为 "true" 以在没有找到论文时也接收邮件
```

## 设置步骤

1. **Fork 本仓库**（可选 - 参见下方的零 Fork 方案）
2. **配置 GitHub Secrets**：在仓库设置中添加所有必需的 secrets
3. **设置仓库 Variables**（可选）：通过变量自定义行为
4. **启用 GitHub Actions**：确保仓库设置中 Actions 已启用
5. **测试**：通过 `Actions > Send emails daily > Run workflow` 手动触发工作流
6. **验证**：检查邮箱中的论文推荐

## 重要说明

### 零 Fork 方案
本仓库仅包含工作流配置。运行时代码会在执行期间自动从上游 `TideDra/zotero-arxiv-daily` 拉取。无需手动同步！

### 性能考虑
- **本地 LLM 模式**：每篇论文摘要约 70 秒，模型下载约需 3GB 存储空间
- **API 模式**：速度更快，成本取决于使用量和模型选择
- **GitHub 限制**：公共仓库（6 小时/运行），私有仓库（20 小时/运行）

### 邮箱配置
对于 Gmail 用户，您需要：
- 启用两步验证
- 创建应用专用密码
- 使用 `smtp.gmail.com:465` 作为 SMTP 服务器

## 故障排除

- **未收到邮件**：检查垃圾邮件文件夹，验证 SMTP 凭据
- **工作流失败**：查看 GitHub Actions 日志中的错误信息
- **无论文推荐**：检查 `ARXIV_QUERY` 分类和 Zotero 文献库内容

## 链接

- **上游项目**：https://github.com/TideDra/zotero-arxiv-daily
- **Zotero API 密钥**：https://www.zotero.org/settings/keys
- **arXiv 分类目录**：https://arxiv.org/category_taxonomy
- **GitHub Actions 文档**：https://docs.github.com/zh/actions
