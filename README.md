# HLPM - Electron Builder Action
**GitHub Action for building and releasing Electron apps**

**This is a fork from [samuelmeuli/action-electron-builder](https://github.com/samuelmeuli/action-electron-builder). Thanks to Samiel Meuli for his work 🙏🏽**

[![Lint](https://github.com/helpmii-team/action-electron-builder/actions/workflows/lint.yml/badge.svg)](https://github.com/helpmii-team/action-electron-builder/actions/workflows/lint.yml)

## Diff
1. node12 -> node16

## Usage
```yaml
name: Build/release

on: push

jobs:
  release:
    runs-on: ${{ matrix.os }}

    strategy:
      matrix:
        os: [macos-latest, ubuntu-latest, windows-latest]

    steps:
      - name: Check out Git repository
        uses: actions/checkout@v3

      - name: Install Node.js, NPM and Yarn
        uses: actions/setup-node@v3
        with:
          node-version: 18

      - name: Build/release Electron app
        uses: helpmii-teams/action-electron-builder@stable
        with:
          # GitHub token, automatically provided to the action
          # (No need to define this secret in the repo settings)
          github_token: ${{ secrets.github_token }}

          # If the commit is tagged with a version (e.g. "v1.0.0"),
          # release the app after building
          release: ${{ startsWith(github.ref, 'refs/tags/v') }}
```

