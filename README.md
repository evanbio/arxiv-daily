# arXiv Daily

[中文](./README_ZH.md) | English

Personal arXiv paper recommendation system powered by [zotero-arxiv-daily](https://github.com/TideDra/zotero-arxiv-daily), running on GitHub Actions.

## How It Works

This system automatically recommends relevant arXiv papers based on your Zotero library:

1. **Data Collection**: Retrieves your Zotero library and yesterday's arXiv papers in specified categories
2. **Relevance Scoring**: Calculates embedding-based similarity between arXiv papers and your collection
3. **AI Summarization**: Generates TL;DR summaries using LLM (local or API-based)
4. **Email Delivery**: Sends ranked papers with summaries to your email daily at 22:00 UTC

**Workflow Execution**:
- Automatically triggered daily via GitHub Actions (cron: `0 22 * * *`)
- Manually triggerable via GitHub Actions UI (workflow_dispatch)
- Runs on free GitHub-hosted runners (ubuntu-latest)
- Uses `uv` for fast Python dependency management

## Key Features

- **Zero Cost**: Free deployment through GitHub Actions
- **AI-Powered**: Automatic TL;DR generation for quick review
- **Smart Ranking**: Papers ranked by relevance to your research interests
- **Flexible LLM**: Supports local models (free, slower) or API-based models (faster, paid)
- **Pattern Filtering**: Gitignore-style rules to exclude unwanted papers
- **Affiliation Display**: Shows author affiliations when available

## Configuration

### Required Secrets

Configure in `Settings > Secrets and variables > Actions > Repository secrets`:

```
ZOTERO_ID              # Your Zotero user ID (find at https://www.zotero.org/settings/keys)
ZOTERO_KEY             # Zotero API key (create at https://www.zotero.org/settings/keys)
ARXIV_QUERY            # Paper categories, e.g., cs.AI+cs.CV+cs.LG
SMTP_SERVER            # SMTP server address (e.g., smtp.gmail.com)
SMTP_PORT              # SMTP port (typically 465 for SSL)
SENDER                 # Sender email address
SENDER_PASSWORD        # Email password or app-specific password
RECEIVER               # Receiver email address (can be same as SENDER)
```

### Optional Secrets (LLM API Mode)

```
USE_LLM_API            # Set to "true" to use API instead of local model
OPENAI_API_KEY         # OpenAI API key (or compatible service)
OPENAI_API_BASE        # Custom API base URL (optional)
MODEL_NAME             # Model name (default: gpt-4o)
MAX_PAPER_NUM          # Daily recommendation limit (optional)
```

### Optional Variables

Configure in `Settings > Secrets and variables > Actions > Repository variables`:

```
REPOSITORY             # TideDra/zotero-arxiv-daily (auto-pull upstream code)
REF                    # main (stable) or dev (development branch)
LANGUAGE               # Summary language: zh-CN (Chinese) or en-US (English)
ZOTERO_IGNORE          # Gitignore-style patterns to exclude papers
SEND_EMPTY             # Set to "true" to receive emails even when no papers found
```

## Setup Instructions

1. **Fork this repository** (optional - see Zero-fork approach below)
2. **Configure GitHub Secrets**: Add all required secrets in repository settings
3. **Set Repository Variables** (optional): Customize behavior with variables
4. **Enable GitHub Actions**: Ensure Actions are enabled in repository settings
5. **Test**: Manually trigger workflow via `Actions > Send emails daily > Run workflow`
6. **Verify**: Check email for paper recommendations

## Important Notes

### Zero-Fork Approach
This repo contains only workflow configuration. Runtime code is automatically pulled from upstream `TideDra/zotero-arxiv-daily` during execution. No manual sync needed!

### Performance Considerations
- **Local LLM Mode**: ~70 seconds per paper summary, ~3GB storage for model download
- **API Mode**: Much faster, costs depend on usage and model selection
- **GitHub Limits**: Public repos (6 hours/run), Private repos (20 hours/run)

### Email Configuration
For Gmail users, you need to:
- Enable 2-factor authentication
- Create an app-specific password
- Use `smtp.gmail.com:465` as SMTP server

## Troubleshooting

- **No emails received**: Check spam folder, verify SMTP credentials
- **Workflow fails**: Review GitHub Actions logs for error messages
- **No papers recommended**: Check `ARXIV_QUERY` categories and Zotero library content

## Links

- **Upstream Project**: https://github.com/TideDra/zotero-arxiv-daily
- **Zotero API Keys**: https://www.zotero.org/settings/keys
- **arXiv Categories**: https://arxiv.org/category_taxonomy
- **GitHub Actions Docs**: https://docs.github.com/en/actions
