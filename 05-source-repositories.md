---
title: Official Source Repositories
category: Source Code
license: GPLv2+ / MIT / CC0
last_updated: 2026-05-20
---

# WordPress Official Source Repositories

## WordPress Core Repository
### Overview
Official source code repository for WordPress Core. Contains PHP, JS, CSS, and build tooling for the CMS.

### Core Sections
- **Directory Structure Overview**: `wp-admin/`, `wp-includes/`, `wp-content/`, `node_modules/`, `tests/`
- **Build & Development Environment**: `npm install`, `grunt build`, `wp-env`, local MySQL setup
- **Contribution Guidelines**: Branching strategy, commit message format, PR template, code review checklist
- **Trunk vs Branches vs Tags**: `trunk` (dev), `branches/*` (release), `tags/*` (stable releases)
- **Automated Testing & CI**: PHPUnit, JavaScript tests, PHPStan, GitHub Actions workflows
- **Security & Vulnerability Reporting**: HackerOne process, embargo policy, credit guidelines
- **Release Tagging Workflow**: Version bump, changelog generation, zip packaging, checksum signing

## Gutenberg Block Editor Repository
### Overview
Source repository for the WordPress Block Editor. Drives modern editing experience, FSE, and block development APIs.

### Core Sections
- **Monorepo Structure**: `packages/` (shared libs), `plugins/` (Gutenberg plugin), `docs/`, `test/`
- **Block Development Workflow**: `@wordpress/create-block`, `block.json`, attribute schemas, validation
- **Interactivity & State Management**: `@wordpress/interactivity`, directives, hydration, server/client sync
- **Build & Release Process**: `npm run build`, Webpack config, asset extraction, plugin zip generation
- **Contribution & PR Guidelines**: Label system, reviewer assignment, CI checks, merge requirements
- **Testing & Benchmarking**: Jest, Playwright, Lighthouse, memory profiling, render cycle tracking
- **Backward Compatibility Policies**: Deprecation cycles, legacy support windows, migration guides

## WordPress Coding Standards Repository
### Overview
PHPCS rulesets enforcing WordPress PHP, JS, and CSS coding standards. Used for automated linting in CI/CD pipelines.

### Core Sections
- **Installation & Configuration**: Composer install, `phpcs.xml.dist`, `ruleset.xml` customization
- **Ruleset Breakdown**: `WordPress` (base), `WordPress-Core` (formatting), `WordPress-Docs` (PHPDoc), `WordPress-Extra` (strict)
- **Customizing & Extending Rules**: Exclude paths, modify severity, add custom sniffs, inherit rulesets
- **CI/CD Integration Examples**: GitHub Actions, GitLab CI, pre-commit hooks, PR status checks
- **Sniff Updates & Deprecations**: Version tracking, breaking changes, migration scripts
- **Migration from Legacy Standards**: PHP Compatibility, VIP Standards, WooCommerce Standards mapping

## Handbook Source Repositories
### Overview
Markdown source repositories powering developer.wordpress.org handbooks.

### Core Sections
- **Developer Plugins Handbook**: `https://github.com/WordPress/developer-plugins-handbook` → `/src/` structure, build pipeline
- **Developer Themes Handbook**: `https://github.com/WordPress/developer-themes-handbook` → FSE migration notes, theme.json examples
- **Gutenberg Docs**: `https://github.com/WordPress/gutenberg/tree/trunk/docs` → API references, tutorials, deprecation logs
- **WP-CLI Handbook**: `https://github.com/wp-cli/handbook` → Command docs, internal architecture, contribution guides

> 📝 **Where to Update**: Track `trunk` vs `tags` for stable releases. Update PHPCS ruleset references when `wpcs` releases new versions. Sync handbook source URLs if GitHub org structure changes. Note deprecation windows for Gutenberg packages.