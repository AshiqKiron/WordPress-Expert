# File: DISCLAIMER-NOTES.md
---
title: Disclaimer, Notes & Footnotes
category: Compliance
license: CC0 / GPLv2+
last_updated: 2026-05-20
---

# Disclaimer, Notes & Footnotes

## ⚠️ Disclaimer

- This knowledge base contains curated excerpts from official WordPress.org documentation. It is provided for developer guidance and educational purposes only.

- Generated code and scaffolding templates are GPLv2+ compatible and include baseline security patterns. They MUST be reviewed, tested in staging, and audited before production deployment.

- WordPress.org, the WordPress Foundation, and Automattic are not affiliated with, endorsing, or responsible for this GPT configuration or its outputs.

## 📌 Usage Notes

- GPT Knowledge performs optimally with focused, well-structured Markdown. Avoid PDFs, complex tables, or files exceeding 50MB.

- Scaffolding via Code Interpreter produces temporary `.zip` download links (~1 hour expiration). Download immediately after generation.

- API Actions require explicit user confirmation. Never auto-execute state-changing or write endpoints without consent.

- Always verify generated code against your specific hosting environment, PHP version, and active plugin/theme ecosystem.

- Keep `INSTRUCTIONS.md` under 3,000 characters to prevent token truncation and instruction fatigue.

## 🔍 Footnotes & Sources

### Official Handbooks
- Plugin Developer: https://developer.wordpress.org/plugins/
- Theme Developer: https://developer.wordpress.org/themes/
- REST API: https://developer.wordpress.org/rest-api/
- Block Editor: https://developer.wordpress.org/block-editor/

### Standards & Tools
- Coding Standards: https://developer.wordpress.org/coding-standards/
- WP-CLI Docs: https://make.wordpress.org/cli/handbook/
- Security Guidelines: https://developer.wordpress.org/plugins/security/
- Theme Review: https://make.wordpress.org/themes/handbook/

### Legal & Licensing
- License Text: https://wordpress.org/about/license/
- Schema Updates: https://schemas.wp.org/trunk/theme.json

## 🔄 Maintenance Protocol

### Monthly
- Check handbook footers for "Last updated" changes

### Quarterly
- Replace outdated files
- Run test suite
- Update version notes

### Post-Release
- Validate `theme.json` schema
- Check REST endpoints
- Verify PHP compatibility

### Backup & Version Control
- Store all files in version-controlled private repository
- Log all changes in git commit history for compliance tracking
- Tag releases with semantic versioning (e.g., v1.0.0, v1.1.0)

### Testing Checklist
- Test scaffolding with sample plugin/theme requests
- Validate API Actions with live endpoints
- Verify security patterns in generated code
- Check citation accuracy for handbook references
- Confirm error handling for edge cases