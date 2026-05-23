---
title: Reference & Developer Tools
category: Reference
license: CC0 / GPLv2+
last_updated: 2026-05-20
---

# WordPress Reference & Developer Tools

## Code Reference
### Overview
Auto-generated reference for WordPress core functions, classes, methods, and hooks. Serves as the authoritative API catalog.

### Core Sections
- **Function Reference**: Categorized by feature (admin, database, HTTP, options, users, plugins, themes)
- **Class Reference**: Core WP classes (`WP_Query`, `WP_User`, `WP_Roles`, `WP_Hook`, `WP_Error`)
- **Hook Reference**: Actions vs filters, priority/args, dynamic hooks, deprecation notices
- **Method Reference**: Object-oriented patterns, static vs instance, inheritance chains
- **Changelog & Version History**: `@since` tracking, deprecated/removed functions, migration paths
- **Usage Examples & Parameter Tables**: Type hints, default values, return types, edge cases

## WordPress Playground
### Overview
Browser-based WordPress environment for testing code, plugins, themes, and APIs without local setup.

### Core Sections
- **Getting Started & URL Parameters**: `https://playground.wordpress.net/?plugin=slug&theme=slug&wp=6.5`
- **Plugin & Theme Testing**: Upload zip, activate, test conflicts, switch PHP versions
- **Database & Filesystem Sandbox**: In-memory SQLite, temporary uploads, reset on refresh
- **API & Block Editor Testing**: REST endpoint testing, block preview, template editing
- **Export/Import Workflows**: Download site state, import WXR/JSON, migrate to local
- **Limitations & Security Model**: No external network calls, ephemeral storage, PHP/WebAssembly sandbox

## WordPress.tv
### Overview
Archive of official WordPress conference talks, WordCamps, and contributor day presentations.

### Core Sections
- **Developer Talks & Technical Deep Dives**: Core architecture, performance, security, REST API
- **Block Editor & FSE Sessions**: Block development, theme.json, patterns, interactivity
- **Security & Performance Workshops**: Hardening, caching, database optimization, CDN setup
- **Community & Governance Panels**: Contributor workflows, release planning, team coordination
- **Search & Filter Guidelines**: Topic tagging, speaker indexing, playlist curation
- **Embed & Transcript Policies**: CC licensing, subtitle availability, download restrictions

> 📝 **Where to Update**: Add new core functions/classes when WP releases introduce them. Update Playground URL schemes if parameters change. Index new WordPress.tv talks quarterly. Replace deprecated reference links with current handbook equivalents.