# Copilot Instructions — JVI Ecosystem

## Dashboard
All work is tracked on [JVI Dashboard](https://github.com/users/jasonv2610/projects/1) (GitHub Projects #1).

## When Working on Issues
1. **Read the repo CLAUDE.md first** — it contains domain-specific rules, constraints, and agent definitions
2. **Update the project board** when starting work (Status → In Progress) and when done (Status → Done)
3. **Link PRs to issues** — every PR should reference the issue it resolves
4. **Follow quality gates**: REG-001 (no workflow deletion), REG-002 (no agent node changes without approval), REG-003 (validate after workflow edits)
5. **Security**: Never commit secrets, .env files, or credentials. All repos have a pre-commit secret scanner

## Pipeline Fields to Set
When creating or updating issues, ensure these fields are set on the project board:
- **Status**: Todo → In Progress → Done (or Needs Attention if blocked)
- **Domain**: Match to the area of work (orchestration, data-analytics, infrastructure, etc.)
- **Priority**: P0-critical through P3-low based on impact
- **Type**: Workflow, Agent, Script, Task, or Infrastructure

## Code Standards

### Language Defaults
- TypeScript for all new Node.js code. Use `import type { }` for type-only imports. Prefer branded types for IDs.
- Python for data pipelines, ML, and scripting. Use `pytest` with `test_*.py` colocated.
- Conventional commits: `feat:`, `fix:`, `chore:`, `docs:`, `refactor:`, `test:`. No AI attribution in messages.
- Mobile-first for all web projects.

### Before Coding (Required)
- Ask clarifying questions before non-trivial work.
- Confirm approach for complex changes. List pros/cons if multiple valid paths exist.
- Read the target file before editing. Never implement blindly.

### While Coding
- TDD: write failing test first, then implement (REG-POW-001).
- Name functions using existing domain vocabulary. Read the codebase first.
- No classes when simple testable functions suffice.
- No comments unless the WHY is non-obvious (a constraint, a workaround, a subtle invariant).
- No premature function extraction. Extract only if: reused in 2+ places, OR only way to unit-test, OR original requires inline comments everywhere.

### Testing
- Colocate unit tests: `*.spec.ts` (TS) or `test_*.py` (Python) in same directory as source.
- Separate pure-logic unit tests from DB-touching integration tests. Always.
- Prefer integration tests over mocking. JVI uses real Supabase in tests.
- Use strong assertions: `toEqual(1)` not `toBeGreaterThanOrEqual(1)`.
- Every test must be able to fail for a real defect.

### Tooling Gates (all must pass before commit)
1. `prettier --check` (JS/TS)
2. `eslint` (JS/TS) or `pytest --tb=short` (Python)
3. Project test suite

### Q-Shortcuts (Claude Code only)
`QNEW` load best practices | `QPLAN` confirm approach | `QCODE` implement + run gates | `QCHECK` full review | `QGIT` format + commit + push

Full definitions in `~/.claude/CLAUDE.md`.

## Anti-Loop Protocol
- Maximum 3 fix attempts per strategy before escalating
- Each attempt must use a different approach
- If stuck, set Health=Red and Status=Needs Attention on the project board

## jviscapfold-agent-debug: JVI Scapfold Debugging Protocol
- **The 4-Second Camo Rule**: GitHub Camo CDN (`camo.githubusercontent.com`) enforces a strict 4.0s timeout when proxying external markdown images. Any upstream latency spike poisons the edge cache with `"Error Fetching Resource"` for 24 hours.
- **Cache Invalidation (`PURGE`)**: Invalidate poisoned Camo caches instantly via `curl -X PURGE "https://camo.githubusercontent.com/<hash>/<hex>"`.
- **Target URL Decoding**: Camo path suffixes contain hex-encoded ASCII of the origin target URL.
- **Upstream Resilience**: Always append `&cache_seconds=86400` to dynamic SVG badges or generate static SVGs via daily GitHub Actions (e.g. `raw.githubusercontent.com/.../output/badge.svg`).
- **Windows CUDA & CPython Runtime**: Guard `torch.compile` (`compile_if_supported`), calibrate VRAM micro-batches ($16 \times 16$), and disable `gc.freeze()` on Windows.


