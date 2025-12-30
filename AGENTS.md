# Claude Code Plugins Marketplace

A curated collection of 57 plugins, 84 agents, and 120+ skills for Claude Code.

## Structure

```
claude-code-plugins/
├── shared/agents/           # 84 unique agents (symlinked into plugins)
├── plugins/                 # 57 domain-specific plugins
│   ├── */agents/            # Symlinks to shared/agents
│   ├── */commands/          # Slash commands
│   └── */skills/            # Modular knowledge packages
├── workflows/               # Composable workflow templates
└── .claude-plugin/marketplace.json
```

## Key Capabilities

### Structured Reasoning (FPF)
Hypothesis-driven decision making with auditable evidence trails:
- `/q0-init` — Initialize reasoning knowledge base
- `/q1-hypothesize <problem>` — Generate competing hypotheses
- `/q2-verify` — Logical verification
- `/q3-validate` — Empirical evidence gathering
- `/q5-decide` — Create Design Rationale Record

### Development Workflows
- **Subagent-Driven Development** — Fresh subagent per task with code review checkpoints
- **Git Worktrees** — Isolated workspaces for parallel feature development
- **Root Cause Tracing** — Trace errors to source, not symptoms

### Cloud & Infrastructure
- **Kubernetes** — Cluster design, Helm, GitOps
- **Terraform** — IaC patterns and modules
- **Multi-Cloud** — AWS/Azure/GCP infrastructure patterns

### AI/ML Development
- **MCP Builder** — Create high-quality MCP servers
- **Prompt Engineering** — Optimization techniques
- **RAG Systems** — Vector databases, embeddings

---

## Model Tiers

| Tier | Model | Use Case |
|------|-------|----------|
| **Tier 1** | `opus` | Critical architecture, security, code review, production coding |
| **Tier 2** | `inherit` | Complex tasks - uses session default model |
| **Tier 3** | `sonnet` | Support tasks with intelligence |
| **Tier 4** | `haiku` | Fast operational tasks |

---

## Available Agents

### Orchestration & Meta

| Agent | Model | Description |
|-------|-------|-------------|
| `task-planner` | opus | Decomposes complex tasks, delegates to agents, coordinates execution |
| `output-critic` | opus | Reviews agent outputs for correctness, completeness, quality |
| `context-researcher` | sonnet | Gathers context before implementation, builds understanding |
| `codebase-navigator` | sonnet | Maps project structure, traces data flows, locates code |
| `api-designer` | inherit | Designs clean REST/GraphQL/gRPC APIs with best practices |
| `test-strategist` | inherit | Plans comprehensive testing strategies, identifies edge cases |

### Architecture & Design

| Agent | Model | Description |
|-------|-------|-------------|
| `architect-review` | opus | Software architecture patterns, clean architecture, microservices |
| `backend-architect` | inherit | Scalable API design, microservices, distributed systems |
| `cloud-architect` | opus | AWS/Azure/GCP multi-cloud infrastructure, IaC patterns |
| `database-architect` | opus | Data layer design, technology selection, schema design |
| `graphql-architect` | inherit | GraphQL schema design, federation, performance |
| `hybrid-cloud-architect` | inherit | Multi-cloud networking, hybrid deployments |
| `kubernetes-architect` | inherit | K8s cluster design, helm charts, GitOps |
| `monorepo-architect` | opus | Monorepo structure, tooling, dependency management |
| `service-mesh-expert` | inherit | Istio, Linkerd, service mesh patterns |

### Languages

#### Systems Programming
| Agent | Model | Description |
|-------|-------|-------------|
| `c-pro` | opus | C with memory management, system calls, embedded |
| `cpp-pro` | opus | Modern C++ (11/14/17/20/23), RAII, templates |
| `rust-pro` | opus | Safe Rust, async patterns, systems programming |
| `golang-pro` | opus | Go concurrency, microservices, cloud-native |

#### Web & Backend
| Agent | Model | Description |
|-------|-------|-------------|
| `python-pro` | opus | Modern Python 3.12+, async, type hints |
| `django-pro` | opus | Django 5.x, DRF, Celery, async views |
| `fastapi-pro` | opus | FastAPI, async patterns, Pydantic |

#### JVM & Functional
| Agent | Model | Description |
|-------|-------|-------------|
| `java-pro` | inherit | Modern Java, Spring Boot, enterprise |
| `scala-pro` | inherit | Functional Scala, Akka, Cats |
| `csharp-pro` | inherit | C# with records, pattern matching, async |
| `elixir-pro` | inherit | Elixir, OTP, Phoenix LiveView |
| `haskell-pro` | inherit | Pure functional Haskell patterns |

#### Specialized
| Agent | Model | Description |
|-------|-------|-------------|
| `julia-pro` | inherit | Scientific computing, numerical code |
| `bash-pro` | sonnet | Defensive Bash scripting, automation |
| `posix-shell-pro` | sonnet | POSIX-compliant shell scripts |

### AI & Machine Learning

| Agent | Model | Description |
|-------|-------|-------------|
| `ai-engineer` | inherit | LLM applications, RAG systems, agents |
| `prompt-engineer` | opus | Prompt engineering, optimization techniques |
| `ml-engineer` | inherit | Model training, deployment, pipelines |
| `mlops-engineer` | sonnet | MLOps workflows, experiment tracking |
| `data-scientist` | inherit | Analytics, statistical modeling |
| `vector-database-engineer` | inherit | Vector DBs, embeddings, similarity search |
| `reasoning-orchestrator` | opus | FPF structured reasoning, decision making |
| `context-manager` | inherit | Context engineering, knowledge management |
| `mcp-architect` | opus | MCP server development, tool design |

### Infrastructure & DevOps

| Agent | Model | Description |
|-------|-------|-------------|
| `terraform-specialist` | inherit | Terraform modules, IaC patterns |
| `deployment-engineer` | haiku | CI/CD pipelines, GitOps workflows |
| `devops-troubleshooter` | sonnet | Incident response, debugging |
| `incident-responder` | sonnet | Production incidents, triage |
| `observability-engineer` | inherit | Metrics, logs, traces, dashboards |
| `network-engineer` | inherit | Networking, load balancing, DNS |

### Security

| Agent | Model | Description |
|-------|-------|-------------|
| `security-auditor` | opus | Security analysis, vulnerability detection |
| `threat-modeling-expert` | opus | STRIDE analysis, attack trees |
| `backend-security-coder` | sonnet | Secure coding, input validation |
| `frontend-security-coder` | inherit | XSS prevention, CSP, CORS |
| `mobile-security-coder` | inherit | Mobile app security patterns |

### Data & Databases

| Agent | Model | Description |
|-------|-------|-------------|
| `data-engineer` | opus | ETL pipelines, data warehouses |
| `database-optimizer` | inherit | Query optimization, performance tuning |
| `database-admin` | sonnet | Database operations, automation |
| `sql-pro` | opus | Advanced SQL, optimization |

### Frontend & Mobile

| Agent | Model | Description |
|-------|-------|-------------|
| `frontend-developer` | inherit | React, Vue, modern frontend |
| `mobile-developer` | inherit | React Native, cross-platform |
| `ios-developer` | inherit | Swift, iOS native development |
| `flutter-expert` | inherit | Flutter, Dart, cross-platform |
| `ui-ux-designer` | inherit | Design systems, user experience |

### Quality & Testing

| Agent | Model | Description |
|-------|-------|-------------|
| `code-reviewer` | opus | Code review, quality analysis |
| `test-automator` | inherit | Test automation, coverage |
| `tdd-orchestrator` | opus | Test-driven development workflows |
| `debugger` | sonnet | Debugging, troubleshooting |
| `error-detective` | sonnet | Error analysis, log correlation |
| `performance-engineer` | inherit | Performance optimization, profiling |

### Documentation

| Agent | Model | Description |
|-------|-------|-------------|
| `docs-architect` | sonnet | Technical documentation architecture |
| `api-documenter` | sonnet | OpenAPI specs, API docs |
| `tutorial-engineer` | sonnet | Tutorial creation, examples |
| `reference-builder` | sonnet | Reference documentation |
| `mermaid-expert` | sonnet | Diagrams, flowcharts |

### Finance

| Agent | Model | Description |
|-------|-------|-------------|
| `quant-analyst` | opus | Quantitative finance, trading strategies |
| `risk-manager` | opus | Portfolio risk, VaR, position sizing |
| `ml-quant-developer` | opus | ML for quant finance, factor investing, deep learning |

### Blockchain

| Agent | Model | Description |
|-------|-------|-------------|
| `blockchain-developer` | opus | Smart contracts, DeFi, Web3 |

### Business

| Agent | Model | Description |
|-------|-------|-------------|
| `business-analyst` | sonnet | Business analysis, KPIs, dashboards |
| `content-marketer` | haiku | Content strategy, marketing |
| `customer-support` | haiku | Support automation, ticketing |
| `sales-automator` | haiku | Sales workflows, CRM |
| `search-specialist` | haiku | Search optimization, research |

### Modernization

| Agent | Model | Description |
|-------|-------|-------------|
| `legacy-modernizer` | opus | Legacy code modernization, systematic refactoring |
| `event-sourcing-architect` | opus | Event sourcing, CQRS patterns |
| `temporal-python-pro` | opus | Temporal workflows, orchestration |

---

## Usage

Agents are automatically available when using plugins. To invoke directly:

```
@agent-name your request here
```

Example:
```
@rust-pro Review this unsafe block for memory safety issues
@quant-analyst Build a momentum strategy with proper backtesting
@cloud-architect Design a serverless architecture for this API
```

---

## Sources

This marketplace combines:
- [wshobson/agents](https://github.com/wshobson/agents) — Base structure
- [ComposioHQ/awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills) — Skills
- [m0n0x41d/quint-code](https://github.com/m0n0x41d/quint-code) — FPF reasoning
- [obra/superpowers](https://github.com/obra/superpowers) — Development workflows
