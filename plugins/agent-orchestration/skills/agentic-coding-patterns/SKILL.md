---
name: agentic-coding-patterns
description: Best practices for writing code that works well with AI assistants. Covers code structure, documentation, and patterns that enable effective AI collaboration.

summary: |
  - Use explicit types over implicit magic (AI needs clarity)
  - Self-documenting structure: features/, shared/, types.ts
  - Include "why" in docstrings, not just "what"
  - Typed errors with context: `InsufficientInventoryError(product_id, requested, available)`
  - Factories over fixtures in tests for clear intent

context_cost: medium
load_when:
  - "ai-friendly code"
  - "writing for claude"
  - "code structure"
  - "documentation patterns"
---

# Agentic Coding Patterns

Patterns and practices for writing code that AI assistants can understand, modify, and extend effectively.

## Core Principles

### 1. Explicit Over Implicit
AI works best with explicit, clear code rather than clever implicit patterns.

```python
# ❌ Implicit - AI may miss the magic
class User(metaclass=AutoValidatingMeta):
    name: str
    email: str

# ✅ Explicit - AI understands the validation
class User(BaseModel):
    name: str = Field(..., min_length=1, max_length=100)
    email: EmailStr
    
    @validator('name')
    def validate_name(cls, v):
        return v.strip()
```

### 2. Self-Documenting Structure
Code organization should reveal intent.

```
# ✅ Clear structure
src/
├── features/
│   └── user-registration/
│       ├── api.py           # HTTP handlers
│       ├── service.py       # Business logic
│       ├── repository.py    # Data access
│       └── types.py         # Type definitions
└── shared/
    ├── auth/
    └── database/
```

### 3. Type Everything
Types are documentation that AI can reason about.

```typescript
// ❌ AI must guess the shape
function processOrder(order, options) {
  // ...
}

// ✅ AI understands the contract
interface Order {
  id: string;
  items: OrderItem[];
  status: OrderStatus;
}

interface ProcessOptions {
  validateInventory: boolean;
  sendNotification: boolean;
}

function processOrder(order: Order, options: ProcessOptions): Promise<ProcessedOrder> {
  // ...
}
```

## Documentation Patterns

### Function-Level Context
Include "why" not just "what":

```python
def calculate_risk_score(portfolio: Portfolio) -> float:
    """
    Calculate portfolio risk using modified VaR approach.
    
    Why: Standard VaR underestimates tail risk; we use CVaR
    with 99% confidence for regulatory compliance.
    
    Context: Called during daily risk assessment (5am UTC)
    and before any trade execution.
    
    Args:
        portfolio: Current holdings with market values
        
    Returns:
        Risk score between 0.0 (no risk) and 1.0 (maximum risk)
        
    Raises:
        InsufficientDataError: If < 252 days of price history
    """
```

### Module-Level README
Each significant module should have a README:

```markdown
# User Registration Module

## Purpose
Handles new user signups with email verification.

## Key Flows
1. User submits registration form
2. Validate email uniqueness
3. Create pending user record
4. Send verification email
5. User clicks link, account activated

## Integration Points
- **Auth Service**: Creates session after activation
- **Email Service**: Sends verification emails
- **Analytics**: Tracks signup funnel

## Configuration
- `VERIFICATION_TTL`: How long links are valid (default: 24h)
- `MAX_ATTEMPTS`: Rate limiting for resend (default: 3/hour)

## Testing
Run `pytest tests/user_registration/` for full suite
```

## Error Handling Patterns

### Typed Errors with Context
```python
class OrderError(Exception):
    """Base for order-related errors."""
    pass

class InsufficientInventoryError(OrderError):
    """Raised when product inventory is too low."""
    
    def __init__(self, product_id: str, requested: int, available: int):
        self.product_id = product_id
        self.requested = requested
        self.available = available
        super().__init__(
            f"Product {product_id}: requested {requested}, "
            f"only {available} available"
        )
```

### Error Boundaries
```typescript
// Clear error handling at boundaries
async function handleCreateOrder(req: Request): Promise<Response> {
  try {
    const order = await orderService.create(req.body);
    return Response.json(order, { status: 201 });
  } catch (error) {
    if (error instanceof ValidationError) {
      return Response.json({ error: error.details }, { status: 400 });
    }
    if (error instanceof InsufficientInventoryError) {
      return Response.json({ 
        error: 'Out of stock',
        product: error.productId 
      }, { status: 409 });
    }
    // Unknown error - log and return generic message
    logger.error('Order creation failed', { error });
    return Response.json({ error: 'Internal error' }, { status: 500 });
  }
}
```

## Configuration Patterns

### Centralized, Typed Config
```typescript
// config/index.ts
import { z } from 'zod';

const ConfigSchema = z.object({
  database: z.object({
    url: z.string().url(),
    poolSize: z.number().min(1).max(100).default(10),
  }),
  redis: z.object({
    url: z.string().url(),
    ttl: z.number().default(3600),
  }),
  features: z.object({
    newCheckout: z.boolean().default(false),
    betaUsers: z.array(z.string()).default([]),
  }),
});

export type Config = z.infer<typeof ConfigSchema>;

export const config = ConfigSchema.parse({
  database: {
    url: process.env.DATABASE_URL,
    poolSize: parseInt(process.env.DB_POOL_SIZE || '10'),
  },
  // ...
});
```

## Testing Patterns

### Factories Over Fixtures
```python
# ✅ Factories make test intent clear
def test_order_total_with_discount():
    user = UserFactory.create(membership='premium')
    product = ProductFactory.create(price=100.00)
    order = OrderFactory.create(
        user=user,
        items=[OrderItemFactory.create(product=product, quantity=2)]
    )
    
    assert order.total == 180.00  # 10% premium discount
```

### Descriptive Test Names
```python
# ✅ Tests document behavior
def test_user_cannot_register_with_existing_email():
    ...

def test_order_is_cancelled_when_payment_fails_after_3_retries():
    ...

def test_notification_is_sent_when_inventory_drops_below_threshold():
    ...
```

## AI-Friendly Patterns Checklist

- [ ] All public functions have type annotations
- [ ] Complex logic has inline comments explaining "why"
- [ ] Modules have README.md with purpose and integration points
- [ ] Errors are typed with context information
- [ ] Configuration is centralized and validated
- [ ] Tests use descriptive names that document behavior
- [ ] Magic strings are constants with documentation
- [ ] Dependencies are injected, not imported directly

