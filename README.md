# Svelte-Check PR Annotator

## Usage

Annotate pull requests with [`svelte-check`](https://github.com/sveltejs/language-tools/tree/master/packages/svelte-check) errors detected during CI.

Note: This doesn't install or run `svelte-check`, it just sets up the PR annotations.

### Example workflow

```yaml
name: My Workflow
on: [push, pull_request]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Install pnpm
        uses: pnpm/action-setup@v2.2.2
        with:
          version: 7
      - name: Use Node.js 18
        uses: actions/setup-node@v3
        with:
          node-version: 18
          cache: "pnpm"
      - name: Install build dependencies 🧰
        run: |
          pnpm install
          pnpm svelte-kit sync

      - name: Add Svelte Check annotator
        uses: prgm-dev/svelte-check-pr-annotator@main

      - name: Run Svelte-Check
        run: pnpm svelte-check --output machine --use-new-transformation true
```
