---
name: autosmirk
description: Use when the user invokes @autosmirk or asks for AutoSmirk conventions, especially Firecrawl-based analysis of API documentation URLs, VitePress front matter generation, and a logic-first confirmation step before complex coding.
---

# AutoSmirk

## Scope
- **API Analysis**: Prioritize Firecrawl analysis for API documentation URLs.
- **Front Matter**: Generate VitePress YAML front matter for Markdown files with preview confirmation.
- **Logic-First Gate**: Require logic-first confirmation before complex coding.
- **Default Conventions**: Apply default stack/style preferences unless the user overrides them.

## Workflow

### 0) Front Matter Generation (VitePress)
**Trigger**: `@autosmirk fm <file-or-directory-path>`

**Process**:
1. Read the target Markdown file(s)
2. Analyze content and extract:
   - `title`: First `#` heading, fallback to `##`, or "未命名文档"
   - `description`: First meaningful paragraph (max 200 chars)
   - `date`: Current date in ISO format `YYYY-MM-DD`
   - `tags`: Smart inference based on path keywords (90+ mappings)
   - `author`: Default "舒一笑不秃头"
   - `layout`: Fixed value "doc"
3. **ALWAYS show preview** before writing:
   ```yaml
   ---
   layout: doc
   title: [提取的标题]
   description: >-
     [提取的描述...]
   date: 'YYYY-MM-DD'
   tags:
     - [标签1]
     - [标签2]
   author: 舒一笑不秃头
   ---
   ```
4. Ask for confirmation: "是否写入文件？(确认/取消/修改)"
5. After user confirms, write to file; if "修改", adjust based on user input
6. Skip files that already have front matter (detected by existing `---`)

**Tag Inference Rules** (90+ keywords):
| Path Keyword | Auto Tags |
|-------------|-----------|
| `java`, `spring`, `mybatis` | Java, Spring Boot, MyBatis |
| `python`, `django`, `fastapi` | Python, Django, FastAPI |
| `rust`, `cargo` | Rust |
| `algorithm`, `dynamic-programming` | 算法, 动态规划 |
| `architecture`, `microservice`, `distributed` | 系统架构, 微服务, 分布式 |
| `security`, `auth`, `sso`, `oauth` | 安全, 认证鉴权, 单点登录, OAuth |
| `performance`, `jvm`, `monitoring` | 性能优化, JVM调优, 监控 |
| `database`, `redis`, `mysql`, `mongodb` | 数据库, Redis, MySQL, MongoDB |
| `message-queue`, `kafka`, `rabbitmq` | 消息队列, Kafka, RabbitMQ |
| `claude`, `ai`, `llm`, `prompt` | Claude, AI, 大模型, 提示工程 |
| `idea`, `plugin`, `vscode` | IDEA, 插件开发, VSCode |
| Default fallback | 技术 |

**Usage Examples**:
- Single file: `@autosmirk fm docs/article.md`
- Directory: `@autosmirk fm docs/articles`
- Current file: `@autosmirk fm`

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

### Front Matter Generation
**User**: "@autosmirk fm docs/spring-security-auth.md"

**Assistant**:
1. Read `docs/spring-security-auth.md`
2. Extract title: "Spring Security 实现 JWT 认证与授权"
3. Extract description from first paragraph: "本文详细介绍如何使用 Spring Security 6 实现 JWT 认证..."
4. Infer tags from path `spring` + `security` + `auth`: Spring Boot, Spring Security, 认证鉴权, JWT
5. Show preview:
   ```yaml
   ---
   layout: doc
   title: Spring Security 实现 JWT 认证与授权
   description: >-
     本文详细介绍如何使用 Spring Security 6 实现 JWT 认证，包括用户登录、令牌生成、权限验证等完整流程。
   date: '2026-01-23'
   tags:
     - Spring Boot
     - Spring Security
     - 认证鉴权
     - JWT
   author: 舒一笑不秃头
   ---
   ```
6. Ask: "是否写入文件？(确认/取消/修改)"

**User**: "确认"

**Assistant**: Write front matter to file.

---

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
