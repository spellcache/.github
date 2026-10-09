# Contributing to spellcache

Thanks for your interest! This guide applies to every repository of the
spellcache organisation unless a repository has its own `CONTRIBUTING.md`.

## Before you start

- **Bugs**: open an issue with the *Bug report* form. Search existing issues
  first.
- **Features**: open an issue with the *Feature request* form, or start a
  [Discussion](https://github.com/orgs/spellcache/discussions) for open-ended
  ideas. Agree on the approach before writing a large change.
- **Security issues**: never in a public issue — see [SECURITY.md](SECURITY.md).
- **Visual changes**: the app has a deliberate design language. New screens are
  built from existing components and design tokens; discuss anything visually
  new in an issue first.

## Development setup

The app's repository documents its local setup, commands and conventions in
[`docs/development.md`](https://github.com/spellcache/spellcache/blob/main/docs/development.md).
In short:

```bash
cp .env.example .env          # then set AUTH_SECRET
docker compose up -d postgres redis
pnpm install
pnpm db:migrate
pnpm dev
```

## Pull request workflow

1. Fork the repository and create a branch from `main`
   (`feat/short-description`, `fix/short-description`).
2. Keep the change focused: one feature or fix per pull request.
3. Run the checks locally before pushing:

   ```bash
   pnpm lint
   pnpm typecheck
   pnpm test          # unit + integration (needs Docker for the test database)
   pnpm test:e2e      # when you change a user flow
   ```

4. Open the pull request against `main` and fill in the template. CI runs
   lint, typecheck, tests, the build and both Docker images.
5. A maintainer reviews it. Address the comments with new commits; they will be
   squashed when merging.

## Commit messages

We use [Conventional Commits](https://www.conventionalcommits.org/). They drive
the changelog and the version number:

```
feat: add a condition filter to binders
fix(worker): retry the bulk download on 503
docs: explain the reverse proxy headers
```

| Type | Use for | Version |
|---|---|---|
| `feat` | a user-visible feature | minor |
| `fix` | a bug fix | patch |
| `docs`, `refactor`, `test`, `build`, `ci`, `chore` | everything else | none |

Add `!` after the type (`feat!:`) or a `BREAKING CHANGE:` footer for a breaking
change.

## Tests

- New behaviour comes with tests: Vitest for logic and data access
  (`tests/unit`, `tests/integration`), Playwright for user flows (`tests/e2e`).
- Integration tests start a throwaway PostgreSQL through Docker Compose; they
  skip themselves when Docker is not available, but CI always runs them.

## Code of conduct

Everyone taking part in the project is expected to follow the
[Code of Conduct](CODE_OF_CONDUCT.md).

## License

By contributing, you agree that your contributions are licensed under the
license of the repository you contribute to (MIT for the app).
