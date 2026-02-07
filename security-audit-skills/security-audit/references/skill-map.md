# Security Audit Skill Selection Map

## Detection Signals → Auditor Mapping

This reference helps the orchestrator decide which auditors to run based on what's detected in the codebase.

## Frontend Sentinel

**Trigger signals:**
- Files: `*.jsx`, `*.tsx`, `*.vue`, `*.svelte`, `*.html` with `<script>` tags, `*.ejs`, `*.hbs`, `*.pug`
- Directories: `src/components/`, `src/pages/`, `src/views/`, `public/`, `static/`
- Config: `next.config.*`, `nuxt.config.*`, `vite.config.*`, `webpack.config.*`, `angular.json`
- package.json deps: `react`, `vue`, `angular`, `svelte`, `next`, `nuxt`, `gatsby`

**Skip when:**
- Pure API backend with no HTML rendering
- CLI tools
- Data pipelines / batch processing

## Backend Fortifier

**Trigger signals:**
- Files: Route/controller definitions, middleware files, API endpoint handlers
- Patterns: `@app.route`, `router.get/post`, `@GetMapping`, `@api_view`, `Route::`, `func handleX`
- Frameworks: Express, Fastify, Django, Flask, FastAPI, Laravel, Rails, Spring, Gin, Actix, ASP.NET
- API definitions: OpenAPI/Swagger files, GraphQL schemas

**Skip when:**
- Static sites with no server-side logic
- Pure frontend applications (SPA with no custom backend)

## Data Warden

**Trigger signals:**
- ORM: Prisma, Sequelize, TypeORM, Mongoose, SQLAlchemy, ActiveRecord, Eloquent, GORM, Diesel
- Raw queries: SQL strings in code, MongoDB operations, Redis commands
- Migrations: `migrations/` directory, Alembic, Flyway, Knex migrations
- Config: Database connection strings, `DATABASE_URL`, `MONGO_URI`
- Files: `*.sql`, `schema.prisma`, `models.py`, `entities/`

**Skip when:**
- Application uses no persistent storage
- Purely static content

## Identity Manager

**Trigger signals:**
- Auth libraries: Passport.js, NextAuth, Auth0 SDK, Firebase Auth, Devise, Django Auth, Spring Security, JWT libraries
- Patterns: `jwt.sign`, `jwt.verify`, `bcrypt`, `OAuth`, `session`, `login`, `authenticate`, `authorize`
- Config: OAuth client IDs, OIDC configurations, SAML metadata
- Middleware: Auth middleware, guard decorators, policy classes

**Skip when:**
- Application has no user authentication (public read-only API, static site)
- Authentication is entirely handled by an external gateway with no application-level auth code

## AI/LLM Guardian

**Trigger signals:**
- SDKs: `openai`, `anthropic`, `@google/generative-ai`, `langchain`, `llamaindex`, `transformers`
- Patterns: `ChatCompletion`, `messages.create`, `embed`, `vector`, `prompt`, `completion`
- Infrastructure: Vector databases (Pinecone, Weaviate, Chroma, Qdrant, pgvector, FAISS)
- Agent frameworks: LangGraph, CrewAI, AutoGen, Semantic Kernel
- Files: Prompt templates, system message files, tool/function definitions

**Skip when:**
- No AI/LLM integration whatsoever
- This is a clear skip — if there are no LLM dependencies, don't run this

## Infra Sentry

**Trigger signals:**
- Containers: `Dockerfile`, `docker-compose.yml`, `.dockerignore`
- Orchestration: K8s manifests (`kind: Deployment`, `kind: Service`), Helm charts (`Chart.yaml`)
- IaC: `*.tf`, `*.tfvars`, `Pulumi.*`, CloudFormation templates
- CI/CD: `.github/workflows/`, `.gitlab-ci.yml`, `Jenkinsfile`, `bitbucket-pipelines.yml`, `.circleci/`
- Cloud: AWS CDK, serverless.yml, netlify.toml, vercel.json
- Config: nginx.conf, apache configs, Caddyfile

**Skip when:**
- No infrastructure configuration in the repository
- Note: even if infra files are absent, if the user mentions they deploy to containers/K8s/cloud, suggest they provide those configs

## Supply Chain Auditor

**Trigger signals:**
- Always run if any dependency manifest exists
- `package.json`, `package-lock.json`, `yarn.lock`, `pnpm-lock.yaml`
- `requirements.txt`, `Pipfile`, `pyproject.toml`, `poetry.lock`
- `go.mod`, `go.sum`
- `Cargo.toml`, `Cargo.lock`
- `Gemfile`, `Gemfile.lock`
- `composer.json`, `composer.lock`
- `pom.xml`, `build.gradle`
- `*.csproj`, `packages.config`

**Skip when:**
- Never skip — every real application has dependencies

## CISO Synthesizer

**Trigger signals:**
- Always run as the final step after all other auditors complete

**Skip when:**
- Never skip — always produce the synthesis

## Application Type Quick Reference

| App Type | FS | BF | DW | IM | AG | IS | SC | CS |
|----------|----|----|----|----|----|----|----|----|
| Full-Stack Web | ✅ | ✅ | ✅ | ✅ | ? | ✅ | ✅ | ✅ |
| API Backend | ❌ | ✅ | ✅ | ✅ | ? | ✅ | ✅ | ✅ |
| Static/Jamstack | ✅ | ? | ❌ | ❌ | ❌ | ? | ✅ | ✅ |
| AI/LLM App | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Microservices | ✅ | ✅ | ✅ | ✅ | ? | ✅ | ✅ | ✅ |
| Mobile Backend | ❌ | ✅ | ✅ | ✅ | ? | ✅ | ✅ | ✅ |
| CLI Tool | ❌ | ✅ | ? | ? | ? | ? | ✅ | ✅ |
| Data Pipeline | ❌ | ✅ | ✅ | ? | ? | ✅ | ✅ | ✅ |
| WordPress/CMS | ✅ | ✅ | ✅ | ✅ | ❌ | ✅ | ✅ | ✅ |

Legend: ✅ = Always run, ❌ = Skip, ? = Run if detected
