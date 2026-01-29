# 📅 DAY 5 – MATHEMATICAL OPERATIONS & BROADCASTING

> **"One line. Entire dataset. No loops."** — The NumPy Philosophy

![NumPy](https://img.shields.io/badge/NumPy-Day%205-013243?style=for-the-badge&logo=numpy)
![Python](https://img.shields.io/badge/Python-3.x-blue?style=for-the-badge&logo=python)
![Level](https://img.shields.io/badge/Level-Intermediate-yellow?style=for-the-badge)
![Interview](https://img.shields.io/badge/Interview-Favorite-orange?style=for-the-badge)

---

## 🎯 Today's Goals

By the end of Day 5, you will:

| Goal | Description | Importance |
|------|-------------|------------|
| ➕ | Perform math on **entire arrays** at once | ⭐⭐⭐⭐ |
| 📡 | Understand **broadcasting** (interview favorite!) | ⭐⭐⭐⭐⭐ |
| 🚫 | Stop writing unnecessary loops **forever** | ⭐⭐⭐⭐⭐ |

> 🎯 **Broadcasting is asked in 80% of NumPy interviews!**

---

## 📚 Table of Contents

- [Step 1: Element-wise Operations](#-step-1-element-wise-operations-core-idea)
- [Step 2: Array-to-Array Operations](#-step-2-array-to-array-operations)
- [Step 3: Broadcasting Magic](#-step-3-broadcasting-the-magic-)
- [Step 4: Broadcasting 1D + 2D](#-step-4-broadcasting-with-1d--2d)
- [Step 5: Real-Life Example](#-step-5-real-life-example-marks-normalization-)
- [Step 6: Comparison Operations](#-step-6-comparison-operations)
- [Step 7: Universal Functions](#-step-7-universal-functions-ufuncs)
- [Step 8: Common Errors](#%EF%B8%8F-step-8-common-broadcasting-errors)
- [Step 9: Broadcasting Rules](#-step-9-broadcasting-rules-memorize-)
- [Practice Exercises](#-day-5-practice-mandatory-)
- [Checkpoint](#-day-5-checkpoint)

---

## 🧠 Step 1: Element-wise Operations (Core Idea)

### The Power of Vectorization

In NumPy, mathematical operations apply to **every element automatically**!

```python
import numpy as np

a = np.array([10, 20, 30, 40])
```

### Basic Math Operations

```python
a + 5    # [15 25 35 45]
a - 2    # [ 8 18 28 38]
a * 3    # [ 30  60  90 120]
a / 2    # [ 5. 10. 15. 20.]
a ** 2   # [ 100  400  900 1600]
a % 3    # [1 2 0 1]
```

### Visual Representation

```
Original:     [10]  [20]  [30]  [40]
               ↓     ↓     ↓     ↓
Operation:    +5    +5    +5    +5     (applied to EACH element)
               ↓     ↓     ↓     ↓
Result:       [15]  [25]  [35]  [45]
```

### 📢 Analogy

> **Like announcing on a microphone** 📢
> 
> One instruction → Everyone follows!

### Python Loop vs NumPy (Speed Comparison)

| Approach | Code | Time (1M elements) |
|----------|------|-------------------|
| Python Loop | `[x + 5 for x in arr]` | ~150 ms |
| NumPy | `arr + 5` | ~1 ms |

```python
# ❌ Python way (SLOW)
result = []
for x in a:
    result.append(x + 5)

# ✅ NumPy way (150x FASTER!)
result = a + 5
```

---

## 🔥 Step 2: Array-to-Array Operations

### When Two Arrays Meet

```python
a = np.array([10, 20, 30, 40])
b = np.array([1, 2, 3, 4])
```

### Element-wise Operations

```python
a + b    # [11 22 33 44]
a - b    # [ 9 18 27 36]
a * b    # [ 10  40  90 160]
a / b    # [10. 10. 10. 10.]
a ** b   # [   10   400 27000 2560000]
```

### Visual Representation

```
Array a:      [10]  [20]  [30]  [40]
               ↓     ↓     ↓     ↓
Operation:     +     +     +     +
               ↓     ↓     ↓     ↓
Array b:      [ 1]  [ 2]  [ 3]  [ 4]
               ↓     ↓     ↓     ↓
Result:       [11]  [22]  [33]  [44]

Position-by-position operation!
```

### 📌 The Rule

```
┌─────────────────────────────────────────────────────┐
│  Shapes must MATCH or be BROADCASTABLE              │
│                                                     │
│  (4,) + (4,) = ✅ Works                             │
│  (4,) + (3,) = ❌ Error (shapes don't match)        │
└─────────────────────────────────────────────────────┘
```

### What's "Broadcastable"? 👀

That's the magic we'll learn in the next step!

---

## 🧠 Step 3: Broadcasting (THE MAGIC 🔮)

### What is Broadcasting?

> **Broadcasting** = NumPy's ability to **stretch** a smaller array to match a larger one — **without copying data**!

### Simple Example: Scalar + Array

```python
c = np.array([[1, 2, 3],
              [4, 5, 6]])

c + 10
```

### Output

```python
[[11 12 13]
 [14 15 16]]
```

### How NumPy Thinks

```
Original Array c:              Scalar 10:
┌───┬───┬───┐                     │
│ 1 │ 2 │ 3 │                    10
├───┼───┼───┤                     │
│ 4 │ 5 │ 6 │                     ▼
└───┴───┴───┘           
    (2, 3)                       (1,)

NumPy "broadcasts" 10 to match shape (2, 3):

┌────┬────┬────┐       ┌────┬────┬────┐       ┌────┬────┬────┐
│  1 │  2 │  3 │   +   │ 10 │ 10 │ 10 │   =   │ 11 │ 12 │ 13 │
├────┼────┼────┤       ├────┼────┼────┤       ├────┼────┼────┤
│  4 │  5 │  6 │       │ 10 │ 10 │ 10 │       │ 14 │ 15 │ 16 │
└────┴────┴────┘       └────┴────┴────┘       └────┴────┴────┘

Note: NumPy doesn't ACTUALLY copy 10 six times!
      It's a virtual stretch for efficiency.
```

### 🧠 NumPy's Internal Monologue

> *"Oh, a single value with a 2D array? I'll apply it everywhere — efficiently!"*

---

## 🔥 Step 4: Broadcasting with 1D + 2D

### The Real Power

```python
c = np.array([[1, 2, 3],
              [4, 5, 6]])

d = np.array([10, 20, 30])

c + d
```

### Output

```python
[[11 22 33]
 [14 25 36]]
```

### Visual: How Broadcasting Works

```
2D Array c (2, 3):           1D Array d (3,):
┌───┬───┬───┐               ┌────┬────┬────┐
│ 1 │ 2 │ 3 │               │ 10 │ 20 │ 30 │
├───┼───┼───┤               └────┴────┴────┘
│ 4 │ 5 │ 6 │                       │
└───┴───┴───┘                       │
                                    ▼
                            NumPy "stretches" d:
                            ┌────┬────┬────┐
                            │ 10 │ 20 │ 30 │
                            ├────┼────┼────┤
                            │ 10 │ 20 │ 30 │
                            └────┴────┴────┘

Result (2, 3):
┌────┬────┬────┐
│ 11 │ 22 │ 33 │   (1+10, 2+20, 3+30)
├────┼────┼────┤
│ 14 │ 25 │ 36 │   (4+10, 5+20, 6+30)
└────┴────┴────┘
```

### 📌 The Broadcasting Rule

```
┌─────────────────────────────────────────────────────┐
│  1. Last dimensions must MATCH                      │
│  2. OR one of them must be 1                        │
│  3. Smaller array "stretches" to match              │
└─────────────────────────────────────────────────────┘
```

### More Examples

```python
# Shape (2, 3) + Shape (3,) = Works!
# Last dim: 3 == 3 ✅

# Shape (2, 3) + Shape (2, 1) = Works!
# Broadcasting happens in column direction

matrix = np.array([[1, 2, 3],
                   [4, 5, 6]])  # Shape: (2, 3)

col_vector = np.array([[10],
                       [20]])   # Shape: (2, 1)

matrix + col_vector
# [[11 12 13]
#  [24 25 26]]
```

### Column Broadcasting Visualization

```
Matrix (2, 3):           Column Vector (2, 1):
┌───┬───┬───┐            ┌────┐
│ 1 │ 2 │ 3 │            │ 10 │
├───┼───┼───┤            ├────┤
│ 4 │ 5 │ 6 │            │ 20 │
└───┴───┴───┘            └────┘
                              │
                              ▼
                         Stretched:
                         ┌────┬────┬────┐
                         │ 10 │ 10 │ 10 │
                         ├────┼────┼────┤
                         │ 20 │ 20 │ 20 │
                         └────┴────┴────┘

Result:
┌────┬────┬────┐
│ 11 │ 12 │ 13 │
├────┼────┼────┤
│ 24 │ 25 │ 26 │
└────┴────┴────┘
```

---

## 🧠 Step 5: Real-Life Example (Marks Normalization 🎓)

### The Scenario

You have student marks and want to **normalize** them (convert to z-scores).

### The Formula

```
z = (x - mean) / std
```

### NumPy Implementation

```python
marks = np.array([70, 80, 90])

# Calculate statistics
mean = marks.mean()   # 80.0
std = marks.std()     # 8.16...

# Normalize (using broadcasting!)
normalized = (marks - mean) / std

print(normalized)
# [-1.22474487  0.          1.22474487]
```

### What Happened (Step by Step)

```python
marks = [70, 80, 90]
mean = 80.0

# Step 1: Subtraction (broadcasting!)
marks - mean
# [70-80, 80-80, 90-80]
# [-10, 0, 10]

# Step 2: Division (broadcasting!)
[-10, 0, 10] / 8.16
# [-1.22, 0, 1.22]
```

### 🔥 Why This Matters

| Aspect | Description |
|--------|-------------|
| 🔥 Real formula | Used in ML/statistics daily |
| 🔥 No loops | Entire operation in one line |
| 🔥 Clean code | Easy to read and maintain |
| 🔥 Fast | Vectorized C operations |

### More Real-World Examples

```python
# Temperature: Celsius to Fahrenheit
celsius = np.array([0, 25, 100])
fahrenheit = celsius * 9/5 + 32
# [32.0, 77.0, 212.0]

# Percentage calculation
scores = np.array([45, 67, 89, 92])
total = 100
percentages = (scores / total) * 100
# [45., 67., 89., 92.]

# Min-Max Normalization (scale to 0-1)
data = np.array([10, 20, 30, 40, 50])
normalized = (data - data.min()) / (data.max() - data.min())
# [0.   0.25 0.5  0.75 1.  ]
```

---

## 🔢 Step 6: Comparison Operations

### Comparing Arrays

Comparison operators also work element-wise!

```python
a = np.array([10, 20, 30, 40])

a > 25     # [False False  True  True]
a == 20    # [False  True False False]
a >= 20    # [False  True  True  True]
a != 30    # [ True  True False  True]
a < 15     # [ True False False False]
```

### All Comparison Operators

| Operator | Meaning | Example |
|----------|---------|---------|
| `>` | Greater than | `a > 25` |
| `<` | Less than | `a < 25` |
| `>=` | Greater or equal | `a >= 25` |
| `<=` | Less or equal | `a <= 25` |
| `==` | Equal | `a == 25` |
| `!=` | Not equal | `a != 25` |

### Connection to Day 3 (Boolean Masking!)

```python
# Create mask
mask = a > 25
print(mask)  # [False False True True]

# Use mask to filter (from Day 3!)
filtered = a[mask]
print(filtered)  # [30 40]

# One-liner
a[a > 25]  # [30 40]
```

### Comparing Arrays to Arrays

```python
a = np.array([10, 20, 30])
b = np.array([15, 20, 25])

a > b    # [False False  True]
a == b   # [False  True False]
```

---

## 🧠 Step 7: Universal Functions (ufuncs)

### What are ufuncs?

**Universal Functions (ufuncs)** are NumPy's optimized functions that operate on arrays element-by-element.

```python
a = np.array([1, 4, 9, 16, 25])
```

### Mathematical Functions

```python
np.sqrt(a)     # [1. 2. 3. 4. 5.]     Square root
np.square(a)   # [1 16 81 256 625]   Square
np.power(a, 3) # [1 64 729 ...]      Power
np.abs([-1, -2, 3])  # [1 2 3]       Absolute value
```

### Exponential & Logarithmic

```python
b = np.array([1, 2, 3])

np.exp(b)      # [2.718, 7.389, 20.085]  e^x
np.log(b)      # [0., 0.693, 1.098]      Natural log (ln)
np.log10(b)    # [0., 0.301, 0.477]      Base-10 log
np.log2(b)     # [0., 1., 1.585]         Base-2 log
```

### Trigonometric Functions

```python
angles = np.array([0, np.pi/2, np.pi])

np.sin(angles)  # [0., 1., 0.]
np.cos(angles)  # [1., 0., -1.]
np.tan(angles)  # [0., very large, 0.]
```

### Rounding Functions

```python
c = np.array([1.2, 2.5, 3.7, 4.4])

np.round(c)     # [1. 2. 4. 4.]   Round to nearest
np.floor(c)     # [1. 2. 3. 4.]   Round down
np.ceil(c)      # [2. 3. 4. 5.]   Round up
np.trunc(c)     # [1. 2. 3. 4.]   Truncate decimals
```

### Aggregation Functions

```python
a = np.array([10, 20, 30, 40, 50])

np.sum(a)       # 150      Sum all
np.mean(a)      # 30.0     Average
np.std(a)       # 14.14... Standard deviation
np.var(a)       # 200.0    Variance
np.min(a)       # 10       Minimum
np.max(a)       # 50       Maximum
np.argmin(a)    # 0        Index of minimum
np.argmax(a)    # 4        Index of maximum
np.cumsum(a)    # [10 30 60 100 150]  Cumulative sum
np.prod(a)      # 12000000  Product of all
```

### 📊 Ufuncs Quick Reference Table

| Category | Functions |
|----------|-----------|
| **Math** | `sqrt`, `square`, `power`, `abs` |
| **Exp/Log** | `exp`, `log`, `log10`, `log2` |
| **Trig** | `sin`, `cos`, `tan`, `arcsin`, `arccos` |
| **Rounding** | `round`, `floor`, `ceil`, `trunc` |
| **Aggregate** | `sum`, `mean`, `std`, `var`, `min`, `max` |
| **Comparison** | `maximum`, `minimum`, `greater`, `less` |

---

## ⚠️ Step 8: Common Broadcasting Errors

### The Dreaded Shape Mismatch

```python
x = np.array([1, 2, 3])      # Shape: (3,)
y = np.array([1, 2])          # Shape: (2,)

x + y
```

### ❌ Error!

```
ValueError: operands could not be broadcast together 
with shapes (3,) (2,)
```

### Why It Failed

```
Shape Analysis:
x: (3,)
y: (2,)
    ↓
Last dimensions: 3 vs 2
Neither is 1, and they're not equal
    ↓
❌ CANNOT BROADCAST!
```

### Visual Explanation

```
x: [1] [2] [3]      (3 elements)
y: [1] [2]          (2 elements)

NumPy asks: "How do I stretch 2 elements to match 3?"
Answer: "I CAN'T! They don't align!"

     [1]  [2]  [3]
      +    +    +
     [1]  [2]   ?   ← What goes here?!
```

### Common Error Scenarios

| Shape A | Shape B | Result | Reason |
|---------|---------|--------|--------|
| `(3,)` | `(3,)` | ✅ Works | Same shape |
| `(3,)` | `(1,)` | ✅ Works | 1 stretches to 3 |
| `(3,)` | `(2,)` | ❌ Error | 3 ≠ 2, neither is 1 |
| `(2, 3)` | `(3,)` | ✅ Works | Last dims match |
| `(2, 3)` | `(2,)` | ❌ Error | 3 ≠ 2 |
| `(2, 3)` | `(2, 1)` | ✅ Works | 1 stretches to 3 |
| `(2, 3)` | `(1, 3)` | ✅ Works | 1 stretches to 2 |

### How to Fix Broadcasting Errors

```python
# Method 1: Reshape to match
x = np.array([1, 2, 3])      # (3,)
y = np.array([1, 2])          # (2,)

# Add dimension to make compatible
x_reshaped = x.reshape(3, 1)  # (3, 1)
y_reshaped = y.reshape(1, 2)  # (1, 2)

result = x_reshaped + y_reshaped  # (3, 2) ✅
# [[2 3]
#  [3 4]
#  [4 5]]

# Method 2: Use np.newaxis
x[:, np.newaxis] + y  # Same result
```

---

## 🧠 Step 9: Broadcasting Rules (MEMORIZE 🔥)

### The Three Golden Rules

```
┌─────────────────────────────────────────────────────────────┐
│                  BROADCASTING RULES                         │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  1️⃣  Compare shapes from RIGHT to LEFT                      │
│                                                             │
│  2️⃣  Dimensions are compatible if:                          │
│      • They are EQUAL, or                                   │
│      • One of them is 1                                     │
│                                                             │
│  3️⃣  If not compatible → ERROR                              │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### Rule Application Examples

#### Example 1: (4, 3) + (3,) ✅

```
Step 1: Align from right
        (4, 3)
           (3,)
           
Step 2: Compare dimensions (right to left)
        3 vs 3 → Equal ✅
        4 vs _ → Missing = treated as 1 ✅
        
Step 3: Result shape = (4, 3) ✅
```

#### Example 2: (2, 3, 4) + (3, 4) ✅

```
Step 1: Align from right
        (2, 3, 4)
           (3, 4)
           
Step 2: Compare
        4 vs 4 → Equal ✅
        3 vs 3 → Equal ✅
        2 vs _ → Missing = 1 ✅
        
Step 3: Result shape = (2, 3, 4) ✅
```

#### Example 3: (2, 3) + (2,) ❌

```
Step 1: Align from right
        (2, 3)
           (2,)
           
Step 2: Compare
        3 vs 2 → Not equal, neither is 1 ❌
        
Step 3: ERROR! Cannot broadcast ❌
```

#### Example 4: (2, 1) + (1, 3) ✅

```
Step 1: Align from right
        (2, 1)
        (1, 3)
        
Step 2: Compare
        1 vs 3 → One is 1 ✅ → Result: 3
        2 vs 1 → One is 1 ✅ → Result: 2
        
Step 3: Result shape = (2, 3) ✅
```

### Visual Broadcasting Matrix

```
        (1,)    (3,)    (1,3)   (3,1)   (2,3)
(1,)     ✅      ✅      ✅      ✅      ✅
(3,)     ✅      ✅      ✅      ❌      ✅
(1,3)    ✅      ✅      ✅      ✅      ✅
(3,1)    ✅      ❌      ✅      ✅      ❌
(2,3)    ✅      ✅      ✅      ❌      ✅
```

### 🧠 Quick Memory Trick

> **"Same or One, We're Done!"**
> 
> If dimensions are the **same** OR **one is 1** → ✅ Broadcast works!

---

## 📝 DAY 5 PRACTICE (MANDATORY 😤)

### Task 1: Basic Operations

```python
arr = np.array([5, 10, 15, 20])
```

**Complete these operations:**

- [ ] Multiply all elements by 2
- [ ] Subtract the mean from each element

<details>
<summary>💡 Solution (Try First!)</summary>

```python
import numpy as np

arr = np.array([5, 10, 15, 20])

# Multiply all by 2
result1 = arr * 2
print("Multiplied:", result1)
# [10 20 30 40]

# Subtract mean
mean_val = arr.mean()  # 12.5
result2 = arr - mean_val
print("Mean subtracted:", result2)
# [-7.5 -2.5  2.5  7.5]

# Or in one line:
print(arr - arr.mean())
```

</details>

---

### Task 2: 2D Broadcasting

```python
data = np.array([[10, 20, 30],
                 [40, 50, 60]])
```

**Add this 1D array using broadcasting:**

```python
add_this = np.array([1, 2, 3])
```

<details>
<summary>💡 Solution (Try First!)</summary>

```python
import numpy as np

data = np.array([[10, 20, 30],
                 [40, 50, 60]])

add_this = np.array([1, 2, 3])

result = data + add_this
print(result)
# [[11 22 33]
#  [41 52 63]]

# Shape analysis:
# data:     (2, 3)
# add_this:    (3,)
# Last dims: 3 == 3 ✅
# Result:   (2, 3)
```

</details>

---

### Task 3: Column-wise Broadcasting

```python
matrix = np.array([[1, 2, 3],
                   [4, 5, 6],
                   [7, 8, 9]])
```

**Multiply each column by a different factor:**

```python
factors = np.array([[10], [20], [30]])  # Shape: (3, 1)
```

<details>
<summary>💡 Solution (Try First!)</summary>

```python
import numpy as np

matrix = np.array([[1, 2, 3],
                   [4, 5, 6],
                   [7, 8, 9]])

factors = np.array([[10], [20], [30]])

result = matrix * factors
print(result)
# [[ 10  20  30]   (row 0 × 10)
#  [ 80 100 120]   (row 1 × 20)
#  [210 240 270]]  (row 2 × 30)

# Shape analysis:
# matrix:  (3, 3)
# factors: (3, 1)
# 3 vs 1 → 1 stretches to 3 ✅
# 3 vs 3 → Equal ✅
# Result: (3, 3)
```

</details>

---

### Task 4: Pro Thinking 🧠

**Question:** Why is broadcasting faster than loops?

<details>
<summary>💡 Answer</summary>

### Broadcasting is Faster Because:

#### 1. **No Memory Duplication**

```python
# Loop approach (conceptually):
# Creates copies of data
temp = []
for i in range(1000000):
    temp.append(arr[i] + 5)  # 1M append operations

# Broadcasting:
# No copies created!
arr + 5  # Virtual stretch, operates in-place
```

#### 2. **Compiled C Code**

```python
# Python loop:
# Each iteration goes through Python interpreter
# Slow: ~100+ CPU cycles per operation

# NumPy broadcasting:
# Runs pre-compiled C code
# Fast: ~1-5 CPU cycles per operation
```

#### 3. **Vectorized Operations (SIMD)**

```
Python Loop:        NumPy Broadcasting:
[Process 1]         [Process 1, 2, 3, 4] ← Parallel!
[Process 2]         [Process 5, 6, 7, 8]
[Process 3]         [Process 9, 10, 11, 12]
[Process 4]         ...
...                 Done in 1/4 the time!
```

Modern CPUs can process multiple numbers simultaneously (SIMD = Single Instruction, Multiple Data).

#### 4. **Memory Cache Efficiency**

```
Loop: Random memory access
      Cache misses → Slow

Broadcasting: Sequential memory access
              Cache hits → Fast
```

### Benchmark Proof

```python
import numpy as np
import time

arr = np.random.rand(10_000_000)

# Python loop
start = time.time()
result = [x + 5 for x in arr]
print(f"Loop: {time.time() - start:.3f}s")

# NumPy broadcasting
start = time.time()
result = arr + 5
print(f"NumPy: {time.time() - start:.3f}s")

# Typical output:
# Loop: 1.234s
# NumPy: 0.008s  ← ~150x faster!
```

### Summary

| Factor | Loop | Broadcasting |
|--------|------|--------------|
| Memory | Copies data | Virtual stretch |
| Code | Python interpreter | Compiled C |
| Processing | Sequential | Parallel (SIMD) |
| Cache | Misses | Hits |
| **Speed** | Slow | **~100-150x faster** |

</details>

---

### Task 5: Fix the Error

```python
a = np.array([[1, 2, 3],
              [4, 5, 6]])    # Shape: (2, 3)

b = np.array([10, 20])        # Shape: (2,)

# This causes an error:
# a + b
```

**Fix it so addition works!**

<details>
<summary>💡 Solution (Try First!)</summary>

```python
import numpy as np

a = np.array([[1, 2, 3],
              [4, 5, 6]])    # Shape: (2, 3)

b = np.array([10, 20])        # Shape: (2,)

# Problem: Last dims 3 vs 2 don't match!

# Solution 1: Reshape b to (2, 1)
b_reshaped = b.reshape(2, 1)  # Shape: (2, 1)
print(a + b_reshaped)
# [[11 12 13]    (row + 10)
#  [24 25 26]]   (row + 20)

# Solution 2: Use np.newaxis
print(a + b[:, np.newaxis])
# Same result

# Solution 3: Use b with matching last dimension
b_alt = np.array([10, 20, 30])  # Shape: (3,)
print(a + b_alt)
# [[11 22 33]
#  [14 25 36]]

# Shape analysis for Solution 1:
# a:          (2, 3)
# b_reshaped: (2, 1)
# 3 vs 1 → 1 stretches ✅
# 2 vs 2 → Equal ✅
# Result: (2, 3) ✅
```

</details>

---

## 🚫 Today's Rules

| ❌ FORBIDDEN | ✅ REQUIRED |
|--------------|-------------|
| `for` loops for math | Vectorized operations |
| Manual iteration | Broadcasting |
| Overthinking | Trust NumPy |
| Ignoring shapes | Check shapes first |

---

## 🔒 Day 5 Checkpoint

### Self-Assessment Checklist

Before moving to Day 6, ensure you can:

- [ ] **Apply math without loops**
  ```python
  arr * 2           # Not: [x*2 for x in arr]
  arr - arr.mean()  # Not: [x-mean for x in arr]
  ```

- [ ] **Explain broadcasting**
  - NumPy stretches smaller arrays to match larger ones
  - No actual data copying (virtual stretch)
  - Compare dimensions from right to left

- [ ] **Fix shape mismatch errors**
  ```python
  # Error: (2,3) + (2,)
  # Fix: reshape (2,) to (2,1)
  ```

- [ ] **Use ufuncs**
  ```python
  np.sqrt(arr), np.mean(arr), np.sum(arr)
  ```

---

## 📊 Quick Reference Card

```python
# ═══════════════════════════════════════════════════════════
#                  ELEMENT-WISE OPERATIONS
# ═══════════════════════════════════════════════════════════

arr + 5          # Add to all
arr - 5          # Subtract from all
arr * 5          # Multiply all
arr / 5          # Divide all
arr ** 2         # Square all
arr % 2          # Modulo all

# ═══════════════════════════════════════════════════════════
#                  ARRAY-TO-ARRAY
# ═══════════════════════════════════════════════════════════

arr1 + arr2      # Element-wise addition
arr1 * arr2      # Element-wise multiplication
arr1 / arr2      # Element-wise division

# ═══════════════════════════════════════════════════════════
#                  BROADCASTING RULES
# ═══════════════════════════════════════════════════════════

# Rule 1: Compare shapes from RIGHT
# Rule 2: Dimensions must be EQUAL or ONE must be 1
# Rule 3: Otherwise → Error

# ═══════════════════════════════════════════════════════════
#                  UNIVERSAL FUNCTIONS
# ═══════════════════════════════════════════════════════════

np.sqrt(arr)     # Square root
np.exp(arr)      # Exponential
np.log(arr)      # Natural log
np.sin(arr)      # Sine
np.abs(arr)      # Absolute value
np.round(arr)    # Round

# ═══════════════════════════════════════════════════════════
#                  AGGREGATIONS
# ═══════════════════════════════════════════════════════════

np.sum(arr)      # Sum
np.mean(arr)     # Mean
np.std(arr)      # Standard deviation
np.min(arr)      # Minimum
np.max(arr)      # Maximum
np.argmax(arr)   # Index of maximum

# ═══════════════════════════════════════════════════════════
#                  COMPARISONS
# ═══════════════════════════════════════════════════════════

arr > 5          # Greater than
arr == 5         # Equal to
arr != 5         # Not equal to
```

---

## 🔗 Navigation

| Previous | Current | Next |
|----------|---------|------|
| [Day 4: Reshaping & Memory](https://github.com/Saad-Shaikh095/30-Days-Numpy-for-Data-Science-/tree/main/Phase%201%20Foundations/Day%204%20RESHAPING%2C%20FLATTENING%20%26%20MEMORY%20MAGIC) | **Day 5: Math & Broadcasting** | [Day 6: Aggregations](https://github.com/Saad-Shaikh095/30-Days-Numpy-for-Data-Science-/tree/main/Phase%201%20Foundations/Day%206%20Aggregations%20and%20Axis) |

---

<div align="center">

### 💡 Key Insight of Day 5

*"Broadcasting is NumPy's superpower — it lets you write clean, fast code without loops!"*

---

### 🎯 Interview Tip

```
┌─────────────────────────────────────────────────────────────┐
│  "What is broadcasting in NumPy?"                           │
│                                                             │
│  Answer: Broadcasting is NumPy's ability to perform         │
│  operations on arrays of different shapes by virtually      │
│  stretching the smaller array to match the larger one,      │
│  without copying data. Shapes are compared from right       │
│  to left, and dimensions must be equal or one must be 1.    │
└─────────────────────────────────────────────────────────────┘
```

---

### 🏆 Achievement Unlocked!

**🎖️ Broadcasting Master**

*You now think in vectors, not loops!*

---

**Happy Coding! 🚀**

![Made with NumPy](https://img.shields.io/badge/Made%20with-NumPy-013243?style=flat&logo=numpy)
![No Loops](https://img.shields.io/badge/No-Loops-red?style=flat)
![Vectorized](https://img.shields.io/badge/100%25-Vectorized-green?style=flat)

</div>

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.