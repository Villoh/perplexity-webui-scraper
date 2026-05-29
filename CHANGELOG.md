# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0).

## [Unreleased]

### Added

- **TOTP 2FA support in session token generation:** The `perplexity-webui-scraper token` wizard now handles Perplexity accounts with TOTP-based two-factor authentication enabled. After email OTP verification, the CLI detects the TOTP challenge redirect, prompts for the authenticator app code, and completes the login flow automatically.
- **Unified CLI test coverage:** Added `tests/test_cli.py` to verify root help output and lazy delegation for `token`, `api`, and `mcp` subcommands.
- **Native executable release pipeline:** Added GitHub Actions matrix builds that package standalone, optimized executables for Linux AMD64, Linux ARM64, macOS ARM64, and Windows AMD64 using Nuitka.
- **Optional MCP container image:** Added `Containerfile.mcp` plus GHCR publishing for explicit MCP tags (`mcp`, `X.Y.Z-mcp`, `vX.Y.Z-mcp`) alongside the default API image.
- **Manual publish workflow controls:** Added `workflow_dispatch` inputs for version override plus selective publish toggles for PyPI, GHCR (Podman), and GitHub Releases.
- **Executable branding assets:** Added packaged application icons for Windows (`.ico`) and macOS (`.icns`) release builds.
- **TOTP 2FA support in session token generation:** The `perplexity-webui-scraper token` CLI wizard now handles Perplexity accounts with TOTP-based two-factor authentication. After email OTP verification, the CLI detects the TOTP challenge redirect, prompts for the authenticator app code, and completes the login flow automatically.
- **`chat` CLI command:** New interactive REPL command `perplexity-webui-scraper chat "query"` for querying Perplexity AI directly from the terminal with real-time streaming token output via Rich Live panels. It maintains the conversation context until exited and features a clean, borderless UX inspired by Claude Code. Supports all `ConversationConfig` options as CLI arguments with short aliases, file attachments, clipboard copy, and raw output mode.
- **`chat setup` subcommand:** Interactive setup wizard that configures and saves the session token (Fernet-encrypted in the platform-specific config directory) and the default model. First-time users are guided to configure their token before using `chat`.
- **`all` optional dependency extra:** New `[all]` meta-extra that installs all optional dependencies (`cli`, `api`, `mcp`) in one go: `uv add "perplexity-webui-scraper[all]"`.
- **Encrypted token storage:** Session tokens are now encrypted with Fernet and stored in the platform-specific config directory (`platformdirs`). The `ask` command reads from this store automatically.

### Changed

- **CI Workflows:** Updated `ci.yml` to use `pnpm/action-setup`, restrict `uv sync` to the `test` and `lint` groups with `--frozen`, and execute `just format` and `just lint` directly.
- **CLI surface simplified:** Replaced the legacy `get-perplexity-session-token`, `perplexity-webui-scraper-api`, and `perplexity-webui-scraper-mcp` scripts with one canonical `perplexity-webui-scraper` command exposing `token`, `api`, and `mcp` subcommands.
- **Dependency layout:** Moved `typer` into base dependencies so the unified root CLI is always available.
- **MCP startup guidance:** Updated missing-token runtime messaging to reference `PERPLEXITY_SESSION_TOKEN=<token> perplexity-webui-scraper mcp`.
- **Container entrypoint:** Updated the default API container to launch `perplexity-webui-scraper api` instead of the removed legacy command.
- **Release workflow architecture:** Refactored publish automation into separate package, executable, Container, PyPI, and GitHub Release jobs with artifact passing between them.
- **Executable builder choice:** Standardized executable packaging on Nuitka for optimized, high-performance C-compiled binaries and faster CI builds.
- **Container publishing:** The default GHCR image remains API-first (`latest`, `X.Y.Z`, `vX.Y.Z`, semver tags), while MCP publishing is now opt-in via `-mcp` tags.
- **Documentation:** Updated README and docs to consistently use the unified CLI commands, published API container image, and optional MCP container image.

### Removed

- **Legacy console scripts:** Dropped generation and documentation of the three previous standalone command entry points.

## [1.0.2] - 2026-05-01

### Fixed

- **Model Registry:** Corrected Anthropic models by replacing Claude Opus 4.6 with the newly released Claude Sonnet 4.6 (and its Thinking variant). Adjusted the tier requirement from `max` to `pro`.

---
