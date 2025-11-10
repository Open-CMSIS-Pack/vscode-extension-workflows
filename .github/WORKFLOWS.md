# Build and Verify Workflow Usage

This document explains how to use the `build-and-verify.yml` reusable workflow for cross-platform
TypeScript VS Code extension builds with comprehensive CI/CD features.

## Required Platform Matrix File

The workflow **requires** a platform matrix file to be provided. There is no default matrix, ensuring
that each caller explicitly defines their target platforms. This approach provides better control
and prevents unexpected platform builds.

### Platform Matrix File Format

Create a JSON file in your repository with the following format:

```json
[
  {
    "platform": "windows-2022",
    "arch": "amd64"
  },
  {
    "platform": "ubuntu-24.04",
    "arch": "amd64"
  },
  {
    "platform": "macos-14",
    "arch": "arm64"
  }
]
```

## Usage Examples

### Basic Usage

```yaml
jobs:
  build-and-test:
    uses: Open-CMSIS-Pack/vscode-extension-workflows/.github/workflows/build-and-verify.yml@main
    with:
      platform-matrix-file: '.github/platform-matrix.json'
```

### Advanced Usage

```yaml
name: Advanced CI/CD Pipeline

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]

jobs:
  build-and-test:
    permissions:
      contents: write  # Required for release version bumps
    uses: Open-CMSIS-Pack/vscode-extension-workflows/.github/workflows/build-and-verify.yml@main
    with:
      platform-matrix-file: 'config/platforms.json'
      package-manager: 'yarn'
      working-directory: './app'
      build-command: 'build:prod'
      test-command: 'test:ci'
      lint-command: 'lint:check'
      enable-qlty: true
    secrets:
      QLTY_COVERAGE_TOKEN: ${{ secrets.QLTY_COVERAGE_TOKEN }}
      PR_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

### Platform-Specific Configurations

#### Minimal (Single Platform)

```json
[
  {
    "platform": "ubuntu-24.04",
    "arch": "amd64"
  }
]
```

#### Cross-Platform (Current Default)

This is the current configuration used by this repository:

```json
[
  {
    "platform": "windows-2022",
    "arch": "amd64"
  },
  {
    "platform": "ubuntu-24.04",
    "arch": "amd64"
  },
  {
    "platform": "macos-14",
    "arch": "arm64"
  }
]
```

#### Comprehensive (All Platforms & Architectures)

```json
[
  {
    "platform": "ubuntu-22.04",
    "arch": "amd64"
  },
  {
    "platform": "ubuntu-24.04",
    "arch": "amd64"
  },
  {
    "platform": "ubuntu-24.04",
    "arch": "arm64"
  },
  {
    "platform": "windows-2022",
    "arch": "amd64"
  },
  {
    "platform": "windows-2022",
    "arch": "arm64"
  },
  {
    "platform": "macos-13",
    "arch": "amd64"
  },
  {
    "platform": "macos-14",
    "arch": "arm64"
  },
  {
    "platform": "macos-15",
    "arch": "arm64"
  }
]
```

## Required Inputs

| Input | Required | Description |
|-------|----------|-------------|
| `platform-matrix-file` | ✅ | Path to JSON file containing platform matrix |

## Optional Inputs

| Input | Default | Description |
|-------|---------|-------------|
| `node-version-file` | `./package.json` | Path to package.json file for Node.js version detection |
| `package-manager` | `npm` | Package manager to use (npm or yarn) with auto-detection |
| `working-directory` | `.` | Working directory for the build |
| `build-command` | `build` | npm/yarn script name for building |
| `test-command` | `test` | npm/yarn script name for testing |
| `lint-command` | `lint` | npm/yarn script name for linting |
| `enable-qlty` | `false` | Enable Qlty coverage upload (requires QLTY_COVERAGE_TOKEN) |

## Secrets

| Secret | Required | Description |
|--------|----------|-------------|
| `QLTY_COVERAGE_TOKEN` | Optional | Required only if `enable-qlty: true` |
| `PR_TOKEN` | Optional | Required only for release workflows to create version bump PRs |
