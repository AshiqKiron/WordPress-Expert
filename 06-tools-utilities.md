---
title: LLM & Documentation Utilities
category: Tooling
license: MIT
last_updated: 2026-05-20
---

# WordPress LLM & Documentation Utilities

## WP Docs Markdown Exporter
### Overview
Community-maintained tool for scraping and converting WordPress.org documentation into clean, LLM-friendly Markdown files.

### Core Sections
- **Installation & Requirements**: Node.js 18+, `npm install`, puppeteer/chrome dependency
- **Usage & Command Flags**: `wp-docs-md --url https://developer.wordpress.org/plugins/ --output ./docs`
- **Output Structure & Organization**: Folder hierarchy, header normalization, link rewriting
- **Handling Images & Code Blocks**: Base64 embedding vs external links, syntax highlighting preservation
- **Rate Limiting & Caching**: Request delays, HTTP cache, resume capability, error retry logic
- **Known Issues & Workarounds**: Dynamic content skipping, table parsing fixes, encoding normalization

## WP Handbook Converter
### Overview
Utility for converting WordPress handbook HTML/Markdown into optimized, chunked files suitable for AI knowledge bases and RAG pipelines.

### Core Sections
- **Installation & Dependencies**: Python 3.10+, `pip install -r requirements.txt`, beautifulsoup4, markdownify
- **Input/Output Formats**: HTML → Markdown, Markdown → Chunked Markdown, JSON metadata export
- **Chunking & Header Preservation**: Semantic splitting, `##` header inheritance, context window optimization
- **Code Block Sanitization**: Language tag validation, nested backtick escaping, placeholder injection
- **Validation & Error Handling**: Schema checking, orphaned links detection, broken image warnings
- **Integration with GPT Knowledge Uploads**: Size compression, duplicate removal, frontmatter injection

> 📝 **Where to Update**: Update Node.js/Python version requirements as dependencies drop legacy support. Patch scraper logic when WordPress.org DOM structure changes. Add new chunking strategies for larger context windows. Maintain compatibility with OpenAI file upload limits.