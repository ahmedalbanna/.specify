# Speckit Tasks Guide

This guide explains how to use and interpret the tasks template for feature implementation.

## Task Format

Each task follows: `[ID] [P?] [Story] Description`

- **ID**: Sequential identifier (T001, T002, ...)
- **[P]**: Parallel marker — tasks with this flag can run simultaneously (different files, no dependencies)
- **[Story]**: User story label (US1, US2, US3) for traceability
- **Description**: Action with exact file path

## Phase Structure

### Phase 1: Setup
Project initialization. Usually minimal — create directories, install dependencies.

### Phase 2: Foundational
Core infrastructure that ALL user stories depend on. This phase MUST complete before any user story work begins.

Examples:
- Database schema and migrations
- Authentication/authorization framework
- API routing and middleware
- Base models/entities
- Error handling and logging
- Environment configuration

### Phase 3+: User Stories
Each user story is an independent, testable slice of functionality. Stories are ordered by priority (P1 = MVP).

**Each story should be:**
- Implementable independently
- Testable independently
- Deployable independently
- Demonstrable to users independently

### Final Phase: Polish
Cross-cutting concerns that affect multiple stories (documentation, performance, security).

## Parallel Execution

Tasks marked `[P]` can run simultaneously:

```bash
# Example: Launch all models for User Story 1 together
Task: "Create User model in backend/src/modules/users/entities/user.entity.ts"
Task: "Create CreateUserDto in backend/src/modules/users/dto/create-user.dto.ts"
Task: "Create UserResponseDto in backend/src/modules/users/dto/user-response.dto.ts"
```

## Implementation Strategy

### MVP First (User Story 1 Only)
1. Complete Phase 1: Setup
2. Complete Phase 2: Foundational (CRITICAL — blocks all stories)
3. Complete Phase 3: User Story 1
4. **STOP and VALIDATE**: Test User Story 1 independently
5. Deploy/demo if ready

### Incremental Delivery
1. Setup + Foundational → Foundation ready
2. Add User Story 1 → Test independently → Deploy/Demo (MVP!)
3. Add User Story 2 → Test independently → Deploy/Demo
4. Add User Story 3 → Test independently → Deploy/Demo
5. Each story adds value without breaking previous stories

### Parallel Team Strategy
With multiple developers:
1. Team completes Setup + Foundational together
2. Once Foundational is done:
   - Developer A: User Story 1
   - Developer B: User Story 2
   - Developer C: User Story 3
3. Stories complete and integrate independently

## Best Practices

- Commit after each task or logical group
- Verify tests fail before implementing (if tests included)
- Stop at any checkpoint to validate story independently
- Avoid: vague tasks, same file conflicts, cross-story dependencies that break independence
- Each user story should deliver standalone value
