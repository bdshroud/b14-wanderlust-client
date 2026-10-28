# AGENTS.md

Single-package Next.js 16.4.2 (App Router). Not a monorepo — no workspace config, no test suite, no CI.

## Commands

- Dev: `npm run dev` (Next dev)
- Build: `npm run build`
- Start: `npm run start`
- Lint: `npm run lint` (ESLint 9, flat config via `eslint-config-next`)
- Typecheck: no script — run `npx tsc --noEmit` (passes currently)
- Verify: `npx tsc --noEmit` → `npm run lint` → `npm run build`
- No test runner configured; don't invent `npm test`.

## Architecture

- App Router under `src/app/` (`page.tsx`, `layout.tsx`). UI in `src/components/`, hooks in `src/hooks/`, helpers in `src/lib/`. `src/proxy.ts` exists (proxy entry).
- Path alias: `@/*` → `./src/*`.
- `next.config.ts`: `cacheComponents: false`, `partialPrefetching: false`, `reactCompiler: true` (Babel React Compiler), `images.remotePatterns` allows `https://**`, Turbopack CSS rule for `@tailwindcss/turbopack`.
- Auth: `better-auth` + `@better-auth/mongo-adapter` + `mongodb` present (expect auth-related setup; look in `src/app/` or lib before assuming).

## shadcn / UI

- Config `components.json`: style `base-nova`, RSC/TSX, Tailwind v4 (CSS-first, no `tailwind.config`), base color `neutral`, CSS variables enabled, icon library `lucide`. **Primitives: `@base-ui/react` (not Radix)** — don't swap imports.
- Add: `npx shadcn add <name>`. Don't hand-edit generated files under `src/components/ui/` (overwritten on add/update).
- `cn` imported directly as `import { cn } from "cn"` (package). `src/lib/utils.ts` only re-exports it — follow neighboring files.
- Theme tokens in `src/app/globals.css`. Add new styles/tokens there.

<!-- BEGIN:nextjs-agent-rules -->

## This is NOT the Next.js you know

This version has breaking changes — APIs, conventions, and file structure may all differ from your training data. Read the relevant guide in `node_modules/next/dist/docs/` (resolved from this file's directory; in monorepos the `next` package may not be visible from the repo root) before writing any code. Heed deprecation notices.

This block is written and re-added by `next dev` — verify at `node_modules/next/dist/server/lib/generate-agent-files.js`. Removing it from a diff only re-creates the uncommitted change; committing it with your work keeps the tree clean.

<!-- END:nextjs-agent-rules -->
