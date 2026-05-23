# File: 07-scaffolding-security.md
---
title: Scaffolding, Security & API Reference
category: Implementation
license: CC0 / GPLv2+
last_updated: 2026-05-20
---

# Scaffolding, Security & API Reference

## Plugin Security & Scaffolding

### Standard Plugin Header
```php
<?php
/**
 * Plugin Name: Plugin Name
 * Plugin URI: https://example.com/plugin-name
 * Description: Short description.
 * Version: 1.0.0
 * Author: Author Name
 * Author URI: https://example.com
 * License: GPLv2 or later
 * License URI: https://www.gnu.org/licenses/gpl-2.0.html
 * Text Domain: plugin-slug
 * Domain Path: /languages
 * Requires at least: 6.0
 * Tested up to: 6.5
 * Requires PHP: 7.4
 */
if ( ! defined( 'ABSPATH' ) ) {
    exit;
}
```

### Security Enforcement Patterns

**Nonce Verification:**
```php
wp_nonce_field( 'plugin_action', 'plugin_nonce' );
if ( ! isset( $_POST['plugin_nonce'] ) || ! wp_verify_nonce( $_POST['plugin_nonce'], 'plugin_action' ) ) {
    wp_die( 'Security check failed.' );
}
```

**Capability Checks:**
```php
if ( ! current_user_can( 'manage_options' ) ) {
    wp_die( 'Insufficient permissions.' );
}
```

**Sanitization & Escaping:**
- Input: `sanitize_text_field()`, `absint()`, `wp_kses_post()`, `sanitize_email()`
- Output: `esc_html()`, `esc_attr()`, `esc_url()`, `wp_kses()`
- Database: `$wpdb->prepare()` for all dynamic queries

**Activation/Deactivation/Uninstall:**
```php
register_activation_hook( __FILE__, 'plugin_slug_activate' );
register_deactivation_hook( __FILE__, 'plugin_slug_deactivate' );

function plugin_slug_activate() {
    // Create tables, set defaults, flush rewrite rules
}

function plugin_slug_deactivate() {
    // Optional cleanup, DO NOT delete user data
}

// uninstall.php
if ( ! defined( 'WP_UNINSTALL_PLUGIN' ) ) {
    exit;
}
delete_option( 'plugin_slug_settings' );
```

**Internationalization:**
```php
load_plugin_textdomain( 'plugin-slug', false, dirname( plugin_basename( __FILE__ ) ) . '/languages/' );
__( 'String', 'plugin-slug' );
_e( 'Output', 'plugin-slug' );
esc_html__( 'Safe', 'plugin-slug' );
```

## Theme Block Architecture

### theme.json v3 Core Structure
```json
{
  "$schema": "https://schemas.wp.org/trunk/theme.json",
  "version": 3,
  "settings": {
    "appearanceTools": true,
    "layout": {
      "contentSize": "800px",
      "wideSize": "1200px"
    },
    "color": {
      "palette": [
        {
          "slug": "primary",
          "color": "#0055ff"
        }
      ]
    }
  },
  "styles": {
    "elements": {
      "link": {
        "color": {
          "text": "var:preset|color|primary"
        }
      }
    },
    "spacing": {
      "padding": {
        "top": "2rem"
      }
    }
  }
}
```

### FSE Template Hierarchy
- `index.html` - Fallback for all requests
- `home.html`, `front-page.html`
- `single-{post-type}.html`
- `archive-{taxonomy}.html`
- `404.html`, `search.html`
- Parts: `header.html`, `footer.html`, `sidebar.html`
- Patterns: Stored in `/patterns/` or registered via `register_block_pattern()`

### Block Registration (Modern)
```json
{
  "name": "namespace/block-name",
  "title": "Block Title",
  "category": "design",
  "attributes": {
    "content": {
      "type": "string",
      "source": "html",
      "selector": "p"
    }
  },
  "editorScript": "file:./build/index.js",
  "style": "file:./build/style-index.css",
  "viewScript": "file:./build/view.js"
}
```

## REST API & Core APIs

### REST Endpoint Patterns
- Base URL: `/wp-json/wp/v2/`
- Custom Route: `register_rest_route( 'namespace/v1', '/endpoint', array( 'methods' => 'GET', 'callback' => 'handler', 'permission_callback' => 'check' ) )`
- Response: `rest_ensure_response( $data )`
- Fields Control: `?_fields=id,title,content,custom_field`

### Authentication Methods
- **Cookie**: Logged-in users (nonce required for state-changing requests)
- **Application Passwords**: `/wp-admin/profile.php` → Generate → Use Basic Auth or Bearer token
- **OAuth2/JWT**: Via plugins (not in Core)

### Core APIs

**Options & Transients:**
```php
add_option( 'key', 'value' );
get_option( 'key' );
update_option( 'key', 'new_value' );
delete_option( 'key' );

set_transient( 'key', $value, HOUR_IN_SECONDS );
get_transient( 'key' );
delete_transient( 'key' );
```

**HTTP API:**
```php
$response = wp_remote_get( 'https://api.example.com', array(
    'timeout' => 15,
    'user-agent' => 'YourPlugin/1.0'
) );
$body = wp_remote_retrieve_body( $response );
$code = wp_remote_retrieve_response_code( $response );
```

**Database ($wpdb):**
```php
global $wpdb;
$table = $wpdb->prefix . 'my_table';
$results = $wpdb->get_results( $wpdb->prepare(
    "SELECT * FROM {$table} WHERE id = %d",
    $id
) );
```

**WP-Cron:**
```php
wp_schedule_event( time(), 'hourly', 'my_cron_hook' );
add_action( 'my_cron_hook', 'my_function' );

// Production: Disable WP-Cron and use system cron
// define( 'DISABLE_WP_CRON', true );
// Server cron: wp cron event run --due-now
```

## Debugging & Performance

### Safe Debug Configuration (wp-config.php)
```php
define( 'WP_DEBUG', true );
define( 'WP_DEBUG_LOG', true );
define( 'WP_DEBUG_DISPLAY', false );
define( 'SAVEQUERIES', true );
@ini_set( 'log_errors', 1 );
@ini_set( 'error_log', WP_CONTENT_DIR . '/debug.log' );
```

### Common Error Resolution
- **Headers already sent**: Whitespace before `<?php`, BOM encoding, premature `echo`
- **Fatal error: Uncaught Error**: Missing class/function, PHP version mismatch, incompatible plugin
- **WSOD (White Screen of Death)**: Syntax error, memory limit (`define( 'WP_MEMORY_LIMIT', '256M' );`), plugin conflict
- **Nonce verification failed**: Cache serving stale pages, URL parameter stripped, session timeout

### Performance Patterns
- Minimize DB queries: Use `get_posts()` with `'fields' => 'ids'` for counts
- Cache expensive results: `wp_cache_get()`, `wp_cache_set()`, object cache plugins
- Lazy-load assets: `defer`/`async` scripts, CSS critical path extraction
- Avoid `query_posts()`: Use `WP_Query` with proper pagination
- Use `wp_suspend_cache_addition( true )` during bulk operations

### Diagnostic Tools
- **Query Monitor**: Hook timing, DB queries, PHP errors, HTTP calls
- **WP-CLI**: `wp doctor check`, `wp cache flush`, `wp transient delete --all`
- **Server**: `top`, `htop`, `php-fpm` logs, Nginx/Apache access logs

## WP-CLI Automation

### Core Management
```bash
wp core download --locale=en_US
wp config create --dbname=wp_db --dbuser=root --dbpass=pass
wp core install --url=https://example.com --title=Site --admin_user=admin --admin_pass=pass --admin_email=admin@example.com
wp option update siteurl https://example.com
```

### Plugin/Theme Operations
```bash
wp plugin install plugin-slug --activate
wp plugin update --all
wp plugin deactivate plugin-slug
wp theme install theme-slug --activate
wp plugin check plugin-slug
```

### Database & Migration
```bash
wp db export backup.sql
wp db import backup.sql
wp search-replace 'old-domain.com' 'new-domain.com' --skip-columns=guid
wp cache flush
wp transient delete --all
```

### CI/CD Integration
```bash
#!/bin/bash
wp --allow-root db reset --yes
wp --allow-root core install --skip-email
wp --allow-root plugin install woocommerce --activate
wp --allow-root import data.xml
```

## Coding Standards Compliance

### PHPCS Setup
```json
{
  "require-dev": {
    "dealerdirect/phpcodesniffer-composer-installer": "*",
    "wp-coding-standards/wpcs": "*"
  },
  "scripts": {
    "phpcs": "phpcs --standard=WordPress",
    "phpcbf": "phpcbf --standard=WordPress"
  }
}
```

Run: `composer run phpcs -- ./path`

Standards: `WordPress`, `WordPress-Core`, `WordPress-Docs`, `WordPress-Extra`

### Key Rules
- **PHP**: `snake_case` functions, `PascalCase` classes, no short tags, strict typing preferred
- **JavaScript**: ESLint `@wordpress/scripts`, `const`/`let` over `var`, async/await over promises
- **CSS**: BEM-like naming, no `!important` unless necessary, logical properties preferred
- **Documentation**: PHPDoc `@param`, `@return`, `@since`, `@see` for hooks/functions
- **i18n**: Wrap all UI strings in `__()`, `_e()`, `esc_html__()`, never concatenate variables inside translation functions

### Plugin Check CLI
```bash
wp plugin check plugin-slug --fields=error,warning
```

Validates: Security, Performance, Code Standards, Readme.txt compliance, Theme Review guidelines

### Accessibility (a11y)
- Semantic HTML (`<nav>`, `<main>`, `<article>`)
- ARIA attributes only when native semantics fail
- Focus states visible, keyboard navigation complete
- Color contrast ≥ 4.5:1 (WCAG AA)

## Update Notes
- Refresh `Tested up to` and PHP versions after major WP/PHP releases
- Track `theme.json` schema updates at https://schemas.wp.org
- Update FSE template names if Core deprecates or renames them
- Add new REST endpoints or Core API functions when WP major releases introduce them
- Update cron/system notes for modern hosting environments
- Update memory limits and PHP version notes after WP releases
- Add new debugging constants if Core introduces them
- Update flags if WP-CLI releases breaking changes
- Add new `wp doctor` or `wp scaffold` commands as available
- Update PHPCS rulesets when `wpcs` releases new versions
- Track Core coding standards changes at developer.wordpress.org/coding-standards