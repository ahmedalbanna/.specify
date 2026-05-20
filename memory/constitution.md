# MVP Project Constitution

## Core Principles

### I. API-First Design
Every feature starts with backend API design. Define endpoints, DTOs, and response contracts before building frontend. Backend and frontend teams agree on API contracts via documentation before implementation begins.

### II. Feature-First Architecture
Code is organized by feature, not by technical layer. Each feature module (auth, products, orders) is self-contained with its own entities, services, controllers, and DTOs. Features must be independently testable and deployable.

### III. Spec-Driven Development (NON-NEGOTIABLE)
Every feature must follow the Speckit workflow: Specification → Plan → Tasks → Implement. No code is written without an approved spec and plan. The `/speckit.specify`, `/speckit.plan`, and `/speckit.tasks` commands are mandatory gates.

### IV. Contract Consistency
API contracts must be identical between backend and frontend. Field names, types, and response shapes are defined once and shared. Any contract change requires updating both sides and running `/workflow.sync.contracts`.

### V. Security Baseline
All endpoints require authentication by default (opt-out, not opt-in). JWT with refresh token flow. Input validation via class-validator on every DTO. Rate limiting on auth endpoints. CORS configured explicitly. No secrets in code — environment variables only.

## Additional Constraints

### Technology Stack
- Backend: NestJS + TypeScript + Prisma + PostgreSQL
- Admin Dashboard: React + TypeScript + Vite + Ant Design + TanStack Query
- Mobile App: Flutter + Clean Architecture + BLoC + GoRouter + GetIt
- Alternative Mobile: React Native (Expo) + TypeScript + TanStack Query

### Code Quality
- TypeScript strict mode — no `any`
- All API responses follow standard shape: `{ success, data, message?, meta? }`
- Prisma ORM only — no raw SQL unless explicitly justified
- BLoC/Cubit for Flutter state, TanStack Query for React server state
- Naming conventions: lowercase modules, kebab-case endpoints, PascalCase screens

### Testing Requirements
- Unit tests for all services and use cases
- E2E tests for critical user flows (auth, core CRUD)
- Coverage target: ≥80% on critical paths
- Tests must pass before merging any feature

## Development Workflow

### Feature Lifecycle
1. `/speckit.specify` — Write user-focused specification (no tech details)
2. `/speckit.plan` — Create technical implementation plan
3. `/speckit.tasks` — Break into actionable, ordered tasks
4. `/speckit.review` — Cross-artifact consistency check
5. `/speckit.implement` — Execute tasks and generate code
6. Test → Review → Merge

### Code Review Standards
- All PRs must reference a spec and plan
- API contract changes require explicit approval
- No bypassing Speckit workflow for production features
- Security-sensitive changes require `@security-guard` review

## Governance

This constitution supersedes all other development practices. Amendments require:
1. Explicit proposal with rationale
2. Impact analysis on existing features
3. Migration plan if breaking existing conventions
4. Team consensus before adoption

All agents and workflows must verify compliance with these principles.

**Version**: 1.0.0 | **Ratified**: 2026-05-20 | **Last Amended**: 2026-05-20
