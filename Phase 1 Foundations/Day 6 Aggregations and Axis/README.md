# 📅 DAY 6 – AGGREGATIONS & AXIS

> **"Numbers → Meaning → Decisions"** — Transform raw data into actionable insights

![NumPy](https://img.shields.io/badge/NumPy-Day%206-013243?style=for-the-badge&logo=numpy)
![Python](https://img.shields.io/badge/Python-3.x-blue?style=for-the-badge&logo=python)
![Level](https://img.shields.io/badge/Level-Intermediate-yellow?style=for-the-badge)
![Data Science](https://img.shields.io/badge/Data%20Science-Core%20Skill-purple?style=for-the-badge)

---

## 🎯 Today's Goals

By the end of Day 6, you will:

| Goal | Description | Real-World Impact |
|------|-------------|-------------------|
| 📊 | Summarize data like a pro | Create reports & dashboards |
| 🎯 | Understand **axis** (most confusing → now easiest!) | Analyze rows & columns correctly |
| 💡 | Extract insights from tables | Make data-driven decisions |

> 🔥 **The `axis` parameter is asked in 90% of NumPy interviews!**

---

## 📚 Table of Contents

- [Step 1: What Are Aggregations?](#-step-1-what-are-aggregations)
- [Step 2: Basic Aggregation Functions](#-step-2-basic-aggregation-functions)
- [Step 3: 2D Data Introduction](#-step-3-2d-data-where-axis-comes-in)
- [Step 4: Understanding Axis](#-step-4-understanding-axis-super-clear-)
- [Step 5: Aggregations with Axis](#-step-5-aggregations-with-axis)
- [Step 6: Real-Life Examples](#-step-6-real-life-examples)
- [Step 7: Arg Functions](#-step-7-arg-functions-find-position)
- [Step 8: Combined Logic](#-step-8-combined-logic-pro-level)
- [Practice Exercises](#-day-6-practice-dont-skip-)
- [Checkpoint](#-day-6-checkpoint)

---

## 🧠 Step 1: What Are Aggregations?

### The Concept

> **Aggregation** = Taking **many values** and producing **one meaningful number**

### Why Aggregations Matter

```
Raw Data:                    Aggregated Insight:
┌─────────────────────┐      ┌────────────────────────┐
│ 85, 90, 78, 92, 88  │  →   │ Average Score: 86.6    │
│ 45, 67, 89, 23, 56  │      │ Total Sales: $280      │
│ 32, 35, 31, 38, 30  │      │ Max Temperature: 38°C  │
└─────────────────────┘      └────────────────────────┘
     Numbers                      Meaning
```

### Common Aggregations in Real Life

| Domain | Raw Data | Aggregation | Insight |
|--------|----------|-------------|---------|
| 📚 Education | Student marks | Mean | Class average |
| 💰 Business | Daily sales | Sum | Monthly revenue |
| 🌡️ Weather | Hourly temps | Max | Day's high |
| 🏥 Healthcare | BP readings | Min/Max | Risk assessment |
| 📈 Finance | Stock prices | Std | Volatility |

### The Data Science Pipeline

```
┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│  Raw Data    │ ──► │ Aggregation  │ ──► │  Decision    │
│  (Numbers)   │     │  (Summary)   │     │  (Action)    │
└──────────────┘     └──────────────┘     └──────────────┘
    1000 rows           1 number         "Hire more staff"
```

---

## 🔢 Step 2: Basic Aggregation Functions

### Setup

```python
import numpy as np

a = np.array([10, 20, 30, 40, 50])
```

### All Basic Aggregations

```python
np.sum(a)      # 150       Total of all elements
np.mean(a)     # 30.0      Average value
np.max(a)      # 50        Maximum value
np.min(a)      # 10        Minimum value
np.std(a)      # 14.14...  Standard deviation
np.var(a)      # 200.0     Variance
np.median(a)   # 30.0      Middle value
np.prod(a)     # 12000000  Product of all elements
```

### Visual Representation

```
Array: [10, 20, 30, 40, 50]
        ↓   ↓   ↓   ↓   ↓
        └───┴───┼───┴───┘
                ↓
        ┌───────────────┐
        │  AGGREGATION  │
        └───────────────┘
                ↓
          One Number
          
sum  → 10+20+30+40+50 = 150
mean → 150/5 = 30
max  → 50
min  → 10
```

### Method vs Function Syntax

```python
# Both work exactly the same!

# Function syntax
np.sum(a)      # 150
np.mean(a)     # 30.0

# Method syntax
a.sum()        # 150
a.mean()       # 30.0
```

### 📌 Daily Use in Data Science

| Function | Use Case |
|----------|----------|
| `sum()` | Total revenue, total items |
| `mean()` | Average performance, typical value |
| `max()` | Peak values, records |
| `min()` | Lowest points, minimum requirements |
| `std()` | Consistency, risk measurement |
| `var()` | Spread of data, uncertainty |

---

## 🧠 Step 3: 2D Data (Where Axis Comes In)

### Creating a Real Dataset

```python
marks = np.array([
    [70, 80, 90],   # Student 0: Math, Science, English
    [60, 75, 85],   # Student 1: Math, Science, English
    [88, 92, 95]    # Student 2: Math, Science, English
])
```

### Visual Structure

```
                    Subjects (Columns)
                   Math  Science  English
                   Col0   Col1    Col2
                  ┌──────┬───────┬───────┐
    Student 0     │  70  │  80   │  90   │  Row 0
    (Rows)        ├──────┼───────┼───────┤
    Student 1     │  60  │  75   │  85   │  Row 1
                  ├──────┼───────┼───────┤
    Student 2     │  88  │  92   │  95   │  Row 2
                  └──────┴───────┴───────┘
```

### The Question

> **"What if I want the average per STUDENT? Or per SUBJECT?"**
> 
> This is where **axis** becomes essential!

### Without Axis (Global Aggregation)

```python
np.mean(marks)  # 81.67 — Average of ALL values
```

```
All 9 values → One number
[70, 80, 90, 60, 75, 85, 88, 92, 95] → 81.67
```

But this doesn't tell us:
- ❓ Which student is performing best?
- ❓ Which subject has highest average?

---

## 🔥 Step 4: Understanding Axis (SUPER CLEAR 🧠)

### The Golden Rule

```
┌─────────────────────────────────────────────────────────────┐
│                                                             │
│   axis=0  →  Operation goes DOWN    ⬇️  (along columns)     │
│   axis=1  →  Operation goes ACROSS  ➡️  (along rows)        │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### Visual Memory Trick

```
         axis=0 (⬇️ DOWN)
              │
              │     Col0    Col1    Col2
              ▼   ┌──────┬───────┬───────┐
    Row 0         │  70  │  80   │  90   │
                  ├──────┼───────┼───────┤
    Row 1         │  60  │  75   │  85   │ ──────► axis=1 (➡️ ACROSS)
                  ├──────┼───────┼───────┤
    Row 2         │  88  │  92   │  95   │
                  └──────┴───────┴───────┘
```

### 🧠 Memory Tricks

| Trick | axis=0 | axis=1 |
|-------|--------|--------|
| **Direction** | ⬇️ Vertical (Down) | ➡️ Horizontal (Across) |
| **Collapses** | Rows (becomes 1 row) | Columns (becomes 1 column) |
| **Result** | Per-column stats | Per-row stats |
| **Think of** | "Flatten rows" | "Flatten columns" |

### Another Way to Remember

```
axis=0: "Along axis 0" = Row indices change (0,1,2...) as you go DOWN
axis=1: "Along axis 1" = Column indices change (0,1,2...) as you go ACROSS
```

### The "Collapse" Mental Model

```
axis=0 COLLAPSES rows into one:

┌──────┬───────┬───────┐
│  70  │  80   │  90   │ ─┐
├──────┼───────┼───────┤  │
│  60  │  75   │  85   │ ─┼─► Collapse DOWN
├──────┼───────┼───────┤  │
│  88  │  92   │  95   │ ─┘
└──────┴───────┴───────┘
         ↓↓↓
┌──────┬───────┬───────┐
│72.67 │ 82.33 │ 90.0  │     Result: (3,) — one value per column
└──────┴───────┴───────┘


axis=1 COLLAPSES columns into one:

┌──────┬───────┬───────┐     ┌───────┐
│  70  │  80   │  90   │ ──► │ 80.0  │
├──────┼───────┼───────┤     ├───────┤
│  60  │  75   │  85   │ ──► │ 73.33 │
├──────┼───────┼───────┤     ├───────┤
│  88  │  92   │  95   │ ──► │ 91.67 │
└──────┴───────┴───────┘     └───────┘
  Collapse ACROSS             Result: (3,) — one value per row
```

---

## 📊 Step 5: Aggregations with Axis

### Average Marks per Subject (axis=0)

```python
np.mean(marks, axis=0)
```

```python
# Output: [72.67, 82.33, 90.0]
#          Math   Science English
```

### How It Works

```
Calculation for axis=0:

Col 0 (Math):    (70 + 60 + 88) / 3 = 72.67
Col 1 (Science): (80 + 75 + 92) / 3 = 82.33
Col 2 (English): (90 + 85 + 95) / 3 = 90.0

Result: [72.67, 82.33, 90.0]
```

### Average Marks per Student (axis=1)

```python
np.mean(marks, axis=1)
```

```python
# Output: [80.0, 73.33, 91.67]
#         Stud0  Stud1   Stud2
```

### How It Works

```
Calculation for axis=1:

Row 0 (Student 0): (70 + 80 + 90) / 3 = 80.0
Row 1 (Student 1): (60 + 75 + 85) / 3 = 73.33
Row 2 (Student 2): (88 + 92 + 95) / 3 = 91.67

Result: [80.0, 73.33, 91.67]
```

### Complete Comparison

```python
marks = np.array([
    [70, 80, 90],
    [60, 75, 85],
    [88, 92, 95]
])

# No axis — Global
np.mean(marks)           # 81.67 (all values)

# axis=0 — Per column (subjects)
np.mean(marks, axis=0)   # [72.67, 82.33, 90.0]

# axis=1 — Per row (students)
np.mean(marks, axis=1)   # [80.0, 73.33, 91.67]
```

### Visual Summary

```
┌──────────────────────────────────────────────────────────┐
│                    marks array (3×3)                     │
│              ┌──────┬───────┬───────┐                    │
│              │  70  │  80   │  90   │ → mean=80.0        │
│              ├──────┼───────┼───────┤                    │
│              │  60  │  75   │  85   │ → mean=73.33       │
│              ├──────┼───────┼───────┤                    │
│              │  88  │  92   │  95   │ → mean=91.67       │
│              └──────┴───────┴───────┘                    │
│                 ↓      ↓       ↓                         │
│               72.67  82.33   90.0                        │
│                                                          │
│  axis=0: Results at bottom (per column)                  │
│  axis=1: Results on right (per row)                      │
└──────────────────────────────────────────────────────────┘
```

---

## 🧠 Step 6: Real-Life Examples

### Example 1: Highest Score per Subject

```python
np.max(marks, axis=0)
```

```python
# Output: [88, 92, 95]
#         Math's highest, Science's highest, English's highest
```

### Visual

```
              Math  Science  English
            ┌──────┬───────┬───────┐
Student 0   │  70  │  80   │  90   │
            ├──────┼───────┼───────┤
Student 1   │  60  │  75   │  85   │
            ├──────┼───────┼───────┤
Student 2   │  88★ │  92★  │  95★  │  ← All max values
            └──────┴───────┴───────┘
                ↓      ↓       ↓
Result:       [88]   [92]    [95]
```

### Example 2: Lowest Score per Student

```python
np.min(marks, axis=1)
```

```python
# Output: [70, 60, 88]
#         Student 0's worst, Student 1's worst, Student 2's worst
```

### Example 3: Total Marks per Student

```python
np.sum(marks, axis=1)
```

```python
# Output: [240, 220, 275]
#         Student 0 total, Student 1 total, Student 2 total
```

### Example 4: Subject Consistency (Standard Deviation)

```python
np.std(marks, axis=0)
```

```python
# Output: [11.67, 7.09, 4.08]
#         Math varies most, English is most consistent
```

### 🔥 Real Report Generation

```python
# Complete Student Performance Report
marks = np.array([
    [70, 80, 90],
    [60, 75, 85],
    [88, 92, 95]
])

print("=" * 50)
print("STUDENT PERFORMANCE REPORT")
print("=" * 50)
print(f"Subject Averages:    {np.mean(marks, axis=0)}")
print(f"Subject Highest:     {np.max(marks, axis=0)}")
print(f"Subject Lowest:      {np.min(marks, axis=0)}")
print("-" * 50)
print(f"Student Averages:    {np.mean(marks, axis=1)}")
print(f"Student Totals:      {np.sum(marks, axis=1)}")
print(f"Class Average:       {np.mean(marks):.2f}")
print("=" * 50)
```

### Output

```
==================================================
STUDENT PERFORMANCE REPORT
==================================================
Subject Averages:    [72.67 82.33 90.  ]
Subject Highest:     [88 92 95]
Subject Lowest:      [60 75 85]
--------------------------------------------------
Student Averages:    [80.   73.33 91.67]
Student Totals:      [240 220 275]
Class Average:       81.67
==================================================
```

---

## 🔍 Step 7: Arg Functions (Find Position)

### What Are Arg Functions?

> **Arg functions** return the **INDEX** (position) of the value, not the value itself!

### Basic Usage

```python
a = np.array([10, 50, 30, 20, 40])

np.argmax(a)    # 1 (index of 50)
np.argmin(a)    # 0 (index of 10)
```

### Visual Explanation

```
Array:    [10]  [50]  [30]  [20]  [40]
Index:      0     1     2     3     4
                  ↑
            argmax → 1 (position of 50)
            
            ↑
      argmin → 0 (position of 10)
```

### Why Index, Not Value?

```python
a = np.array([10, 50, 30, 20, 40])

# If you want the VALUE:
max_value = np.max(a)           # 50

# If you want to FIND it (for further operations):
max_index = np.argmax(a)        # 1
max_value = a[max_index]        # 50

# Useful when you need to access related data:
students = ["Alice", "Bob", "Charlie"]
scores = np.array([85, 92, 78])

top_scorer_idx = np.argmax(scores)  # 1
top_scorer = students[top_scorer_idx]  # "Bob"
```

### Arg Functions with Axis

```python
marks = np.array([
    [70, 80, 90],
    [60, 75, 85],
    [88, 92, 95]
])

# Which student scored highest in each subject?
np.argmax(marks, axis=0)
```

```python
# Output: [2, 2, 2]
# Student 2 topped all subjects!
```

### Visual

```
              Math  Science  English
            ┌──────┬───────┬───────┐
Student 0   │  70  │  80   │  90   │  index 0
            ├──────┼───────┼───────┤
Student 1   │  60  │  75   │  85   │  index 1
            ├──────┼───────┼───────┤
Student 2   │  88★ │  92★  │  95★  │  index 2
            └──────┴───────┴───────┘
                ↓      ↓       ↓
argmax(axis=0): 2      2       2

"Student at index 2 scored highest in each subject"
```

### Which Subject Each Student Scored Best In

```python
np.argmax(marks, axis=1)
```

```python
# Output: [2, 2, 2]
# All students scored best in English (column 2)!
```

### All Arg Functions

| Function | Returns |
|----------|---------|
| `np.argmax(arr)` | Index of maximum value |
| `np.argmin(arr)` | Index of minimum value |
| `np.argsort(arr)` | Indices that would sort the array |
| `np.argwhere(condition)` | Indices where condition is True |

---

## 🧠 Step 8: Combined Logic (Pro Level)

### Problem: Find the Topper

> Who has the highest **total** marks?

```python
marks = np.array([
    [70, 80, 90],   # Student 0: Total = 240
    [60, 75, 85],   # Student 1: Total = 220
    [88, 92, 95]    # Student 2: Total = 275
])

# Step 1: Get total marks per student
totals = np.sum(marks, axis=1)
print(totals)  # [240, 220, 275]

# Step 2: Find who has the highest total
topper_index = np.argmax(totals)
print(f"Topper: Student {topper_index}")  # Student 2

# Step 3: Get topper's marks
topper_marks = marks[topper_index]
print(f"Marks: {topper_marks}")  # [88, 92, 95]
```

### 🔥 Interview-Style Logic Flow

```
┌─────────────────────────────────────────────────────────────┐
│                    FIND THE TOPPER                          │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Step 1: Calculate totals                                   │
│  ┌──────┬───────┬───────┐     ┌─────┐                      │
│  │  70  │  80   │  90   │ ──► │ 240 │                      │
│  ├──────┼───────┼───────┤     ├─────┤                      │
│  │  60  │  75   │  85   │ ──► │ 220 │  sum(axis=1)         │
│  ├──────┼───────┼───────┤     ├─────┤                      │
│  │  88  │  92   │  95   │ ──► │ 275 │                      │
│  └──────┴───────┴───────┘     └─────┘                      │
│                                                             │
│  Step 2: Find max index                                     │
│  [240, 220, 275]  →  argmax()  →  2                        │
│                                                             │
│  Step 3: Get topper's data                                  │
│  marks[2]  →  [88, 92, 95]                                 │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### More Complex Examples

#### Example 1: Find Students Above Average

```python
# Calculate class average
class_avg = np.mean(marks)  # 81.67

# Get each student's average
student_avgs = np.mean(marks, axis=1)  # [80, 73.33, 91.67]

# Find who's above class average
above_avg = student_avgs > class_avg
print(above_avg)  # [False, False, True]

# Get their indices
above_avg_indices = np.where(above_avg)[0]
print(f"Students above average: {above_avg_indices}")  # [2]
```

#### Example 2: Rank Students

```python
totals = np.sum(marks, axis=1)  # [240, 220, 275]

# Get ranks (indices that would sort in descending order)
ranks = np.argsort(totals)[::-1]
print(f"Ranking (best to worst): {ranks}")  # [2, 0, 1]

# Student 2 is 1st, Student 0 is 2nd, Student 1 is 3rd
```

#### Example 3: Grade Distribution

```python
# Count students scoring above 80 in each subject
high_scorers = np.sum(marks > 80, axis=0)
print(f"Students >80 per subject: {high_scorers}")
# [1, 2, 3] → Math: 1 student, Science: 2, English: 3
```

### 🎯 One-Liner Challenge

```python
# Find topper in ONE LINE
topper = np.argmax(np.sum(marks, axis=1))
print(f"Topper: Student {topper}")  # Student 2
```

---

## 📝 DAY 6 PRACTICE (DON'T SKIP 😤)

### Task 1: 1D Aggregations

```python
data = np.array([15, 22, 8, 33, 27, 19, 41, 12])
```

**Complete these operations:**

- [ ] Find the sum
- [ ] Calculate the mean
- [ ] Find the standard deviation
- [ ] Find the range (max - min)

<details>
<summary>💡 Solution (Try First!)</summary>

```python
import numpy as np

data = np.array([15, 22, 8, 33, 27, 19, 41, 12])

# Sum
print(f"Sum: {np.sum(data)}")  # 177

# Mean
print(f"Mean: {np.mean(data)}")  # 22.125

# Standard Deviation
print(f"Std: {np.std(data):.2f}")  # 10.20

# Range
print(f"Range: {np.max(data) - np.min(data)}")  # 41 - 8 = 33

# Bonus: All stats at once
print(f"Min: {np.min(data)}, Max: {np.max(data)}")
print(f"Median: {np.median(data)}")  # 20.5
```

</details>

---

### Task 2: 2D Aggregations with Axis

```python
sales = np.array([
    [150, 200, 180],   # Store 0: Jan, Feb, Mar
    [220, 190, 210],   # Store 1: Jan, Feb, Mar
    [180, 170, 195],   # Store 2: Jan, Feb, Mar
    [200, 230, 185]    # Store 3: Jan, Feb, Mar
])
```

**Complete these operations:**

- [ ] Average sales per store (which stores perform best?)
- [ ] Average sales per month (which months are strongest?)
- [ ] Find the store with highest total sales
- [ ] Find the month with lowest average sales

<details>
<summary>💡 Solution (Try First!)</summary>

```python
import numpy as np

sales = np.array([
    [150, 200, 180],   # Store 0
    [220, 190, 210],   # Store 1
    [180, 170, 195],   # Store 2
    [200, 230, 185]    # Store 3
])

# Average per store (axis=1, across months)
store_avg = np.mean(sales, axis=1)
print(f"Store Averages: {store_avg}")
# [176.67, 206.67, 181.67, 205.0]

# Average per month (axis=0, down stores)
month_avg = np.mean(sales, axis=0)
print(f"Month Averages: {month_avg}")
# [187.5, 197.5, 192.5]

# Store with highest total
store_totals = np.sum(sales, axis=1)
best_store = np.argmax(store_totals)
print(f"Best Store: Store {best_store} (Total: {store_totals[best_store]})")
# Store 1 (Total: 620)

# Month with lowest average
worst_month_idx = np.argmin(month_avg)
months = ["January", "February", "March"]
print(f"Weakest Month: {months[worst_month_idx]} (Avg: {month_avg[worst_month_idx]})")
# January (Avg: 187.5)
```

</details>

---

### Task 3: Deep Thinking 🧠

**Question:** Why is axis important in data analysis?

<details>
<summary>💡 Answer</summary>

### Why Axis is Essential:

#### 1. **Different Questions Require Different Directions**

```python
marks = np.array([
    [70, 80, 90],   # Student 0
    [60, 75, 85],   # Student 1
    [88, 92, 95]    # Student 2
])
#   Math Sci  Eng
```

| Question | Required Axis | Code |
|----------|---------------|------|
| "What's each student's average?" | axis=1 | `np.mean(marks, axis=1)` |
| "What's each subject's average?" | axis=0 | `np.mean(marks, axis=0)` |

Without axis, you'd only get ONE number for all data!

#### 2. **Real Data Has Structure**

```
Sales Data:
           Q1    Q2    Q3    Q4
Region A   100   120   130   150
Region B   80    90    100   110
Region C   150   160   170   180

Questions you NEED to answer:
- Which region performed best? (sum across columns, axis=1)
- Which quarter was strongest? (sum down rows, axis=0)
```

#### 3. **Preserves Data Relationships**

```python
# Without axis: Loses structure
np.mean(marks)  # 81.67 — Just one number, no context

# With axis: Preserves meaning
np.mean(marks, axis=0)  # [72.67, 82.33, 90.0]
# You can now say "English has highest average"
```

#### 4. **Enables Comparative Analysis**

```python
# Compare students to subject averages
subject_avgs = np.mean(marks, axis=0)  # [72.67, 82.33, 90.0]

# Now find who's above average in each subject!
above_avg = marks > subject_avgs
```

#### Summary:
> **Axis gives DIRECTION to aggregation, allowing you to answer specific business questions about your data!**

</details>

---

### Task 4: Practical Challenge

You have exam scores for 5 students in 4 subjects:

```python
exams = np.array([
    [78, 82, 88, 91],   # Alice
    [92, 88, 95, 89],   # Bob
    [65, 70, 72, 68],   # Charlie
    [88, 92, 85, 90],   # Diana
    [75, 78, 80, 82]    # Eve
])
subjects = ["Math", "Science", "English", "History"]
students = ["Alice", "Bob", "Charlie", "Diana", "Eve"]
```

Find:
- [ ] Who has the highest overall average?
- [ ] Which subject has the lowest class average?
- [ ] How many students scored above 85 in each subject?

<details>
<summary>💡 Solution (Try First!)</summary>

```python
import numpy as np

exams = np.array([
    [78, 82, 88, 91],   # Alice
    [92, 88, 95, 89],   # Bob
    [65, 70, 72, 68],   # Charlie
    [88, 92, 85, 90],   # Diana
    [75, 78, 80, 82]    # Eve
])
subjects = ["Math", "Science", "English", "History"]
students = ["Alice", "Bob", "Charlie", "Diana", "Eve"]

# 1. Highest overall average
student_avgs = np.mean(exams, axis=1)
top_student_idx = np.argmax(student_avgs)
print(f"Top Student: {students[top_student_idx]}")
print(f"Average: {student_avgs[top_student_idx]:.2f}")
# Bob with 91.0

# 2. Lowest class average subject
subject_avgs = np.mean(exams, axis=0)
lowest_subject_idx = np.argmin(subject_avgs)
print(f"\nLowest Subject: {subjects[lowest_subject_idx]}")
print(f"Average: {subject_avgs[lowest_subject_idx]:.2f}")
# Math with 79.6

# 3. Students above 85 per subject
above_85_count = np.sum(exams > 85, axis=0)
print(f"\nStudents scoring >85 per subject:")
for i, subject in enumerate(subjects):
    print(f"  {subject}: {above_85_count[i]} students")
# Math: 2, Science: 2, English: 3, History: 4
```

</details>

---

## 🚫 Today's Rules

| ❌ FORBIDDEN | ✅ REQUIRED |
|--------------|-------------|
| Guessing axis | Visualize rows/columns first |
| Blind aggregation | Know what question you're answering |
| Copy-paste coding | Understand the direction |
| Ignoring structure | Preserve data relationships |

---

## 🔒 Day 6 Checkpoint

### Self-Assessment Checklist

Before moving to Day 7, ensure you can:

- [ ] **Explain axis=0 vs axis=1**
  ```
  axis=0: Down columns (⬇️) → Result per column
  axis=1: Across rows (➡️) → Result per row
  ```

- [ ] **Use aggregations confidently**
  ```python
  np.sum(), np.mean(), np.max(), np.min(), np.std()
  ```

- [ ] **Extract insights from tables**
  ```python
  # Per-student stats
  np.mean(marks, axis=1)
  
  # Per-subject stats
  np.mean(marks, axis=0)
  ```

- [ ] **Use arg functions**
  ```python
  np.argmax(arr)  # Index of max
  np.argmin(arr)  # Index of min
  ```

---

## 📊 Quick Reference Card

```python
# ═══════════════════════════════════════════════════════════
#                  BASIC AGGREGATIONS
# ═══════════════════════════════════════════════════════════

np.sum(arr)          # Sum of all elements
np.mean(arr)         # Average
np.max(arr)          # Maximum value
np.min(arr)          # Minimum value
np.std(arr)          # Standard deviation
np.var(arr)          # Variance
np.median(arr)       # Median (middle value)
np.prod(arr)         # Product of all elements

# ═══════════════════════════════════════════════════════════
#                  AXIS PARAMETER
# ═══════════════════════════════════════════════════════════

# 2D Array:
#              Col0  Col1  Col2
#            ┌─────┬─────┬─────┐
#   Row 0    │     │     │     │ ──► axis=1 (across)
#            ├─────┼─────┼─────┤
#   Row 1    │     │     │     │
#            └─────┴─────┴─────┘
#               ↓     ↓     ↓
#             axis=0 (down)

np.sum(arr, axis=0)      # Sum per column
np.sum(arr, axis=1)      # Sum per row
np.mean(arr, axis=0)     # Mean per column
np.mean(arr, axis=1)     # Mean per row

# ═══════════════════════════════════════════════════════════
#                  ARG FUNCTIONS
# ═══════════════════════════════════════════════════════════

np.argmax(arr)           # Index of maximum
np.argmin(arr)           # Index of minimum
np.argsort(arr)          # Indices that would sort
np.argmax(arr, axis=0)   # Index of max per column
np.argmax(arr, axis=1)   # Index of max per row

# ═══════════════════════════════════════════════════════════
#                  COMMON PATTERNS
# ═══════════════════════════════════════════════════════════

# Find topper
totals = np.sum(marks, axis=1)
topper = np.argmax(totals)

# Compare to average
avg = np.mean(arr, axis=0)
above_avg = arr > avg

# Count occurrences
np.sum(arr > threshold, axis=0)

# Normalize data
normalized = (arr - arr.mean()) / arr.std()
```

---

## 🎯 Axis Quick Decision Guide

```
┌─────────────────────────────────────────────────────────────┐
│                    WHICH AXIS TO USE?                       │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Q: "I want one result PER COLUMN"                          │
│  A: axis=0 (collapse rows, keep columns)                    │
│                                                             │
│  Q: "I want one result PER ROW"                             │
│  A: axis=1 (collapse columns, keep rows)                    │
│                                                             │
│  Q: "I want ONE result for everything"                      │
│  A: No axis (or axis=None)                                  │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## 🔗 Navigation

| Previous | Current | Next |
|----------|---------|------|
| [Day 5: Math & Broadcasting](https://github.com/Saad-Shaikh095/30-Days-Numpy-for-Data-Science-/tree/main/Phase%201%20Foundations/Day%205%20Mathematical%20Operations%20and%20Boardcasting) | **Day 6: Aggregations & Axis** | [Day 7: Sorting & Searching](./DAY7.md) |

---

<div align="center">

### 💡 Key Insight of Day 6

*"Axis transforms raw numbers into meaningful insights — it's the difference between data and information!"*

---

### 🧠 The Axis Mantra

```
┌─────────────────────────────────────────────────────────────┐
│                                                             │
│   axis=0  →  DOWN the rows    →  Result per COLUMN  ⬇️      │
│   axis=1  →  ACROSS the cols  →  Result per ROW     ➡️      │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

### 🏆 Achievement Unlocked!

**🎖️ Data Analyst**

*You can now summarize any dataset and extract meaningful insights!*

---

**Happy Coding! 🚀**

![Made with NumPy](https://img.shields.io/badge/Made%20with-NumPy-013243?style=flat&logo=numpy)
![Axis Master](https://img.shields.io/badge/Axis-Mastered-green?style=flat)
![Insights](https://img.shields.io/badge/Data-Insights-blue?style=flat)

</div>

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.