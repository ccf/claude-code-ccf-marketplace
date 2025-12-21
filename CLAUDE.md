# Claude Code Plugins Marketplace

A curated collection of 64 plugins, 86 agents, and 120+ skills for Claude Code.

## Quick Reference

- **[AGENTS.md](./AGENTS.md)** — Complete list of 86 specialized agents with descriptions
- **[README.md](./README.md)** — Full documentation and installation guide

## Structure

```
claude-code-plugins/
├── shared/agents/           # 86 unique agents (symlinked into plugins)
├── plugins/                 # 64 domain-specific plugins
│   ├── */agents/            # Symlinks to shared/agents
│   ├── */commands/          # Slash commands
│   └── */skills/            # Modular knowledge packages
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
- **AWS Development** — CDK, serverless, event-driven architecture
- **Kubernetes** — Cluster design, Helm, GitOps
- **Terraform** — IaC patterns and modules

### AI/ML Development
- **MCP Builder** — Create high-quality MCP servers
- **Prompt Engineering** — Optimization techniques
- **RAG Systems** — Vector databases, embeddings

## Agent Model Tiers

| Tier | Model | When Used |
|------|-------|-----------|
| 1 | `opus` | Architecture, security, code review |
| 2 | `inherit` | Complex tasks (uses session default) |
| 3 | `sonnet` | Support tasks with intelligence |
| 4 | `haiku` | Fast operational tasks |

## Installation

```bash
# Clone repository
git clone https://github.com/YOUR_USERNAME/claude-code-plugins.git

# Option 1: Symlink entire marketplace
ln -s $(pwd)/claude-code-plugins ~/.config/claude-code/plugins

# Option 2: Copy specific plugins
cp -r claude-code-plugins/plugins/structured-reasoning ~/.config/claude-code/plugins/
```

## Sources

This marketplace combines:
- [wshobson/agents](https://github.com/wshobson/agents) — Base structure
- [ComposioHQ/awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills) — Skills
- [m0n0x41d/quint-code](https://github.com/m0n0x41d/quint-code) — FPF reasoning
- [obra/superpowers](https://github.com/obra/superpowers) — Development workflows
- [zxkane/aws-skills](https://github.com/zxkane/aws-skills) — AWS patterns

