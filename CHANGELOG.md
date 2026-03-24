# @dschz/tsconfig

## 0.1.0

### Minor Changes

- Initial release — shared TypeScript configurations for `@dschz` packages

### Configs

Three configurations are available:

**`@dschz/tsconfig/base`** — Foundation config for any bundler-based project. No DOM types included; add them in framework-specific configs. Targets ESNext with strict mode fully enabled.

**`@dschz/tsconfig/solid`** — Extends `base` with DOM lib and SolidJS JSX transform. Use for SolidJS libraries and apps.

**`@dschz/tsconfig/react`** — Extends `base` with DOM lib and React JSX transform. Use for React libraries and apps.

### Compiler options of note

- `erasableSyntaxOnly: true` — enforces modern type-erasure philosophy; blocks enums, `namespace`, parameter properties, and legacy decorators
- `verbatimModuleSyntax: true` — enforces explicit `import type` for type-only imports
- `exactOptionalPropertyTypes: true` — distinguishes between `undefined` and missing properties
- `noUncheckedIndexedAccess: true` — array/object index access always returns `T | undefined`
- `moduleResolution: "Bundler"` — correct resolution for Vite, tsup, and other bundler-based toolchains
- `moduleDetection: "force"` — treats every file as a module, eliminating global scope surprises

### Philosophy

Configs are fully self-contained with no external `tsconfig` dependencies. Every setting is explicit and visible — no transitive options hidden behind extended packages.
