AGENTS.md

AI agent operating manual for release-it-calver-plugin. Read fully before any action.

---

Project: release-it-calver-plugin

- Purpose: A Release It! plugin implementing Calendar Versioning (CalVer) for Node projects.
- Owner: repository owner (human). The agent acts as an assistive, non-autonomous tool.
- Runtime: Node.js >= 18 (ESM module `type: "module"` in package.json).

Principles (strict)
- Always be conservative: prefer asking before any high-impact action (git writes, installs, releases).
- Follow repository conventions exactly (code style, ESM, test runner). Do not introduce unrelated tooling.
- Changes must be minimal, well-scoped, and fix root causes rather than gluing over problems.
- No TODO placeholders left in produced code; every TODO must be tracked in an issue before leaving it in the repo.

Do (allowed, without explicit approval)
- Read files and list directories in the repository.
- Run tests and test-related commands locally: `npm test` (uses `nyc` + `mocha`).
- Run single-file lint/type-checks if a linter/typ checker exists (none required by default here).
- Create or modify files when the user explicitly asks for changes in the repo.
- Add focused documentation files (e.g., `AGENTS.md`) when requested by the repo owner.

Don't (forbidden unless owner explicitly authorizes)
- Never perform any git write operation: `git commit`, `git push`, `git merge`, `git tag`, `git rebase`, `git reset`.
- Never publish packages or run `npm publish` or `release-it` unless explicitly authorized.
- Never run `npm install` or modify package dependencies without owner approval.
- Never deploy or run CI-affecting operations (e.g., `gh release create`) without owner consent.

Safety & Permissions

Allowed without asking:
- Read repo files and metadata.
- Run the repository's test command: `npm test`.
- Run single-file or focused checks (unit tests that target changed files).

Ask first (must get explicit permission):
- Any package installation or changes to `package.json` / `package-lock.json`.
- Any change that updates or modifies repository author/ownership/credits.
- Any git write operations or pushes to remote repositories.
- Running `release-it` or publishing artifacts.

Commands (repo-specific)
- Run tests (from repo root):
  - `npm test`
    - Runs: `nyc --reporter=lcovonly mocha **/*-tests.js --timeout 10000`
- Create a release (owner only, locally):
  - `npm run release`
    - Configured: `release-it -- --ci` (the repo's `release-it` configuration uses the plugin and format `yyyy.mm.minor`).

Versioning rules
- This repository uses CalVer as configured in `package.json` release-it plugin: format `yyyy.mm.minor`.
- Version components must be updated only via the release process (via `release-it` configured in this repo).
- When proposing version string changes, state the exact new version and justification.

Repository specifics
- Node requirement: Node >= 18 (see `package.json` `engines` field).
- Module type: ESM (`type: "module"` in `package.json`).
- Test framework: `mocha` with `nyc` for coverage.

PR Checklist (every PR produced or assisted by the agent must meet these before human finalization)
- [ ] Tests covering the change are added or updated where applicable.
- [ ] `npm test` passes locally (unit tests and coverage run).
- [ ] No TODO placeholders remain in modified files.
- [ ] Change is small and focused; docs updated if public API behavior changed.
- [ ] Any dependency changes are explicitly justified and requested by the owner.

When stuck or uncertain
- Ask a single, concise clarifying question describing the ambiguity and up to two possible actions.
- If a change risks breaking behavior, produce a minimal reproducible test demonstrating the issue before attempting a fix.

When making edits (agent behavior requirements)
- Produce minimal diffs: change only the lines required to implement the behavior.
- Include focused tests to validate behavior changes; run `npm test` locally if possible.
- Do not change repository tooling or CI configuration unless asked.

Examples of unacceptable actions
- Adding a new build system (webpack, rollup, etc.) without owner approval.
- Replacing test framework or upgrading major dependency versions without an explicit request.

Execute. Be precise. Ask when in doubt.