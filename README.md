[![OpenSSF Scorecard](https://api.securityscorecards.dev/projects/github.com/Open-CMSIS-Pack/vscode-extension-workflows/badge)](https://securityscorecards.dev/viewer/?uri=github.com/Open-CMSIS-Pack/vscode-extension-workflows)

# vscode-extension-workflows - Reusable CI/CD Workflows

This repository provides **reusable GitHub Actions workflows** for building, testing, and packaging TypeScript
VS Code extensions across multiple platforms. The repository itself serves as a self-testing infrastructure
to validate the workflows.

## Purpose

- Reusable GitHub Actions workflows for TypeScript VS Code extensions
- Self-test infrastructure to validate workflow functionality

## Using the Reusable Workflow

### Quick Start

For detailed usage instructions, see [WORKFLOWS.md](.github/WORKFLOWS.md).

## Self-Test Infrastructure Development

If you're contributing to or testing the workflows themselves, use these commands:

```bash
# Install dependencies
npm install

# Build the project
npm run build

# Run tests with coverage
npm test

# Lint code
npm run lint

# Clean build artifacts
npm run clean

# Package as VSIX
npm run package

# Update TPIP license tracking
npm run tpip:update

# Generate TPIP license report
npm run tpip
```

## 📁 Repository Structure

### Reusable Workflows

```txt
.github/
├── workflows/
│   ├── build-and-verify.yml      # Main reusable workflow
│   └── self-test.yml             # Self-testing workflow
├── platform-matrix.json          # Example platform configuration
└── WORKFLOWS.md                  # Comprehensive workflow documentation
```

### Self-Test Infrastructure

```txt
.
├── src/
│   └── index.ts                      # Test extension entry point
├── dist/                             # Build output
├── scripts/
│   ├── update-tpip.ts                # TPIP license tracking updater
│   └── tpip-reporter.ts              # TPIP license report generator
├── docs/
│   ├── third-party-licenses.json     # TPIP license database
│   └── tpip-header.md                # TPIP report header template
├── package.json                      # Self-test project configuration
├── tsconfig.json                     # TypeScript configuration
├── jest.config.js                    # Jest testing configuration
└── tpip.md                           # Generated TPIP license report
```

### TPIP License Compliance

The self-test infrastructure includes TPIP (Third-Party Intellectual Property) license tracking for
testing purposes:

- `scripts/update-tpip.ts` - License tracking updater
- `scripts/tpip-reporter.ts` - Report generator
- `docs/third-party-licenses.json` - License database

## Contributing

Contributions are welcome! This repository serves dual purposes:

1. **Workflow Improvements**: Enhance the reusable `build-and-verify.yml` workflow
2. **Testing Infrastructure**: Improve the self-test setup to validate workflow features

## Resources

- [Workflow Documentation](.github/WORKFLOWS.md) - Complete workflow usage guide
- [GitHub Actions Reusable Workflows](https://docs.github.com/en/actions/using-workflows/reusing-workflows)

## 📄 License

This project is licensed under the MIT License, see [LICENSE](./LICENSE).
