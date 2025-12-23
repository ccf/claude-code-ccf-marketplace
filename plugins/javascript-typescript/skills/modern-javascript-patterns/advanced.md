# Advanced JavaScript Patterns

## Generators & Iterators

```javascript
// Generator function
function* range(start, end) {
  for (let i = start; i <= end; i++) {
    yield i;
  }
}

for (const num of range(1, 5)) {
  console.log(num); // 1, 2, 3, 4, 5
}

// Async generator
async function* fetchPages(url) {
  let page = 1;
  while (true) {
    const response = await fetch(`${url}?page=${page}`);
    const data = await response.json();
    if (data.length === 0) break;
    yield data;
    page++;
  }
}

for await (const page of fetchPages('/api/items')) {
  processPage(page);
}
```

## Proxy & Reflect

```javascript
// Validation proxy
const validator = {
  set(obj, prop, value) {
    if (prop === 'age' && typeof value !== 'number') {
      throw new TypeError('Age must be a number');
    }
    return Reflect.set(obj, prop, value);
  },
};

const user = new Proxy({}, validator);
user.age = 25;  // OK
user.age = 'young';  // Throws TypeError

// Logging proxy
const logged = new Proxy(target, {
  get(obj, prop) {
    console.log(`Accessed: ${prop}`);
    return Reflect.get(obj, prop);
  },
});
```

## WeakMap & WeakSet

```javascript
// Private data pattern
const privateData = new WeakMap();

class User {
  constructor(name, password) {
    this.name = name;
    privateData.set(this, { password });
  }

  checkPassword(input) {
    return privateData.get(this).password === input;
  }
}

// Object tagging (auto garbage-collected)
const processed = new WeakSet();

function processOnce(obj) {
  if (processed.has(obj)) return;
  processed.add(obj);
  // Process object...
}
```

## Symbols

```javascript
// Unique keys
const id = Symbol('id');
const user = {
  name: 'John',
  [id]: 12345,  // Not enumerable
};

// Well-known symbols
class Collection {
  *[Symbol.iterator]() {
    for (const item of this.items) {
      yield item;
    }
  }
}

// Symbol registry
const globalKey = Symbol.for('app.key');
const sameKey = Symbol.for('app.key');
console.log(globalKey === sameKey); // true
```

## Currying & Composition

```javascript
// Currying
const curry = (fn) => (...args) =>
  args.length >= fn.length
    ? fn(...args)
    : curry(fn.bind(null, ...args));

const add = curry((a, b, c) => a + b + c);
add(1)(2)(3);    // 6
add(1, 2)(3);    // 6
add(1, 2, 3);    // 6

// Function composition
const compose = (...fns) => (x) =>
  fns.reduceRight((acc, fn) => fn(acc), x);

const pipe = (...fns) => (x) =>
  fns.reduce((acc, fn) => fn(acc), x);

const process = pipe(
  trim,
  toLowerCase,
  removeSpaces
);
```

## Memoization

```javascript
const memoize = (fn) => {
  const cache = new Map();
  return (...args) => {
    const key = JSON.stringify(args);
    if (cache.has(key)) return cache.get(key);
    const result = fn(...args);
    cache.set(key, result);
    return result;
  };
};

const expensiveCalc = memoize((n) => {
  console.log('Computing...');
  return n * n;
});

expensiveCalc(5); // Computing... 25
expensiveCalc(5); // 25 (cached)
```

## Module Patterns

```javascript
// Named exports
export const util1 = () => {};
export const util2 = () => {};

// Default export
export default class MyClass {}

// Re-exports
export { default as Component } from './Component';
export * from './utils';

// Dynamic imports
const module = await import('./heavy-module.js');
```

