---
description: "Task list template for feature implementation"
---

# Tasks: [FEATURE NAME]

**Input**: Design documents from `/specs/[###-feature-name]/`
**Prerequisites**: plan.md (required), spec.md (required), data-model.md, contracts/

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (e.g., US1, US2)
- Include exact file paths in descriptions

## Phase 1: Setup

- [ ] T001 Create project structure per implementation plan

---

## Phase 2: Foundational (Blocks all user stories)

**⚠️ CRITICAL**: No user story work can begin until this phase is complete

- [ ] T002 Setup database schema and migrations
- [ ] T003 [P] Implement authentication framework
- [ ] T004 [P] Setup API routing and middleware
- [ ] T005 Create base models/entities all stories depend on

**Checkpoint**: Foundation ready — user story implementation can begin

---

## Phase 3: User Story 1 — [Title] (Priority: P1) 🎯 MVP

**Goal**: [What this story delivers]
**Independent Test**: [How to verify independently]

- [ ] T006 [P] [US1] Create models in backend/src/modules/[feature]/entities/
- [ ] T007 [P] [US1] Create DTOs in backend/src/modules/[feature]/dto/
- [ ] T008 [US1] Implement service in backend/src/modules/[feature]/[feature].service.ts
- [ ] T009 [US1] Implement controller in backend/src/modules/[feature]/[feature].controller.ts
- [ ] T010 [US1] Create admin page in admin/src/features/[feature]/pages/
- [ ] T011 [US1] Create admin hooks in admin/src/features/[feature]/hooks/
- [ ] T012 [US1] Create mobile feature in mobile/lib/features/[feature]/
- [ ] T013 [US1] Register routes and DI

**Checkpoint**: User Story 1 is fully functional and testable independently

---

## Phase 4: User Story 2 — [Title] (Priority: P2)

**Goal**: [What this story delivers]
**Independent Test**: [How to verify independently]

- [ ] T014 [P] [US2] Create models and DTOs
- [ ] T015 [US2] Implement backend service and controller
- [ ] T016 [US2] Implement admin page
- [ ] T017 [US2] Implement mobile feature
- [ ] T018 [US2] Integrate with User Story 1 components (if needed)

**Checkpoint**: User Stories 1 AND 2 both work independently

---

## Phase 5: User Story 3 — [Title] (Priority: P3)

**Goal**: [What this story delivers]
**Independent Test**: [How to verify independently]

- [ ] T019 [P] [US3] Create models and DTOs
- [ ] T020 [US3] Implement backend service and controller
- [ ] T021 [US3] Implement admin page
- [ ] T022 [US3] Implement mobile feature

**Checkpoint**: All user stories are independently functional

---

[Add more user story phases as needed]

---

## Phase N: Polish & Cross-Cutting Concerns

- [ ] TXXX [P] Documentation updates
- [ ] TXXX Code cleanup and refactoring
- [ ] TXXX Performance optimization
- [ ] TXXX Security hardening

---

## Dependencies & Execution Order

- **Setup (Phase 1)**: No dependencies
- **Foundational (Phase 2)**: Blocks all user stories
- **User Stories (Phase 3+)**: All depend on Foundational; can run in parallel if staffed
- **Polish (Final)**: Depends on all desired user stories complete

### Within Each User Story
- Models before services
- Services before endpoints
- Backend before frontend (admin + mobile)
- Core implementation before integration
