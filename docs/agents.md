# Agent Reference

Complete reference for all **99 specialized AI agents** organized by category with model assignments.

## Agent Categories

### Architecture & System Design

#### Core Architecture

| Agent | Model | Description |
|-------|-------|-------------|
| [backend-architect](../plugins/backend-development/agents/backend-architect.md) | opus | RESTful API design, microservice boundaries, database schemas |
| [graphql-architect](../plugins/backend-development/agents/graphql-architect.md) | opus | GraphQL schemas, resolvers, federation architecture |
| [architect-reviewer](../plugins/code-quality/agents/architect-review.md) | opus | Architectural consistency analysis and pattern validation |
| [cloud-architect](../plugins/infrastructure/agents/cloud-architect.md) | opus | AWS/Azure/GCP infrastructure design and cost optimization |
| [hybrid-cloud-architect](../plugins/infrastructure/agents/hybrid-cloud-architect.md) | opus | Multi-cloud strategies across cloud and on-premises environments |
| [kubernetes-architect](../plugins/infrastructure/agents/kubernetes-architect.md) | opus | Cloud-native infrastructure with Kubernetes and GitOps |
| [service-mesh-expert](../plugins/infrastructure/agents/service-mesh-expert.md) | opus | Istio/Linkerd service mesh architecture, mTLS, and traffic management |
| [event-sourcing-architect](../plugins/backend-development/agents/event-sourcing-architect.md) | opus | Event sourcing, CQRS patterns, event stores, and saga orchestration |
| [monorepo-architect](../plugins/developer-essentials/agents/monorepo-architect.md) | opus | Monorepo tooling with Nx, Turborepo, Bazel, and workspace optimization |

### Programming Languages

#### Systems & Low-Level

| Agent | Model | Description |
|-------|-------|-------------|
| [c-pro](../plugins/systems-programming/agents/c-pro.md) | sonnet | System programming with memory management and OS interfaces |
| [cpp-pro](../plugins/systems-programming/agents/cpp-pro.md) | sonnet | Modern C++ with RAII, smart pointers, STL algorithms |
| [rust-pro](../plugins/systems-programming/agents/rust-pro.md) | sonnet | Memory-safe systems programming with ownership patterns |
| [golang-pro](../plugins/systems-programming/agents/golang-pro.md) | sonnet | Concurrent programming with goroutines and channels |

#### Web & Application

| Agent | Model | Description |
|-------|-------|-------------|
| [python-pro](../plugins/python-development/agents/python-pro.md) | sonnet | Python development with advanced features and optimization |
| [temporal-python-pro](../plugins/backend-development/agents/temporal-python-pro.md) | sonnet | Temporal workflow orchestration with Python SDK, durable workflows, saga patterns |

#### API & Web Frameworks

| Agent | Model | Description |
|-------|-------|-------------|
| [django-pro](../plugins/api-development/agents/django-pro.md) | sonnet | Django development with ORM and async views |
| [fastapi-pro](../plugins/api-development/agents/fastapi-pro.md) | sonnet | FastAPI with async patterns and Pydantic |
| [sql-pro](../plugins/database/agents/sql-pro.md) | sonnet | Complex SQL queries and database optimization |

### Infrastructure & Operations

#### DevOps & Deployment

| Agent | Model | Description |
|-------|-------|-------------|
| [devops-troubleshooter](../plugins/incident-response/agents/devops-troubleshooter.md) | sonnet | Production debugging, log analysis, deployment troubleshooting |
| [deployment-engineer](../plugins/infrastructure/agents/deployment-engineer.md) | sonnet | CI/CD pipelines, containerization, cloud deployments |
| [terraform-specialist](../plugins/infrastructure/agents/terraform-specialist.md) | sonnet | Infrastructure as Code with Terraform modules and state management |

#### Database Management

| Agent | Model | Description |
|-------|-------|-------------|
| [database-optimizer](../plugins/observability-monitoring/agents/database-optimizer.md) | sonnet | Query optimization, index design, migration strategies |
| [database-admin](../plugins/database-migrations/agents/database-admin.md) | sonnet | Database operations, backup, replication, monitoring |
| [database-architect](../plugins/database/agents/database-architect.md) | opus | Database design from scratch, technology selection, schema modeling |

#### Incident Response & Network

| Agent | Model | Description |
|-------|-------|-------------|
| [incident-responder](../plugins/incident-response/agents/incident-responder.md) | opus | Production incident management and resolution |
| [network-engineer](../plugins/observability-monitoring/agents/network-engineer.md) | sonnet | Network debugging, load balancing, traffic analysis |

### Quality Assurance & Security

#### Code Quality & Review

| Agent | Model | Description |
|-------|-------|-------------|
| [code-reviewer](../plugins/code-quality/agents/code-reviewer.md) | opus | Code review with security focus and production reliability |
| [security-auditor](../plugins/security/agents/security-auditor.md) | opus | Vulnerability assessment and OWASP compliance |
| [backend-security-coder](../plugins/data-validation-suite/agents/backend-security-coder.md) | opus | Secure backend coding practices, API security implementation |
| [threat-modeling-expert](../plugins/security/agents/threat-modeling-expert.md) | opus | STRIDE threat modeling, attack trees, and security requirements |

#### Testing & Debugging

| Agent | Model | Description |
|-------|-------|-------------|
| [test-automator](../plugins/testing/agents/test-automator.md) | sonnet | Comprehensive test suite creation (unit, integration, e2e) |
| [tdd-orchestrator](../plugins/backend-development/agents/tdd-orchestrator.md) | sonnet | Test-Driven Development methodology guidance |
| [debugger](../plugins/debugging/agents/debugger.md) | sonnet | Error resolution and test failure analysis |
| [error-detective](../plugins/debugging/agents/error-detective.md) | sonnet | Log analysis and error pattern recognition |

#### Performance & Observability

| Agent | Model | Description |
|-------|-------|-------------|
| [performance-engineer](../plugins/observability-monitoring/agents/performance-engineer.md) | opus | Application profiling and optimization |
| [observability-engineer](../plugins/observability-monitoring/agents/observability-engineer.md) | opus | Production monitoring, distributed tracing, SLI/SLO management |

### Data & AI

#### Data Engineering & Analytics

| Agent | Model | Description |
|-------|-------|-------------|
| [data-scientist](../plugins/machine-learning-ops/agents/data-scientist.md) | opus | Data analysis, SQL queries, BigQuery operations |
| [data-engineer](../plugins/data-engineering/agents/data-engineer.md) | sonnet | ETL pipelines, data warehouses, streaming architectures |

#### Machine Learning & AI

| Agent | Model | Description |
|-------|-------|-------------|
| [ai-engineer](../plugins/llm-application-dev/agents/ai-engineer.md) | opus | LLM applications, RAG systems, prompt pipelines |
| [ml-engineer](../plugins/machine-learning-ops/agents/ml-engineer.md) | opus | ML pipelines, model serving, feature engineering |
| [mlops-engineer](../plugins/machine-learning-ops/agents/mlops-engineer.md) | opus | ML infrastructure, experiment tracking, model registries |
| [prompt-engineer](../plugins/llm-application-dev/agents/prompt-engineer.md) | opus | LLM prompt optimization and engineering |
| [vector-database-engineer](../plugins/llm-application-dev/agents/vector-database-engineer.md) | opus | Vector databases, embeddings, similarity search, and hybrid retrieval |

### Documentation & Technical Writing

| Agent | Model | Description |
|-------|-------|-------------|
| [docs-architect](../plugins/code-documentation/agents/docs-architect.md) | opus | Comprehensive technical documentation generation |
| [api-documenter](../plugins/documentation/agents/api-documenter.md) | sonnet | OpenAPI/Swagger specifications and developer docs |
| [reference-builder](../plugins/documentation/agents/reference-builder.md) | haiku | Technical references and API documentation |
| [tutorial-engineer](../plugins/code-documentation/agents/tutorial-engineer.md) | sonnet | Step-by-step tutorials and educational content |
| [mermaid-expert](../plugins/documentation/agents/mermaid-expert.md) | sonnet | Diagram creation (flowcharts, sequences, ERDs) |

### Business & Operations

#### Business Analysis & Finance

| Agent | Model | Description |
|-------|-------|-------------|
| [quant-analyst](../plugins/quantitative-trading/agents/quant-analyst.md) | opus | Financial modeling, trading strategies, market analysis |
| [risk-manager](../plugins/quantitative-trading/agents/risk-manager.md) | sonnet | Portfolio risk monitoring and management |

### Specialized Domains

| Agent | Model | Description |
|-------|-------|-------------|
| [legacy-modernizer](../plugins/refactoring/agents/legacy-modernizer.md) | sonnet | Legacy code refactoring and modernization |
| [context-manager](../plugins/agent-orchestration/agents/context-manager.md) | haiku | Multi-agent context management |

## Model Configuration

Agents are assigned to specific Claude models based on task complexity and computational requirements.

### Model Distribution Summary

| Model | Agent Count | Use Case |
|-------|-------------|----------|
| Opus | 42 | Critical architecture, security, code review, production coding |
| Sonnet | 39 | Complex tasks, support with intelligence |
| Haiku | 18 | Fast operational tasks |

### Model Selection Criteria

#### Haiku - Fast Execution & Deterministic Tasks

**Use when:**
- Generating code from well-defined specifications
- Creating tests following established patterns
- Writing documentation with clear templates
- Executing infrastructure operations
- Performing database query optimization
- Handling customer support responses
- Managing deployment pipelines

#### Sonnet - Complex Reasoning & Architecture

**Use when:**
- Designing system architecture
- Making technology selection decisions
- Performing security audits
- Reviewing code for architectural patterns
- Creating complex AI/ML pipelines
- Providing language-specific expertise
- Orchestrating multi-agent workflows
- Handling business-critical legal/HR matters

### Hybrid Orchestration Patterns

The plugin ecosystem leverages Sonnet + Haiku orchestration for optimal performance and cost efficiency:

#### Pattern 1: Planning → Execution
```
Sonnet: backend-architect (design API architecture)
  ↓
Haiku: Generate API endpoints following spec
  ↓
Haiku: test-automator (generate comprehensive tests)
  ↓
Sonnet: code-reviewer (architectural review)
```

#### Pattern 2: Reasoning → Action (Incident Response)
```
Sonnet: incident-responder (diagnose issue, create strategy)
  ↓
Haiku: devops-troubleshooter (execute fixes)
  ↓
Haiku: deployment-engineer (deploy hotfix)
  ↓
Haiku: Implement monitoring alerts
```

#### Pattern 3: Complex → Simple (Database Design)
```
Sonnet: database-architect (schema design, technology selection)
  ↓
Haiku: sql-pro (generate migration scripts)
  ↓
Haiku: database-admin (execute migrations)
  ↓
Haiku: database-optimizer (tune query performance)
```

#### Pattern 4: Multi-Agent Workflows
```
Full-Stack Feature Development:
Sonnet: backend-architect (design API components)
  ↓
Haiku: Generate code following designs
  ↓
Haiku: test-automator (unit + integration tests)
  ↓
Sonnet: security-auditor (security review)
  ↓
Haiku: deployment-engineer (CI/CD setup)
  ↓
Haiku: Setup observability stack
```

## Agent Invocation

### Natural Language

Agents can be invoked through natural language when you need Claude to reason about which specialist to use:

```
"Use backend-architect to design the authentication API"
"Have security-auditor scan for OWASP vulnerabilities"
"Get performance-engineer to optimize this database query"
```

### Slash Commands

Many agents are accessible through plugin slash commands for direct invocation:

```bash
/backend-development:feature-development user authentication
/security-scanning:security-sast
/incident-response:smart-fix "memory leak in payment service"
```

## Contributing

To add a new agent:

1. Create `plugins/{plugin-name}/agents/{agent-name}.md`
2. Add frontmatter with name, description, and model assignment
3. Write comprehensive system prompt
4. Update plugin definition in `.claude-plugin/marketplace.json`

See [Contributing Guide](../CONTRIBUTING.md) for details.
