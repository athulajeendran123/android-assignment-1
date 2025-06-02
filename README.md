# android-assignment-1

#  Data Structures in Python

This repository contains Python implementations of two fundamental data structures from Android Assignment Set 1:

- Q1: **Least Recently Used (LRU) Cache**
- Q2: **Custom HashMap Implementation (without built-in dict)**
Both are implemented with optimal time complexity and are suitable for high-performance systems.

---

## File Structure

```
.
├── lru_cache_and_hashmap.py  # Python file with both implementations
├── README.md                 # This documentation file
```

---

##  Q1: LRU Cache (O(1) Operations)

### 📌 Problem Statement

Design a cache with a fixed capacity. It should support:

- `get(key)`: Retrieve the value (if present), else return -1
- `put(key, value)`: Insert or update the key. If the cache exceeds capacity, evict the least recently used item.

### 🚀 Key Features

- Uses `OrderedDict` from `collections` to maintain access order
- Evicts least recently used key on overflow
- All operations are **O(1)**

### 🧠 Code Summary

```python
from collections import OrderedDict

class LRUCache:
    def __init__(self, capacity: int):
        self.cache = OrderedDict()
        self.capacity = capacity

    def get(self, key: int) -> int:
        if key not in self.cache:
            return -1
        self.cache.move_to_end(key)
        return self.cache[key]

    def put(self, key: int, value: int) -> None:
        if key in self.cache:
            self.cache.move_to_end(key)
        self.cache[key] = value
        if len(self.cache) > self.capacity:
            self.cache.popitem(last=False)
```

### 🧪 Example Output

```python
lru = LRUCache(2)
lru.put(1, 1)
lru.put(2, 2)
print(lru.get(1))  # Output: 1
lru.put(3, 3)
print(lru.get(2))  # Output: -1 (evicted)
lru.put(4, 4)
print(lru.get(1))  # Output: -1 (evicted)
print(lru.get(3))  # Output: 3
```

---

##  Q2: Custom HashMap (Without Built-in dict)

###  Problem Statement

Design a HashMap that supports the following in average O(1) time:

- `put(key, value)`
- `get(key)`
- `remove(key)`

**Do not use `dict` or other hash map libraries.**

###  Key Features

- Uses a list of buckets with **chaining** to handle collisions
- Hash function: `key % size`, where size is a prime number (1009)
- All operations are **average O(1)**

###  Code Summary

```python
class MyHashMap:
    def __init__(self):
        self.size = 1009
        self.buckets = [[] for _ in range(self.size)]

    def _hash(self, key):
        return key % self.size

    def put(self, key: int, value: int) -> None:
        h = self._hash(key)
        for i, (k, v) in enumerate(self.buckets[h]):
            if k == key:
                self.buckets[h][i] = (key, value)
                return
        self.buckets[h].append((key, value))

    def get(self, key: int) -> int:
        h = self._hash(key)
        for k, v in self.buckets[h]:
            if k == key:
                return v
        return -1

    def remove(self, key: int) -> None:
        h = self._hash(key)
        self.buckets[h] = [(k, v) for k, v in self.buckets[h] if k != key]
```

###  Example Output

```python
obj = MyHashMap()
obj.put(1, 10)
obj.put(2, 20)
print(obj.get(1))  # Output: 10
print(obj.get(3))  # Output: -1
obj.put(2, 30)
print(obj.get(2))  # Output: 30
obj.remove(2)
print(obj.get(2))  # Output: -1
```

---

##  Constraints

- Capacity (Q1): `1 <= capacity <= 3000`
- Keys & Values: `0 <= key, value <= 10^6`
- Max operations: `10^5`
- Time complexity: All operations should be **O(1)**

---

##  Author

athul ajeendran — Android Assignment Set 1, Questions 1 & 2

---


