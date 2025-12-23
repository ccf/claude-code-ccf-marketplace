---
name: nodejs-backend-patterns
description: Build production-ready Node.js backends with Express/Fastify, middleware, auth, and database patterns.

summary: |
  - Fastify preferred for performance; Express for ecosystem
  - Structure: routes/ → controllers/ → services/ → repositories/
  - Always: helmet, cors, compression, rate-limiting
  - Error handling: centralized middleware with typed errors
  - Validation: Zod/Yup at API boundary

context_cost: high
load_when:
  - "nodejs backend"
  - "express setup"
  - "fastify"
  - "api server"
  - "node microservice"

enhances:
  - javascript-testing-patterns
  - typescript-advanced-types
---

# Node.js Backend Patterns

Production-ready patterns for Node.js servers and APIs.

## When to Use

- Building REST APIs or GraphQL servers
- Creating microservices
- Implementing authentication and authorization
- Designing scalable backend architectures

## Framework Selection

| Framework | Strength | Use When |
|-----------|----------|----------|
| **Fastify** | Performance, TypeScript | New projects, high-throughput |
| **Express** | Ecosystem, simplicity | Rapid prototyping, rich middleware |
| **NestJS** | Structure, enterprise | Large teams, complex apps |

## Quick Setup

### Fastify (Recommended)

```typescript
import Fastify from 'fastify';
import helmet from '@fastify/helmet';
import cors from '@fastify/cors';

const app = Fastify({ logger: true });

await app.register(helmet);
await app.register(cors, { origin: true });

app.get('/health', async () => ({ status: 'ok' }));

await app.listen({ port: 3000 });
```

### Express

```typescript
import express from 'express';
import helmet from 'helmet';
import cors from 'cors';

const app = express();

app.use(helmet());
app.use(cors());
app.use(express.json());

app.get('/health', (req, res) => res.json({ status: 'ok' }));

app.listen(3000);
```

## Project Structure

```
src/
├── routes/          # Route definitions
├── controllers/     # Request handling
├── services/        # Business logic
├── repositories/    # Data access
├── middleware/      # Custom middleware
├── utils/           # Helpers
├── types/           # TypeScript types
└── config/          # Configuration
```

## Error Handling

```typescript
// errors/AppError.ts
export class AppError extends Error {
  constructor(
    public statusCode: number,
    public code: string,
    message: string
  ) {
    super(message);
  }
}

// middleware/errorHandler.ts
export const errorHandler = (err, req, res, next) => {
  if (err instanceof AppError) {
    return res.status(err.statusCode).json({
      error: err.code,
      message: err.message,
    });
  }
  
  console.error(err);
  res.status(500).json({ error: 'INTERNAL_ERROR' });
};
```

## Validation (Zod)

```typescript
import { z } from 'zod';

const createUserSchema = z.object({
  email: z.string().email(),
  name: z.string().min(2).max(100),
  age: z.number().int().positive().optional(),
});

app.post('/users', async (req, res) => {
  const result = createUserSchema.safeParse(req.body);
  if (!result.success) {
    return res.status(400).json({ errors: result.error.flatten() });
  }
  // result.data is typed
});
```

## Authentication

```typescript
import jwt from 'jsonwebtoken';

export const authMiddleware = (req, res, next) => {
  const token = req.headers.authorization?.replace('Bearer ', '');
  if (!token) return res.status(401).json({ error: 'Unauthorized' });
  
  try {
    req.user = jwt.verify(token, process.env.JWT_SECRET);
    next();
  } catch {
    res.status(401).json({ error: 'Invalid token' });
  }
};
```

---

*For database patterns, see [database.md](./database.md)*
*For middleware examples, see [middleware.md](./middleware.md)*
