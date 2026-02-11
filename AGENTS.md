# Repository Guidelines

- Repo: https://github.com/openclaw/openclaw
- Language: TypeScript (ESM), Node 22+
- Package manager: pnpm 10.23.0

## Build, Test & Development Commands

| Command | Description |
|---------|-------------|
| `pnpm install` | Install dependencies |
| `pnpm build` | Build TypeScript + bundle UI |
| `pnpm dev` | Run CLI in dev mode |
| `pnpm test` | Run all tests (vitest) |
| `pnpm test:coverage` | Run tests with coverage |
| `pnpm test:watch` | Watch mode for tests |
| `bun vitest run --reporter=verbose --testNamePattern="test name"` | Run single test |
| `pnpm check` | Full lint + format + type check |
| `pnpm lint` | Run oxlint |
| `pnpm format:fix` | Auto-fix formatting |
| `pnpm tsgo` | TypeScript checks |

Pre-commit: `prek install`

## Code Style Guidelines

### Types & Formatting
- Use strict TypeScript typing; avoid `any`
- Run `pnpm check` before committing
- Formatting via Oxlint/Oxfmt; no manual formatting
- Keep files under ~500 LOC; refactor when needed

### Imports & Structure
- Named imports preferred: `import { foo } from 'bar'`
- Colocate tests: `*.test.ts` next to source files
- Use `createDefaultDeps` for dependency injection

### Naming Conventions
- **OpenClaw**: product/app/docs headings
- `openclaw`: CLI command, package, binary, paths, config keys
- PascalCase for types/classes, camelCase for variables/functions
- kebab-case for file names

### Error Handling
- Use `Result<T>` patterns where appropriate
- Propagate errors with context; don't silently catch
- Never log secrets or credentials

### Comments
- Add brief comments for non-obvious logic
- Document public APIs and complex algorithms
- Avoid commenting obvious code

### General Patterns
- Extract helpers instead of duplicating code
- Avoid "V2" copies; refactor towards shared helpers
- Use existing CLI option patterns (see `src/cli`)

## Project Structure

```
src/
  cli/          # CLI wiring
  commands/     # Command implementations
  channels/    # Built-in messaging channels
  infra/       # Infrastructure code
  media/       # Media processing pipeline
  telegram/, discord/, slack/, signal/, imessage/, web/  # Channel providers
extensions/   # Plugin workspace packages
docs/         # Mintlify documentation
dist/         # Built output
```

## Testing Guidelines

- Framework: Vitest with V8 coverage (70% threshold)
- Test files: `*.test.ts` colocated; e2e in `*.e2e.test.ts`
- Run `pnpm test` before pushing logic changes
- Live tests: `CLAWDBOT_LIVE_TEST=1 pnpm test:live`

## Git & PR Workflow

- Commit with: `scripts/committer "<msg>" <files>`
- Concise, action-oriented messages (e.g., `CLI: add verbose flag`)
- See `.agents/skills/PR_WORKFLOW.md` for full PR process

## Important Notes

- Never edit `node_modules`
- When adding channels/extensions, update `.github/labeler.yml`
- Release guardrails: ask before changing version numbers
- Multi-agent: don't create git stash or switch branches unless asked
