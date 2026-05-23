---
title: Core Developer Handbooks
category: Core Documentation
license: CC0 (Text) / GPLv2+ (Code)
last_updated: 2026-05-20
---

# WordPress Core Developer Handbooks

## Plugin Developer Handbook
### Overview
Official documentation for building secure, standards-compliant WordPress plugins. Covers architecture, hooks, APIs, security, testing, and distribution.

### Core Sections
- **Plugin Basics & Headers**: Standard header fields, `ABSPATH` guard, activation/deactivation/uninstall hooks
- **Hooks: Actions & Filters**: `add_action()`, `apply_filters()`, priority/args, custom hooks
- **Plugin Security**: Nonces, capabilities, sanitization (`sanitize_text_field()`, `absint()`), escaping (`esc_html()`, `esc_attr()`, `esc_url()`, `wp_kses()`), `$wpdb->prepare()`
- **Database Interactions**: `$wpdb` global, prefix usage, prepared statements, custom tables
- **Shortcodes & Admin Menus**: `add_shortcode()`, `add_menu_page()`, capability mapping
- **AJAX & REST API Integration**: `wp_ajax_*` hooks, `admin-ajax.php`, `register_rest_route()`
- **Internationalization**: `load_plugin_textdomain()`, `__()`, `_e()`, `esc_html__()`, text domain best practices
- **Testing & Debugging**: PHPUnit setup, WP_DEBUG, error isolation, staging workflows
- **Distribution & Submission**: WordPress.org review guidelines, readme.txt compliance, versioning

## Theme Developer Handbook
### Overview
Comprehensive guide for classic and block theme development, template hierarchy, theme.json, FSE, and Theme Review guidelines.

### Core Sections
- **Theme Basics & style.css**: Required headers, screenshot.png, theme structure
- **Template Hierarchy**: `index.php`, `single-{post-type}.php`, `archive.php`, `404.php`, `front-page.php`
- **Block Themes & FSE**: `theme.json` v3 schema, `block-theme.json`, template parts, patterns, `index.html` fallback
- **theme.json Configuration**: Settings, styles, custom templates, color/typography/spacing presets
- **Classic Theme Development**: `functions.php`, enqueue system (`wp_enqueue_style/script`), customizer (legacy), template tags
- **Theme Security & Escaping**: Output escaping, nonce verification, capability checks, file permission handling
- **Internationalization & RTL**: Text domains, translation files, RTL stylesheet generation
- **Theme Review & Submission**: Required code standards, performance checks, accessibility requirements

## REST API Handbook
### Overview
Documentation for using, extending, and authenticating with the built-in WordPress REST API (`/wp-json/wp/v2/`).

### Core Sections
- **Architecture & Routing**: Namespace/versioning, route registration, callback/permission patterns
- **Default Endpoints**: Posts, Pages, Users, Terms, Media, Settings, Comments
- **Authentication Methods**: Cookie auth (nonce required), Application Passwords, OAuth2/JWT plugins
- **Extending the API**: `register_rest_route()`, custom controllers, response formatting, error handling
- **Request/Response Control**: `_fields` parameter, pagination, filtering, batch requests, embedding
- **Testing & Debugging**: Browser dev tools, `wp_remote_*`, Postman/cURL examples, rate limiting
- **Security Best Practices**: Permission callbacks, capability mapping, data validation, rate limiting

## Block Editor (Gutenberg) Handbook
### Overview
Developer guide for block creation, editor customization, Interactivity API, and modern JavaScript WordPress development.

### Core Sections
- **Block Architecture**: `registerBlockType()`, `block.json` schema, attributes, supports, example
- **useBlockProps & Context**: Block wrapper, context providers, inner blocks, alignment/layout
- **Server-Side Rendering**: `render_callback` in PHP, dynamic blocks, fallback content
- **Block Patterns & Variations**: Pattern registration, category grouping, template locking
- **Editor Customization**: Filters, settings overrides, custom panels, plugin extensions
- **Interactivity API**: Client-side state, directives, hydration, performance optimization
- **Testing & Performance**: Jest/Playwright setup, bundle splitting, tree shaking, lazy loading

## Common APIs Handbook
### Overview
Reference for core WordPress APIs used across plugins, themes, and administration.

### Core Sections
- **HTTP API**: `wp_remote_get/post()`, timeouts, headers, user-agent, error handling
- **Options & Transients**: CRUD operations, autoload behavior, expiration strategies, cache fallbacks
- **Filesystem API**: `WP_Filesystem`, direct/ftp/ssh methods, secure file operations
- **WP-Cron & Scheduling**: Event scheduling, `wp_schedule_single_event()`, system cron replacement
- **Rewrite Rules**: Permalink structure, custom endpoints, flush rules, query vars
- **User & Capability APIs**: `current_user_can()`, `user_can()`, custom roles, capability mapping
- **Heartbeat API**: AJAX polling, revision locking, custom heartbeat events

## WP-CLI Handbook
### Overview
Command-line interface documentation for managing WordPress installations, plugins, themes, database, and automation.

### Core Sections
- **Installation & Configuration**: Composer/global install, `wp-cli.yml`, environment variables
- **Core Commands**: `wp core download/install/update`, `wp config create`, `wp option`
- **Plugin/Theme Management**: Install, activate, update, check, scaffold
- **Database Operations**: Export/import, search-replace, query execution, backup strategies
- **User & Role Management**: Create, update, delete, role/capability assignment
- **Cron & Cache**: Event listing/run, transients, object cache flush
- **Custom Commands**: `WP_CLI::add_command()`, argument parsing, progress bars, error handling
- **CI/CD Integration**: Headless execution, `--allow-root`, automated testing hooks

## Advanced Administration Handbook
### Overview
Advanced topics for production WordPress environments: multisite, performance, security hardening, debugging, and deployment.

### Core Sections
- **Multisite Architecture**: Network setup, subdomain/subdirectory, site mapping, plugin/theme network activation
- **Performance Optimization**: Object caching, query optimization, CDN integration, asset optimization
- **Security Hardening**: Headers, file permissions, XML-RPC disable, login protection, `.htaccess` rules
- **Debugging & Logging**: `WP_DEBUG`, `SAVEQUERIES`, error logs, query monitoring, staging isolation
- **Backup & Migration**: Database dumps, file sync, search-replace, domain migration
- **Scaling & High Availability**: Load balancing, database replication, session handling, cache layers
- **Compliance & Privacy**: GDPR, CCPA, data export/erase, cookie consent, audit logging

## Coding Standards Handbook
### Overview
Official style and formatting guidelines for PHP, JavaScript, CSS, HTML, and documentation.

### Core Sections
- **PHP Standards**: Naming conventions, spacing, control structures, strict types, docblocks
- **JavaScript Standards**: ESLint config, `@wordpress/scripts`, modern syntax, async patterns
- **CSS/HTML Standards**: Indentation, vendor prefixes, semantic markup, accessibility attributes
- **Inline Documentation**: PHPDoc `@param`/`@return`/`@since`/`@see`, hook documentation format
- **Accessibility (a11y)**: Semantic HTML, ARIA usage, keyboard navigation, contrast ratios
- **Internationalization Standards**: String wrapping, placeholder usage, translator comments
- **Automated Linting**: PHPCS setup, `WordPress-Extra` ruleset, CI integration, auto-fix workflows

> 📝 **Where to Update**: Refresh version requirements, deprecated functions, and schema references after each WordPress major release. Replace legacy patterns with modern equivalents (FSE, Interactivity API, REST v2). Update PHPCS/ESLint configs when upstream packages release new versions.