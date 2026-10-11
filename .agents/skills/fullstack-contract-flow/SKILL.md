---
name: fullstack-contract-flow
description: >-
  Orchestrates end-to-end Full-Stack feature development using a Contract-Driven Pipeline with specialized subagents
  (researcher, backend-specialist, frontend-specialist, qa-tester).
  Use when the user requests a new feature, API integration, or full-stack task across backend and frontend.
---

# Full-Stack Contract-Driven Workflow

This skill standardizes the multi-agent pipeline to build features across Spring Boot/Spring AI backend and React frontend without schema drift or field mismatches.

```
[1. Research] ──▶ [2. Contract Spec] ──▶ [3. TDD Test (Red)] ──▶ [4. Dual Code (Green)] ──▶ [5. QA & Review]
   researcher        contracts/*.yaml           qa-tester           backend & frontend          qa-tester
```

---

## 5-Phase Pipeline Execution

### Phase 1: Research & Best-Practice Discovery
* **Role**: `research` subagent (or primary agent).
* **Task**:
  - Investigate industry standards, RFC guidelines, or Spring AI documentation for the target feature.
  - Determine required data structures, authentication constraints, and edge-case errors.
  - Provide a concise schema brief back to the Lead Agent.

### Phase 2: Contract Specification (Single Source of Truth)
* **Role**: Primary Lead Agent.
* **Task**:
  - Create or update the contract file at `contracts/<feature>.contract.yaml` using the [TEMPLATE.contract.yaml](../../../contracts/TEMPLATE.contract.yaml).
  - Define exact endpoints, HTTP verbs, payload types, headers, and error codes.
  - **Rule**: All field names MUST be `camelCase`. Timestamps MUST be ISO-8601. Error models MUST follow RFC-7807.
  - Present the contract summary to the user for quick validation before invoking implementation agents.

### Phase 3: Contract Test Generation (TDD Red Phase)
* **Role**: Invoke `qa-tester` subagent via `invoke_subagent`.
* **Task**:
  - Read `contracts/<feature>.contract.yaml`.
  - Write MockMvc / integration tests in `backend/src/test/...` checking positive (200/201) and negative (400 ProblemDetails) scenarios.
  - Write MSW / Vitest contract test mocks in `frontend/src/...`.
  - Verify that tests fail as expected (Red phase) because implementation is pending.

### Phase 4: Parallel Dual Implementation (Green Phase)
* **Role**: Invoke `backend-specialist` and `frontend-specialist` subagents concurrently via `invoke_subagent`.
* **Subagent 1: `backend-specialist`**:
  - Read `contracts/<feature>.contract.yaml`.
  - Implement Java Records for DTOs matching the exact contract field names.
  - Implement Spring Boot Controller, Service, and Repository / Spring AI components.
* **Subagent 2: `frontend-specialist`**:
  - Read `contracts/<feature>.contract.yaml`.
  - Implement TypeScript types / interfaces matching the exact contract field names.
  - Implement TanStack Query hooks, Zustand UI state slices, and Shadcn components.

### Phase 5: Verification, Green Phase & Visual Artifact
* **Role**: `qa-tester` subagent & Primary Lead Agent.
* **Task**:
  - Run the test suite: verify all tests transition from Red to Green.
  - If any test fails, run the diagnostic loop using `.agents/skills/diagnosing-bugs/`.
  - Produce a Visual Artifact summarizing:
    1. Contract endpoint & schema.
    2. Backend classes created.
    3. Frontend components & hooks created.
    4. Test execution results (All Passed).
