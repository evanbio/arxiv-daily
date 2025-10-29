# arXiv Daily

[中文](./README_ZH.md) | English

Personal arXiv paper recommendation system powered by [zotero-arxiv-daily](https://github.com/TideDra/zotero-arxiv-daily), running on GitHub Actions.

## Configuration

### Secrets

```
ZOTERO_ID              # Your Zotero user ID
ZOTERO_KEY             # Zotero API key
ARXIV_QUERY            # Paper categories, e.g., cs.AI+cs.CV+cs.LG
SMTP_SERVER            # SMTP server address
SMTP_PORT              # SMTP port (465)
SENDER                 # Sender email address
SENDER_PASSWORD        # Email password/app-specific password
```

### Variables

```
REPOSITORY             # TideDra/zotero-arxiv-daily (auto-pull upstream code)
REF                    # main (stable) or dev (development)
OPENAI_API_KEY         # OpenAI API key
MODEL_NAME             # Model name (default: gpt-4o)
LANGUAGE               # zh-CN
MAX_PAPER_NUM          # Daily recommendation limit
```

## Notes

Zero-fork approach: This repo only contains workflow config. Runtime code is automatically pulled from upstream. No manual sync needed.

## Links

- Upstream: https://github.com/TideDra/zotero-arxiv-daily
- Zotero API: https://www.zotero.org/settings/keys
