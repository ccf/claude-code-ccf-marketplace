# Usage Guide

Complete guide to using agents, slash commands, and multi-agent workflows.

## Overview

The plugin ecosystem provides two primary interfaces:

1. **Slash Commands** - Direct invocation of tools and workflows
2. **Natural Language** - Claude reasons about which agents to use

## Slash Commands

Slash commands are the primary interface for working with agents and workflows. Each plugin provides namespaced commands that you can run directly.

### Command Format

```bash
/plugin-name:command-name [arguments]
```

### Discovering Commands

List all available slash commands from installed plugins:

```bash
/plugin
```

### Benefits of Slash Commands

- **Direct invocation** - No need to describe what you want in natural language
- **Structured arguments** - Pass parameters explicitly for precise control
- **Composability** - Chain commands together for complex workflows
- **Discoverability** - Use `/plugin` to see all available commands

## Natural Language

Agents can also be invoked through natural language when you need Claude to reason about which specialist to use:

```
"Use backend-architect to design the authentication API"
"Have security-auditor scan for OWASP vulnerabilities"
"Get performance-engineer to optimize this database query"
```

Claude Code automatically selects and coordinates the appropriate agents based on your request.

## Command Reference by Category

### Development & Features

| Command                                    | Description                            |
| ------------------------------------------ | -------------------------------------- |
| `/backend-development:feature-development` | End-to-end backend feature development |

### Testing & Quality

| Command                  | Description                           |
| ------------------------ | ------------------------------------- |
| `/testing:test-generate` | Generate comprehensive unit tests     |
| `/testing:tdd-cycle`     | Complete TDD red-green-refactor cycle |
| `/testing:tdd-red`       | Write failing tests first             |
| `/testing:tdd-green`     | Implement code to pass tests          |
| `/testing:tdd-refactor`  | Refactor with passing tests           |

### Code Quality & Review

| Command                            | Description                |
| ---------------------------------- | -------------------------- |
| `/code-quality:ai-review`          | AI-powered code review     |
| `/code-quality:full-review`        | Multi-perspective analysis |
| `/code-quality:pr-enhance`         | Enhance pull requests      |
| `/code-quality:multi-agent-review` | Multi-agent code review    |

### Debugging & Troubleshooting

| Command                                | Description                    |
| -------------------------------------- | ------------------------------ |
| `/debugging:smart-debug`               | Interactive smart debugging    |
| `/debugging:error-analysis`            | Deep error analysis            |
| `/debugging:error-trace`               | Stack trace debugging          |
| `/debugging:debug-trace`               | Distributed system tracing     |
| `/debugging:multi-agent-review`        | Multi-agent problem diagnosis  |
| `/incident-response:incident-response` | Production incident management |
| `/incident-response:smart-fix`         | Automated incident resolution  |

### Security

| Command                           | Description                         |
| --------------------------------- | ----------------------------------- |
| `/security:security-hardening`    | Comprehensive security hardening    |
| `/security:security-sast`         | Static application security testing |
| `/security:security-dependencies` | Dependency vulnerability scanning   |
| `/security:compliance-check`      | SOC2/HIPAA/GDPR compliance          |

### Infrastructure & Deployment

| Command                                   | Description                     |
| ----------------------------------------- | ------------------------------- |
| `/infrastructure:workflow-automate`       | CI/CD pipeline automation       |
| `/infrastructure:config-validate`         | Pre-deployment validation       |
| `/observability-monitoring:monitor-setup` | Setup monitoring infrastructure |
| `/observability-monitoring:slo-implement` | Implement SLO/SLI metrics       |

### Database

| Command                             | Description                   |
| ----------------------------------- | ----------------------------- |
| `/database:sql-migrations`          | Database migration automation |
| `/database:migration-observability` | Migration monitoring          |
| `/database:cost-optimize`           | Database cost optimization    |

### Refactoring & Modernization

| Command                         | Description                  |
| ------------------------------- | ---------------------------- |
| `/refactoring:refactor-clean`   | Code cleanup and refactoring |
| `/refactoring:tech-debt`        | Technical debt management    |
| `/refactoring:deps-audit`       | Dependency auditing          |
| `/refactoring:legacy-modernize` | Legacy code modernization    |
| `/refactoring:code-migrate`     | Code migration               |
| `/refactoring:deps-upgrade`     | Dependency upgrades          |

### Data & ML

| Command                                 | Description                        |
| --------------------------------------- | ---------------------------------- |
| `/machine-learning-ops:ml-pipeline`     | ML training pipeline orchestration |
| `/data-engineering:data-pipeline`       | ETL/ELT pipeline construction      |
| `/data-engineering:data-driven-feature` | Data-driven feature development    |

### Documentation

| Command                               | Description                |
| ------------------------------------- | -------------------------- |
| `/documentation:doc-generate`         | Generate documentation     |
| `/documentation:code-explain`         | Explain code functionality |
| `/documentation:doc-generate-openapi` | Generate OpenAPI specs     |

### Git & PR Workflows

| Command                            | Description             |
| ---------------------------------- | ----------------------- |
| `/git-pr-workflows:git-workflow`   | Git workflow automation |
| `/git-pr-workflows:pr-workflow`    | PR workflow automation  |
| `/git-pr-workflows:branch-cleanup` | Branch cleanup          |

### Structured Reasoning (FPF)

| Command                                | Description                         |
| -------------------------------------- | ----------------------------------- |
| `/structured-reasoning:q0-init`        | Initialize reasoning knowledge base |
| `/structured-reasoning:q1-hypothesize` | Generate competing hypotheses       |
| `/structured-reasoning:q2-verify`      | Logical verification                |
| `/structured-reasoning:q3-validate`    | Empirical validation                |
| `/structured-reasoning:q4-specify`     | Create formal specification         |
| `/structured-reasoning:q5-decide`      | Create Design Rationale Record      |

### Agent Orchestration

| Command                                     | Description              |
| ------------------------------------------- | ------------------------ |
| `/agent-orchestration:multi-agent-optimize` | Multi-agent optimization |
| `/agent-orchestration:improve-agent`        | Agent improvement        |
| `/agent-orchestration:context-save`         | Save context             |

---

## Multi-Agent Workflows

### Workflow Templates

The marketplace includes composable workflow templates in `workflows/`:

#### Feature Development

```
@task-planner → @codebase-navigator → @architect-review → @{lang}-pro → @code-reviewer
```

#### Bug Investigation

```
@codebase-navigator → @debugger → @error-detective → @{lang}-pro → @test-strategist
```

#### Architecture Decision

```
@context-researcher → @reasoning-orchestrator → /q1-hypothesize → /q5-decide
```

### Invoking Multi-Agent Workflows

```bash
# Complex feature development with multiple agents
"Build user authentication with JWT tokens, database storage, and API endpoints"

# Claude coordinates: backend-architect → python-pro → security-auditor → test-automator
```

### Agent Coordination Patterns

#### Pattern 1: Planning → Execution

```
@task-planner (decompose task)
  ↓
@context-researcher (gather context)
  ↓
@{specialist}-pro (implement)
  ↓
@output-critic (review)
```

#### Pattern 2: Diagnosis → Fix

```
@debugger (identify issue)
  ↓
@error-detective (trace cause)
  ↓
@{lang}-pro (implement fix)
  ↓
@test-strategist (verify)
```

---

## Best Practices

### 1. Use Slash Commands for Repeatability

Instead of:

```
"Review my code for security issues"
```

Use:

```bash
/security:security-sast
```

### 2. Chain Commands for Complex Tasks

```bash
# Step 1: Analyze
/debugging:error-analysis "Memory leak in payment service"

# Step 2: Fix
/incident-response:smart-fix "Memory leak in payment service"

# Step 3: Verify
/testing:test-generate "payment service memory management"
```

### 3. Use Natural Language for Exploratory Work

When you're not sure what you need:

```
"I'm getting intermittent 500 errors in production. Help me investigate."
```

Claude will coordinate the appropriate agents.

### 4. Leverage Agent Specialization

Each agent has specific expertise. Use the right agent for the job:

| Task                  | Best Agent              |
| --------------------- | ----------------------- |
| API design            | `@backend-architect`    |
| Security review       | `@security-auditor`     |
| Performance tuning    | `@performance-engineer` |
| Database optimization | `@database-optimizer`   |
| ML pipeline           | `@ml-engineer`          |

---

## Troubleshooting

### Command Not Found

If a slash command doesn't work:

1. Check the plugin is installed: `/plugin`
2. Verify command name: Check plugin's `commands/` directory
3. Reinstall if needed: `/plugin install <plugin-name>`

### Agent Not Available

If an agent isn't responding:

1. Verify the agent exists in `shared/agents/`
2. Check the plugin includes the agent in its manifest
3. Try natural language invocation as fallback

### Context Issues

For context-related problems:

1. Use `/agent-orchestration:context-save` to preserve context
2. Break large tasks into smaller steps
3. Use progressive disclosure skills
