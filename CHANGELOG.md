# Changelog

All notable changes to Nex Life Logger.

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
