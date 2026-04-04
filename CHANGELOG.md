# Changelog

All notable changes to Nex Life Logger.

## [1.1.0] - 2026-04-05

### Added
- FTS5 full-text search with Porter stemming (matches "containers" when searching "container", "deploying" when searching "deployment")
- Search filters: `--kind`, `--source`, `--category`, `--limit` for targeted queries
- `--output json` flag on search command for machine-readable structured output
- Relevance scoring combining FTS5 BM25 rank + recency weighting
- `config set-api-base` command for custom API endpoints
- `config set-poll-interval` command for adjustable collection frequency (5-3600 seconds)
- `config rebuild-fts` command to rebuild search indexes after bulk imports or database sync
- FTS5 auto-sync triggers: search indexes update automatically on every insert/update/delete
- Source index on activities table for faster source-filtered queries
- LIKE fallback when FTS5 tables aren't populated yet

### Changed
- Search command now uses FTS5 instead of SQL LIKE for significantly faster and smarter matching
- Search results now include relevance scores (60% text match quality + 40% recency)
- SKILL.md bumped to v1.1.0 with full documentation of new features

## [1.0.3] - 2026-04-04

### Changed
- License changed from MIT-0 to CC BY-NC 4.0 (free for personal use, commercial use requires paid license)
- Added LICENSE file with full terms and commercial licensing info

## [1.0.2] - 2026-04-04

### Fixed
- setup.sh: CLI wrapper now correctly references nex-life-logger.py
- Systemd service and LaunchAgent now install properly on first setup
- Removed compiled Python cache files from ClawHub package

## [1.0.1] - 2026-04-03

### Added
- ClawHub skill package for OpenClaw agent integration
- CLI tool (nex-life-logger) with commands: search, summary, activities, keywords, transcript, transcripts, stats, generate, export, service, config
- Headless collector for Linux/Pi deployment
- systemd user service support
- macOS LaunchAgent support
- Setup script with cross-platform installer

## [1.0.0] - 2026-03-28

### Added
- Initial release
- Desktop application with system tray icon (Windows, macOS, Linux)
- Browser history tracking (Chrome, Edge, Brave, Firefox)
- Active window focus tracking
- YouTube video transcript capture
- AI-powered hierarchical summaries (daily, weekly, monthly, yearly)
- Natural language AI search across all tracked data
- Desktop viewer with 3 themes (Cyberpunk, Executive Chronicle, Neon Pulse)
- AI chat window with database context and filter management
- Keyword and topic extraction
- Content filtering (productivity-only, chat/messaging excluded)
- Secure API key storage (Windows Credential Manager / DPAPI)
- Data export (JSON, CSV, HTML reports)
- Automatic database backups
- Windows auto-start on login
- Support for any OpenAI-compatible API provider
