# Changelog

All notable changes to this project are documented here. The format follows
[Keep a Changelog](https://keepachangelog.com/), and versions follow
[Semantic Versioning](https://semver.org/).

## [0.3.0] — 2026-07-04

### Changed

- **Reverted the plugin id `dna` → `design-dna`**, so the commands read
  `/design-dna:extract`, `/design-dna:build`, and so on. The six-command split
  from 0.2.0 stays; only the prefix changed. Install is `design-dna@design-dna`
  again — matching the marketplace and repo name.

## [0.2.0] — 2026-07-04

### Changed

- **Split the single `/design-dna` command into a `/dna:*` family**, one per slice
  of the method: `/dna:extract` (full), `/dna:measure`, `/dna:tokens`,
  `/dna:build`, `/dna:verify`, `/dna:adr`. Each has its own description and
  examples. This makes the "measure once, build many" flow first-class —
  `/dna:build` reuses an existing `tokens.css` without re-measuring.
- **Renamed the plugin id `design-dna` → `dna`** so commands read `/dna:*`. The
  marketplace and repo stay `design-dna`; install is now `dna@design-dna`. The
  skill (`design-dna`), the `design-engineer` subagent, and the method are unchanged.

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
