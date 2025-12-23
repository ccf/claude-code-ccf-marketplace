---
name: context-optimization
description: Techniques for managing context windows effectively when working with AI assistants. Covers progressive disclosure, context budgeting, and efficient information loading.

summary: |
  - Budget: System 10%, History 25%, Active 45%, Response 20%
  - Load in tiers: Metadata → Signatures → Full implementation
  - Never load entire large files; use semantic search
  - Refresh context at task boundaries
  - Summarize, don't dump; elide middle sections

context_cost: low
load_when:
  - "context window"
  - "token limit"
  - "too much context"
  - "context management"
---

# Context Optimization

Strategies for making the most of limited context windows when working with AI.

## Core Concept: Context Budget

Every AI interaction has a finite context window. Use it wisely:

```
┌─────────────────────────────────────────┐
│           Context Window                │
├─────────────────────────────────────────┤
│ System Prompt        │ ~5-10%           │
│ Conversation History │ ~20-30%          │
│ Active Context       │ ~40-50%  ← Focus │
│ Response Space       │ ~20%             │
└─────────────────────────────────────────┘
```

## Progressive Disclosure

Load information in layers, starting with summaries:

### Tier 1: Metadata Only
```markdown
## Available Files
- `src/auth/service.ts` (245 lines) - Authentication service
- `src/auth/middleware.ts` (89 lines) - Auth middleware
- `src/auth/types.ts` (34 lines) - Type definitions
```

### Tier 2: Signatures & Structure
```typescript
// src/auth/service.ts - Key exports
export class AuthService {
  async login(email: string, password: string): Promise<Session>;
  async logout(sessionId: string): Promise<void>;
  async validateSession(token: string): Promise<User | null>;
  async refreshToken(refreshToken: string): Promise<TokenPair>;
}
```

### Tier 3: Full Implementation
Only load when actively working on specific functions.

## Context Loading Strategies

### Strategy 1: Just-In-Time Loading
```markdown
## Task: Fix login bug

### Initial Context (Tier 1)
- Project structure overview
- Bug report details

### On-Demand (Tier 2)
- Auth service interface when discussing approach

### Deep Dive (Tier 3)
- Full login() implementation when fixing
```

### Strategy 2: Breadth-First Exploration
```markdown
## Task: Understand codebase

1. Load all README files (summaries)
2. Load package.json / pyproject.toml (dependencies)
3. Load key types/interfaces (contracts)
4. Load specific implementations as needed
```

### Strategy 3: Depth-First Investigation
```markdown
## Task: Trace specific bug

1. Start from error location
2. Load calling function
3. Load dependencies of that function
4. Work outward until root cause found
```

## Chunking Patterns

### By Functionality
```markdown
✅ Good chunks:
- Complete function with docstring
- Related functions that work together
- Type definitions used by a module

❌ Bad chunks:
- Half a function
- Random lines from different files
- Mixed concerns
```

### By Dependencies
```markdown
When loading code, include:
1. The target function/class
2. Type definitions it uses
3. Key dependencies it calls
4. NOT: unrelated code in same file
```

## Context Compression Techniques

### Summarization
```markdown
## Module Summary: Payment Processing

### Purpose
Handles payment transactions via Stripe.

### Key Functions
- `createPayment(amount, customer)` - Initiates payment
- `confirmPayment(paymentId)` - Completes after 3DS
- `refundPayment(paymentId, reason)` - Full or partial refund

### Dependencies
- Stripe SDK (external)
- CustomerService (internal)
- TransactionLog (internal)

### Common Errors
- `PaymentDeclined` - Card rejected
- `InsufficientFunds` - Not enough balance
```

### Elision
```python
def complex_function(data):
    # Validation (50 lines)
    # ... validation logic ...
    
    # Core processing (what you need to see)
    result = process_core_logic(data)
    
    # Cleanup (30 lines)
    # ... cleanup logic ...
    
    return result
```

## Working with Large Files

### Don't Load Entire Files
```markdown
❌ "Show me src/services/order.ts" (2000 lines)

✅ "Show me the createOrder function in src/services/order.ts"
✅ "What functions are exported from src/services/order.ts?"
✅ "Show lines 150-200 of src/services/order.ts"
```

### Use Semantic Search
```markdown
✅ "Find where user sessions are validated"
✅ "Show code that handles payment failures"
✅ "Where is the discount calculation logic?"
```

## Context Refresh Patterns

### When to Refresh
- Starting a new subtask
- After significant file changes
- When conversation becomes confused
- Before final review/commit

### How to Refresh
```markdown
## Context Refresh

### Current Task
[Restate what we're doing]

### Key Files
- `file1.ts` - [brief purpose]
- `file2.ts` - [brief purpose]

### Progress
- [x] Step 1
- [ ] Step 2 (current)
- [ ] Step 3

### Decisions Made
- Using approach X because Y
- Not doing Z because W
```

## Anti-Patterns

### Context Pollution
```markdown
❌ Loading entire codebase "just in case"
❌ Keeping irrelevant conversation history
❌ Copy-pasting full stack traces when one frame matters
```

### Context Starvation
```markdown
❌ Not providing enough context for the task
❌ Assuming AI remembers from 50 messages ago
❌ Not refreshing context after major changes
```

## Checklist

- [ ] Start with high-level overview, drill down as needed
- [ ] Load only code relevant to current task
- [ ] Include type definitions when loading implementations
- [ ] Summarize large files instead of loading entirely
- [ ] Refresh context at task boundaries
- [ ] State current goal when context might be ambiguous

