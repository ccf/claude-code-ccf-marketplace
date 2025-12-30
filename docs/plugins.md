# Complete Plugin Reference

Browse all **26 consolidated plugins** organized by category.

## Quick Start - Essential Plugins

> 💡 **Getting Started?** Install these popular plugins for immediate productivity gains.

### Development Essentials

**debugging** - Comprehensive debugging toolkit

```bash
/plugin install debugging
```

Error analysis, root cause tracing, distributed debugging, and multi-agent problem diagnosis.

**testing** - Complete testing framework

```bash
/plugin install testing
```

Unit tests, TDD methodology, red-green-refactor cycles, and test automation.

**code-quality** - Multi-perspective code analysis

```bash
/plugin install code-quality
```

AI-powered review, architectural analysis, security auditing, and performance assessment.

### Infrastructure & Operations

**infrastructure** - Complete cloud infrastructure

```bash
/plugin install infrastructure
```

AWS/Azure/GCP, Kubernetes, Terraform, CI/CD, GitOps, service mesh - all in one plugin.

**security** - Comprehensive security toolkit

```bash
/plugin install security
```

SAST, vulnerability scanning, threat modeling, compliance, and API security.

### AI & ML Development

**agent-orchestration** - Multi-agent AI development

```bash
/plugin install agent-orchestration
```

Task planning, context management, subagent patterns, and Anthropic best practices.

---

## Complete Plugin Catalog

### 🎨 Core Development (5 plugins)

| Plugin | Description | Install |
|--------|-------------|---------|
| **debugging** | Error analysis, root cause tracing, distributed debugging | `/plugin install debugging` |
| **testing** | TDD, unit tests, integration tests, red-green-refactor | `/plugin install testing` |
| **code-quality** | AI review, architecture analysis, security, performance | `/plugin install code-quality` |
| **refactoring** | Migrations, tech debt, modernization, dependencies | `/plugin install refactoring` |
| **backend-development** | Backend API design with GraphQL and TDD | `/plugin install backend-development` |

### 🤖 AI & ML (5 plugins)

| Plugin | Description | Install |
|--------|-------------|---------|
| **agent-orchestration** | Multi-agent orchestration, context, subagent patterns | `/plugin install agent-orchestration` |
| **structured-reasoning** | FPF methodology for auditable decisions | `/plugin install structured-reasoning` |
| **llm-application-dev** | LLM apps, RAG systems, prompt pipelines | `/plugin install llm-application-dev` |
| **mcp-development** | Build MCP servers for LLM integrations | `/plugin install mcp-development` |
| **machine-learning-ops** | ML pipelines, MLOps, experiment tracking | `/plugin install machine-learning-ops` |

### ☁️ Infrastructure (1 consolidated plugin)

| Plugin | Description | Install |
|--------|-------------|---------|
| **infrastructure** | Cloud (AWS/Azure/GCP), K8s, Terraform, CI/CD, GitOps, service mesh | `/plugin install infrastructure` |

### 🗄️ Data & Database (3 plugins)

| Plugin | Description | Install |
|--------|-------------|---------|
| **database** | Schema design, migrations, optimization, SQL | `/plugin install database` |
| **data-engineering** | ETL pipelines, data warehouses, streaming | `/plugin install data-engineering` |
| **data-validation-suite** | Schema validation and data quality | `/plugin install data-validation-suite` |

### 🔒 Security (1 consolidated plugin)

| Plugin | Description | Install |
|--------|-------------|---------|
| **security** | SAST, compliance, threat modeling, API security | `/plugin install security` |

### 📚 Documentation (1 consolidated plugin)

| Plugin | Description | Install |
|--------|-------------|---------|
| **documentation** | Code docs, OpenAPI, diagrams, ADRs, changelogs | `/plugin install documentation` |

### 🌐 API Development (1 consolidated plugin)

| Plugin | Description | Install |
|--------|-------------|---------|
| **api-development** | REST, GraphQL, FastAPI, Django, testing, mocking | `/plugin install api-development` |

### 🚨 Operations (2 plugins)

| Plugin | Description | Install |
|--------|-------------|---------|
| **incident-response** | Production incident management | `/plugin install incident-response` |
| **observability-monitoring** | Metrics, logging, tracing, SLO | `/plugin install observability-monitoring` |

### ⚡ Performance (1 plugin)

| Plugin | Description | Install |
|--------|-------------|---------|
| **application-performance** | Profiling and optimization | `/plugin install application-performance` |

### 💻 Languages (3 plugins)

| Plugin | Description | Install |
|--------|-------------|---------|
| **python-development** | Python 3.12+, async, type hints | `/plugin install python-development` |
| **systems-programming** | C, C++, Rust, Go | `/plugin install systems-programming` |
| **shell-scripting** | Bash and POSIX shell | `/plugin install shell-scripting` |

### 💹 Finance (1 plugin)

| Plugin | Description | Install |
|--------|-------------|---------|
| **quantitative-trading** | Quant analysis, risk management, ML finance | `/plugin install quantitative-trading` |

### 🔄 Workflows (2 plugins)

| Plugin | Description | Install |
|--------|-------------|---------|
| **git-pr-workflows** | Git automation and PR enhancement | `/plugin install git-pr-workflows` |
| **developer-essentials** | Core development utilities | `/plugin install developer-essentials` |

---

## Plugin Installation

### Install from Marketplace

```bash
# Install a specific plugin
/plugin install <plugin-name>

# Example
/plugin install infrastructure
```

### Manual Installation

```bash
# Clone the marketplace
git clone https://github.com/ccf/claude-code-ccf-marketplace.git

# Symlink to Claude Code configuration
ln -s $(pwd)/claude-code-ccf-marketplace ~/.claude/plugins/claude-code-ccf-marketplace
```

---

## Plugin Architecture

Each plugin follows a consistent structure:

```
plugins/<name>/
├── agents/           # Symlinks to shared/agents/
├── commands/         # Slash commands (*.md)
└── skills/           # Knowledge packages
    └── <skill-name>/
        ├── SKILL.md  # Main skill content
        └── *.md      # Supporting files
```

### Key Files

- **agents/*.md** - Agent definitions (symlinked for deduplication)
- **commands/*.md** - Executable slash commands
- **skills/*/SKILL.md** - Modular knowledge with frontmatter

---

## Skills System

Skills use progressive disclosure for efficient context loading:

```yaml
---
name: example-skill
summary: One-line description for discovery
context_cost: low|medium|high
load_when: Trigger conditions
---
```

See [SKILLS_INDEX.md](../SKILLS_INDEX.md) for the complete skill catalog.
