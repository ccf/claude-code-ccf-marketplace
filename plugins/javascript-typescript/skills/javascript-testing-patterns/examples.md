# Testing Examples

Extended examples for common testing scenarios.

## Unit Testing Pure Functions

```typescript
// utils/calculator.ts
export const add = (a: number, b: number): number => a + b;
export const divide = (a: number, b: number): number => {
  if (b === 0) throw new Error('Division by zero');
  return a / b;
};

// utils/calculator.test.ts
describe('Calculator', () => {
  describe('add', () => {
    it.each([
      [1, 2, 3],
      [-1, 1, 0],
      [0, 0, 0],
    ])('add(%i, %i) = %i', (a, b, expected) => {
      expect(add(a, b)).toBe(expected);
    });
  });

  describe('divide', () => {
    it('divides numbers correctly', () => {
      expect(divide(10, 2)).toBe(5);
    });

    it('throws on division by zero', () => {
      expect(() => divide(10, 0)).toThrow('Division by zero');
    });
  });
});
```

## Testing Async Services

```typescript
// services/user-service.ts
export class UserService {
  constructor(private repo: UserRepository, private email: EmailService) {}

  async createUser(data: CreateUserDTO): Promise<User> {
    const user = await this.repo.save(data);
    await this.email.sendWelcome(user.email);
    return user;
  }
}

// services/user-service.test.ts
describe('UserService', () => {
  let service: UserService;
  let mockRepo: jest.Mocked<UserRepository>;
  let mockEmail: jest.Mocked<EmailService>;

  beforeEach(() => {
    mockRepo = { save: jest.fn() } as any;
    mockEmail = { sendWelcome: jest.fn() } as any;
    service = new UserService(mockRepo, mockEmail);
  });

  it('creates user and sends welcome email', async () => {
    const userData = { email: 'test@example.com', name: 'Test' };
    const savedUser = { id: '1', ...userData };
    mockRepo.save.mockResolvedValue(savedUser);

    const result = await service.createUser(userData);

    expect(result).toEqual(savedUser);
    expect(mockEmail.sendWelcome).toHaveBeenCalledWith('test@example.com');
  });

  it('throws if save fails', async () => {
    mockRepo.save.mockRejectedValue(new Error('DB error'));

    await expect(service.createUser({ email: 'test@example.com' }))
      .rejects.toThrow('DB error');
  });
});
```

## Integration Testing APIs

```typescript
import request from 'supertest';
import { app } from '../app';
import { prisma } from '../db';

describe('POST /api/users', () => {
  beforeEach(async () => {
    await prisma.user.deleteMany();
  });

  it('creates a new user', async () => {
    const response = await request(app)
      .post('/api/users')
      .send({ email: 'test@example.com', name: 'Test User' })
      .expect(201);

    expect(response.body).toMatchObject({
      email: 'test@example.com',
      name: 'Test User',
    });

    const dbUser = await prisma.user.findUnique({
      where: { email: 'test@example.com' },
    });
    expect(dbUser).toBeTruthy();
  });

  it('returns 400 for invalid email', async () => {
    const response = await request(app)
      .post('/api/users')
      .send({ email: 'invalid', name: 'Test' })
      .expect(400);

    expect(response.body.error).toContain('email');
  });
});
```

## Testing React Hooks

```typescript
import { renderHook, act } from '@testing-library/react';
import { useCounter } from './useCounter';

describe('useCounter', () => {
  it('initializes with default value', () => {
    const { result } = renderHook(() => useCounter());
    expect(result.current.count).toBe(0);
  });

  it('increments counter', () => {
    const { result } = renderHook(() => useCounter());
    
    act(() => {
      result.current.increment();
    });
    
    expect(result.current.count).toBe(1);
  });

  it('accepts initial value', () => {
    const { result } = renderHook(() => useCounter(10));
    expect(result.current.count).toBe(10);
  });
});
```

## Snapshot Testing

```typescript
import { render } from '@testing-library/react';
import { UserCard } from './UserCard';

describe('UserCard', () => {
  it('renders correctly', () => {
    const { container } = render(
      <UserCard user={{ name: 'John', email: 'john@example.com' }} />
    );
    expect(container).toMatchSnapshot();
  });
});
```

