# Changelog

All notable changes to this project are documented here. The format follows
[Keep a Changelog](https://keepachangelog.com/), and versions follow
[Semantic Versioning](https://semver.org/).

## [0.1.0] — 2026-07-04

Initial release.

### Added

- The **Design DNA** method: a seven-step workflow (Capture → Measure → Distill
  → Tokenize → Lab → Verify → Record) for reverse-engineering a design system
  from reference images and rebuilding it faithfully.
- **Claude Code plugin**: a `design-dna` skill, a `/design-dna` slash command,
  and a `design-engineer` subagent, installable via the plugin marketplace.
- **Reference recipes**: measuring colors and sizes from pixels, verifying
  fidelity in the browser, and an ADR template.
- **Cross-tool adapters**: a portable `AGENTS.md` (Codex, Gemini CLI, etc.) plus
  ready-to-copy rules for Cursor, Windsurf, and GitHub Copilot.
- **Worked example** (`examples/sleep-card/`): the artifacts the method produces
  on an original reference — `REFERENCE.md`, `tokens.css`, and an ADR.
- README with per-tool install and usage, and illustrated diagrams in `assets/`.
