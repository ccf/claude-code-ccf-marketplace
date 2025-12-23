# Middleware Patterns

Common middleware implementations for Node.js backends.

## Rate Limiting

```typescript
import rateLimit from 'express-rate-limit';

export const apiLimiter = rateLimit({
  windowMs: 15 * 60 * 1000, // 15 minutes
  max: 100,
  message: { error: 'Too many requests' },
  standardHeaders: true,
  legacyHeaders: false,
});

// Per-route limits
export const authLimiter = rateLimit({
  windowMs: 60 * 60 * 1000, // 1 hour
  max: 5, // 5 attempts per hour
  message: { error: 'Too many login attempts' },
});
```

## Request Logging

```typescript
import morgan from 'morgan';
import { v4 as uuid } from 'uuid';

// Add request ID
app.use((req, res, next) => {
  req.id = uuid();
  res.setHeader('X-Request-ID', req.id);
  next();
});

// Custom morgan format
morgan.token('id', (req) => req.id);
app.use(morgan(':id :method :url :status :response-time ms'));
```

## Request Validation

```typescript
import { z, ZodSchema } from 'zod';

export const validate = (schema: ZodSchema) => {
  return (req, res, next) => {
    const result = schema.safeParse({
      body: req.body,
      query: req.query,
      params: req.params,
    });

    if (!result.success) {
      return res.status(400).json({
        error: 'Validation failed',
        details: result.error.flatten(),
      });
    }

    req.validated = result.data;
    next();
  };
};

// Usage
const createUserSchema = z.object({
  body: z.object({
    email: z.string().email(),
    name: z.string().min(2),
  }),
});

app.post('/users', validate(createUserSchema), createUser);
```

## CORS Configuration

```typescript
import cors from 'cors';

const corsOptions = {
  origin: (origin, callback) => {
    const allowedOrigins = process.env.ALLOWED_ORIGINS?.split(',') || [];
    if (!origin || allowedOrigins.includes(origin)) {
      callback(null, true);
    } else {
      callback(new Error('Not allowed by CORS'));
    }
  },
  credentials: true,
  methods: ['GET', 'POST', 'PUT', 'DELETE', 'PATCH'],
  allowedHeaders: ['Content-Type', 'Authorization'],
};

app.use(cors(corsOptions));
```

## Request Timeout

```typescript
import timeout from 'connect-timeout';

app.use(timeout('30s'));

app.use((req, res, next) => {
  if (!req.timedout) next();
});
```

## Compression

```typescript
import compression from 'compression';

app.use(compression({
  filter: (req, res) => {
    if (req.headers['x-no-compression']) return false;
    return compression.filter(req, res);
  },
  threshold: 1024, // Only compress > 1KB
}));
```

## Security Headers

```typescript
import helmet from 'helmet';

app.use(helmet({
  contentSecurityPolicy: {
    directives: {
      defaultSrc: ["'self'"],
      styleSrc: ["'self'", "'unsafe-inline'"],
      scriptSrc: ["'self'"],
      imgSrc: ["'self'", "data:", "https:"],
    },
  },
  hsts: {
    maxAge: 31536000,
    includeSubDomains: true,
  },
}));
```

## Async Handler Wrapper

```typescript
// Catch async errors without try-catch
export const asyncHandler = (fn: RequestHandler) => {
  return (req: Request, res: Response, next: NextFunction) => {
    Promise.resolve(fn(req, res, next)).catch(next);
  };
};

// Usage
app.get('/users/:id', asyncHandler(async (req, res) => {
  const user = await userService.findById(req.params.id);
  if (!user) throw new NotFoundError('User not found');
  res.json(user);
}));
```

