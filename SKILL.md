---
name: autosmirk
description: Use when the user invokes @autosmirk or asks for AutoSmirk conventions, especially Firecrawl-based analysis of API documentation URLs and a logic-first confirmation step before complex coding.
---

# AutoSmirk

## Scope
- Prioritize Firecrawl analysis for API documentation URLs.
- Require logic-first confirmation before complex coding.
- Apply default stack/style preferences unless the user overrides them.

## Workflow

### 1) Collect Inputs
- Require the API docs URL when analysis is requested.
- Ask for the goal (what to build) and target stack if missing.
- If Firecrawl is unavailable, ask the user to paste the relevant docs sections.

### 2) Firecrawl Analysis
- Use Firecrawl to crawl the provided API documentation URL.
- Extract and summarize: base URL, auth, endpoints, parameters, request/response examples, errors, pagination, rate limits, webhooks, data models.
- Produce a concise brief and a structured endpoint list.

### 3) Logic-First Gate for Complex Work
- Treat as complex when any apply: multi-file change, new module/feature, multi-step integration, API + UI combined, or >60 lines of new code.
- Before coding, provide a high-level Logic Outline (no chain-of-thought), list assumptions, and ask for explicit confirmation.
- Wait for confirmation; only code after user agrees or adjusts the plan.

### 4) Default Coding Conventions
- Use React + TypeScript for frontend tasks when not specified.
- Avoid `any` in TypeScript; use explicit types.
- Add concise Chinese comments only for non-trivial logic blocks.
- Provide complete, runnable components or files.
- When creating multiple files, show a minimal file tree and label code blocks with paths.

## Output Templates

### API Analysis
- **API Brief**: purpose, base URL, auth
- **Endpoints**: method, path, params, description
- **Requests/Responses**: examples or shapes
- **Errors**: codes and meanings
- **Pagination/Rate limits/Webhooks**: as applicable
- **Open Questions**: missing or ambiguous items

### Logic First (Complex Tasks)
- **Logic Outline**: ordered steps
- **Assumptions**: inputs/constraints
- **Proceed?**: ask for confirmation

### Implementation (After Confirmation)
- Provide code only after confirmation for complex tasks.
- Keep output focused and runnable.

## Examples

### Firecrawl API Analysis
User: "Use @autosmirk to analyze https://example.com/api-docs and summarize endpoints."
Assistant:
- Run Firecrawl on the URL, extract endpoints, auth, errors, and examples.
- Return API Analysis sections and ask Open Questions.

### Logic-First Gate
User: "Build a full React + TS client for this API with auth, pagination, and caching."
Assistant:
- Provide Logic Outline and Assumptions.
- Ask for confirmation before writing code.
