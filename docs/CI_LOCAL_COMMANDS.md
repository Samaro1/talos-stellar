# CI Local Commands

This document provides the local commands that match each CI gate in the Python Package and Web/SDK CI workflows.

## Python Package CI

The CI workflow `ci-python-package.yml` runs the following checks on the `packages/prime-agent` directory:

### Lint
```bash
cd packages/prime-agent
uv sync --frozen --all-extras --all-groups
uv run ruff check src tests
```

### Test
```bash
cd packages/prime-agent
uv sync --frozen --all-extras --all-groups
uv run pytest tests/ -v
```

### Run all Python checks locally
```bash
cd packages/prime-agent
uv sync --frozen --all-extras --all-groups
uv run ruff check src tests
uv run pytest tests/ -v
```

## Web and SDK CI

The CI workflow `ci-web-sdk.yml` runs the following checks on the `web` and `packages/sdk` directories:

### Web type check
```bash
pnpm install --frozen-lockfile
cd web
pnpm build
```

### Web lint
```bash
pnpm install --frozen-lockfile
cd web
pnpm lint
```

### Web unit tests
```bash
pnpm install --frozen-lockfile
cd web
pnpm test:unit
```

### SDK type check
```bash
pnpm install --frozen-lockfile
cd packages/sdk
pnpm build:esm
```

### SDK tests
```bash
pnpm install --frozen-lockfile
cd packages/sdk
pnpm test
```

### Run all Web/SDK checks locally
```bash
pnpm install --frozen-lockfile

# Web checks
cd web
pnpm build
pnpm lint
pnpm test:unit

# SDK checks
cd ../packages/sdk
pnpm build:esm
pnpm test
```

## Path Filters

The CI workflows use path filters to ensure they only run when relevant changes are made:

### Python Package CI (`ci-python-package.yml`)
- `packages/prime-agent/**`
- `.github/workflows/ci-python-package.yml`

### Web and SDK CI (`ci-web-sdk.yml`)
- `web/**`
- `packages/sdk/**`
- `pnpm-lock.yaml`
- `package.json`
- `.github/workflows/ci-web-sdk.yml`

This ensures that unrelated changes don't trigger unnecessary CI runs.
