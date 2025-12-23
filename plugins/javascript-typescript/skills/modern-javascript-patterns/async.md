# Async JavaScript Patterns

## Promise Fundamentals

```javascript
// Creating promises
const fetchData = () => new Promise((resolve, reject) => {
  setTimeout(() => {
    Math.random() > 0.5 
      ? resolve({ data: 'success' })
      : reject(new Error('Failed'));
  }, 1000);
});

// Chaining
fetchData()
  .then(data => processData(data))
  .then(result => saveResult(result))
  .catch(error => handleError(error))
  .finally(() => cleanup());
```

## Async/Await Patterns

### Sequential vs Parallel

```javascript
// Sequential (slow)
const data1 = await fetch('/api/1');
const data2 = await fetch('/api/2');
const data3 = await fetch('/api/3');

// Parallel (fast)
const [data1, data2, data3] = await Promise.all([
  fetch('/api/1'),
  fetch('/api/2'),
  fetch('/api/3'),
]);

// Parallel with error handling per request
const results = await Promise.allSettled([
  fetch('/api/1'),
  fetch('/api/2'),
  fetch('/api/3'),
]);

results.forEach((result, i) => {
  if (result.status === 'fulfilled') {
    console.log(`Request ${i}: ${result.value}`);
  } else {
    console.log(`Request ${i} failed: ${result.reason}`);
  }
});
```

### Retry Pattern

```javascript
const retry = async (fn, maxAttempts = 3, delay = 1000) => {
  for (let attempt = 1; attempt <= maxAttempts; attempt++) {
    try {
      return await fn();
    } catch (error) {
      if (attempt === maxAttempts) throw error;
      await new Promise(r => setTimeout(r, delay * attempt));
    }
  }
};

const data = await retry(() => fetchData(), 3, 1000);
```

### Timeout Pattern

```javascript
const withTimeout = (promise, ms) => {
  const timeout = new Promise((_, reject) =>
    setTimeout(() => reject(new Error('Timeout')), ms)
  );
  return Promise.race([promise, timeout]);
};

const data = await withTimeout(fetchData(), 5000);
```

### Debounce & Throttle

```javascript
// Debounce - execute after pause
const debounce = (fn, ms) => {
  let timeout;
  return (...args) => {
    clearTimeout(timeout);
    timeout = setTimeout(() => fn(...args), ms);
  };
};

// Throttle - execute at most once per interval
const throttle = (fn, ms) => {
  let lastCall = 0;
  return (...args) => {
    const now = Date.now();
    if (now - lastCall >= ms) {
      lastCall = now;
      fn(...args);
    }
  };
};

// Async debounce
const asyncDebounce = (fn, ms) => {
  let timeout;
  return (...args) => {
    clearTimeout(timeout);
    return new Promise(resolve => {
      timeout = setTimeout(async () => {
        resolve(await fn(...args));
      }, ms);
    });
  };
};
```

### Concurrent Limit

```javascript
const pLimit = (concurrency) => {
  let active = 0;
  const queue = [];

  const next = () => {
    if (active >= concurrency || queue.length === 0) return;
    active++;
    const { fn, resolve, reject } = queue.shift();
    fn().then(resolve).catch(reject).finally(() => {
      active--;
      next();
    });
  };

  return (fn) => new Promise((resolve, reject) => {
    queue.push({ fn, resolve, reject });
    next();
  });
};

// Usage: max 3 concurrent requests
const limit = pLimit(3);
const results = await Promise.all(
  urls.map(url => limit(() => fetch(url)))
);
```

## Event Loop & Microtasks

```javascript
// Execution order
console.log('1');  // Sync

setTimeout(() => console.log('2'), 0);  // Macrotask

Promise.resolve().then(() => console.log('3'));  // Microtask

queueMicrotask(() => console.log('4'));  // Microtask

console.log('5');  // Sync

// Output: 1, 5, 3, 4, 2
```

## AbortController

```javascript
const controller = new AbortController();

// Cancel after 5 seconds
setTimeout(() => controller.abort(), 5000);

try {
  const response = await fetch('/api/data', {
    signal: controller.signal,
  });
} catch (error) {
  if (error.name === 'AbortError') {
    console.log('Request was cancelled');
  }
}

// Manual cancel
cancelButton.onclick = () => controller.abort();
```

