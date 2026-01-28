# 📅 DAY 3 – BOOLEAN MASKING & FANCY INDEXING

> **"Filtering data without loops = PRO"** — Think like NumPy, not Python

![NumPy](https://img.shields.io/badge/NumPy-Day%203-013243?style=for-the-badge&logo=numpy)
![Python](https://img.shields.io/badge/Python-3.x-blue?style=for-the-badge&logo=python)
![Level](https://img.shields.io/badge/Level-Intermediate-yellow?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=for-the-badge)

---

## 🎯 Today's Goals

By the end of Day 3, you will:

| Goal | Description |
|------|-------------|
| 🔍 | Filter data like SQL `WHERE` clause |
| ⚡ | Select data using conditions (no loops!) |
| 💪 | Feel the power of NumPy thinking |

---

## 📚 Table of Contents

- [Step 1: Boolean Masking (Core Concept)](#-step-1-boolean-masking-core-concept-)
- [Step 2: Filter Data with Masks](#-step-2-use-mask-to-filter-data)
- [Step 3: Real-Life Example](#-step-3-real-life-example-marks-filter-)
- [Step 4: Multiple Conditions](#-step-4-multiple-conditions-and--or)
- [Step 5: Boolean Masking in 2D](#-step-5-boolean-masking-in-2d-arrays)
- [Step 6: Modify Data Using Mask](#-step-6-modify-data-using-mask)
- [Step 7: Fancy Indexing](#-step-7-fancy-indexing-selective-power)
- [Step 8: Fancy Indexing in 2D](#-step-8-fancy-indexing-in-2d)
- [Step 9: Boolean vs Fancy](#-step-9-boolean-vs-fancy-when-to-use-what)
- [Practice Exercises](#-day-3-practice-no-escape-)
- [Checkpoint](#-day-3-checkpoint)

---

## 🧠 Step 1: Boolean Masking (Core Concept 🔥)

### What is Boolean Masking?

Boolean masking is asking your array a **yes/no question** and getting a **True/False answer** for each element.

### Example

```python
import numpy as np

a = np.array([10, 25, 40, 55, 70])
```

### Ask: "Give me values greater than 30"

```python
a > 30
```

### Output

```python
[False False True True True]
```

### Visual Representation

```
Original Array:    [10]  [25]  [40]  [55]  [70]
                    ↓     ↓     ↓     ↓     ↓
Condition (>30):   10>30 25>30 40>30 55>30 70>30
                    ↓     ↓     ↓     ↓     ↓
Boolean Mask:      False False True  True  True
```

> 🎯 This array of `True`/`False` values is called a **Boolean Mask**

---

## 🔥 Step 2: Use Mask to Filter Data

### Apply the Mask

```python
a[a > 30]
```

### Output

```python
[40 55 70]
```

### How It Works

```
Array:        [10]  [25]  [40]  [55]  [70]
               ↓     ↓     ↓     ↓     ↓
Mask:        False False True  True  True
               ↓     ↓     ↓     ↓     ↓
Result:        ✗     ✗    [40]  [55]  [70]
                          ─────────────────
                          Final: [40 55 70]
```

### 🎫 Analogy

> **Mask = Permission Card** 🎫
> 
> - `True` = ✅ You may enter
> - `False` = ❌ Access denied

---

## 🧠 Step 3: Real-Life Example (Marks Filter 🎓)

### The Scenario

```python
marks = np.array([45, 60, 72, 88, 35, 90])

# Get all passing marks (>= 50)
passed = marks[marks >= 50]
print(passed)
```

### Output

```python
[60 72 88 90]
```

### Why This is Powerful

| Traditional Python | NumPy Way |
|-------------------|-----------|
| ```python passed = [] for m in marks: if m >= 50: passed.append(m)``` | ```python passed = marks[marks >= 50]``` |
| 4 lines | 1 line |
| Slow (loop) | Fast (vectorized) |

### 💡 Key Benefits

- ✅ **No loop** — NumPy handles iteration internally
- ✅ **Clean** — One readable line
- ✅ **Fast** — Optimized C operations

> 🏭 **This is industry-style filtering!**

---

## 🔥 Step 4: Multiple Conditions (AND / OR)

### AND Condition (`&`)

```python
# Marks between 50 and 80
marks[(marks >= 50) & (marks < 80)]
```

```python
# Output: [60 72]
```

### OR Condition (`|`)

```python
# Marks below 40 OR above 85
marks[(marks < 40) | (marks > 85)]
```

```python
# Output: [35 88 90]
```

### Visual: Multiple Conditions

```
marks = [45, 60, 72, 88, 35, 90]

Condition 1: marks >= 50
Result:     [F,  T,  T,  T,  F,  T]

Condition 2: marks < 80
Result:     [T,  T,  T,  F,  T,  F]

Combined (AND - &):
            [F,  T,  T,  F,  F,  F]
             ↓   ↓   ↓
Final:         [60, 72]
```

### ⚠️ CRITICAL WARNING

| ❌ WRONG | ✅ CORRECT |
|----------|------------|
| `and` | `&` |
| `or` | `\|` |
| `not` | `~` |

```python
# ❌ This will ERROR
marks[(marks >= 50) and (marks < 80)]  # ValueError!

# ✅ This works
marks[(marks >= 50) & (marks < 80)]    # Correct!
```

### 🧠 Memory Trick

> **NumPy thinks in BITWISE, not English!**
> 
> - `and`/`or` → Python keywords (for single values)
> - `&`/`|` → Bitwise operators (for arrays)

### Parentheses are MANDATORY!

```python
# ❌ Wrong (operator precedence issue)
marks[marks >= 50 & marks < 80]

# ✅ Correct
marks[(marks >= 50) & (marks < 80)]
```

---

## 🧠 Step 5: Boolean Masking in 2D Arrays

### Create 2D Dataset

```python
data = np.array([
    [65, 70, 80],   # Student 1
    [90, 85, 88],   # Student 2
    [40, 55, 60]    # Student 3
])
```

### Get All Values > 70

```python
data[data > 70]
```

```python
# Output: [80 90 85 88]
```

### Get All Values < 50

```python
data[data < 50]
```

```python
# Output: [40]
```

### Visual Explanation

```
Original 2D Array:
┌────┬────┬────┐
│ 65 │ 70 │ 80 │
├────┼────┼────┤
│ 90 │ 85 │ 88 │
├────┼────┼────┤
│ 40 │ 55 │ 60 │
└────┴────┴────┘

Mask (data > 70):
┌───────┬───────┬───────┐
│ False │ False │ True  │
├───────┼───────┼───────┤
│ True  │ True  │ True  │
├───────┼───────┼───────┤
│ False │ False │ False │
└───────┴───────┴───────┘

Result: [80, 90, 85, 88]  ← Flattened!
```

> ⚠️ **Note:** Result is always **1D** (flattened) when using boolean masking

---

## 🎯 Step 6: Modify Data Using Mask

### Give Grace Marks

```python
marks = np.array([45, 60, 72, 88, 35, 90])

# Everyone below 50 gets +5
marks[marks < 50] += 5

print(marks)
```

### Output

```python
[50 60 72 88 40 90]
#↑              ↑
# 45+5=50    35+5=40
```

### 🧠 Plain English

> *"Everyone below 50, get +5 marks"*

### More Examples

```python
# Cap maximum at 100
scores[scores > 100] = 100

# Set negatives to zero
data[data < 0] = 0

# Double all passing marks
marks[marks >= 50] *= 2
```

### Real-World Use Cases

| Scenario | Code |
|----------|------|
| Remove outliers | `data[data > threshold] = threshold` |
| Replace missing values | `data[data == -999] = 0` |
| Normalize extreme values | `data[data > max_val] = max_val` |

---

## 💎 Step 7: Fancy Indexing (Selective Power)

### What is Fancy Indexing?

> **Fancy Indexing = Select elements using a LIST of indices**

### Basic Example

```python
a = np.array([10, 20, 30, 40, 50])

# Select elements at index 0, 2, and 4
a[[0, 2, 4]]
```

### Output

```python
[10 30 50]
```

### Visual Representation

```
Array:     [10]  [20]  [30]  [40]  [50]
Index:       0     1     2     3     4
             ↓           ↓           ↓
Requested: [0,         2,          4]
             ↓           ↓           ↓
Result:    [10]       [30]       [50]

Final: [10 30 50]
```

### 🧠 Use Cases

| Use Case | Example |
|----------|---------|
| Select specific rows | `data[[0, 5, 10]]` |
| Pick random samples | `data[[random_indices]]` |
| Reorder elements | `a[[2, 0, 1]]` → reorders |
| Duplicate selections | `a[[0, 0, 1]]` → `[10 10 20]` |

---

## 🧠 Step 8: Fancy Indexing in 2D

### Create Matrix

```python
matrix = np.array([
    [10, 20],    # Row 0
    [30, 40],    # Row 1
    [50, 60]     # Row 2
])
```

### Select Specific Rows

```python
# Select row 0 and row 2
matrix[[0, 2]]
```

### Output

```python
[[10 20]
 [50 60]]
```

### Visual Explanation

```
Original Matrix:
┌────┬────┐
│ 10 │ 20 │  ← Row 0 ✓
├────┼────┤
│ 30 │ 40 │  ← Row 1 ✗
├────┼────┤
│ 50 │ 60 │  ← Row 2 ✓
└────┴────┘

Select: [[0, 2]]

Result:
┌────┬────┐
│ 10 │ 20 │
├────┼────┤
│ 50 │ 60 │
└────┴────┘
```

### Advanced: Select Specific Elements

```python
# Select (row 0, col 1) and (row 2, col 0)
matrix[[0, 2], [1, 0]]
```

```python
# Output: [20 50]
```

```
Requested: (0,1) → 20
           (2,0) → 50
Result: [20 50]
```

---

## 🧠 Step 9: Boolean vs Fancy (When to Use What)

### Comparison Table

| Situation | Method | Example |
|-----------|--------|---------|
| Filter by **condition** | Boolean Masking | `a[a > 50]` |
| Pick **specific positions** | Fancy Indexing | `a[[0, 2, 4]]` |
| Filter with **multiple conditions** | Boolean Masking | `a[(a > 20) & (a < 80)]` |
| Select **non-contiguous rows** | Fancy Indexing | `matrix[[0, 2, 5]]` |
| **Modify** filtered data | Boolean Masking | `a[a < 0] = 0` |
| **Reorder** elements | Fancy Indexing | `a[[2, 0, 1]]` |

### Decision Flowchart

```
Do you want to select data?
           │
           ▼
    ┌──────────────┐
    │ Based on a   │
    │ CONDITION?   │
    └──────────────┘
      │         │
     YES        NO
      │         │
      ▼         ▼
  ┌───────┐  ┌──────────────┐
  │Boolean│  │ Based on     │
  │Masking│  │ specific     │
  └───────┘  │ POSITIONS?   │
             └──────────────┘
                    │
                   YES
                    │
                    ▼
              ┌──────────┐
              │  Fancy   │
              │ Indexing │
              └──────────┘
```

---

## 📝 DAY 3 PRACTICE (NO ESCAPE 😤)

### Task 1: Basic Boolean Masking

```python
arr = np.array([12, 45, 67, 23, 90, 34])
```

**Complete these operations:**

- [ ] Get all values > 40
- [ ] Get all values between 20 and 70 (inclusive)

<details>
<summary>💡 Solution (Try First!)</summary>

```python
import numpy as np

arr = np.array([12, 45, 67, 23, 90, 34])

# Values > 40
print(arr[arr > 40])
# Output: [45 67 90]

# Values between 20 and 70
print(arr[(arr >= 20) & (arr <= 70)])
# Output: [45 67 23 34]
```

</details>

---

### Task 2: 2D Array Operations

Create a 2D marks array:

```python
marks_2d = np.array([
    [78, 85, 92],
    [45, 55, 48],
    [88, 76, 94],
    [38, 42, 51]
])
```

**Complete these operations:**

- [ ] Extract all marks > 80
- [ ] Increase all marks < 50 by +10

<details>
<summary>💡 Solution (Try First!)</summary>

```python
import numpy as np

marks_2d = np.array([
    [78, 85, 92],
    [45, 55, 48],
    [88, 76, 94],
    [38, 42, 51]
])

# Extract all marks > 80
high_marks = marks_2d[marks_2d > 80]
print("Marks > 80:", high_marks)
# Output: [85 92 88 94]

# Increase marks < 50 by +10
marks_2d[marks_2d < 50] += 10
print("Updated marks:")
print(marks_2d)
# Output:
# [[78 85 92]
#  [55 55 58]
#  [88 76 94]
#  [48 52 51]]
```

</details>

---

### Task 3: Brain Exercise 🧠

**Question:** Why does NumPy use `&` instead of `and`?

<details>
<summary>💡 Answer</summary>

### The Technical Reason:

1. **`and` is a Python keyword** designed for **single boolean values**
   ```python
   True and False  # Works: returns False
   ```

2. **`&` is a bitwise operator** that works **element-by-element** on arrays
   ```python
   [True, False] & [True, True]  # Works: returns [True, False]
   ```

### Why `and` Fails with Arrays:

```python
arr1 = np.array([True, False, True])
arr2 = np.array([True, True, False])

# Python's 'and' doesn't know how to handle arrays
arr1 and arr2  # ValueError: ambiguous!
```

Python asks: *"Is the entire array True or False?"* — but an array has MULTIPLE values!

### Solution: Use Bitwise Operators

| Python Keyword | NumPy Operator | Meaning |
|----------------|----------------|---------|
| `and` | `&` | Element-wise AND |
| `or` | `\|` | Element-wise OR |
| `not` | `~` | Element-wise NOT |

### Memory Trick:
> **NumPy arrays need ELEMENT-WISE operations, not WHOLE-ARRAY logic!**

</details>

---

### Task 4: Fancy Indexing Practice

```python
data = np.array([100, 200, 300, 400, 500, 600])
```

- [ ] Select elements at positions 0, 3, and 5
- [ ] Reverse the array using fancy indexing

<details>
<summary>💡 Solution (Try First!)</summary>

```python
import numpy as np

data = np.array([100, 200, 300, 400, 500, 600])

# Select positions 0, 3, and 5
selected = data[[0, 3, 5]]
print(selected)
# Output: [100 400 600]

# Reverse using fancy indexing
reversed_arr = data[[5, 4, 3, 2, 1, 0]]
print(reversed_arr)
# Output: [600 500 400 300 200 100]

# Alternative (using slicing - simpler!)
print(data[::-1])
# Output: [600 500 400 300 200 100]
```

</details>

---

## 🚫 Today's Rules

| ❌ FORBIDDEN | ✅ REQUIRED |
|--------------|-------------|
| `for` loops | Boolean masking |
| `if-else` statements | Fancy indexing |
| `while` loops | Vectorized operations |
| Python's `and`/`or` | NumPy's `&`/`\|` |

---

## 🔒 Day 3 Checkpoint

### Self-Assessment Checklist

Before moving to Day 4, ensure you can:

- [ ] **Filter data without loops**
  ```python
  arr[arr > 50]  # Not for loops!
  ```

- [ ] **Explain Boolean masks**
  - A mask is an array of True/False values
  - True = include, False = exclude

- [ ] **Use multiple conditions correctly**
  ```python
  arr[(condition1) & (condition2)]  # AND
  arr[(condition1) | (condition2)]  # OR
  ```

- [ ] **Modify data using conditions**
  ```python
  arr[arr < 0] = 0  # Replace negatives with zero
  ```

- [ ] **Use fancy indexing for specific selections**
  ```python
  arr[[0, 2, 4]]  # Select indices 0, 2, and 4
  ```

---

## 📊 Quick Reference Card

```python
# ═══════════════════════════════════════════════════════════
#                    BOOLEAN MASKING
# ═══════════════════════════════════════════════════════════

# Create mask
mask = arr > 50              # Returns: [False, True, True, ...]

# Apply mask
arr[arr > 50]                # Filter: get values > 50

# Multiple conditions
arr[(arr > 20) & (arr < 80)] # AND condition
arr[(arr < 20) | (arr > 80)] # OR condition
arr[~(arr > 50)]             # NOT condition (inverse)

# Modify using mask
arr[arr < 0] = 0             # Replace negatives with 0
arr[arr > 100] = 100         # Cap at 100

# ═══════════════════════════════════════════════════════════
#                    FANCY INDEXING
# ═══════════════════════════════════════════════════════════

# 1D fancy indexing
arr[[0, 2, 4]]               # Select specific indices

# 2D fancy indexing (rows)
matrix[[0, 2]]               # Select rows 0 and 2

# 2D fancy indexing (specific elements)
matrix[[0, 1], [2, 3]]       # Select (0,2) and (1,3)

# ═══════════════════════════════════════════════════════════
#                    OPERATOR REFERENCE
# ═══════════════════════════════════════════════════════════

# Comparison operators (return boolean arrays)
arr > 50                     # Greater than
arr >= 50                    # Greater than or equal
arr < 50                     # Less than
arr <= 50                    # Less than or equal
arr == 50                    # Equal to
arr != 50                    # Not equal to

# Logical operators (for combining conditions)
&                            # AND (element-wise)
|                            # OR (element-wise)
~                            # NOT (element-wise)
```

---

## 🎯 Real-World Applications

| Industry | Use Case | Example |
|----------|----------|---------|
| 📊 Finance | Filter profitable stocks | `stocks[stocks['return'] > 0.05]` |
| 🏥 Healthcare | Find abnormal readings | `bp[bp > 140]` |
| 🛒 E-commerce | Select premium customers | `customers[customers['spend'] > 1000]` |
| 🌡️ Weather | Extreme temperature days | `temps[(temps < 0) \| (temps > 40)]` |
| 🎮 Gaming | High-score players | `scores[scores > threshold]` |

---

## 🔗 Navigation

| Previous | Current | Next |
|----------|---------|------|
| [Day 2: Indexing & Slicing](https://github.com/Saad-Shaikh095/30-Days-Numpy-for-Data-Science-/tree/main/Phase%201%20Foundations/Day%202%20Indexing%20and%20Slicing) | **Day 3: Boolean Masking & Fancy Indexing** | [Day 4: Array Operations](https://github.com/Saad-Shaikh095/30-Days-Numpy-for-Data-Science-/tree/main/Phase%201%20Foundations/Day%204%20RESHAPING%2C%20FLATTENING%20%26%20MEMORY%20MAGIC) |

---

<div align="center">

### 💡 Key Insight

*"In NumPy, think in CONDITIONS, not in LOOPS"*

---

### 🏆 Achievement Unlocked!

**🎖️ Data Filter Master**

*You can now filter data like a Data Scientist!*

---

**Happy Coding! 🚀**

![Made with NumPy](https://img.shields.io/badge/Made%20with-NumPy-013243?style=flat&logo=numpy)
![PRO Level](https://img.shields.io/badge/Level-PRO-gold?style=flat)

</div>

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.