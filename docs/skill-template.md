# Skill Template with Progressive Disclosure

Use this template when creating new skills to maximize context efficiency.

## Frontmatter Schema

```yaml
---
name: skill-name
description: One-line description for discovery and filtering.

# TIER 1: Quick Reference (loaded first, always visible)
summary: |
  - Key point 1 (actionable)
  - Key point 2 (actionable)
  - Key point 3 (actionable)
  - Primary command or pattern

# Context Management
context_cost: low | medium | high # Token impact when fully loaded
load_when: # Trigger phrases for auto-loading
  - 'relevant phrase 1'
  - 'relevant phrase 2'

# Optional: Dependencies
requires: # Other skills this depends on
  - other-skill-name
enhances: # Skills this adds value to
  - related-skill-name
---
```

## Content Structure

### Tier 1: Summary (in frontmatter)

- 3-5 bullet points
- Immediately actionable
- No code blocks
- < 200 tokens

### Tier 2: Core Content (SKILL.md body)

- When to use this skill
- Core concepts (brief)
- Primary patterns
- Common commands
- < 1000 tokens ideal

### Tier 3: Extended Content (separate files)

- Detailed templates
- Complex examples
- Edge cases
- Reference material

## Directory Structure

```
skills/my-skill/
├── SKILL.md           # Tier 1 + 2: Frontmatter + Core
├── templates.md       # Tier 3: Code templates
├── examples.md        # Tier 3: Detailed examples
├── reference.md       # Tier 3: API reference
└── scripts/           # Tier 3: Helper scripts
    └── helper.py
```

## Example: Well-Structured Skill

```yaml
---
name: api-rate-limiting
description: Implement rate limiting for APIs using token bucket and sliding window algorithms.

summary: |
  - Token bucket: `rate_limiter = TokenBucket(rate=100, capacity=1000)`
  - Sliding window: Better for bursty traffic
  - Redis recommended for distributed systems
  - Return 429 with Retry-After header

context_cost: medium
load_when:
  - "rate limit"
  - "throttling"
  - "429 error"
  - "API abuse prevention"

requires:
  - redis-patterns
enhances:
  - api-design-principles
---

# API Rate Limiting

## When to Use
- Protecting APIs from abuse
- Ensuring fair resource usage
- Meeting SLA requirements

## Core Patterns

### Token Bucket (Recommended)
[Brief explanation + minimal code]

### Sliding Window
[Brief explanation + minimal code]

## Quick Reference
| Algorithm | Use Case | Complexity |
|-----------|----------|------------|
| Token Bucket | General purpose | Low |
| Sliding Window | Precise limits | Medium |
| Leaky Bucket | Smooth output | Medium |

---
*For detailed implementations, see [templates.md](./templates.md)*
```

## Anti-Patterns

❌ **Don't**: Put everything in one large file
❌ **Don't**: Skip the summary
❌ **Don't**: Include extensive code in Tier 2
❌ **Don't**: Forget context_cost estimation

✅ **Do**: Keep SKILL.md focused and concise
✅ **Do**: Use summary for quick decisions
✅ **Do**: Split templates into separate files
✅ **Do**: Include load_when triggers
