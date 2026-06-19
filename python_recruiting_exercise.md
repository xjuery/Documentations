# Python Recruiting Kit — Debug the Code

Three progressively harder scripts, each containing real-world bugs. Give candidates the buggy script only. Use hints for guided debriefs and solutions to close the loop.

---

## 01 — Simple: List Average Calculator

**Skills assessed:** Basic Python syntax · Edge case handling · Type awareness

This function should compute the average of a list of numbers and return `0` for empty lists. It contains **2 bugs**.

```python
def calculate_average(numbers):
    if len(numbers) = 0:
        return 0
    
    total = 0
    for num in numbers:
        total =+ num
    
    return total / len(numbers)


# Test
scores = [85, 90, 78, 92, 88]
print(f"Average score: {calculate_average(scores)}")
print(f"Empty list: {calculate_average([])}")
```

<details>
<summary>💡 Hints</summary>

1. Look carefully at the condition operator on line 2.
2. Pay attention to the accumulation operator inside the loop.

</details>

<details>
<summary>✅ Solution</summary>

```python
# Bug 1: Assignment '=' instead of comparison '==' on line 2
# Bug 2: '=+' resets total to +num each iteration instead of '+=' which accumulates

def calculate_average(numbers):
    if len(numbers) == 0:   # Fix 1: == not =
        return 0
    
    total = 0
    for num in numbers:
        total += num         # Fix 2: += not =+
    
    return total / len(numbers)
```

</details>

---

## 02 — Medium: User Cache System

**Skills assessed:** OOP & mutability · Default argument pitfall · Time handling

A simple in-memory cache for user objects with expiry. It contains **3 bugs** — logic, mutability, and scoping.

```python
import time

class UserCache:
    def __init__(self, ttl=60, store={}):
        self.ttl = ttl
        self.store = store
    
    def set(self, user_id, data):
        self.store[user_id] = {
            "data": data,
            "expires_at": time.time() - self.ttl
        }
    
    def get(self, user_id):
        entry = self.store.get(user_id)
        if not entry:
            return None
        if time.time() > entry["expires_at"]:
            del self.store[user_id]
            return None
        return entry["data"]


cache = UserCache(ttl=30)
cache.set("u1", {"name": "Alice"})
print(cache.get("u1"))
```

<details>
<summary>💡 Hints</summary>

1. Mutable default arguments in Python are shared across all instances.
2. Check the expiry timestamp calculation in `set()`.
3. No scoping bug — there are exactly 2 bugs to find.

</details>

<details>
<summary>✅ Solution</summary>

```python
# Bug 1: Mutable default argument 'store={}' is shared across ALL instances
#         → Fix: use store=None and initialise inside __init__
# Bug 2: expires_at uses '-' instead of '+', so entries expire immediately

import time

class UserCache:
    def __init__(self, ttl=60, store=None):   # Fix 1
        self.ttl = ttl
        self.store = store if store is not None else {}

    def set(self, user_id, data):
        self.store[user_id] = {
            "data": data,
            "expires_at": time.time() + self.ttl  # Fix 2: + not -
        }

    def get(self, user_id):
        entry = self.store.get(user_id)
        if not entry:
            return None
        if time.time() > entry["expires_at"]:
            del self.store[user_id]
            return None
        return entry["data"]
```

</details>

---

## 03 — Complex: Async Rate-Limited API Fetcher

**Skills assessed:** Async/await & semaphores · Exception chaining · Race conditions · Generator vs list

Fetches URLs concurrently with a semaphore-based rate limiter and retry logic. It contains **3 subtle bugs** involving async, exception handling, and data integrity.

```python
import asyncio
import aiohttp

async def fetch(session, url, semaphore, retries=3):
    async with semaphore:
        for attempt in range(retries):
            try:
                async with session.get(url, timeout=5) as resp:
                    resp.raise_for_status()
                    return await resp.json()
            except Exception as e:
                if attempt == retries:
                    raise RuntimeError(f"Failed: {url}") from None
                await asyncio.sleep(2 ** attempt)

async def fetch_all(urls, rate_limit=5):
    semaphore = asyncio.Semaphore(rate_limit)
    async with aiohttp.ClientSession() as session:
        tasks = (
            fetch(session, url, semaphore)
            for url in urls
        )
        results = await asyncio.gather(*tasks, return_exceptions=True)
    return results


urls = ["https://api.example.com/item/1",
        "https://api.example.com/item/2"]
print(asyncio.run(fetch_all(urls)))
```

<details>
<summary>💡 Hints</summary>

1. Retry logic: what is the last valid index in `range(retries)`?
2. Exception context: `from None` suppresses the original error — is that always what you want?
3. `asyncio.gather` expects awaitables — check what you're actually passing it.

</details>

<details>
<summary>✅ Solution</summary>

```python
# Bug 1: 'attempt == retries' is never True; last index in range(3) is 2, not 3.
#         → Fix: attempt == retries - 1
# Bug 2: 'from None' discards the original exception, making debugging impossible.
#         → Fix: 'from e'
# Bug 3: tasks is a generator expression — consumed once; gather unpacks it into
#         coroutines but the session may already be closed for later items.
#         → Fix: wrap in list() so all coroutines are created before gather runs.

import asyncio
import aiohttp

async def fetch(session, url, semaphore, retries=3):
    async with semaphore:
        for attempt in range(retries):
            try:
                async with session.get(url, timeout=5) as resp:
                    resp.raise_for_status()
                    return await resp.json()
            except Exception as e:
                if attempt == retries - 1:                   # Fix 1
                    raise RuntimeError(f"Failed: {url}") from e  # Fix 2
                await asyncio.sleep(2 ** attempt)

async def fetch_all(urls, rate_limit=5):
    semaphore = asyncio.Semaphore(rate_limit)
    async with aiohttp.ClientSession() as session:
        tasks = [                                             # Fix 3: list, not generator
            fetch(session, url, semaphore)
            for url in urls
        ]
        results = await asyncio.gather(*tasks, return_exceptions=True)
    return results
```

</details>

---

> **Tip for interviewers:** share the buggy script only. Use hints for guided debriefs, and the solution to close the loop. On the complex exercise, catching 2 out of 3 bugs is a strong signal — catching all three is exceptional.
