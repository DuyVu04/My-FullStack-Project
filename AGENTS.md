# Workspace Rules & AI Agent Operating Guide

Welcome to the **Full-Stack AI Project**. This repository is configured to work with Google Antigravity and its extended ecosystem (Skills, Rules, MCP, Subagents, and Lifecycle Workflows).

---

## 1. Core Operating Principles

1. **Plan Before Execution**:
   - For any multi-step architectural change, database migration, or large feature implementation, use Planning Mode (`/plan` or `/boost`) to establish a clear roadmap and outline visual artifacts before writing code.
2. **Progressive Disclosure**:
   - Keep the main context window lean. Rely on modular instructions stored in [`.agents/skills/`](file:///E:/My-FullStack-Project/.agents/skills/) rather than inlining massive prompt blocks. Read reference files only when triggered.
3. **Test-Driven & Defensive**:
   - Implement features following Test-Driven Development (TDD). Write unit and integration tests before finishing feature modules.
   - Maintain documentation integrity: never delete existing architectural comments or docstrings unless explicitly refactoring them.

---

## 2. Workflows & Slash Commands

Use the following slash commands to trigger specialized Agent workflows:

| Slash Command | Workflow Purpose | Associated Skill / Tool |
| :--- | :--- | :--- |
| `/plan` | Generate step-by-step implementation plan with artifact checklist | Built-in Planning Engine |
| `/grill-me` | Conduct a deep, relentless design interview to stress-test ideas | [`.agents/skills/grill-me/`](file:///E:/My-FullStack-Project/.agents/skills/grill-me/SKILL.md) |
| `/tdd` | Test-driven development workflow (Red-Green-Refactor) | [`.agents/skills/tdd/`](file:///E:/My-FullStack-Project/.agents/skills/tdd/SKILL.md) |
| `/diagnose` | Systematic debugging loop for hard crashes, regressions, or slowness | [`.agents/skills/diagnosing-bugs/`](file:///E:/My-FullStack-Project/.agents/skills/diagnosing-bugs/SKILL.md) |
| `/boost` | Deep thinking and multi-perspective verification for complex tasks | Built-in Boost Mode |
| `/browser` | Launch automated browser for live UI & E2E inspection | Built-in Browser Tool |

---

## 3. Skill Activation Matrix

Antigravity auto-discovers skills registered in [`.agents/skills.json`](file:///E:/My-FullStack-Project/.agents/skills.json). Whenever a prompt touches a specific domain, the Agent MUST adopt the conventions defined in that skill:

### A. General Engineering & Workflow Skills
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

## 4. Project Workspace Boundaries

- **Root Directory**: Reserved exclusively for configuration (`AGENTS.md`, `.gitignore`, `skills-lock.json`, and `.agents/`). Do not add arbitrary source code files here.
- **`backend/`** (to be created): Dedicated exclusively to the Java Spring Boot & Spring AI service.
- **`frontend/`** (to be created): Dedicated exclusively to the web user interface (React, Vite, Tailwind, Shadcn).
- **Subagents & Delegation**: When running long builds, complex research, or test suites, utilize subagents (`invoke_subagent`) to preserve the main interactive conversation flow.
