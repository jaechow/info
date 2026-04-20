# Node.js & JS Toolchain

Package managers, runners, debugging, and TypeScript workflows.

## Package Managers

### npm

Install dependencies:

```shell
npm install
```

Add a dev dependency:

```shell
npm install -D vitest
```

Run a script from `package.json`:

```shell
npm run build
```

Check for outdated packages:

```shell
npm outdated
```

Update interactively:

```shell
npx npm-check-updates -i
```

### pnpm

Drop-in npm replacement with faster installs and disk savings:

```shell
pnpm install
pnpm add -D typescript
pnpm run dev
```

> Install: `brew install pnpm` · `npm install -g pnpm`

### Bun

All-in-one runtime, bundler, and package manager:

```shell
bun install             # install deps (reads package.json)
bun run dev             # run scripts
bun add hono            # add a dependency
```

Run a file directly (no build step):

```shell
bun run server.ts
```

> Install: `brew install oven-sh/bun/bun` · `curl -fsSL https://bun.sh/install | bash`

---

## npx — Run Without Installing

Run a package without installing globally:

```shell
npx create-next-app@latest my-app
```

Use a specific version:

```shell
npx -p typescript@5 tsc --init
```

---

## tsx — Run TypeScript Directly

Execute TypeScript without a build step (via Node.js):

```shell
tsx src/script.ts
```

Watch mode:

```shell
tsx watch src/server.ts
```

> Install: `npm install -g tsx`

---

## Debugging

### Node.js Inspector

Start with the debugger:

```shell
node --inspect src/index.js
```

Break on first line:

```shell
node --inspect-brk src/index.js
```

Then open `chrome://inspect` in Chrome to connect.

### Environment Variables

Inline environment variables:

```shell
NODE_ENV=production node src/index.js
```

Load from `.env` file (Node.js 20.6+):

```shell
node --env-file=.env src/index.js
```

---

## Vitest / Jest CLI

Run tests:

```shell
npx vitest run
```

Watch mode:

```shell
npx vitest
```

Run a specific test file:

```shell
npx vitest run src/auth.test.ts
```

Run tests matching a pattern:

```shell
npx jest --testPathPattern="auth"
```

Show coverage:

```shell
npx vitest run --coverage
```

---

## Comparison

| Feature | npm | pnpm | Bun |
|---------|-----|------|-----|
| **Speed** | Baseline | ~2x faster | ~5x faster |
| **Disk usage** | Duplicates deps | Hard links (saves space) | Compact |
| **Lockfile** | `package-lock.json` | `pnpm-lock.yaml` | `bun.lockb` |
| **Built-in runner** | No | No | Yes (TypeScript, JSX) |
| **Compatibility** | Universal | High | Growing |
