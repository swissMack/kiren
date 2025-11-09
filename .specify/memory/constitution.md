<!--
═══════════════════════════════════════════════════════════════════════════════
SYNC IMPACT REPORT - Constitution Update
═══════════════════════════════════════════════════════════════════════════════

Version Change: NONE → 1.0.0

Rationale: Initial constitution establishment for Kiren project. This is the
first formal version defining core principles and governance model.

Modified Principles:
- N/A (initial creation)

Added Sections:
- Core Principles (5 principles):
  I. Library-First Architecture
  II. Test-Driven Development (NON-NEGOTIABLE)
  III. Simplicity & YAGNI
  IV. Observability
  V. Versioning & Breaking Changes
- Web Application Standards
- Development Workflow
- Governance

Removed Sections:
- N/A (initial creation)

Templates Requiring Updates:
✅ plan-template.md - Reviewed, constitution check section already generic
✅ spec-template.md - Reviewed, no updates needed
✅ tasks-template.md - Reviewed, template structure supports TDD-first approach
✅ Command files - Reviewed, all use generic guidance (no agent-specific refs)

Follow-up TODOs:
- None

═══════════════════════════════════════════════════════════════════════════════
-->

# Kiren Constitution

## Core Principles

### I. Library-First Architecture

Every feature MUST start as a standalone library with clear boundaries and
responsibilities. Libraries MUST be:

- Self-contained with minimal external dependencies
- Independently testable without requiring full application context
- Documented with clear API contracts and usage examples
- Purpose-driven - no organizational-only libraries without functional value

**Rationale**: Library-first design enforces modularity, enables code reuse
across web frontend and backend, reduces coupling, and makes testing tractable.
It prevents the monolith anti-pattern common in web applications.

### II. Test-Driven Development (NON-NEGOTIABLE)

TDD is MANDATORY for all production code. The workflow is strict:

1. Tests MUST be written first
2. User MUST approve test scenarios before implementation
3. Tests MUST fail initially (red phase)
4. Implementation makes tests pass (green phase)
5. Refactor with confidence (refactor phase)

**Rationale**: TDD ensures requirements are understood before coding begins,
produces living documentation, prevents scope creep, and enables fearless
refactoring. This principle is non-negotiable because it fundamentally changes
how quality is achieved - quality is designed in, not tested in.

### III. Simplicity & YAGNI

Start with the simplest solution that solves the immediate problem. MUST NOT:

- Build features for hypothetical future needs (You Aren't Gonna Need It)
- Add abstraction layers before they prove necessary
- Choose complex patterns when simple ones suffice

Complexity MUST be justified explicitly when unavoidable (see Governance
section). Every layer of indirection requires documented rationale.

**Rationale**: Premature optimization and speculative generality are the root
of unmaintainable systems. Simple code is easier to understand, modify, test,
and deploy. For web applications, this prevents framework bloat and
over-engineered architectures.

### IV. Observability

All components MUST be debuggable and monitorable. Required practices:

- Structured logging at appropriate levels (debug, info, warn, error)
- Text-based I/O protocols where feasible (enables debugging via CLI/curl)
- Meaningful error messages with context (not just stack traces)
- Request tracing for distributed operations (correlation IDs)

**Rationale**: Web applications fail in production, not just in development.
Observability enables rapid diagnosis of issues, understanding user behavior,
and measuring performance. Text-based protocols allow manual testing and
debugging without specialized tools.

### V. Versioning & Breaking Changes

All APIs (both internal libraries and external endpoints) MUST follow semantic
versioning (MAJOR.MINOR.PATCH):

- MAJOR: Breaking changes (incompatible API changes)
- MINOR: New features (backward-compatible additions)
- PATCH: Bug fixes (backward-compatible fixes)

Breaking changes MUST:
- Be documented with migration guides
- Provide deprecation warnings in at least one minor version before removal
- Include automated migration tools when feasible

**Rationale**: Web applications often have multiple consumers (frontend, mobile
apps, third-party integrations). Semantic versioning provides a contract that
enables independent deployment and reduces coordination overhead.

## Web Application Standards

As a web application, Kiren MUST adhere to these additional standards:

- **API Design**: RESTful principles for HTTP APIs; GraphQL when complex query
  needs are documented
- **Frontend/Backend Contracts**: OpenAPI or similar schema for all endpoints
  (see Library-First principle)
- **Security**: Authentication and authorization at API layer; input validation
  and sanitization; HTTPS in production
- **Performance**: Response times <200ms p95 for API endpoints unless
  documented otherwise; frontend <3s initial load on 3G
- **Accessibility**: WCAG 2.1 AA compliance for all user-facing interfaces

These standards may be adjusted via constitution amendment for documented
technical constraints.

## Development Workflow

### Test-First Mandate

Before any implementation:
1. Write contract tests for library boundaries
2. Write integration tests for user-facing workflows
3. Get user approval on test scenarios
4. Ensure tests fail (red phase)
5. Implement until tests pass (green phase)
6. Refactor without changing behavior

### Code Review Gates

All changes MUST pass review verifying:
- TDD process followed (test commits before implementation commits)
- No unjustified complexity (see Simplicity principle)
- Libraries are self-contained (see Library-First principle)
- Observability hooks present (see Observability principle)
- Breaking changes properly versioned (see Versioning principle)

### Continuous Integration

Automated CI MUST verify:
- All tests pass
- Code coverage meets minimum threshold (80% for libraries, 60% for integration)
- Linting and formatting rules enforced
- No security vulnerabilities in dependencies

## Governance

**Authority**: This constitution supersedes all other development practices,
style guides, and conventions unless explicitly documented as exceptions.

**Amendments**: Changes to this constitution require:
1. Documented rationale explaining why current principles are insufficient
2. Impact analysis on existing codebase and templates
3. Migration plan for affected code
4. Approval from project maintainers
5. Version bump according to semantic versioning (applied to constitution itself)

**Compliance Review**: All pull requests and code reviews MUST verify
compliance with constitutional principles. Violations MUST be rejected unless
accompanied by explicit exception approval.

**Complexity Justification**: When violating Simplicity & YAGNI principle is
unavoidable, MUST document in plan.md Complexity Tracking section:
- What simpler alternative was considered
- Why the simpler alternative is insufficient
- What specific problem the complexity solves

**Living Document**: This constitution evolves with the project. Use
`/speckit.constitution` command to update and ensure dependent templates remain
synchronized.

**Version**: 1.0.0 | **Ratified**: 2025-11-09 | **Last Amended**: 2025-11-09
