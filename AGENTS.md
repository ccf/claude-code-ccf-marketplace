# Claude Code Plugins Marketplace

A curated collection of 10 specialized plugins and 16 unique agents for Claude Code.

**Focus**: Capabilities NOT covered by Claude Code's built-in agents.

## Structure

```
claude-code-plugins/
├── shared/agents/           # Agent definitions (symlinked into plugins)
├── plugins/                 # 10 specialized domain plugins
│   ├── */agents/            # Symlinks to shared/agents
│   ├── */commands/          # Slash commands
│   └── */skills/            # Modular knowledge packages
└── .claude-plugin/marketplace.json
```

---

## Why These Agents?

Claude Code has 100+ built-in agents covering languages (Python, Rust, Go, etc.), infrastructure (Kubernetes, Terraform), databases, testing, and more. This marketplace focuses on **gaps**:

| Category             | Built-in Coverage | This Marketplace Adds                              |
| -------------------- | ----------------- | -------------------------------------------------- |
| Finance/Quant        | None              | quant-analyst, risk-manager, ml-quant-developer    |
| Structured Reasoning | None              | reasoning-orchestrator (FPF methodology)           |
| MCP Development      | Basic             | mcp-architect (advanced patterns)                  |
| LLM Applications     | Basic             | ai-engineer, prompt-engineer (RAG, agents)         |
| Shell Scripting      | Basic             | bash-pro, posix-shell-pro (defensive patterns)     |
| Documentation        | API docs only     | docs-architect, mermaid-expert (architecture docs) |
| Modernization        | Basic             | legacy-modernizer (systematic migration)           |
| Monorepos            | None              | monorepo-architect (Nx/Turborepo/Bazel)            |
| Event Sourcing       | None              | event-sourcing-architect, temporal-python-pro      |
| Threat Modeling      | Basic security    | threat-modeling-expert (STRIDE, attack trees)      |

---

## Model Tiers

| Tier       | Model     | Use Case                                                        |
| ---------- | --------- | --------------------------------------------------------------- |
| **Tier 1** | `opus`    | Critical architecture, security, code review, production coding |
| **Tier 2** | `inherit` | Complex tasks - uses session default model                      |
| **Tier 3** | `sonnet`  | Support tasks with intelligence                                 |
| **Tier 4** | `haiku`   | Fast operational tasks                                          |

---

## Available Agents (16)

### Finance & Quantitative Trading

| Agent                | Model | Plugin               | Description                                           |
| -------------------- | ----- | -------------------- | ----------------------------------------------------- |
| `quant-analyst`      | opus  | quantitative-trading | Quantitative finance, trading strategies, backtesting |
| `risk-manager`       | opus  | quantitative-trading | Portfolio risk, VaR, position sizing, hedging         |
| `ml-quant-developer` | opus  | quantitative-trading | ML for finance: LSTM, transformers, factor investing  |

### AI & LLM Development

| Agent                    | Model   | Plugin               | Description                                        |
| ------------------------ | ------- | -------------------- | -------------------------------------------------- |
| `reasoning-orchestrator` | opus    | structured-reasoning | FPF methodology, hypothesis-driven decision making |
| `mcp-architect`          | opus    | mcp-development      | MCP server development, tool design patterns       |
| `ai-engineer`            | inherit | llm-application-dev  | RAG systems, AI agents, LLM applications           |
| `prompt-engineer`        | opus    | llm-application-dev  | Prompt optimization, few-shot, chain-of-thought    |

### Backend & Architecture

| Agent                      | Model | Plugin               | Description                                 |
| -------------------------- | ----- | -------------------- | ------------------------------------------- |
| `event-sourcing-architect` | opus  | backend-development  | Event sourcing, CQRS patterns, projections  |
| `temporal-python-pro`      | opus  | backend-development  | Temporal workflows, orchestration patterns  |
| `monorepo-architect`       | opus  | developer-essentials | Nx, Turborepo, Bazel, dependency management |

### Shell & Scripting

| Agent             | Model  | Plugin          | Description                                |
| ----------------- | ------ | --------------- | ------------------------------------------ |
| `bash-pro`        | sonnet | shell-scripting | Defensive Bash, error handling, shellcheck |
| `posix-shell-pro` | sonnet | shell-scripting | POSIX-compliant scripts, portability       |

### Documentation

| Agent            | Model  | Plugin        | Description                             |
| ---------------- | ------ | ------------- | --------------------------------------- |
| `docs-architect` | sonnet | documentation | Technical documentation architecture    |
| `mermaid-expert` | sonnet | documentation | Diagrams, flowcharts, sequence diagrams |

### Modernization & Security

| Agent                    | Model | Plugin      | Description                                      |
| ------------------------ | ----- | ----------- | ------------------------------------------------ |
| `legacy-modernizer`      | opus  | refactoring | Legacy code modernization, systematic migration  |
| `threat-modeling-expert` | opus  | security    | STRIDE analysis, attack trees, threat mitigation |

---

## Key Capabilities

### Structured Reasoning (FPF)

Hypothesis-driven decision making with auditable evidence trails:

```bash
/q0-init                           # Initialize knowledge base
/q1-hypothesize "API caching"      # Generate competing hypotheses
/q2-verify H1                      # Logical verification
/q3-validate H1                    # Empirical evidence
/q5-decide H1                      # Create Design Rationale Record
```

### ML Quantitative Finance

Comprehensive ML-based asset management:

- Deep learning (LSTM, transformers, autoencoders)
- Reinforcement learning for portfolio optimization
- Lopez de Prado framework (CPCV, meta-labeling, PBO)
- Factor investing with ML

### MCP Development

Build high-quality MCP servers for LLM integrations:

- Agent-centric design patterns
- Tool design best practices
- Evaluation framework

---

## Usage

Agents are automatically available when plugins are enabled. To invoke directly:

```
@agent-name your request here
```

Examples:

```
@quant-analyst Build a momentum strategy with proper backtesting
@reasoning-orchestrator Help me decide between REST vs GraphQL
@mcp-architect Design a MCP server for database queries
@bash-pro Write a defensive deployment script
```

---

## Sources

This marketplace combines:

- [wshobson/agents](https://github.com/wshobson/agents) - Base structure
- [ComposioHQ/awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills) - Skills
- [m0n0x41d/quint-code](https://github.com/m0n0x41d/quint-code) - FPF reasoning
- [obra/superpowers](https://github.com/obra/superpowers) - Development workflows
