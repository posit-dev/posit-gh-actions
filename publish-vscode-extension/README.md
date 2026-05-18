# Publish VS Code Extension

A composite GitHub Action to publish VS Code extensions to the [VS Marketplace](https://marketplace.visualstudio.com/) or the [Open VSX Registry](https://open-vsx.org/).

This is a drop-in replacement for [`HaaLeo/publish-vscode-extension@v2`](https://github.com/HaaLeo/publish-vscode-extension), implemented as a composite action with shell steps to avoid Node.js runtime version dependencies.

## Usage

### Publish to VS Marketplace

```yaml
- uses: posit-dev/posit-gh-actions/publish-vscode-extension@main
  with:
    pat: ${{ secrets.VSCE_PAT }}
    registryUrl: https://marketplace.visualstudio.com
```

### Publish to Open VSX

```yaml
- uses: posit-dev/posit-gh-actions/publish-vscode-extension@main
  with:
    pat: ${{ secrets.OVSX_PAT }}
```

### Publish a pre-built VSIX

```yaml
- uses: posit-dev/posit-gh-actions/publish-vscode-extension@main
  with:
    pat: ${{ secrets.VSCE_PAT }}
    registryUrl: https://marketplace.visualstudio.com
    extensionFile: path/to/extension.vsix
```

### Package only (dry run)

```yaml
- uses: posit-dev/posit-gh-actions/publish-vscode-extension@main
  id: package
  with:
    pat: unused
    dryRun: 'true'

- run: echo "Packaged to ${{ steps.package.outputs.vsixPath }}"
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `pat` | Personal access token | Yes | — |
| `extensionFile` | Path to a pre-built `.vsix` file. Cannot be used with `packagePath`. | No | — |
| `registryUrl` | Registry API base URL | No | `https://open-vsx.org` |
| `packagePath` | Path to the extension source. Cannot be used with `extensionFile`. | No | `./` |
| `baseContentUrl` | Base URL for relative links in README.md | No | — |
| `baseImagesUrl` | Base URL for relative image links in README.md | No | — |
| `yarn` | Use yarn instead of npm for packaging | No | `false` |
| `dryRun` | Package the extension but skip publishing | No | `false` |
| `noVerify` | Allow publishing extensions using proposed APIs | No | `false` |
| `preRelease` | Mark as a pre-release version | No | `false` |
| `dependencies` | Verify dependencies in node_modules. Set to `false` for pnpm or yarn PnP. | No | `true` |
| `skipDuplicate` | Fail silently if the version already exists | No | `false` |
| `target` | Target architecture(s), space-separated | No | — |

## Outputs

| Output | Description |
|--------|-------------|
| `vsixPath` | Path to the packaged `.vsix` file |

## Migrating from HaaLeo/publish-vscode-extension

Replace:

```yaml
- uses: HaaLeo/publish-vscode-extension@v2
  with:
    pat: ${{ secrets.SOME_PAT }}
    registryUrl: https://marketplace.visualstudio.com
```

With:

```yaml
- uses: posit-dev/posit-gh-actions/publish-vscode-extension@main
  with:
    pat: ${{ secrets.SOME_PAT }}
    registryUrl: https://marketplace.visualstudio.com
```

All inputs and outputs are compatible. No other changes are needed.
