# ClawAutoResearch Docs

This repository hosts the standalone VitePress documentation site for ClawAutoResearch.

The site is intentionally split into two tracks:

- user docs: installation, quickstart, project startup, and recovery flows
- technical docs: architecture, runtime behavior, state contracts, and operations

## Local development

```bash
npm install
npm run docs:dev
```

## Build

```bash
npm run docs:build
```

## Deployment

GitHub Pages deployment is handled by:

- `.github/workflows/deploy-docs.yml`
