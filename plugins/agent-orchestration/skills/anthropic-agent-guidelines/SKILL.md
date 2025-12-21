---
name: anthropic-agent-guidelines
description: Official best practices from Anthropic for building effective AI agents. Covers tool design, agentic loops, error handling, and safety patterns.
---

# Anthropic Agent Guidelines

Best practices for building effective AI agents based on Anthropic's official guidance.

## Tool Design Principles

### 1. Extremely Detailed Descriptions
Tool descriptions should be comprehensive and anticipate edge cases:

```json
{
  "name": "execute_sql",
  "description": "Execute a SQL query against the database. Returns results as JSON array. 
    
IMPORTANT CONSTRAINTS:
- Only SELECT queries allowed (no INSERT, UPDATE, DELETE)
- Maximum 1000 rows returned (use LIMIT)
- Timeout after 30 seconds
- Table names are case-sensitive

COMMON TABLES:
- users (id, email, created_at, status)
- orders (id, user_id, total, status, created_at)
- products (id, name, price, inventory)

EXAMPLES:
- Get active users: SELECT * FROM users WHERE status = 'active' LIMIT 100
- Order count by user: SELECT user_id, COUNT(*) FROM orders GROUP BY user_id

IF QUERY FAILS:
- Check table/column names for typos
- Verify JOIN conditions
- Ensure WHERE clause types match column types"
}
```

### 2. Anticipate Edge Cases
Include handling instructions in tool descriptions:

```json
{
  "name": "send_email",
  "description": "Send an email to specified recipients.

EDGE CASES:
- Empty recipient list: Return error, don't send
- Invalid email format: Return validation error with details
- Rate limit hit: Return 'retry_after' seconds, suggest batching
- Large attachment: Maximum 10MB, return error if exceeded

WHEN TO USE:
- Sending notifications to users
- Sharing reports or documents
- Follow-up communications

WHEN NOT TO USE:
- Bulk marketing (use campaign_email instead)
- Transactional emails (use transactional_email)
- Internal team messages (use slack_message)"
}
```

### 3. Tools for Structured Output
Use tools to get structured responses, not just for external actions:

```json
{
  "name": "provide_analysis",
  "description": "Structure your analysis in a consistent format.",
  "parameters": {
    "summary": "One-paragraph summary of findings",
    "confidence": "low | medium | high",
    "key_findings": ["Array of main discoveries"],
    "recommendations": ["Array of suggested actions"],
    "risks": ["Array of potential issues"],
    "next_steps": ["Array of follow-up actions"]
  }
}
```

## Agentic Loop Patterns

### Checkpoints for Long Tasks
Implement explicit checkpoints:

```python
async def agentic_task(goal: str):
    plan = await create_plan(goal)
    
    for i, step in enumerate(plan.steps):
        # Checkpoint before potentially risky steps
        if step.is_destructive or step.requires_approval:
            await request_human_approval(step)
        
        result = await execute_step(step)
        
        # Checkpoint after significant progress
        if (i + 1) % 5 == 0:
            await save_checkpoint(plan, completed=i+1)
        
        # Check for stop conditions
        if result.requires_clarification:
            return await request_clarification(result.question)
```

### Stop and Ask Conditions
Define explicit conditions for pausing:

```markdown
## Stop and Ask When:
1. **Ambiguous Requirements**
   - Multiple valid interpretations exist
   - Success criteria are unclear
   
2. **High Risk Actions**
   - Deleting data or files
   - Modifying production systems
   - Actions that can't be easily undone
   
3. **Unexpected State**
   - Assumptions don't match reality
   - Error conditions not in the plan
   
4. **Significant Decisions**
   - Choosing between major architectural approaches
   - Trade-offs that affect performance/cost/security
```

### Reasoning Logs
Maintain explicit reasoning for debugging:

```python
class AgentContext:
    def __init__(self):
        self.reasoning_log = []
    
    def log_decision(self, decision: str, rationale: str, alternatives: list):
        self.reasoning_log.append({
            "timestamp": datetime.now(),
            "decision": decision,
            "rationale": rationale,
            "alternatives_considered": alternatives
        })
    
    def log_observation(self, observation: str, implications: list):
        self.reasoning_log.append({
            "timestamp": datetime.now(),
            "observation": observation,
            "implications": implications
        })
```

## Error Handling

### Retry with Exponential Backoff
```python
async def resilient_tool_call(tool, params, max_retries=3):
    for attempt in range(max_retries):
        try:
            return await tool.execute(params)
        except TransientError as e:
            if attempt == max_retries - 1:
                raise
            wait_time = 2 ** attempt  # 1, 2, 4 seconds
            await asyncio.sleep(wait_time)
        except PermanentError:
            raise  # Don't retry permanent failures
```

### Graceful Degradation
```python
async def get_user_context(user_id: str) -> UserContext:
    context = UserContext()
    
    # Try to get full context, degrade gracefully
    try:
        context.preferences = await get_preferences(user_id)
    except ServiceUnavailable:
        context.preferences = default_preferences()
        context.warnings.append("Using default preferences")
    
    try:
        context.history = await get_history(user_id)
    except ServiceUnavailable:
        context.history = []
        context.warnings.append("History unavailable")
    
    return context
```

### Helpful Error Messages
```python
class ToolError(Exception):
    def __init__(self, message: str, suggestion: str = None, 
                 retry_after: int = None):
        self.message = message
        self.suggestion = suggestion
        self.retry_after = retry_after
    
    def to_agent_message(self):
        msg = f"Error: {self.message}"
        if self.suggestion:
            msg += f"\nSuggestion: {self.suggestion}"
        if self.retry_after:
            msg += f"\nRetry after: {self.retry_after} seconds"
        return msg

# Usage
raise ToolError(
    message="Database query timed out",
    suggestion="Try adding a LIMIT clause or more specific WHERE conditions",
    retry_after=5
)
```

## Safety Patterns

### Confirmation for Destructive Actions
```python
def execute_with_confirmation(action: Action) -> Result:
    if action.is_destructive:
        preview = generate_preview(action)
        confirmed = request_confirmation(
            f"This will: {preview}\n\nProceed? (yes/no)"
        )
        if not confirmed:
            return Result.cancelled("User declined")
    
    return execute(action)
```

### Scope Limiting
```python
class ScopedAgent:
    def __init__(self, allowed_paths: list[str], allowed_tools: list[str]):
        self.allowed_paths = allowed_paths
        self.allowed_tools = allowed_tools
    
    def can_access(self, path: str) -> bool:
        return any(path.startswith(p) for p in self.allowed_paths)
    
    def can_use(self, tool: str) -> bool:
        return tool in self.allowed_tools
```

### Audit Logging
```python
def audited_action(action_type: str):
    def decorator(func):
        async def wrapper(*args, **kwargs):
            log_entry = {
                "action": action_type,
                "args": sanitize_for_log(args),
                "timestamp": datetime.now(),
                "agent_id": get_current_agent_id()
            }
            
            try:
                result = await func(*args, **kwargs)
                log_entry["status"] = "success"
                return result
            except Exception as e:
                log_entry["status"] = "error"
                log_entry["error"] = str(e)
                raise
            finally:
                await audit_log.write(log_entry)
        
        return wrapper
    return decorator
```

## Checklist

### Tool Design
- [ ] Descriptions are comprehensive (200+ words for complex tools)
- [ ] Edge cases are documented with handling instructions
- [ ] Examples show common usage patterns
- [ ] Clear guidance on when to use vs. alternatives

### Agentic Loops
- [ ] Checkpoints implemented for long-running tasks
- [ ] Explicit stop-and-ask conditions defined
- [ ] Reasoning logged for debugging
- [ ] Progress can be saved and resumed

### Error Handling
- [ ] Transient errors retried with backoff
- [ ] Permanent errors fail fast
- [ ] Graceful degradation when possible
- [ ] Error messages help the agent recover

### Safety
- [ ] Destructive actions require confirmation
- [ ] Agent scope is limited appropriately
- [ ] All actions are audit logged
- [ ] Rollback procedures exist for critical operations

