# Implementation Plan: [FEATURE]

**Branch**: `[###-feature-name]` | **Date**: [DATE] | **Spec**: [link]
**Input**: Feature specification from `/specs/[###-feature-name]/spec.md`

**Note**: This template is filled in by the `/speckit.plan` command.

## Summary

[Extract from feature spec: primary requirement + technical approach from research]

## Technical Context

**Language/Version**: TypeScript 5+, Dart 3+
**Primary Dependencies**: NestJS, Prisma, PostgreSQL, React, Ant Design, TanStack Query, Flutter, BLoC, GoRouter
**Storage**: PostgreSQL via Prisma ORM
**Testing**: Jest (backend), Vitest + Testing Library (admin), flutter_test + integration_test (mobile)
**Target Platform**: Linux server (backend), Web (admin), iOS + Android (mobile)
**Project Type**: Full-stack application (Backend API + Admin Dashboard + Mobile App)
**Performance Goals**: API response < 200ms p95, admin page load < 2s, mobile 60fps
**Constraints**: JWT auth, RBAC, feature-first architecture, API contract consistency
**Scale/Scope**: MVP — single tenant, < 10k users

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

- [ ] API-first: Backend API defined before frontend implementation
- [ ] Feature-first: Code organized by feature, not by layer
- [ ] Spec-driven: No code without approved spec and plan
- [ ] Contract consistency: API contracts identical between backend and clients
- [ ] Security baseline: Auth by default, input validation, no secrets in code

## Project Structure

### Documentation (this feature)

```text
specs/[###-feature]/
├── plan.md              # This file
├── research.md          # Phase 0 output
├── data-model.md        # Phase 1 output
├── quickstart.md        # Phase 1 output
├── contracts/           # Phase 1 output
└── tasks.md             # Phase 2 output (/speckit.tasks command)
```

### Source Code

```text
backend/
├── src/
│   ├── main.ts
│   ├── app.module.ts
│   ├── config/          # env, Swagger, database
│   ├── common/          # Filters, Guards, Interceptors
│   ├── modules/         # Feature modules (auth, users, products...)
│   └── shared/          # PrismaService, shared utilities
├── prisma/
│   └── schema.prisma
└── test/

admin/
├── src/
│   ├── main.tsx
│   ├── App.tsx
│   ├── core/            # API client, routes, providers, theme
│   ├── features/        # Feature modules (auth, users, products...)
│   ├── layouts/         # MainLayout, AuthLayout
│   └── shared/          # DataTable, FormModal, ErrorBoundary

mobile/
├── lib/
│   ├── main.dart
│   ├── app.dart
│   ├── core/            # constants, errors, network, routing, theme
│   ├── features/        # Feature modules (data/domain/presentation)
│   └── dependency_injection/
└── test/
```

**Structure Decision**: Full-stack with three independent apps sharing a common API contract. Backend exposes REST API consumed by both admin (React) and mobile (Flutter).

## Complexity Tracking

> **Fill ONLY if Constitution Check has violations that must be justified**

| Violation | Why Needed | Simpler Alternative Rejected Because |
|-----------|------------|-------------------------------------|
| [e.g., 4th project] | [current need] | [why 3 projects insufficient] |
| [e.g., Repository pattern] | [specific problem] | [why direct DB access insufficient] |
