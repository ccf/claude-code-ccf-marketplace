# Claude Code Plugins: Curated Marketplace

> **⚡ Unified Marketplace** — Combining the best of wshobson/agents, ComposioHQ/awesome-claude-skills, m0n0x41d/quint-code, and community best practices

A comprehensive, curated plugin marketplace featuring **71+ focused plugins**, **100+ specialized agents**, **120+ skills**, and production-ready workflows for Claude Code.

## What's Included

This repository combines and enhances multiple best-in-class Claude Code plugin sources:

| Source | What It Brings |
|--------|----------------|
| **[wshobson/agents](https://github.com/wshobson/agents)** | 67 focused plugins, 99 agents, marketplace structure |
| **[ComposioHQ/awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills)** | MCP builder, skill creator, changelog generator, document skills |
| **[m0n0x41d/quint-code](https://github.com/m0n0x41d/quint-code)** | Structured reasoning (FPF), auditable decision making |
| **[obra/superpowers](https://github.com/obra/superpowers)** | Git worktrees, root-cause tracing, subagent-driven development |
| **[NeoLabHQ/context-engineering-kit](https://github.com/NeoLabHQ/context-engineering-kit)** | Prompt engineering, software architecture, kaizen methodology |
| **[zxkane/aws-skills](https://github.com/zxkane/aws-skills)** | AWS CDK, serverless, event-driven architecture patterns |

## Highlighted New Plugins

### Structured Reasoning (FPF)
Hypothesis-driven decision making with auditable evidence trails:
```bash
/q0-init                           # Initialize knowledge base
/q1-hypothesize "API caching"      # Generate hypotheses
/q2-verify H1                      # Logical verification
/q5-decide H1                      # Create Design Rationale Record
```

### AWS Development
Full-stack AWS with CDK, serverless, and event-driven patterns:
- AWS CDK best practices and construct patterns
- Serverless architecture (Lambda, API Gateway, Step Functions)
- Event-driven design (EventBridge, SQS, SNS)
- Well-Architected Framework compliance

### MCP Development  
Build high-quality MCP servers for LLM integrations:
- Agent-centric design patterns
- Tool design best practices
- Evaluation framework
- Python and TypeScript guides

### Enhanced Quantitative Trading
Comprehensive quant and risk management:
- Factor-based strategies and statistical arbitrage
- VaR, CVaR, and stress testing
- R-multiple tracking and expectancy calculation
- Kelly criterion position sizing

## Plugin Categories

| Category | Plugins | Description |
|----------|---------|-------------|
| **Development** | 5 | Debugging, backend, frontend, multi-platform, developer essentials |
| **Documentation** | 3 | Code docs, API specs, C4 architecture |
| **Workflows** | 4 | Git, full-stack, TDD, development workflows |
| **AI & ML** | 5 | LLM apps, agents, context, MLOps, structured reasoning |
| **Infrastructure** | 6 | Deployment, K8s, cloud, CI/CD, AWS |
| **Security** | 4 | Scanning, compliance, backend/API, frontend/mobile |
| **Languages** | 8 | Python, JS/TS, systems (Rust/Go/C/C++), JVM, shell |
| **Finance** | 1 | Quantitative trading, risk management |
| **And more...** | 35+ | Data, operations, performance, business, gaming |

## Quick Start

### Install All Plugins
```bash
git clone https://github.com/YOUR_USERNAME/claude-code-plugins.git
cd claude-code-plugins
# Copy to Claude Code configuration
cp -r .claude-plugin ~/.config/claude-code/
```

### Install Specific Plugin
```bash
# Copy individual plugin
cp -r plugins/structured-reasoning ~/.config/claude-code/plugins/
```

## Key Skills

### From ComposioHQ
- **mcp-builder** — Guide for creating MCP servers
- **skill-creator** — Create effective Claude skills
- **changelog-generator** — Transform commits to release notes

### From Superpowers
- **using-git-worktrees** — Isolated workspaces for feature development
- **subagent-driven-development** — Fresh subagent per task with code review
- **root-cause-tracing** — Trace errors to their source, not symptoms

### From Context Engineering Kit
- **prompt-engineering** — Few-shot, chain-of-thought, persuasion principles
- **software-architecture** — Clean Architecture, DDD, SOLID patterns

### From AWS Skills
- **aws-cdk-development** — CDK constructs, patterns, validation
- **aws-serverless-eda** — Lambda, Step Functions, EventBridge

## Three-Tier Model Strategy

Strategic model assignment for optimal performance:

| Tier | Model | Use Case |
|------|-------|----------|
| **Tier 1** | Opus | Architecture, security, code review, production coding |
| **Tier 2** | Inherit | Complex tasks - user chooses (AI/ML, backend, frontend) |
| **Tier 3** | Sonnet | Support tasks (docs, testing, debugging) |
| **Tier 4** | Haiku | Fast operations (SEO, deployment, content) |

## Repository Structure

```
claude-code-plugins/
├── .claude-plugin/
│   └── marketplace.json          # 71+ plugins
├── plugins/
│   ├── structured-reasoning/     # FPF methodology
│   │   ├── agents/
│   │   ├── commands/             # q0-init, q1-hypothesize, etc.
│   │   └── skills/
│   ├── aws-development/          # AWS CDK, serverless
│   ├── mcp-development/          # MCP server building
│   ├── quantitative-trading/     # Enhanced quant/risk
│   ├── development-workflows/    # Subagent patterns
│   └── ... (65+ more plugins)
├── docs/                         # Comprehensive documentation
└── README.md
```

## Contributing

To add new agents, skills, or commands:

1. Identify or create the appropriate plugin in `plugins/`
2. Add `.md` files in the appropriate subdirectory:
   - `agents/` — Specialized agents
   - `commands/` — Tools and workflows  
   - `skills/` — Modular knowledge packages
3. Update the plugin definition in `.claude-plugin/marketplace.json`
4. Submit a pull request

## Credits

This curated marketplace builds upon the excellent work of:

- **Seth Hobson** ([@wshobson](https://github.com/wshobson)) — Original agents marketplace
- **Composio** ([@ComposioHQ](https://github.com/ComposioHQ)) — Awesome Claude Skills
- **m0n0x41d** ([@m0n0x41d](https://github.com/m0n0x41d)) — Quint-Code FPF framework
- **Jesse Vincent** ([@obra](https://github.com/obra)) — Superpowers skills
- **NeoLabHQ** ([@NeoLabHQ](https://github.com/NeoLabHQ)) — Context Engineering Kit
- **Kane** ([@zxkane](https://github.com/zxkane)) — AWS Skills

## License

MIT License — see individual plugins for specific licensing.
