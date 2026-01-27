# 📅 DAY 2 – INDEXING & SLICING

> **Think in Rows & Columns** — Master the art of data extraction

![NumPy](https://img.shields.io/badge/NumPy-Day%202-013243?style=for-the-badge&logo=numpy)
![Python](https://img.shields.io/badge/Python-3.x-blue?style=for-the-badge&logo=python)
![Level](https://img.shields.io/badge/Level-Beginner-green?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=for-the-badge)

---

## 🎯 Today's Goals

By the end of Day 2, you will:

| Goal | Description |
|------|-------------|
| ✅ | Access any element confidently |
| ✅ | Slice data like a Data Scientist |
| ✅ | Stop fearing 2D arrays (tables) |

---

## 📚 Table of Contents

- [Step 1: Indexing (1D Arrays)](#-step-1-indexing-start-simple)
- [Step 2: Slicing](#-step-2-slicing-cutting-data-cleanly)
- [Step 3: 2D Arrays Introduction](#-step-3-2d-arrays-this-is-where-ds-begins)
- [Step 4: Indexing in 2D](#-step-4-indexing-in-2d-arrays)
- [Step 5: Slicing in 2D](#-step-5-slicing-in-2d-excel-magic-)
- [Step 6: Real-Life Example](#-step-6-real-life-example-student-marks)
- [Step 7: Modifying Arrays](#-step-7-modify-using-indexing)
- [Practice Exercises](#-day-2-practice-mandatory-)
- [Checkpoint](#-day-2-checkpoint)

---

## 🧠 Step 1: Indexing (Start Simple)

### 1D Array Basics

```python
import numpy as np

a = np.array([10, 20, 30, 40, 50])
```

### 📌 Understanding Index Positions

```
Index:    0    1    2    3    4
        ┌────┬────┬────┬────┬────┐
Value:  │ 10 │ 20 │ 30 │ 40 │ 50 │
        └────┴────┴────┴────┴────┘
Index:   -5   -4   -3   -2   -1
```

### Accessing Elements

```python
a[0]    # Output: 10
a[3]    # Output: 40
a[-1]   # Output: 50 (last element)
```

### 💡 Memory Trick

| Direction | Index Type | Description |
|-----------|------------|-------------|
| ➡️ Forward | Positive (`0, 1, 2...`) | Count from **start** |
| ⬅️ Backward | Negative (`-1, -2...`) | Count from **end** |

---

## 🔪 Step 2: Slicing (Cutting Data Cleanly)

### Syntax

```python
array[start : stop : step]
```

| Parameter | Description | Default |
|-----------|-------------|---------|
| `start` | Beginning index (inclusive) | `0` |
| `stop` | Ending index (exclusive) | `len(array)` |
| `step` | Increment between elements | `1` |

### Examples

```python
a[1:4]      # Output: [20 30 40]
a[:3]       # Output: [10 20 30]
a[::2]      # Output: [10 30 50]
a[::-1]     # Output: [50 40 30 20 10] (reversed!)
```

### 🎂 Analogy

> **Slicing is like cutting a cake** — decide where to start, where to end, and how big each piece should be.

---

## 🧠 Step 3: 2D Arrays (THIS IS WHERE DS BEGINS)

> Think of a 2D array as an **Excel spreadsheet** 📊

```python
b = np.array([
    [10, 20, 30],
    [40, 50, 60],
    [70, 80, 90]
])
```

### Visual Representation

```
              Col 0   Col 1   Col 2
            ┌───────┬───────┬───────┐
    Row 0   │  10   │  20   │  30   │
            ├───────┼───────┼───────┤
    Row 1   │  40   │  50   │  60   │
            ├───────┼───────┼───────┤
    Row 2   │  70   │  80   │  90   │
            └───────┴───────┴───────┘
            
            Row ↓    Col →
```

---

## 🔍 Step 4: Indexing in 2D Arrays

### Access Single Element

```python
b[0, 1]   # Output: 20 (Row 0, Column 1)
b[2, 2]   # Output: 90 (Row 2, Column 2)
```

### Access Whole Row

```python
b[1]      # Output: [40 50 60]
```

### Access Whole Column

```python
b[:, 1]   # Output: [20 50 80]
```

### 🧠 Golden Rule

```
array[ROW, COLUMN]
         ↓      ↓
       First  Second
```

| Syntax | Returns |
|--------|---------|
| `b[i]` | Row `i` |
| `b[:, j]` | Column `j` |
| `b[i, j]` | Element at row `i`, column `j` |

---

## 🔪 Step 5: Slicing in 2D (Excel Magic ✨)

```python
b[0:2, 1:3]
```

### Output

```python
[[20 30]
 [50 60]]
```

### 📌 Breaking It Down

```
b[0:2, 1:3]
   ↓     ↓
  Rows  Columns
  0-1   1-2
```

### Visual Explanation

```
Original Array:              Sliced Result:
┌────┬────┬────┐            ┌────┬────┐
│ 10 │[20]│[30]│  Row 0 ──► │ 20 │ 30 │
├────┼────┼────┤            ├────┼────┤
│ 40 │[50]│[60]│  Row 1 ──► │ 50 │ 60 │
├────┼────┼────┤            └────┴────┘
│ 70 │ 80 │ 90 │
└────┴────┴────┘
```

---

## 🧠 Step 6: Real-Life Example (Student Marks)

### Create Dataset

```python
marks = np.array([
    [70, 80, 90],   # Student 1: Math, Science, English
    [60, 75, 85],   # Student 2: Math, Science, English
    [88, 92, 95]    # Student 3: Math, Science, English
])
```

### Common Operations

| Task | Code | Output |
|------|------|--------|
| Get marks of Student 2 | `marks[1]` | `[60 75 85]` |
| Get Math marks (all students) | `marks[:, 0]` | `[70 60 88]` |
| Get top 2 students, last 2 subjects | `marks[:2, 1:]` | `[[80 90] [75 85]]` |

```python
# Get marks of Student 2
marks[1]              # Output: [60 75 85]

# Get Math marks of all students (column 0)
marks[:, 0]           # Output: [70 60 88]

# Get top 2 students, last 2 subjects
marks[:2, 1:]         # Output: [[80 90]
                      #          [75 85]]
```

> 🔥 **This is real Data Science slicing!**

---

## 🧠 Step 7: Modify Using Indexing

### Modify Single Element

```python
a[0] = 100
print(a)    # Output: [100 20 30 40 50]
```

### Modify in 2D Array

```python
b[1, 1] = 999
print(b)
# Output:
# [[ 10  20  30]
#  [ 40 999  60]
#  [ 70  80  90]]
```

### ⚠️ Important Warning

> **Arrays are mutable** — modifications change the **original array** in memory!

```python
# Be careful with assignments
original = np.array([1, 2, 3])
copy = original          # This is a VIEW, not a copy!
copy[0] = 999
print(original)          # [999 2 3] — Original changed!

# Use .copy() for independent copy
safe_copy = original.copy()
```

---

## 📝 DAY 2 PRACTICE (MANDATORY 🔴)

### Task 1: 1D Array Operations

Create this array:

```python
arr = np.array([5, 10, 15, 20, 25, 30])
```

**Complete these operations:**

- [ ] Print last 3 elements
- [ ] Print alternate elements

<details>
<summary>💡 Solution (Try First!)</summary>

```python
import numpy as np

arr = np.array([5, 10, 15, 20, 25, 30])

# Last 3 elements
print(arr[-3:])      # Output: [20 25 30]

# Alternate elements
print(arr[::2])      # Output: [5 15 25]
```

</details>

---

### Task 2: 2D Array Operations

Create a 3×3 matrix:

```python
matrix = np.array([
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
])
```

**Complete these operations:**

- [ ] Print middle element
- [ ] Print first row
- [ ] Print last column

<details>
<summary>💡 Solution (Try First!)</summary>

```python
import numpy as np

matrix = np.array([
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
])

# Middle element
print(matrix[1, 1])    # Output: 5

# First row
print(matrix[0])       # Output: [1 2 3]

# Last column
print(matrix[:, -1])   # Output: [3 6 9]
```

</details>

---

### Task 3: Think Like a Pro 🧠

**Question:** Explain in your own words — Why do we use `:` in `array[:, 1]`?

<details>
<summary>💡 Answer</summary>

The `:` (colon) means **"select all"** in that dimension.

- `[:, 1]` → Select **ALL rows**, but **only column 1**
- `[0, :]` → Select **row 0**, but **ALL columns**
- `[:, :]` → Select **everything**

Think of `:` as saying *"give me everything in this dimension"*.

</details>

---

## 🚫 Today's Rules

| ❌ Don't | ✅ Do |
|---------|------|
| Use loops | Use NumPy indexing |
| Copy-paste code | Type everything yourself |
| Skip exercises | Complete all tasks |
| Memorize blindly | Understand the logic |

---

## 🔒 Day 2 Checkpoint

Before moving to Day 3, you **must be able to explain**:

- [ ] **Indexing vs Slicing**
  - Indexing: Access single element (`a[0]`)
  - Slicing: Access range of elements (`a[0:3]`)

- [ ] **1D vs 2D Arrays**
  - 1D: Single row of data
  - 2D: Table with rows and columns

- [ ] **Row vs Column Access**
  - Row: `array[row_index]`
  - Column: `array[:, column_index]`

---

## 📊 Quick Reference Card

```python
# ═══════════════════════════════════════
#           1D ARRAY OPERATIONS
# ═══════════════════════════════════════
a[i]        # Element at index i
a[-1]       # Last element
a[i:j]      # Elements from i to j-1
a[::2]      # Every 2nd element
a[::-1]     # Reversed array

# ═══════════════════════════════════════
#           2D ARRAY OPERATIONS
# ═══════════════════════════════════════
b[i, j]     # Element at row i, column j
b[i]        # Entire row i
b[:, j]     # Entire column j
b[i:k, j:l] # Submatrix (rows i to k-1, cols j to l-1)
```

---

## 🔗 Navigation

| Previous | Current | Next |
|----------|---------|------|
| [Day 1: NumPy Basics](https://github.com/Saad-Shaikh095/30-Days-Numpy-for-Data-Science-/tree/main/Phase%201%20Foundations/Day%2001%20What%20Numpy%20Really%20Is) | **Day 2: Indexing & Slicing** | [Day 3: Operations](https://github.com/Saad-Shaikh095/30-Days-Numpy-for-Data-Science-/tree/main/Phase%201%20Foundations/Day%203%20Boolean%20Masking%20and%20Fancy%20Indexing) |

---

<div align="center">

### 🌟 Keep Practicing!

*"The best way to learn is by doing."*

**Happy Coding! 🚀**

</div>

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.