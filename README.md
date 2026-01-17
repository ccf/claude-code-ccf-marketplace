# Claude Code Plugins: Curated Marketplace

> **Focused Plugins** — Capabilities NOT covered by Claude Code's 100+ built-in agents

A curated plugin marketplace featuring **10 specialized plugins**, **16 unique agents**, and **40+ skills** for Claude Code.

---

## Why This Marketplace?

Claude Code includes built-in agents for:

- Languages (Python, Rust, Go, TypeScript, etc.)
- Infrastructure (Kubernetes, Terraform, AWS/Azure/GCP)
- Databases (PostgreSQL, SQL optimization)
- Testing, debugging, code review

**This marketplace fills the gaps:**

| Category                 | What We Add                                         |
| ------------------------ | --------------------------------------------------- |
| **Finance/Quant**        | Trading strategies, risk management, ML for finance |
| **Structured Reasoning** | FPF methodology with auditable decision trails      |
| **MCP Development**      | Advanced MCP server patterns                        |
| **LLM Applications**     | RAG systems, prompt engineering, AI agents          |
| **Event Sourcing**       | CQRS, Temporal workflows                            |
| **Monorepos**            | Nx, Turborepo, Bazel architecture                   |
| **Threat Modeling**      | STRIDE analysis, attack trees                       |

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
- Lopez de Prado framework (CPCV, meta-labeling, PBO)
- Factor investing with ML

### MCP Development

Build high-quality MCP servers for LLM integrations:

- Agent-centric design patterns
- Tool design best practices

---

## Available Plugins (10)

| Plugin                 | Agents | Skills | Focus                           |
| ---------------------- | ------ | ------ | ------------------------------- |
| `quantitative-trading` | 3      | 2      | Quant finance, ML trading, risk |
| `structured-reasoning` | 1      | 1      | FPF methodology                 |
| `mcp-development`      | 1      | 1      | MCP server patterns             |
| `llm-application-dev`  | 2      | 9      | RAG, prompts, AI agents         |
| `shell-scripting`      | 2      | 3      | Defensive Bash, POSIX           |
| `documentation`        | 2      | 4      | Docs architecture, diagrams     |
| `refactoring`          | 1      | 4      | Legacy modernization            |
| `developer-essentials` | 1      | 12     | Monorepo architecture           |
| `backend-development`  | 2      | 10     | Event sourcing, Temporal        |
| `security`             | 1      | 5      | Threat modeling, STRIDE         |

---

## Repository Structure

```
claude-code-plugins/
├── .claude-plugin/
│   └── marketplace.json          # 10 plugins
├── shared/
│   └── agents/                   # Agent definitions
├── plugins/
│   ├── quantitative-trading/     # Finance specialty
│   ├── structured-reasoning/     # FPF methodology
│   ├── mcp-development/          # MCP servers
│   ├── llm-application-dev/      # LLM applications
│   ├── shell-scripting/          # Bash/POSIX
│   ├── documentation/            # Docs architecture
│   ├── refactoring/              # Modernization
│   ├── developer-essentials/     # Monorepos
│   ├── backend-development/      # Event sourcing
│   └── security/                 # Threat modeling
├── AGENTS.md                     # Agent catalog
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
cp -r plugins/quantitative-trading ~/.claude/plugins/
```

---

## Model Tiers

| Tier       | Model     | Use Case                                   |
| ---------- | --------- | ------------------------------------------ |
| **Tier 1** | `opus`    | Architecture, security, critical decisions |
| **Tier 2** | `inherit` | Complex tasks - session default            |
| **Tier 3** | `sonnet`  | Support tasks (docs, testing)              |
| **Tier 4** | `haiku`   | Fast operations                            |

---

## Contributing

1. Add agents to `shared/agents/` (single source of truth)
2. Create symlinks in relevant `plugins/*/agents/`
3. Add skills to appropriate `plugins/*/skills/`
4. Update `.claude-plugin/marketplace.json`
5. Submit a pull request

---

## Credits

| Source                                                                                      | What It Brings                      |
| ------------------------------------------------------------------------------------------- | ----------------------------------- |
| **[wshobson/agents](https://github.com/wshobson/agents)**                                   | Base structure, marketplace pattern |
| **[ComposioHQ/awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills)** | MCP builder, skill creator          |
| **[m0n0x41d/quint-code](https://github.com/m0n0x41d/quint-code)**                           | Structured reasoning (FPF)          |
| **[obra/superpowers](https://github.com/obra/superpowers)**                                 | Git worktrees, root-cause tracing   |

---

## License

MIT License - see individual plugins for specific licensing.
