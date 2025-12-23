---
name: modern-javascript-patterns
description: Master ES6+ features including async/await, destructuring, spread operators, and functional programming patterns.

summary: |
  - Arrow functions: `const fn = (x) => x * 2` (lexical this)
  - Destructuring: `const { name, age } = user`
  - Spread: `[...arr1, ...arr2]`, `{ ...obj1, ...obj2 }`
  - Optional chaining: `user?.profile?.name`
  - Nullish coalescing: `value ?? defaultValue`

context_cost: high
load_when:
  - "modern javascript"
  - "es6"
  - "destructuring"
  - "async await"
  - "functional programming"
---

# Modern JavaScript Patterns

ES6+ features and functional programming for clean, maintainable code.

## When to Use

- Refactoring legacy JavaScript to modern syntax
- Implementing functional programming patterns
- Working with asynchronous operations
- Writing maintainable and readable code

## ES6+ Quick Reference

### Arrow Functions

```javascript
// Concise syntax
const add = (a, b) => a + b;
const double = x => x * 2;
const getUser = () => ({ name: 'John' });

// Lexical 'this' (preserves context)
class Timer {
  start() {
    setInterval(() => {
      this.tick(); // 'this' works correctly
    }, 1000);
  }
}
```

### Destructuring

```javascript
// Object destructuring
const { name, age, city = 'Unknown' } = user;
const { data: users, error } = response;

// Array destructuring
const [first, second, ...rest] = items;
const [, , third] = arr; // Skip elements

// Function parameters
const greet = ({ name, title = 'Mr.' }) => 
  `Hello, ${title} ${name}`;
```

### Spread & Rest

```javascript
// Array spread
const combined = [...arr1, ...arr2];
const copy = [...original];

// Object spread
const updated = { ...user, name: 'New Name' };
const merged = { ...defaults, ...options };

// Rest parameters
const sum = (...nums) => nums.reduce((a, b) => a + b, 0);
```

### Optional Chaining & Nullish Coalescing

```javascript
// Optional chaining (?.)
const name = user?.profile?.name;
const first = arr?.[0];
const result = obj?.method?.();

// Nullish coalescing (??)
const value = input ?? 'default'; // Only null/undefined
const count = data.count ?? 0;    // 0 is kept, not replaced
```

## Async Patterns

### Promises & Async/Await

```javascript
// Async/await (preferred)
const fetchUser = async (id) => {
  const response = await fetch(`/api/users/${id}`);
  if (!response.ok) throw new Error('User not found');
  return response.json();
};

// Parallel execution
const [users, posts] = await Promise.all([
  fetchUsers(),
  fetchPosts(),
]);

// Error handling
try {
  const data = await fetchData();
} catch (error) {
  console.error('Failed:', error.message);
}
```

### Promise Utilities

```javascript
// Promise.allSettled - wait for all, get results
const results = await Promise.allSettled([p1, p2, p3]);
// [{ status: 'fulfilled', value }, { status: 'rejected', reason }]

// Promise.any - first success wins
const first = await Promise.any([slow, medium, fast]);

// Promise.race - first to resolve/reject
const winner = await Promise.race([fetchWithTimeout, timeoutPromise]);
```

## Functional Patterns

### Array Methods

```javascript
// Map, filter, reduce chain
const result = users
  .filter(u => u.active)
  .map(u => ({ name: u.name, email: u.email }))
  .sort((a, b) => a.name.localeCompare(b.name));

// Reduce for aggregation
const grouped = items.reduce((acc, item) => {
  (acc[item.category] ??= []).push(item);
  return acc;
}, {});
```

### Immutable Updates

```javascript
// Add to array
const added = [...items, newItem];

// Remove from array
const removed = items.filter(i => i.id !== id);

// Update in array
const updated = items.map(i => 
  i.id === id ? { ...i, name: 'Updated' } : i
);

// Deep update
const newState = {
  ...state,
  user: {
    ...state.user,
    profile: { ...state.user.profile, name: 'New' },
  },
};
```

---

*For advanced patterns, see [advanced.md](./advanced.md)*
*For async patterns, see [async.md](./async.md)*
