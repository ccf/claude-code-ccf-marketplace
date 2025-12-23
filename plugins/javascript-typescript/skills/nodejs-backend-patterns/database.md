# Database Patterns

Database integration patterns for Node.js backends.

## Prisma (Recommended)

```typescript
// prisma/schema.prisma
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

model User {
  id        String   @id @default(uuid())
  email     String   @unique
  name      String?
  posts     Post[]
  createdAt DateTime @default(now())
}

model Post {
  id        String   @id @default(uuid())
  title     String
  content   String?
  author    User     @relation(fields: [authorId], references: [id])
  authorId  String
}
```

```typescript
// repositories/user.repository.ts
import { PrismaClient } from '@prisma/client';

const prisma = new PrismaClient();

export const userRepository = {
  findById: (id: string) => 
    prisma.user.findUnique({ where: { id } }),

  findByEmail: (email: string) => 
    prisma.user.findUnique({ where: { email } }),

  create: (data: { email: string; name?: string }) => 
    prisma.user.create({ data }),

  update: (id: string, data: Partial<User>) => 
    prisma.user.update({ where: { id }, data }),

  findWithPosts: (id: string) => 
    prisma.user.findUnique({
      where: { id },
      include: { posts: true },
    }),
};
```

## Drizzle ORM

```typescript
import { pgTable, uuid, text, timestamp } from 'drizzle-orm/pg-core';
import { drizzle } from 'drizzle-orm/node-postgres';

export const users = pgTable('users', {
  id: uuid('id').primaryKey().defaultRandom(),
  email: text('email').notNull().unique(),
  name: text('name'),
  createdAt: timestamp('created_at').defaultNow(),
});

const db = drizzle(pool);

// Queries
const allUsers = await db.select().from(users);
const user = await db.select().from(users).where(eq(users.id, id));
```

## Connection Pooling

```typescript
import { Pool } from 'pg';

const pool = new Pool({
  connectionString: process.env.DATABASE_URL,
  max: 20,
  idleTimeoutMillis: 30000,
  connectionTimeoutMillis: 2000,
});

// Graceful shutdown
process.on('SIGTERM', async () => {
  await pool.end();
  process.exit(0);
});
```

## Transactions

```typescript
// Prisma
await prisma.$transaction(async (tx) => {
  const user = await tx.user.create({ data: userData });
  await tx.profile.create({ data: { userId: user.id, ...profileData } });
  return user;
});

// Raw SQL
const client = await pool.connect();
try {
  await client.query('BEGIN');
  await client.query('INSERT INTO users...');
  await client.query('INSERT INTO profiles...');
  await client.query('COMMIT');
} catch (e) {
  await client.query('ROLLBACK');
  throw e;
} finally {
  client.release();
}
```

## Redis Caching

```typescript
import Redis from 'ioredis';

const redis = new Redis(process.env.REDIS_URL);

export const cache = {
  get: async <T>(key: string): Promise<T | null> => {
    const data = await redis.get(key);
    return data ? JSON.parse(data) : null;
  },

  set: async <T>(key: string, value: T, ttl = 3600) => {
    await redis.setex(key, ttl, JSON.stringify(value));
  },

  del: async (key: string) => {
    await redis.del(key);
  },
};

// Usage with caching
export const getUser = async (id: string) => {
  const cached = await cache.get<User>(`user:${id}`);
  if (cached) return cached;

  const user = await userRepository.findById(id);
  if (user) await cache.set(`user:${id}`, user);
  return user;
};
```

