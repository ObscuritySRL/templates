# Templates

Project templates for Bun/TypeScript.

## Usage

```bash
# Base (library/non-React)
bunx tiged ObscuritySRL/templates/base my-project

# React
bunx tiged ObscuritySRL/templates/react my-app
```

## Contents

| Template | Description |
|----------|-------------|
| `base` | TypeScript + Bun, no DOM |
| `react` | TypeScript + Bun + React |

Both include:
- `AGENTS.md` — agent configuration
- `.prettierrc.json` — 120 width, single quotes
- `.prettierignore`
- `.gitignore`
- `tsconfig.json`
