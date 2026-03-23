# @dschz/tsconfig

Shared TypeScript configurations for `@dschz` packages. Strict by default, layered by environment.

## Install

```bash
bun add -D @dschz/tsconfig
```

## Configs

| Config | Use case |
|--------|----------|
| `@dschz/tsconfig/base` | Strict base — no JSX, no DOM |
| `@dschz/tsconfig/lib` | Library packages (ESNext, declarations) |
| `@dschz/tsconfig/app` | Applications (ESNext + DOM) |
| `@dschz/tsconfig/lib/solid` | SolidJS library |
| `@dschz/tsconfig/lib/react` | React library |
| `@dschz/tsconfig/app/solid` | SolidJS application |
| `@dschz/tsconfig/app/react` | React application |

## Usage

```json
// SolidJS library
{
  "extends": "@dschz/tsconfig/lib/solid",
  "compilerOptions": {
    "baseUrl": ".",
    "paths": { "@scope/*": ["./packages/*/src"] }
  },
  "include": ["**/*.ts", "**/*.tsx"],
  "exclude": ["node_modules", "dist", "coverage"]
}
```

```json
// SolidJS app
{
  "extends": "@dschz/tsconfig/app/solid",
  "compilerOptions": {
    "baseUrl": ".",
    "types": ["vite/client"]
  },
  "include": ["**/*.ts", "**/*.tsx"],
  "exclude": ["node_modules", "dist"]
}
```

```json
// Vanilla TypeScript library (no framework)
{
  "extends": "@dschz/tsconfig/lib",
  "compilerOptions": {
    "baseUrl": "."
  },
  "include": ["**/*.ts"],
  "exclude": ["node_modules", "dist"]
}
```

## What's included in `base`

All settings from `@tsconfig/strictest` plus:

- `moduleResolution: Bundler`
- `moduleDetection: force`
- `verbatimModuleSyntax: true`
- `isolatedModules: true`
- `exactOptionalPropertyTypes: true`
- `noPropertyAccessFromIndexSignature: true`
- `noImplicitReturns: true`

## Notes

- `paths`, `baseUrl`, `outDir`, and `types` are intentionally omitted — set these per-project
- `lib/` configs omit DOM — add it explicitly if your library targets the browser
- `app/` configs set `noEmit: true` — bundler (Vite/tsup) handles output
