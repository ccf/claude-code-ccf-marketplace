# Claude Code Plugins: Curated Marketplace

> **⚡ Unified Marketplace** — Combining my favorite Claude Code sub-agents and skills in an agent orchestration architecture with workflows

A comprehensive, curated plugin marketplace featuring **62 focused plugins**, **93 specialized agents**, **130+ skills**, and production-ready workflows for Claude Code.

---

## Agent Orchestration Architecture

### Coordination Agents
Multi-agent workflows with specialized coordination:

| Agent | Purpose |
|-------|---------|
| `@task-planner` | Decomposes complex tasks, delegates to specialists |
| `@output-critic` | Reviews outputs before finalization |
| `@context-researcher` | Gathers context before implementation |
| `@codebase-navigator` | Maps project structure, locates code |

### Workflow Templates
Composable patterns in `workflows/`:

```
Feature Development:
@task-planner → @codebase-navigator → @architect-review → @{lang}-pro → @code-reviewer

Bug Investigation:
@codebase-navigator → @debugger → @error-detective → @{lang}-pro → @test-strategist

Architecture Decision:
@context-researcher → @reasoning-orchestrator → /q1-hypothesize → /q5-decide
```

### Best Practice Skills
| Skill | What It Teaches |
|-------|-----------------|
| `agentic-coding-patterns` | Writing code that works well with AI |
| `context-optimization` | Managing context windows effectively |
| `anthropic-agent-guidelines` | Official Anthropic agent best practices |
| `eval-driven-development` | Testing and evaluating AI outputs |
| `uncertainty-communication` | When/how to ask clarifying questions |

> 📚 **Progressive Disclosure**: Skills now include `summary`, `context_cost`, and `load_when` frontmatter for efficient context loading. See [SKILLS_INDEX.md](./SKILLS_INDEX.md) for the full catalog.

---

## Highlighted Capabilities

### Structured Reasoning (FPF)
Hypothesis-driven decision making with auditable evidence trails:
```bash
/q0-init                           # Initialize knowledge base
/q1-hypothesize "API caching"      # Generate hypotheses
/q2-verify H1                      # Logical verification
/q5-decide H1                      # Create Design Rationale Record
```

### ML Quantitative Finance
Comprehensive ML-based asset management:
- Deep learning (LSTM, transformers, autoencoders)
- Reinforcement learning for portfolio optimization
- López de Prado framework (CPCV, meta-labeling, PBO)
- Factor investing with ML

### AWS Development
Full-stack AWS with CDK, serverless, and event-driven patterns:
- AWS CDK best practices and construct patterns
- Serverless architecture (Lambda, API Gateway, Step Functions)
- Event-driven design (EventBridge, SQS, SNS)

### MCP Development  
Build high-quality MCP servers for LLM integrations:
- Agent-centric design patterns
- Tool design best practices
- Evaluation framework

---

## Model Tiers

Strategic model assignment for optimal performance:

| Tier | Model | Use Case |
|------|-------|----------|
| **Tier 1** | `opus` | Architecture, security, code review, critical coding |
| **Tier 2** | `inherit` | Complex tasks - uses session default model |
| **Tier 3** | `sonnet` | Support tasks (docs, testing, debugging) |
| **Tier 4** | `haiku` | Fast operations (deployment, content) |

---

## Repository Structure

```
claude-code-ccf-marketplace/
├── .claude-plugin/
│   └── marketplace.json          # 64 plugins defined
├── shared/
│   └── agents/                   # 93 unique agents (single source of truth)
├── plugins/
│   ├── agent-orchestration/      # Coordination agents + best practice skills
│   ├── structured-reasoning/     # FPF methodology + commands
│   ├── aws-development/          # AWS CDK, serverless
│   ├── mcp-development/          # MCP server building
│   ├── quantitative-trading/     # Quant, risk, ML finance
│   └── ... (59+ more plugins)
├── workflows/                    # Composable workflow templates
├── AGENTS.md                     # Complete agent catalog
├── SKILLS_INDEX.md               # Skill discovery with context costs
├── CLAUDE.md                     # Entry point (@AGENTS.md)
└── README.md
```

---

## Quick Start

### Install All Plugins
```bash
git clone https://github.com/ccf/claude-code-ccf-marketplace.git
cd claude-code-ccf-marketplace
# Symlink to Claude Code configuration
ln -s $(pwd) ~/.claude/plugins/claude-code-ccf-marketplace
```

### Install Specific Plugin
```bash
# Copy individual plugin
cp -r plugins/agent-orchestration ~/.claude/plugins/
```

---

## Key Skills by Source

### Agent Orchestration
- **agentic-coding-patterns** — Writing AI-friendly code
- **context-optimization** — Managing context windows
- **anthropic-agent-guidelines** — Official best practices
- **eval-driven-development** — Testing AI outputs
- **uncertainty-communication** — Asking clarifying questions

### From Superpowers
- **using-git-worktrees** — Isolated workspaces for feature development
- **subagent-driven-development** — Fresh subagent per task
- **root-cause-tracing** — Trace errors to source

### From Context Engineering Kit
- **prompt-engineering** — Few-shot, chain-of-thought techniques
- **software-architecture** — Clean Architecture, DDD, SOLID

### From AWS Skills
- **aws-cdk-development** — CDK constructs and patterns
- **aws-serverless-eda** — Lambda, Step Functions, EventBridge

---

## Plugin Categories

| Category | Count | Examples |
|----------|-------|----------|
| **AI & ML** | 6 | agent-orchestration, structured-reasoning, llm-application-dev |
| **Infrastructure** | 7 | aws-development, kubernetes-operations, cloud-infrastructure |
| **Languages** | 8 | python-development, systems-programming, javascript-typescript |
| **Development** | 5 | debugging-toolkit, backend-development, code-refactoring |
| **Documentation** | 3 | documentation-generation, c4-architecture, code-documentation |
| **Security** | 4 | security-scanning, backend-api-security, frontend-mobile-security |
| **Finance** | 1 | quantitative-trading (quant-analyst, risk-manager, ml-quant-developer) |
| **And more...** | 30+ | data-engineering, observability, performance, business |

---

## Contributing

1. Add agents to `shared/agents/` (single source of truth)
2. Create symlinks in relevant `plugins/*/agents/`
3. Add skills to appropriate `plugins/*/skills/`
4. Update `.claude-plugin/marketplace.json`
5. Submit a pull request

---

## Credits

This repository combines and enhances multiple best-in-class Claude Code plugin sources:

| Source | What It Brings |
|--------|----------------|
| **[wshobson/agents](https://github.com/wshobson/agents)** | 67 focused plugins, 99 agents, marketplace structure |
| **[ComposioHQ/awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills)** | MCP builder, skill creator, changelog generator |
| **[m0n0x41d/quint-code](https://github.com/m0n0x41d/quint-code)** | Structured reasoning (FPF), auditable decision making |
| **[obra/superpowers](https://github.com/obra/superpowers)** | Git worktrees, root-cause tracing, subagent-driven development |
| **[NeoLabHQ/context-engineering-kit](https://github.com/NeoLabHQ/context-engineering-kit)** | Prompt engineering, software architecture |
| **[zxkane/aws-skills](https://github.com/zxkane/aws-skills)** | AWS CDK, serverless, event-driven architecture |

---

## License

MIT License — see individual plugins for specific licensing.
