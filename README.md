# @dschz/tsconfig

Shared TypeScript configurations for `@dschz` packages. Strict by default, layered by environment.

## Install

```bash
bun add -D @dschz/tsconfig
```

## Configs

| Config | Use case |
|--------|----------|
| `@dschz/tsconfig/base` | Environment-agnostic libraries (no DOM) |
| `@dschz/tsconfig/solid` | SolidJS libraries and applications |
| `@dschz/tsconfig/react` | React libraries and applications |

## Usage

```json
// SolidJS library or app
{
  "extends": "@dschz/tsconfig/solid",
  "compilerOptions": {
    "baseUrl": ".",
    "paths": { "@scope/*": ["./packages/*/src"] }
  },
  "include": ["**/*.ts", "**/*.tsx"],
  "exclude": ["node_modules", "dist", "coverage"]
}
```

```json
// React library or app
{
  "extends": "@dschz/tsconfig/react",
  "compilerOptions": {
    "baseUrl": "."
  },
  "include": ["**/*.ts", "**/*.tsx"],
  "exclude": ["node_modules", "dist", "coverage"]
}
```

```json
// Vanilla TypeScript library (no DOM, no JSX)
{
  "extends": "@dschz/tsconfig/base",
  "compilerOptions": {
    "baseUrl": "."
  },
  "include": ["**/*.ts"],
  "exclude": ["node_modules", "dist"]
}
```

## What's included in `base`

- `moduleResolution: Bundler`
- `moduleDetection: force`
- `verbatimModuleSyntax: true`
- `isolatedModules: true`
- `lib: ["ESNext"]` — no DOM
- Full strict suite: `exactOptionalPropertyTypes`, `noUncheckedIndexedAccess`, `noUnusedLocals`, `noUnusedParameters`, `noImplicitReturns`, and more
- `erasableSyntaxOnly: true` — disallows enums, namespaces, and parameter properties (enforces TypeScript as pure type erasure)

## Notes

- `paths`, `baseUrl`, `outDir`, `noEmit`, `declaration`, and `types` are intentionally omitted — set these per-project
- `solid` and `react` configs add `lib: ["ESNext", "DOM", "DOM.Iterable"]` on top of base
