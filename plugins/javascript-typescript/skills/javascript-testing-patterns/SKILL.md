---
name: javascript-testing-patterns
description: Comprehensive testing strategies using Jest, Vitest, and Testing Library for JS/TS applications.

summary: |
  - Jest: `npm i -D jest @types/jest ts-jest` + `jest.config.ts`
  - Vitest: `npm i -D vitest` + `vitest.config.ts` (faster, Vite-native)
  - Structure: Arrange → Act → Assert (AAA pattern)
  - Mock modules: `jest.mock('./module')` or `vi.mock('./module')`
  - Coverage: aim for 80%+ on branches, functions, lines

context_cost: high
load_when:
  - "testing javascript"
  - "jest setup"
  - "vitest"
  - "testing library"
  - "mock functions"

enhances:
  - modern-javascript-patterns
  - nodejs-backend-patterns
---

# JavaScript Testing Patterns

Modern testing strategies for JavaScript/TypeScript applications.

## When to Use

- Setting up test infrastructure for new projects
- Writing unit tests for functions and classes
- Creating integration tests for APIs
- Testing React, Vue, or frontend components
- Implementing test-driven development (TDD)

## Quick Setup

### Jest

```typescript
// jest.config.ts
import type { Config } from 'jest';

const config: Config = {
  preset: 'ts-jest',
  testEnvironment: 'node',
  roots: ['<rootDir>/src'],
  testMatch: ['**/__tests__/**/*.ts', '**/?(*.)+(spec|test).ts'],
  coverageThreshold: {
    global: { branches: 80, functions: 80, lines: 80, statements: 80 },
  },
};

export default config;
```

### Vitest (Faster)

```typescript
// vitest.config.ts
import { defineConfig } from 'vitest/config';

export default defineConfig({
  test: {
    globals: true,
    environment: 'node',
    coverage: { provider: 'v8', reporter: ['text', 'html'] },
  },
});
```

## Core Patterns

### AAA Pattern (Arrange-Act-Assert)

```typescript
describe('UserService', () => {
  it('creates user with valid data', async () => {
    // Arrange
    const userData = { email: 'test@example.com', name: 'Test' };
    const mockRepo = { save: jest.fn().mockResolvedValue({ id: '1', ...userData }) };
    const service = new UserService(mockRepo);

    // Act
    const result = await service.createUser(userData);

    // Assert
    expect(result.id).toBeDefined();
    expect(mockRepo.save).toHaveBeenCalledWith(userData);
  });
});
```

### Mocking

```typescript
// Mock module
jest.mock('./database', () => ({
  query: jest.fn().mockResolvedValue([{ id: 1 }]),
}));

// Mock function
const mockFn = jest.fn()
  .mockReturnValueOnce('first')
  .mockReturnValueOnce('second');

// Spy on existing method
const spy = jest.spyOn(console, 'log').mockImplementation();
```

### Async Testing

```typescript
it('fetches data successfully', async () => {
  const data = await fetchData();
  expect(data).toHaveProperty('users');
});

it('rejects with error', async () => {
  await expect(fetchInvalidData()).rejects.toThrow('Not found');
});
```

## Testing React Components

```typescript
import { render, screen, fireEvent } from '@testing-library/react';

it('handles click events', async () => {
  render(<Counter />);
  
  const button = screen.getByRole('button', { name: /increment/i });
  await fireEvent.click(button);
  
  expect(screen.getByText('Count: 1')).toBeInTheDocument();
});
```

## Commands

```bash
# Run all tests
npm test

# Watch mode
npm test -- --watch

# Coverage report
npm test -- --coverage

# Run specific file
npm test -- user.test.ts
```

---

*For complete examples, see [examples.md](./examples.md)*
*For mocking patterns, see [mocking.md](./mocking.md)*
