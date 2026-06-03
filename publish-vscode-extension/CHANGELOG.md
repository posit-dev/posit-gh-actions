# Changelog

All notable changes to the `publish-vscode-extension` action will be documented in this file.

This project follows [Semantic Versioning](https://semver.org/). Breaking changes bump the major version.

## [Unreleased]

### Added
- Initial release of the `publish-vscode-extension` composite action.
- Publish pre-built `.vsix` files to the VS Marketplace or Open VSX Registry.
- Support for `skipDuplicate` to silently handle duplicate versions.
- Support for `dryRun` mode to validate inputs without publishing.
- `resolvedTool` output indicating whether `vsce` or `ovsx` was selected.
- Secure PAT handling via native `VSCE_PAT`/`OVSX_PAT` environment variables (no CLI argument exposure).
- Trailing-slash normalization for `registryUrl` input.
- Cross-platform support (Linux, macOS, Windows).
