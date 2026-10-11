# Workspace Rules & AI Agent Operating Guide

Welcome to the **Full-Stack AI Project**. This repository is configured to operate with Google Antigravity and its extended ecosystem (Skills, Rules, MCP, Subagents, and Contract-Driven Lifecycle Workflows).

---

## 1. Core Operating Principles

1. **Contract-First & Zero-Drift**:
   - Before any code is written across frontend and backend, an API Contract MUST be established in [`contracts/`](file:///E:/My-FullStack-Project/contracts/).
   - Every field name in JSON payloads MUST be `camelCase`.
   - Every timestamp MUST adhere to ISO-8601 (`YYYY-MM-DDTHH:mm:ssZ`).
   - Every error response MUST follow RFC-7807 Problem Details.
2. **Plan Before Execution**:
   - For multi-step tasks, use Planning Mode (`/plan` or `/boost`) or invoke the workflow skill [**`fullstack-contract-flow`**](file:///E:/My-FullStack-Project/.agents/skills/fullstack-contract-flow/SKILL.md) before generating code.
3. **Progressive Disclosure**:
   - Keep the main context window lean. Rely on modular instructions stored in [`.agents/skills/`](file:///E:/My-FullStack-Project/.agents/skills/) rather than inlining massive prompt blocks. Read reference files only when triggered.
4. **Test-Driven Development (TDD)**:
   - Implement features following TDD: Red (failing test) -> Green (passing implementation) -> Refactor.
   - Maintain documentation integrity: never delete existing architectural comments or docstrings.

---

## 2. Multi-Agent Ecosystem (Subagents)

When implementing tasks, the Primary Agent coordinates 4 specialized subagents:

| Subagent Name | Role & Scope | Core Responsibilities |
| :--- | :--- | :--- |
| **`research`** (Built-in) | Research & Standards | Investigates RFC standards, Spring AI docs, third-party libraries, and industry best practices. |
| **`backend-specialist`** | Java 21, Spring Boot 3, Spring AI | Implements Java Records (DTOs), Controllers, Services, Repositories, and LLM integrations strictly matching contracts. Boundary: `backend/`. |
| **`frontend-specialist`** | React, TypeScript, Tailwind, Shadcn | Implements TypeScript interfaces, TanStack Query hooks, Zustand store slices, and UI components strictly matching contracts. Boundary: `frontend/`. |
| **`qa-tester`** | Quality Assurance & TDD | Writes contract conformance tests (JUnit/MockMvc for Backend, Vitest/MSW for Frontend), validates Red-Green-Refactor, and diagnoses regressions. |

---

## 3. Workflows & Slash Commands

| Slash Command | Workflow Purpose | Associated Skill / Tool |
| :--- | :--- | :--- |
| `/flow` | Run the complete 5-Phase Contract-Driven Delivery Pipeline | [`.agents/skills/fullstack-contract-flow/`](file:///E:/My-FullStack-Project/.agents/skills/fullstack-contract-flow/SKILL.md) |
| `/plan` | Generate step-by-step implementation plan with artifact checklist | Built-in Planning Engine |
| `/grill-me` | Conduct a deep, relentless design interview to stress-test ideas | [`.agents/skills/grill-me/`](file:///E:/My-FullStack-Project/.agents/skills/grill-me/SKILL.md) |
| `/tdd` | Test-driven development workflow (Red-Green-Refactor) | [`.agents/skills/tdd/`](file:///E:/My-FullStack-Project/.agents/skills/tdd/SKILL.md) |
| `/diagnose` | Systematic debugging loop for hard crashes, regressions, or slowness | [`.agents/skills/diagnosing-bugs/`](file:///E:/My-FullStack-Project/.agents/skills/diagnosing-bugs/SKILL.md) |
| `/boost` | Deep thinking and multi-perspective verification for complex tasks | Built-in Boost Mode |
| `/browser` | Launch automated browser for live UI & E2E inspection | Built-in Browser Tool |

---

## 4. Contract-Driven Delivery Pipeline

Every feature follows the 5-phase execution flow defined in [**`fullstack-contract-flow`**](file:///E:/My-FullStack-Project/.agents/skills/fullstack-contract-flow/SKILL.md):

```
[Phase 1: Research] ──▶ [Phase 2: Contract Spec] ──▶ [Phase 3: TDD Tests] ──▶ [Phase 4: Dual Code] ──▶ [Phase 5: Verification]
    researcher              contracts/*.yaml             qa-tester              backend & frontend           qa-tester
```

1. **Phase 1 (Research)**: Researcher surveys APIs, libraries, and edge-cases.
2. **Phase 2 (Contract Spec)**: Lead Agent drafts `contracts/<feature>.contract.yaml` using [`TEMPLATE.contract.yaml`](file:///E:/My-FullStack-Project/contracts/TEMPLATE.contract.yaml).
3. **Phase 3 (TDD Red)**: `qa-tester` creates integration tests verifying contract status codes and schemas. Tests must fail (Red).
4. **Phase 4 (Dual Code)**: `backend-specialist` and `frontend-specialist` execute concurrently, each reading the exact same contract.
5. **Phase 5 (Green & Review)**: `qa-tester` re-runs test suite until all pass (Green). Lead Agent presents visual artifact.

---

## 5. Skill Activation Matrix

Antigravity auto-discovers skills registered in [`.agents/skills.json`](file:///E:/My-FullStack-Project/.agents/skills.json). Whenever a prompt touches a specific domain, the Agent MUST adopt the conventions defined in that skill:

### A. General Engineering & Workflow Skills
- [**`fullstack-contract-flow`**](file:///E:/My-FullStack-Project/.agents/skills/fullstack-contract-flow/SKILL.md): 5-phase multi-agent contract delivery pipeline.
- [**`setup-matt-pocock-skills`**](file:///E:/My-FullStack-Project/.agents/skills/setup-matt-pocock-skills/SKILL.md): Standardizing issue tracking, domain docs, and triage.
- [**`grill-me`**](file:///E:/My-FullStack-Project/.agents/skills/grill-me/SKILL.md): Architecture review and design stress-testing.
- [**`tdd`**](file:///E:/My-FullStack-Project/.agents/skills/tdd/SKILL.md): Unit and integration test enforcement.
- [**`diagnosing-bugs`**](file:///E:/My-FullStack-Project/.agents/skills/diagnosing-bugs/SKILL.md): Root-cause analysis and performance triage.
- [**`find-skills`**](file:///E:/My-FullStack-Project/.agents/skills/find-skills/SKILL.md): Discovering additional community skills when needed.

### B. Frontend Engineering Skills (for future `frontend/`)
- [**`vercel-react-best-practices`**](file:///E:/My-FullStack-Project/.agents/skills/vercel-react-best-practices/SKILL.md): Performance optimization, server/client components, render trees.
- [**`tanstack-query-best-practices`**](file:///E:/My-FullStack-Project/.agents/skills/tanstack-query-best-practices/SKILL.md): Server state management, caching strategies, query keys, and optimistic updates.
- [**`zustand-patterns`**](file:///E:/My-FullStack-Project/.agents/skills/zustand-patterns/SKILL.md): Clean global client state slices and store architecture.
- [**`shadcn`**](file:///E:/My-FullStack-Project/.agents/skills/shadcn/SKILL.md): Composition, theming, and accessibility with shadcn/ui.
- [**`tailwind-css-patterns`**](file:///E:/My-FullStack-Project/.agents/skills/tailwind-css-patterns/SKILL.md): Design token architecture, responsive utilities, and clean styling.

### C. Backend Engineering Skills (for future `backend/`)
- [**`spring-ai`**](file:///E:/My-FullStack-Project/.agents/skills/spring-ai/SKILL.md): LLM integrations, ChatClient, Streaming, PromptTemplate, RAG, and Vector Stores.
- [**`springboot-patterns`**](file:///E:/My-FullStack-Project/.agents/skills/springboot-patterns/SKILL.md): Layered architecture (Controller, Service, Repository, DTO), caching, async, and logging.
- [**`java-spring-boot`**](file:///E:/My-FullStack-Project/.agents/skills/java-spring-boot/SKILL.md): Production-grade REST APIs, Actuator, Security, and JPA entities.
- [**`java-springboot`**](file:///E:/My-FullStack-Project/.agents/skills/java-springboot/SKILL.md): Spring Boot idioms and GitHub Copilot best practices.

---

## 6. Project Workspace Boundaries

- **Root Directory**: Reserved exclusively for configuration (`AGENTS.md`, `.gitignore`, `skills-lock.json`, `contracts/`, and `.agents/`). Do not add arbitrary source code files here.
- **`backend/`** (to be created): Dedicated exclusively to the Java Spring Boot & Spring AI service.
- **`frontend/`** (to be created): Dedicated exclusively to the web user interface (React, Vite, Tailwind, Shadcn).
- **Subagents & Delegation**: Long-running research, test suites, or dual implementations MUST be delegated to subagents (`invoke_subagent`).
