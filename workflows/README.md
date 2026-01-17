# Workflow Templates

Composable workflows showing how to orchestrate multiple agents for complex tasks.

## Available Workflows

### 1. Feature Development

Full feature implementation with planning, coding, and review.

```
@task-planner → break down feature requirements
    ↓
@codebase-navigator → understand existing code
    ↓
@architect-review → validate approach (if significant)
    ↓
@{language}-pro → implement feature
    ↓
@test-strategist → plan tests
    ↓
@code-reviewer → review implementation
    ↓
@output-critic → final quality check
```

### 2. Bug Investigation

Systematic debugging with root cause analysis.

```
@codebase-navigator → locate relevant code
    ↓
@context-researcher → gather context
    ↓
@debugger → analyze the issue
    ↓
@error-detective → trace error patterns
    ↓
@{language}-pro → implement fix
    ↓
@test-strategist → add regression test
```

### 3. Code Review

Thorough multi-perspective review.

```
@code-reviewer → quality and patterns
    ↓
@security-auditor → security issues (if applicable)
    ↓
@performance-engineer → performance concerns
    ↓
@output-critic → synthesize feedback
```

### 4. API Design

End-to-end API creation.

```
@context-researcher → understand requirements
    ↓
@api-designer → design endpoints and contracts
    ↓
@backend-architect → validate architecture
    ↓
@{language}-pro → implement
    ↓
@api-documenter → generate documentation
    ↓
@test-strategist → plan API tests
```

### 5. Architecture Decision

Structured approach to significant decisions.

```
@context-researcher → gather context
    ↓
@reasoning-orchestrator → structured analysis (FPF)
    ↓
/q1-hypothesize → generate options
    ↓
/q2-verify → logical verification
    ↓
/q3-validate → empirical evidence
    ↓
@architect-review → expert review
    ↓
/q5-decide → document decision
```

### 6. Legacy Modernization

Systematic approach to updating old code.

```
@codebase-navigator → map legacy system
    ↓
@context-researcher → understand constraints
    ↓
@legacy-modernizer → plan modernization
    ↓
@architect-review → validate approach
    ↓
@test-strategist → ensure test coverage first
    ↓
@{language}-pro → implement changes incrementally
    ↓
@code-reviewer → review each increment
```

### 7. New Project Setup

From zero to productive.

```
@task-planner → break down setup tasks
    ↓
@backend-architect → design structure
    ↓
@{language}-pro → scaffold project
    ↓
@docs-architect → create documentation
    ↓
@test-strategist → set up testing
    ↓
@deployment-engineer → configure CI/CD
```

### 8. ML Strategy Development

Quantitative finance workflow.

```
@context-researcher → gather market context
    ↓
@quant-analyst → design strategy
    ↓
@ml-quant-developer → implement ML components
    ↓
@risk-manager → assess risk profile
    ↓
@test-strategist → plan backtesting
    ↓
@output-critic → review methodology
```

## Usage Pattern

### Sequential Execution

Use when each step depends on the previous:

```
1. Start with @task-planner to create the plan
2. Execute each step with the designated agent
3. Use @output-critic between major phases
4. Document decisions along the way
```

### Parallel Execution

Use when steps are independent:

```
# These can run in parallel:
@frontend-developer → UI components
@backend-architect → API design
@database-architect → Schema design

# Then combine:
@task-planner → integrate results
```

### Iterative Refinement

Use when quality requires iteration:

```
loop until @output-critic approves:
    @{developer} → implement/refine
    @output-critic → review and feedback
```

## Customizing Workflows

Adapt workflows to your needs:

1. **Skip steps** that don't apply to your task
2. **Add steps** for your specific requirements
3. **Change agents** based on domain (e.g., @rust-pro vs @python-pro)
4. **Adjust checkpoints** for your risk tolerance

## Best Practices

1. **Start with planning** — @task-planner prevents wasted work
2. **Understand before changing** — @codebase-navigator first
3. **Review significant work** — @output-critic catches issues
4. **Document decisions** — Use /q5-decide for important choices
5. **Test before deploying** — @test-strategist plans coverage
