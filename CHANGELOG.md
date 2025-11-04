# Changelog

All notable changes to Claude Code Waypoint will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [2.0.0] - 2025-11-04

### BREAKING CHANGES

**Repository Migration: Marketplace → Single-Purpose Tool**

This release represents a complete restructuring from a marketplace approach to a focused, single-purpose tool.

### Changed
- **Repository name**: `dojo-claude-code-plugin-marketplace` → `claude-code-waypoint`
- **Repository URL**: https://github.com/DojoCodingLabs/claude-code-waypoint
- **Structure**: Flattened `plugins/waypoint/*` → root directory
- **Installation**: Changed from plugin marketplace to simple copy/paste
- **Branding**: "Dojo Claude Plugins marketplace" → "Claude Code Waypoint"
- **README**: Completely rewritten with single-purpose focus
- **All documentation**: Updated with new repository name and structure

### Removed
- `.claude-plugin/marketplace.json` - No longer a marketplace
- `plugins/` directory structure - Flattened to root
- `examples/` and `scripts/` directories - Unused
- Plugin marketplace installation method - Simplified to copy/paste

### Migration Guide: v1.x → v2.0

**Old Installation (v1.x):**
```bash
/plugin marketplace add DojoCodingLabs/dojo-claude-code-plugin-marketplace
/plugin install waypoint@dojo-claude-code-plugin-marketplace
```

**New Installation (v2.0):**
```bash
git clone https://github.com/DojoCodingLabs/claude-code-waypoint
cp -r claude-code-waypoint/.claude /your/project/
cp -r claude-code-waypoint/plans /your/project/
cd /your/project/.claude/hooks && npm install && chmod +x *.sh
```

**Why This Change?**
- Simplicity: Users copy `.claude/` to projects (not using marketplace features)
- Clarity: Single purpose easier to understand
- Honesty: Matches actual usage pattern
- Focus: Memory/waypoint is core value

### Rationale

The marketplace structure added unnecessary complexity. Users were copying files directly to projects, not leveraging marketplace features. This release embraces simplicity and focuses on the core value: persistent memory and context management.

---

## [1.0.0] - 2025-01-16

### Added
- **Claude Code Waypoint Plugin**: Production-ready waypoint system for context persistence
- Three memory management skills (memory-management, context-persistence, plan-approval)
- Waypoint plans structure: `plans/active/[task]/` with plan.md, context.md, tasks.md
- SESSION PROGRESS format for instant context recovery after resets
- Opinionated scaffolds for modern web development (Supabase + Next.js + React 19)
- scaffold-customizer agent for tech stack adaptation
- Three commands: `/create-plan`, `/update-context`, `/resume`
- Auto-activation system via skill-activation-prompt hook
- Comprehensive documentation: PHILOSOPHY, INSTALLATION, WAYPOINT_INTEGRATION_GUIDE
- skill-developer meta-skill with memory patterns
- Plugin installation method: `/plugin install waypoint`

### Changed
- **Renamed**: dev/ → plans/ (waypoint storage location)
- **Renamed**: "dev docs" → "waypoint plans" throughout
- **Repositioned**: Memory/context management as PRIMARY feature (not secondary)
- **Repositioned**: Auto-activation as CRITICAL enabler for memory management
- **Updated**: All documentation to reflect "Claude Code Waypoint Plugin" full name
- **Rebranded**: Integrated "waypoint" metaphor throughout (navigation/persistence)
- **Updated**: frontend-dev-guidelines for Next.js 14+ and React 19
- **Updated**: backend-dev-guidelines for Supabase Edge Functions
- **Enhanced**: skill-developer with waypoint pattern examples

### Removed
- route-tester skill (project-specific)
- error-tracking skill (project-specific)
- Multiple project-specific agents (auth-route-tester, auth-route-debugger, etc.)
- Project-specific hooks (tsc-check, trigger-build-resolver, etc.)
- References to Reddit post in documentation (appears only in README)

### Migration Guide: dev/ → plans/

If you have existing waypoint plans structure:

```bash
# Rename dev directory to plans
mv dev plans

# Update any references in commands
# /create-plan now uses plans/active/[task]/
# /update-context now updates plans/active/[task]/context.md
# /resume now resumes from plans/active/[task]/
```

All waypoint functionality remains the same, only directory naming changed.

## [0.1.0] - 2025-01-15

### Added
- Initial repository structure
- Basic skills (backend-dev-guidelines, frontend-dev-guidelines, skill-developer)
- Agent system with 10 specialized agents
- Hook system for skill auto-activation
- Waypoint plans pattern for context persistence
- skill-rules.json for trigger configuration

### Documentation
- CLAUDE_INTEGRATION_GUIDE.md for AI-assisted setup
- Individual skill documentation
- Agent documentation
- Hook setup guides

---

## Version History

### Versioning Strategy

We follow [Semantic Versioning](https://semver.org/):
- **MAJOR** version for incompatible API/structure changes
- **MINOR** version for new features (backward-compatible)
- **PATCH** version for bug fixes (backward-compatible)

### Release Schedule

- **Major releases**: When there are breaking changes
- **Minor releases**: Monthly, or when significant features are added
- **Patch releases**: As needed for bug fixes

---

## Upcoming Features

### v0.2.0 (Planned)
- [ ] Memory dashboard command (/memory-dashboard)
- [ ] Memory export/import functionality
- [ ] Plan template library
- [ ] Skill marketplace integration
- [ ] Memory analytics and insights

### v0.3.0 (Planned)
- [ ] Additional skill scaffolds (Python, Go, Rust)
- [ ] Team collaboration features
- [ ] Shared memory across projects
- [ ] Memory conflict resolution
- [ ] Advanced plan approval workflows

### v1.0.0 (Planned)
- [ ] Stable API for extensions
- [ ] Visual Studio Code extension
- [ ] Web-based configuration UI
- [ ] Enterprise features (SSO, audit logs)
- [ ] Comprehensive test suite

---

## Migration Guides

### From v0.1.0 to v0.2.0

When v0.2.0 is released, the migration guide will be here.

---

## Contributors

Thank you to all contributors who have helped improve this project!

- Initial concept and implementation: [Your Name]
- Community feedback and testing: [List contributors]
- Documentation improvements: [List contributors]

See [CONTRIBUTING.md](CONTRIBUTING.md) for how to contribute.

---

## Support

For questions, issues, or feature requests:
- **Issues**: [GitHub Issues](https://github.com/DojoCodingLabs/claude-code-waypoint/issues)
- **Discussions**: [GitHub Discussions](https://github.com/DojoCodingLabs/claude-code-waypoint/discussions)
