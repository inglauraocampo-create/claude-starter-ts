# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

Package manager is **pnpm** (pinned via `packageManager` in `package.json`). Node ≥20.

- `pnpm install` — install dependencies
- `pnpm build` — compile `src/` to `dist/` with `tsc`
- `pnpm typecheck` — `tsc --noEmit`
- `pnpm test` — run all tests once with Vitest (`pnpm test:watch` for watch mode)
- Single test file: `pnpm test src/index.test.ts`
- Single test by name: `pnpm vitest run -t "<test name>"`
- `pnpm lint` / `pnpm lint:fix` — ESLint over the whole repo (`dist/` and `coverage/` ignored)
- `pnpm format` / `pnpm format:check` — Prettier over the whole repo (respects `.gitignore` and `.prettierignore`)

## Setup notes

- ESM project (`"type": "module"`) compiled with `module`/`moduleResolution: NodeNext`: relative imports in `.ts` files must use the `.js` extension (e.g. `import { sum } from './index.js'`).
- TypeScript runs in `strict` mode. There is a single `tsconfig.json`, which excludes `src/**/*.test.ts` so tests aren't emitted to `dist/`. As a result, `pnpm typecheck` does **not** type-check test files, and Vitest runs them without type-checking.
- Tests live next to their source as `*.test.ts` and run with Vitest's defaults (no `vitest.config`).
- Vitest is pinned to `^4` because Vitest 5 requires Node ≥22.12.
- ESLint 9 uses a flat config in `eslint.config.js` (loaded as ESM): `@eslint/js` recommended + `typescript-eslint` recommended, with Node globals. Linting is **not** type-aware, because test files sit outside `tsconfig.json`, so `projectService` would reject them.
- Prettier owns formatting and ESLint only checks code quality. `eslint-config-prettier/flat` must stay the **last** entry in `eslint.config.js` so it disables any conflicting ESLint style rules. Prettier config is `.prettierrc.json` (only `singleQuote: true`), and Prettier is pinned to an exact version because even minor releases can change its output.
- TypeScript is pinned to 5.x because `typescript-eslint` only supports TypeScript `<6.1`. Don't upgrade TypeScript past that range until typescript-eslint supports it.
