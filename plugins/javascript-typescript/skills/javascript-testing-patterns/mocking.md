# Mocking Patterns

Advanced mocking strategies for JavaScript testing.

## Module Mocking

### Jest

```typescript
// Auto-mock entire module
jest.mock('./database');

// Partial mock (keep some original implementations)
jest.mock('./utils', () => ({
  ...jest.requireActual('./utils'),
  fetchData: jest.fn().mockResolvedValue({ data: 'mocked' }),
}));

// Manual mock file: __mocks__/database.ts
export const query = jest.fn().mockResolvedValue([]);
export const connect = jest.fn().mockResolvedValue(true);
```

### Vitest

```typescript
// Mock module
vi.mock('./database', () => ({
  query: vi.fn().mockResolvedValue([]),
}));

// Inline mock with factory
vi.mock('./api', async () => {
  const actual = await vi.importActual('./api');
  return {
    ...actual,
    fetchUsers: vi.fn().mockResolvedValue([]),
  };
});
```

## HTTP Mocking

### MSW (Mock Service Worker)

```typescript
import { setupServer } from 'msw/node';
import { http, HttpResponse } from 'msw';

const server = setupServer(
  http.get('/api/users', () => {
    return HttpResponse.json([
      { id: 1, name: 'John' },
      { id: 2, name: 'Jane' },
    ]);
  }),

  http.post('/api/users', async ({ request }) => {
    const body = await request.json();
    return HttpResponse.json({ id: 3, ...body }, { status: 201 });
  }),

  http.get('/api/users/:id', ({ params }) => {
    return HttpResponse.json({ id: params.id, name: 'User' });
  })
);

beforeAll(() => server.listen());
afterEach(() => server.resetHandlers());
afterAll(() => server.close());
```

### Nock (Node.js)

```typescript
import nock from 'nock';

beforeEach(() => {
  nock('https://api.example.com')
    .get('/users')
    .reply(200, [{ id: 1, name: 'John' }]);
});

afterEach(() => {
  nock.cleanAll();
});
```

## Timer Mocking

```typescript
// Jest
beforeEach(() => {
  jest.useFakeTimers();
});

afterEach(() => {
  jest.useRealTimers();
});

it('debounces function calls', () => {
  const callback = jest.fn();
  const debounced = debounce(callback, 1000);

  debounced();
  debounced();
  debounced();

  expect(callback).not.toHaveBeenCalled();
  
  jest.advanceTimersByTime(1000);
  
  expect(callback).toHaveBeenCalledTimes(1);
});
```

## Spying

```typescript
// Spy on method
const consoleSpy = jest.spyOn(console, 'log').mockImplementation();

// Spy on object method
const userSpy = jest.spyOn(userService, 'findById');

// Verify calls
expect(consoleSpy).toHaveBeenCalledWith('Hello');
expect(userSpy).toHaveBeenCalledTimes(2);

// Restore original
consoleSpy.mockRestore();
```

## Factory Functions

```typescript
// test/factories/user.ts
export const createUser = (overrides = {}): User => ({
  id: faker.string.uuid(),
  email: faker.internet.email(),
  name: faker.person.fullName(),
  createdAt: new Date(),
  ...overrides,
});

// Usage in tests
const user = createUser({ name: 'Custom Name' });
const admin = createUser({ role: 'admin' });
```

## Mock Patterns Summary

| Pattern | Use Case | Library |
|---------|----------|---------|
| Module mock | Replace entire module | jest.mock / vi.mock |
| Partial mock | Keep some implementations | jest.requireActual |
| HTTP mock | API calls | MSW, nock |
| Timer mock | setTimeout/setInterval | jest.useFakeTimers |
| Spy | Watch method calls | jest.spyOn |
| Factory | Generate test data | Custom + Faker |

