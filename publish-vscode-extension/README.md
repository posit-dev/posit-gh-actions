# Publish VS Code Extension

A composite GitHub Action to publish a pre-built VS Code extension (`.vsix`) to the [VS Marketplace](https://marketplace.visualstudio.com/) or the [Open VSX Registry](https://open-vsx.org/).

This replaces [`HaaLeo/publish-vscode-extension@v2`](https://github.com/HaaLeo/publish-vscode-extension), implemented as a composite action with shell steps to avoid Node.js runtime version dependencies.

## Usage

### Publish to VS Marketplace

```yaml
- uses: posit-dev/posit-gh-actions/publish-vscode-extension@main
  with:
    pat: ${{ secrets.VSCE_PAT }}
    extensionFile: path/to/extension.vsix
    registryUrl: https://marketplace.visualstudio.com
```

### Publish to Open VSX

```yaml
- uses: posit-dev/posit-gh-actions/publish-vscode-extension@main
  with:
    pat: ${{ secrets.OVSX_PAT }}
    extensionFile: path/to/extension.vsix
```

### Dry run (validate file exists, skip publishing)

```yaml
- uses: posit-dev/posit-gh-actions/publish-vscode-extension@main
  with:
    pat: unused
    extensionFile: path/to/extension.vsix
    dryRun: 'true'
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `pat` | Personal access token | Yes | — |
| `extensionFile` | Path to the `.vsix` file to publish | Yes | — |
| `registryUrl` | Registry URL. Use `https://marketplace.visualstudio.com` for VS Marketplace. | No | `https://open-vsx.org` |
| `skipDuplicate` | Fail silently if the version already exists | No | `false` |
| `dryRun` | Skip publishing (useful for CI testing) | No | `false` |

## Outputs

| Output | Description |
|--------|-------------|
| `vsixPath` | Path to the published `.vsix` file (same as `extensionFile` input) |

## Migrating from HaaLeo/publish-vscode-extension

This action requires a pre-built `.vsix` file. If you were using `packagePath` with the HaaLeo action, add a packaging step before calling this action:

```yaml
- name: Package extension
  run: |
    npm install -g @vscode/vsce
    cd path/to/extension
    vsce package --out extension.vsix

- uses: posit-dev/posit-gh-actions/publish-vscode-extension@main
  with:
    pat: ${{ secrets.VSCE_PAT }}
    extensionFile: path/to/extension/extension.vsix
    registryUrl: https://marketplace.visualstudio.com
```
