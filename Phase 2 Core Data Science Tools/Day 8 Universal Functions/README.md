# 📅 DAY 8 – UNIVERSAL FUNCTIONS (ufuncs) & ADVANCED MATH

> **"Math on entire datasets — fast, clean, vectorized."** — The NumPy way

![NumPy](https://img.shields.io/badge/NumPy-Day%208-013243?style=for-the-badge&logo=numpy)
![Python](https://img.shields.io/badge/Python-3.x-blue?style=for-the-badge&logo=python)
![Level](https://img.shields.io/badge/Level-Intermediate-yellow?style=for-the-badge)
![Week 2](https://img.shields.io/badge/Week%202-Started!-orange?style=for-the-badge)

---

## 🎯 Today's Goals

By the end of Day 8, you will:

| Goal | Description | Importance |
|------|-------------|------------|
| ⚡ | Master NumPy **ufuncs** | ⭐⭐⭐⭐⭐ |
| 🧮 | Apply mathematical formulas to **whole datasets** | ⭐⭐⭐⭐⭐ |
| 🚀 | Replace loops with **pure vectorized logic** | ⭐⭐⭐⭐⭐ |

> 🎉 **Welcome to Week 2!** Time to level up your NumPy skills!

---

## 📚 Table of Contents

- [Step 1: What Are ufuncs?](#-step-1-what-are-universal-functions-ufuncs)
- [Step 2: Common ufuncs](#-step-2-common-ufuncs-you-must-know-)
- [Step 3: Log & Exp Functions](#-step-3-log-exp-very-important-for-ml)
- [Step 4: Trigonometric ufuncs](#-step-4-trigonometric-ufuncs)
- [Step 5: Combining ufuncs](#-step-5-combining-ufuncs-real-power)
- [Step 6: Performance Comparison](#-step-6-ufuncs-vs-python-loops-why-it-matters)
- [Step 7: Real-Life Examples](#-step-7-real-life-example-finance-)
- [Step 8: ufuncs with Conditions](#-step-8-ufuncs-with-conditions)
- [Practice Exercises](#-day-8-practice-no-shortcuts-)
- [Checkpoint](#-day-8-checkpoint)

---

## 🧠 Step 1: What Are Universal Functions (ufuncs)?

### Definition

> **Universal Functions (ufuncs)** are NumPy's optimized functions that operate on arrays **element-by-element** at C-level speed.

### The Three Pillars of ufuncs

```
┌─────────────────────────────────────────────────────────────┐
│                    UFUNCS ARE:                              │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ⚡ FAST                                                    │
│     • Written in compiled C code                            │
│     • 10-100x faster than Python loops                      │
│                                                             │
│  🔄 VECTORIZED                                              │
│     • Operate on entire arrays at once                      │
│     • No explicit loops needed                              │
│                                                             │
│  📐 ELEMENT-WISE                                            │
│     • Apply function to each element                        │
│     • Maintain array shape                                  │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### Visual: How ufuncs Work

```
Traditional Python:                NumPy ufunc:
┌─────────────────┐               ┌─────────────────┐
│ for each item:  │               │ np.sqrt(array)  │
│   √1 → 1        │               │                 │
│   √4 → 2        │               │  √[1,4,9,16]    │
│   √9 → 3        │               │       ↓         │
│   √16 → 4       │               │  [1, 2, 3, 4]   │
└─────────────────┘               └─────────────────┘
   ↓                                    ↓
 4 separate                        1 vectorized
 operations                        operation
   
 Time: 🐢 Slow                    Time: 🚀 Fast
```

### Why "Universal"?

```python
import numpy as np

# Works on single value
np.sqrt(16)           # 4.0

# Works on 1D array
np.sqrt([1, 4, 9])    # [1., 2., 3.]

# Works on 2D array
np.sqrt([[1, 4], 
         [9, 16]])    # [[1., 2.], [3., 4.]]

# Works on ANY shape — hence "Universal"!
```

---

## 🔢 Step 2: Common ufuncs (YOU MUST KNOW 🔥)

### Setup

```python
import numpy as np

a = np.array([1, 4, 9, 16, 25])
```

### Arithmetic ufuncs

```python
# Square Root
np.sqrt(a)
# Output: [1. 2. 3. 4. 5.]

# Square
np.square(a)
# Output: [1 16 81 256 625]

# Power (any exponent)
np.power(a, 2)      # Same as square
# Output: [1 16 81 256 625]

np.power(a, 0.5)    # Same as sqrt
# Output: [1. 2. 3. 4. 5.]

# Cube root
np.cbrt([1, 8, 27, 64])
# Output: [1. 2. 3. 4.]
```

### Absolute Value

```python
b = np.array([-10, 5, -3, 8, -1])

np.abs(b)
# Output: [10 5 3 8 1]

# Also works as:
np.absolute(b)
# Output: [10 5 3 8 1]
```

### Sign Function

```python
np.sign(b)
# Output: [-1  1 -1  1 -1]
# Returns: -1 for negative, 0 for zero, 1 for positive
```

### Reciprocal

```python
np.reciprocal([1., 2., 4., 5.])
# Output: [1.   0.5  0.25 0.2]
# Note: Use floats to avoid integer division!
```

### Complete Arithmetic ufuncs Table

| Function | Description | Example |
|----------|-------------|---------|
| `np.sqrt(x)` | Square root | `√16 = 4` |
| `np.square(x)` | Square | `4² = 16` |
| `np.power(x, n)` | x to power n | `2³ = 8` |
| `np.cbrt(x)` | Cube root | `∛27 = 3` |
| `np.abs(x)` | Absolute value | `\|-5\| = 5` |
| `np.sign(x)` | Sign (-1, 0, 1) | `sign(-5) = -1` |
| `np.reciprocal(x)` | 1/x | `1/4 = 0.25` |
| `np.floor(x)` | Round down | `floor(3.7) = 3` |
| `np.ceil(x)` | Round up | `ceil(3.2) = 4` |
| `np.round(x)` | Round nearest | `round(3.5) = 4` |
| `np.trunc(x)` | Truncate decimal | `trunc(3.9) = 3` |

---

## 🧮 Step 3: Log, Exp (VERY IMPORTANT FOR ML)

### Why These Matter

```
┌─────────────────────────────────────────────────────────────┐
│              LOG & EXP IN MACHINE LEARNING                  │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  📊 Feature Scaling                                         │
│     • Log transform skewed data                             │
│     • Normalize wide-ranging values                         │
│                                                             │
│  📈 Probability                                             │
│     • Log probabilities (prevent underflow)                 │
│     • Softmax function uses exp                             │
│                                                             │
│  📉 Loss Functions                                          │
│     • Cross-entropy loss uses log                           │
│     • Logistic regression                                   │
│                                                             │
│  🧠 Neural Networks                                         │
│     • Activation functions (sigmoid = 1/(1+e^-x))           │
│     • Gradient calculations                                 │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### Logarithmic Functions

```python
a = np.array([1, 2, 10, 100])

# Natural logarithm (base e)
np.log(a)
# Output: [0.    0.693 2.303 4.605]

# Base 10 logarithm
np.log10(a)
# Output: [0. 0.301 1. 2.]

# Base 2 logarithm
np.log2(a)
# Output: [0.    1.    3.322 6.644]

# Log of (1 + x) — more accurate for small x
np.log1p([0, 0.001, 0.01])
# Output: [0.    0.001 0.01]  (approximately)
```

### Visual: Logarithm Types

```
log₁₀(x): "How many times multiply 10 to get x?"
    log₁₀(1)    = 0    (10⁰ = 1)
    log₁₀(10)   = 1    (10¹ = 10)
    log₁₀(100)  = 2    (10² = 100)
    log₁₀(1000) = 3    (10³ = 1000)

ln(x) or log(x): "How many times multiply e to get x?"
    ln(1)       = 0    (e⁰ = 1)
    ln(e)       = 1    (e¹ ≈ 2.718)
    ln(e²)      = 2    (e² ≈ 7.389)

log₂(x): "How many times multiply 2 to get x?"
    log₂(1)     = 0    (2⁰ = 1)
    log₂(2)     = 1    (2¹ = 2)
    log₂(8)     = 3    (2³ = 8)
    log₂(1024)  = 10   (2¹⁰ = 1024)
```

### Exponential Functions

```python
b = np.array([0, 1, 2, 3])

# e^x (Euler's number ≈ 2.718)
np.exp(b)
# Output: [1.    2.718 7.389 20.086]

# 2^x
np.exp2(b)
# Output: [1. 2. 4. 8.]

# e^x - 1 (more accurate for small x)
np.expm1([0, 0.001, 0.01])
# Output: [0.    0.001 0.01]  (approximately)
```

### Log-Exp Relationship

```python
x = np.array([1, 2, 3, 4, 5])

# Log and Exp are inverses!
np.exp(np.log(x))
# Output: [1. 2. 3. 4. 5.]  — Back to original!

np.log(np.exp(x))
# Output: [1. 2. 3. 4. 5.]  — Back to original!
```

### Real ML Examples

```python
# 1. Log Transform for Skewed Data
prices = np.array([100, 500, 1000, 50000, 100000])
log_prices = np.log(prices)
print(log_prices)
# [4.605 6.215 6.908 10.820 11.513]
# Much more uniform distribution!

# 2. Softmax Function (Neural Networks)
def softmax(x):
    exp_x = np.exp(x - np.max(x))  # Subtract max for stability
    return exp_x / np.sum(exp_x)

logits = np.array([2.0, 1.0, 0.1])
probabilities = softmax(logits)
print(probabilities)
# [0.659 0.242 0.099]  — Sums to 1!

# 3. Sigmoid Function (Logistic Regression)
def sigmoid(x):
    return 1 / (1 + np.exp(-x))

z = np.array([-2, -1, 0, 1, 2])
print(sigmoid(z))
# [0.119 0.269 0.5 0.731 0.881]
```

---

## 🔥 Step 4: Trigonometric ufuncs

### Basic Trigonometry

```python
# Create angles in degrees
angles_deg = np.array([0, 30, 45, 60, 90])

# Convert to radians (NumPy trig functions use radians!)
radians = np.deg2rad(angles_deg)
print(radians)
# [0.    0.524 0.785 1.047 1.571]

# Trigonometric functions
np.sin(radians)
# [0.   0.5  0.707 0.866 1.  ]

np.cos(radians)
# [1.   0.866 0.707 0.5  0.  ]

np.tan(radians)
# [0.    0.577 1.    1.732 very large]
```

### Visual: Unit Circle

```
                    90° (π/2)
                       │
                    sin=1
                    cos=0
                       │
    180° (π) ─────────┼───────── 0° (0)
    sin=0             │          sin=0
    cos=-1            │          cos=1
                       │
                   270° (3π/2)
                    sin=-1
                    cos=0

At 45°:
  sin(45°) = cos(45°) = √2/2 ≈ 0.707
```

### Conversion Functions

```python
# Degrees to Radians
np.deg2rad(180)    # π ≈ 3.14159
np.radians(180)    # Same thing

# Radians to Degrees
np.rad2deg(np.pi)  # 180.0
np.degrees(np.pi)  # Same thing
```

### Inverse Trigonometric Functions

```python
# arcsin, arccos, arctan (inverse functions)
np.arcsin(0.5)       # 0.524 radians (30°)
np.arccos(0.5)       # 1.047 radians (60°)
np.arctan(1)         # 0.785 radians (45°)

# Convert result to degrees
np.rad2deg(np.arcsin(0.5))  # 30.0
```

### Hyperbolic Functions

```python
x = np.array([-1, 0, 1])

np.sinh(x)   # Hyperbolic sine
np.cosh(x)   # Hyperbolic cosine
np.tanh(x)   # Hyperbolic tangent (used in neural networks!)
```

### 📌 Real-World Applications

| Field | Function | Use Case |
|-------|----------|----------|
| 🤖 Robotics | sin, cos | Joint angles, rotation |
| 📡 Signals | sin, cos | Wave analysis, FFT |
| 🎮 Games | atan2 | Character direction |
| 🧠 ML | tanh | Activation function |
| 📊 Physics | All | Motion, forces, waves |

### Complete Trig ufuncs Table

| Function | Description |
|----------|-------------|
| `np.sin(x)` | Sine |
| `np.cos(x)` | Cosine |
| `np.tan(x)` | Tangent |
| `np.arcsin(x)` | Inverse sine |
| `np.arccos(x)` | Inverse cosine |
| `np.arctan(x)` | Inverse tangent |
| `np.arctan2(y, x)` | Angle from coordinates |
| `np.hypot(x, y)` | Hypotenuse √(x²+y²) |
| `np.deg2rad(x)` | Degrees to radians |
| `np.rad2deg(x)` | Radians to degrees |
| `np.sinh(x)` | Hyperbolic sine |
| `np.cosh(x)` | Hyperbolic cosine |
| `np.tanh(x)` | Hyperbolic tangent |

---

## 🧠 Step 5: Combining ufuncs (REAL POWER)

### The Concept

> **Chain multiple ufuncs together for complex calculations — all vectorized!**

### Basic Combination

```python
x = np.array([1, 2, 3, 4])

# Combine sqrt and log
y = np.sqrt(x) + np.log(x)
print(y)
# [1.0  1.693  2.098  2.386]
```

### How It Works

```
Input:    x = [1, 2, 3, 4]
              ↓
Step 1:   np.sqrt(x) = [1.0, 1.414, 1.732, 2.0]
              ↓
Step 2:   np.log(x)  = [0.0, 0.693, 1.099, 1.386]
              ↓
Step 3:   Add them   = [1.0, 2.107, 2.831, 3.386]

All operations are element-wise!
```

### Complex Formula Example

```python
# Formula: y = √x + log(x) + sin(x) * e^(-x/10)

x = np.linspace(1, 10, 100)  # 100 points from 1 to 10

y = np.sqrt(x) + np.log(x) + np.sin(x) * np.exp(-x/10)

# One line, 100 calculations, no loops! 🔥
```

### Comparison: Traditional vs NumPy

```python
# ❌ Traditional Python (SLOW, VERBOSE)
x = [1, 2, 3, 4]
result = []
for val in x:
    import math
    res = math.sqrt(val) + math.log(val)
    result.append(res)

# ✅ NumPy Way (FAST, CLEAN)
x = np.array([1, 2, 3, 4])
result = np.sqrt(x) + np.log(x)
```

### Chaining for Machine Learning

```python
# Feature Engineering Pipeline
data = np.array([0.1, 0.5, 1.0, 2.0, 5.0])

# Apply multiple transformations
features = np.column_stack([
    data,                    # Original
    np.log1p(data),          # Log transform
    np.sqrt(data),           # Square root
    np.square(data),         # Squared
    1 / (1 + data)           # Inverse transform
])

print(features.shape)  # (5, 5) — 5 samples, 5 features
```

---

## ⚡ Step 6: ufuncs vs Python Loops (WHY IT MATTERS)

### Code Comparison

```python
import numpy as np
import time

# Create large array
x = np.random.rand(1_000_000)
```

### ❌ Loop Version (Slow)

```python
def sqrt_loop(arr):
    result = []
    for i in arr:
        result.append(np.sqrt(i))
    return result

start = time.time()
result_loop = sqrt_loop(x)
print(f"Loop time: {time.time() - start:.4f}s")
# Loop time: 1.2345s
```

### ✅ ufunc Version (Fast)

```python
start = time.time()
result_ufunc = np.sqrt(x)
print(f"ufunc time: {time.time() - start:.4f}s")
# ufunc time: 0.0023s
```

### Speed Comparison

```
┌─────────────────────────────────────────────────────────────┐
│              PERFORMANCE COMPARISON (1M elements)           │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Python Loop:  ████████████████████████████████  1.23s      │
│                                                             │
│  NumPy ufunc:  █                                 0.002s     │
│                                                             │
│  Speedup: ~500x FASTER! 🚀                                  │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### Why ufuncs Are Faster

```
┌─────────────────────────────────────────────────────────────┐
│                    WHY UFUNCS WIN                           │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  1️⃣  COMPILED C CODE                                        │
│      • Python: Interpreted at runtime                       │
│      • ufuncs: Pre-compiled, machine code                   │
│                                                             │
│  2️⃣  NO PYTHON OVERHEAD                                     │
│      • Loop: Each iteration has Python overhead             │
│      • ufunc: One call, everything happens in C             │
│                                                             │
│  3️⃣  SIMD INSTRUCTIONS                                      │
│      • Process multiple elements simultaneously             │
│      • Modern CPUs can do 4-8 operations at once            │
│                                                             │
│  4️⃣  MEMORY EFFICIENCY                                      │
│      • Contiguous memory access                             │
│      • Better CPU cache utilization                         │
│                                                             │
│  5️⃣  NO INTERMEDIATE LISTS                                  │
│      • Loop: Creates Python list, converts back             │
│      • ufunc: Operates directly on array memory             │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### Benchmark Table

| Operation | Loop (1M elements) | ufunc (1M elements) | Speedup |
|-----------|-------------------|---------------------|---------|
| sqrt | ~1.2s | ~0.002s | 600x |
| log | ~1.5s | ~0.003s | 500x |
| sin | ~2.0s | ~0.005s | 400x |
| exp | ~1.3s | ~0.002s | 650x |
| power | ~1.8s | ~0.004s | 450x |

### 🔥 The Rule

```
┌─────────────────────────────────────────────────────────────┐
│                                                             │
│   🚫 NEVER use loops for math operations on NumPy arrays   │
│                                                             │
│   ✅ ALWAYS use ufuncs for vectorized operations           │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## 🧠 Step 7: Real-Life Example (Finance 📈)

### Example 1: Compound Interest (Continuous)

```python
# Formula: A = P * e^(rt)
# A = final amount
# P = principal
# r = interest rate
# t = time in years

principal = np.array([1000, 2000, 3000, 5000, 10000])
rate = 0.05  # 5% annual rate
years = 5

final_amount = principal * np.exp(rate * years)
print("Final amounts:", final_amount.round(2))
# [1284.03 2568.05 3852.08 6420.13 12840.25]

# Calculate returns
returns = final_amount - principal
print("Returns:", returns.round(2))
# [284.03 568.05 852.08 1420.13 2840.25]
```

### Example 2: Stock Returns Analysis

```python
# Daily stock prices
prices = np.array([100, 102, 99, 103, 105, 104, 108])

# Calculate daily returns
returns = np.diff(prices) / prices[:-1]
print("Daily returns:", returns.round(4))
# [0.02  -0.0294  0.0404  0.0194 -0.0095  0.0385]

# Log returns (preferred in finance)
log_returns = np.diff(np.log(prices))
print("Log returns:", log_returns.round(4))
# [0.0198 -0.0299  0.0396  0.0192 -0.0096  0.0377]

# Statistics
print(f"Mean return: {returns.mean()*100:.2f}%")
print(f"Volatility: {returns.std()*100:.2f}%")
```

### Example 3: Portfolio Value Over Time

```python
np.random.seed(42)

# Simulate daily returns for 252 trading days
daily_returns = np.random.normal(0.0008, 0.015, 252)  # ~20% annual, 24% vol

# Calculate cumulative value
initial_investment = 10000
cumulative_returns = np.cumprod(1 + daily_returns)
portfolio_value = initial_investment * cumulative_returns

print(f"Starting value: ${initial_investment:,.2f}")
print(f"Final value: ${portfolio_value[-1]:,.2f}")
print(f"Max value: ${portfolio_value.max():,.2f}")
print(f"Min value: ${portfolio_value.min():,.2f}")
print(f"Total return: {(portfolio_value[-1]/initial_investment - 1)*100:.1f}%")
```

### Example 4: Loan Payment Calculator

```python
# Monthly payment formula: PMT = P * (r(1+r)^n) / ((1+r)^n - 1)

principal = 250000  # Loan amount
annual_rate = 0.065  # 6.5% annual interest
years = 30

monthly_rate = annual_rate / 12
n_payments = years * 12

# Using ufuncs
monthly_payment = principal * (
    monthly_rate * np.power(1 + monthly_rate, n_payments)
) / (
    np.power(1 + monthly_rate, n_payments) - 1
)

print(f"Loan amount: ${principal:,}")
print(f"Interest rate: {annual_rate*100}%")
print(f"Monthly payment: ${monthly_payment:,.2f}")
print(f"Total paid: ${monthly_payment * n_payments:,.2f}")
print(f"Interest paid: ${monthly_payment * n_payments - principal:,.2f}")
```

---

## 🧠 Step 8: ufuncs with Conditions

### The `np.where()` Function

> **Vectorized if-else for arrays!**

### Basic Syntax

```python
np.where(condition, value_if_true, value_if_false)
```

### Example 1: Replace Negative Values

```python
data = np.array([-10, -5, 0, 5, 10])

# Replace negatives with 0
result = np.where(data > 0, data, 0)
print(result)
# [0 0 0 5 10]
```

### How It Works

```
data = [-10, -5, 0, 5, 10]

Condition: data > 0
           [F,   F,  F, T,  T]
              ↓   ↓   ↓  ↓   ↓
If True:                 5  10    (keep original)
If False: 0   0   0            (replace with 0)
              ↓   ↓   ↓  ↓   ↓
Result:   [ 0,  0,  0, 5, 10]
```

### Example 2: Classify Values

```python
scores = np.array([45, 67, 82, 91, 55, 78])

# Pass/Fail classification
result = np.where(scores >= 60, 'Pass', 'Fail')
print(result)
# ['Fail' 'Pass' 'Pass' 'Pass' 'Fail' 'Pass']
```

### Example 3: Multiple Conditions with `np.select()`

```python
grades = np.array([95, 82, 67, 45, 78, 88])

conditions = [
    grades >= 90,
    grades >= 80,
    grades >= 70,
    grades >= 60,
    grades < 60
]

choices = ['A', 'B', 'C', 'D', 'F']

letter_grades = np.select(conditions, choices)
print(letter_grades)
# ['A' 'B' 'D' 'F' 'C' 'B']
```

### Example 4: Clamping Values

```python
# Ensure values are within range [0, 100]
data = np.array([-5, 50, 75, 120, 90, -10])

# Method 1: Nested np.where
result = np.where(data < 0, 0, np.where(data > 100, 100, data))
print(result)
# [0 50 75 100 90 0]

# Method 2: np.clip (better!)
result = np.clip(data, 0, 100)
print(result)
# [0 50 75 100 90 0]
```

### Example 5: Conditional Calculations

```python
x = np.array([-2, -1, 0, 1, 2])

# Apply different functions based on sign
# If positive: x^2, If negative: abs(x), If zero: 0
result = np.where(
    x > 0, 
    np.square(x),
    np.where(x < 0, np.abs(x), 0)
)
print(result)
# [2 1 0 1 4]
```

### Related Conditional Functions

| Function | Description | Example |
|----------|-------------|---------|
| `np.where(cond, x, y)` | Vectorized if-else | Replace values |
| `np.select(conds, choices)` | Multiple conditions | Grade assignment |
| `np.clip(a, min, max)` | Limit range | Clamp values |
| `np.maximum(a, b)` | Element-wise max | `max(a, 0)` |
| `np.minimum(a, b)` | Element-wise min | `min(a, 100)` |
| `np.piecewise(x, conds, funcs)` | Piecewise functions | Complex conditionals |

---

## 📝 DAY 8 PRACTICE (NO SHORTCUTS 🔴)

### Task 1: Basic ufuncs

```python
arr = np.array([2, 4, 6, 8, 10])
```

**Apply these ufuncs:**

- [ ] Square root of all elements
- [ ] Natural log of all elements
- [ ] Exponential (e^x) of all elements
- [ ] Square of all elements

<details>
<summary>💡 Solution (Try First!)</summary>

```python
import numpy as np

arr = np.array([2, 4, 6, 8, 10])

# Square root
sqrt_arr = np.sqrt(arr)
print(f"Square root: {sqrt_arr}")
# [1.414 2.    2.449 2.828 3.162]

# Natural log
log_arr = np.log(arr)
print(f"Natural log: {log_arr}")
# [0.693 1.386 1.792 2.079 2.303]

# Exponential
exp_arr = np.exp(arr)
print(f"Exponential: {exp_arr}")
# [7.389 54.598 403.429 2980.958 22026.466]

# Square
square_arr = np.square(arr)
print(f"Square: {square_arr}")
# [4 16 36 64 100]

# Bonus: Combine them
combined = np.sqrt(arr) + np.log(arr)
print(f"Combined (sqrt + log): {combined}")
```

</details>

---

### Task 2: Trigonometry

**Create angles from 0 to 180 degrees (step 30):**

- [ ] Convert to radians
- [ ] Calculate sine values
- [ ] Calculate cosine values
- [ ] Find where sin = cos

<details>
<summary>💡 Solution (Try First!)</summary>

```python
import numpy as np

# Create angles in degrees
angles_deg = np.arange(0, 181, 30)
print(f"Angles (degrees): {angles_deg}")
# [0 30 60 90 120 150 180]

# Convert to radians
angles_rad = np.deg2rad(angles_deg)
print(f"Angles (radians): {np.round(angles_rad, 3)}")
# [0.    0.524 1.047 1.571 2.094 2.618 3.142]

# Calculate sine values
sin_values = np.sin(angles_rad)
print(f"Sine values: {np.round(sin_values, 3)}")
# [0.    0.5   0.866 1.    0.866 0.5   0.   ]

# Calculate cosine values
cos_values = np.cos(angles_rad)
print(f"Cosine values: {np.round(cos_values, 3)}")
# [1.    0.866 0.5   0.   -0.5  -0.866 -1.   ]

# Find where sin ≈ cos (they're equal at 45°)
# Since 45° isn't in our array, find where they're closest
diff = np.abs(sin_values - cos_values)
closest_idx = np.argmin(diff)
print(f"\nSin and Cos are closest at {angles_deg[closest_idx]}°")
print(f"At this angle: sin={sin_values[closest_idx]:.3f}, cos={cos_values[closest_idx]:.3f}")
```

</details>

---

### Task 3: Financial Calculation

**Calculate compound interest for different principals:**

```python
principals = np.array([1000, 5000, 10000, 25000, 50000])
rate = 0.07  # 7% annual rate
time = 10    # years
```

- [ ] Calculate final amount using continuous compounding: A = P * e^(rt)
- [ ] Calculate total interest earned
- [ ] Find which principal doubled

<details>
<summary>💡 Solution (Try First!)</summary>

```python
import numpy as np

principals = np.array([1000, 5000, 10000, 25000, 50000])
rate = 0.07  # 7% annual rate
time = 10    # years

# Final amount with continuous compounding
final_amounts = principals * np.exp(rate * time)
print("Final amounts:")
for p, f in zip(principals, final_amounts):
    print(f"  ${p:,} → ${f:,.2f}")

# Total interest earned
interest = final_amounts - principals
print(f"\nInterest earned: {interest.round(2)}")

# Find which doubled (final >= 2 * principal)
doubled = final_amounts >= 2 * principals
print(f"\nDoubled investments: {doubled}")
print(f"Principals that doubled: {principals[doubled]}")

# Note: With 7% continuous compounding for 10 years,
# growth factor = e^(0.07*10) = e^0.7 ≈ 2.014
# So ALL investments just barely doubled!

print(f"\nGrowth factor: {np.exp(rate * time):.3f}")
```

</details>

---

### Task 4: Pro Thinking 🧠

**Question:** Why are ufuncs faster than normal Python functions?

<details>
<summary>💡 Answer</summary>

### Why ufuncs Are Faster:

#### 1. **Compiled C Code vs Interpreted Python**

```
Python Function:                 ufunc:
┌─────────────────────┐         ┌─────────────────────┐
│ Read Python code    │         │ Execute compiled    │
│        ↓            │         │ machine code        │
│ Parse/interpret     │         │ directly            │
│        ↓            │         │                     │
│ Execute bytecode    │         │ 🚀 Direct CPU       │
│        ↓            │         │    instructions     │
│ 🐢 Slow!           │         │                     │
└─────────────────────┘         └─────────────────────┘
```

#### 2. **No Loop Overhead**

```python
# Python loop: Each iteration has overhead
for i in range(1000000):   # 1M iterations
    result[i] = sqrt(x[i])  # Each: type check, func call, assignment
    
# ufunc: Single function call
np.sqrt(x)  # One call handles all 1M elements internally
```

#### 3. **SIMD (Single Instruction, Multiple Data)**

```
Python:                    ufunc with SIMD:
Process 1 element         Process 4-8 elements
at a time:                at once:

[1] → √1                  [1,4,9,16] → [1,2,3,4]
[4] → √4                  One CPU instruction!
[9] → √9
[16] → √16
4 operations              1 operation
```

#### 4. **Memory Contiguity**

```
Python list:              NumPy array:
┌───┐   ┌───┐            ┌───┬───┬───┬───┐
│ → │───│ 1 │            │ 1 │ 2 │ 3 │ 4 │
├───┤   └───┘            └───┴───┴───┴───┘
│ → │───┌───┐            Contiguous memory
├───┤   │ 2 │            → CPU cache friendly
│ → │   └───┘            → Faster access
└───┘   ...

Scattered memory          
→ Cache misses
→ Slow
```

#### 5. **No Type Checking Per Element**

```python
# Python: Checks type for EVERY element
for x in arr:
    if isinstance(x, int):
        result = sqrt(x)  # Different path for each type
        
# NumPy: Knows all elements are same type (e.g., float64)
# No per-element type checking needed!
```

### Summary

| Factor | Python Loop | NumPy ufunc |
|--------|-------------|-------------|
| Compilation | Interpreted | Pre-compiled C |
| Loop overhead | Per iteration | None |
| SIMD | No | Yes |
| Memory access | Scattered | Contiguous |
| Type checking | Every element | Once |
| **Result** | 🐢 Slow | 🚀 ~100-1000x faster |

</details>

---

### Task 5: Conditional Operations

```python
data = np.array([-15, -8, 0, 5, 12, -3, 20, -10])
```

- [ ] Replace all negative values with 0
- [ ] Replace values < -10 with -10 and values > 15 with 15
- [ ] Create array where: positive → "P", negative → "N", zero → "Z"

<details>
<summary>💡 Solution (Try First!)</summary>

```python
import numpy as np

data = np.array([-15, -8, 0, 5, 12, -3, 20, -10])
print(f"Original: {data}")

# 1. Replace negatives with 0
result1 = np.where(data < 0, 0, data)
print(f"Negatives → 0: {result1}")
# [0 0 0 5 12 0 20 0]

# Alternative using np.maximum
result1_alt = np.maximum(data, 0)
print(f"Using maximum: {result1_alt}")

# 2. Clamp to range [-10, 15]
result2 = np.clip(data, -10, 15)
print(f"Clamped [-10, 15]: {result2}")
# [-10 -8 0 5 12 -3 15 -10]

# Alternative using nested where
result2_alt = np.where(data < -10, -10, np.where(data > 15, 15, data))
print(f"Using where: {result2_alt}")

# 3. Classify as P/N/Z
conditions = [data > 0, data < 0, data == 0]
choices = ['P', 'N', 'Z']
result3 = np.select(conditions, choices)
print(f"Classification: {result3}")
# ['N' 'N' 'Z' 'P' 'P' 'N' 'P' 'N']
```

</details>

---

## 🚫 Today's Rules

| ❌ FORBIDDEN | ✅ REQUIRED |
|--------------|-------------|
| Writing loops for math | Use ufuncs |
| Ignoring vectorization | Think in arrays |
| Copy-paste without understanding | Know why ufuncs are fast |
| Using `math` module on arrays | Use `numpy` functions |

---

## 🔒 Day 8 Checkpoint

### Self-Assessment Checklist

Before moving to Day 9, ensure you can:

- [ ] **Apply math formulas to datasets**
  ```python
  y = np.sqrt(x) + np.log(x) + np.exp(-x)
  ```

- [ ] **Combine multiple ufuncs**
  ```python
  result = np.sin(np.deg2rad(angles)) * np.exp(-x/10)
  ```

- [ ] **Explain why NumPy is fast**
  - Compiled C code
  - SIMD operations
  - No loop overhead
  - Contiguous memory

- [ ] **Use conditional operations**
  ```python
  np.where(condition, true_value, false_value)
  np.clip(data, min, max)
  ```

---

## 📊 Quick Reference Card

```python
# ═══════════════════════════════════════════════════════════
#                    ARITHMETIC UFUNCS
# ═══════════════════════════════════════════════════════════

np.sqrt(x)           # Square root
np.square(x)         # Square
np.power(x, n)       # x to power n
np.cbrt(x)           # Cube root
np.abs(x)            # Absolute value
np.sign(x)           # Sign (-1, 0, 1)
np.floor(x)          # Round down
np.ceil(x)           # Round up
np.round(x, decimals) # Round to n decimals

# ═══════════════════════════════════════════════════════════
#                    LOG & EXP UFUNCS
# ═══════════════════════════════════════════════════════════

np.log(x)            # Natural log (ln)
np.log10(x)          # Log base 10
np.log2(x)           # Log base 2
np.log1p(x)          # log(1 + x), accurate for small x
np.exp(x)            # e^x
np.exp2(x)           # 2^x
np.expm1(x)          # e^x - 1, accurate for small x

# ═══════════════════════════════════════════════════════════
#                    TRIGONOMETRIC UFUNCS
# ═══════════════════════════════════════════════════════════

np.sin(x)            # Sine (x in radians)
np.cos(x)            # Cosine
np.tan(x)            # Tangent
np.arcsin(x)         # Inverse sine
np.arccos(x)         # Inverse cosine
np.arctan(x)         # Inverse tangent
np.deg2rad(x)        # Degrees to radians
np.rad2deg(x)        # Radians to degrees
np.hypot(x, y)       # √(x² + y²)

# ═══════════════════════════════════════════════════════════
#                    CONDITIONAL OPERATIONS
# ═══════════════════════════════════════════════════════════

np.where(cond, x, y)      # if cond: x else: y
np.select(conds, choices) # Multiple conditions
np.clip(x, min, max)      # Clamp to range
np.maximum(x, y)          # Element-wise max
np.minimum(x, y)          # Element-wise min

# ═══════════════════════════════════════════════════════════
#                    COMMON PATTERNS
# ═══════════════════════════════════════════════════════════

# Sigmoid function
sigmoid = 1 / (1 + np.exp(-x))

# Softmax function
softmax = np.exp(x) / np.sum(np.exp(x))

# Normalize to [0, 1]
normalized = (x - x.min()) / (x.max() - x.min())

# Z-score standardization
z_score = (x - np.mean(x)) / np.std(x)

# Log transform
log_transformed = np.log1p(x)  # log(1+x), handles x=0
```

---

## 🔗 Navigation

| Previous | Current | Next |
|----------|---------|------|
| [Day 7: Random & Simulation](https://github.com/Saad-Shaikh095/30-Days-Numpy-for-Data-Science-/tree/main/Phase%201%20Foundations/Day%207%20Random%20Number%20and%20Simulation) | **Day 8: ufuncs & Advanced Math** | [Day 9: Sorting & Searching](./DAY9.md) |

---

<div align="center">

### 💡 Key Insight of Day 8

*"ufuncs are the heart of NumPy — they transform slow Python loops into blazing-fast C-level operations!"*

---

### 🧮 The ufunc Mantra

```
┌─────────────────────────────────────────────────────────────┐
│                                                             │
│   🚫 for i in range(len(arr)):                             │
│          result[i] = math.sqrt(arr[i])                     │
│                                                             │
│   ✅ result = np.sqrt(arr)                                  │
│                                                             │
│   Same result, 100x faster, 10x cleaner! 🚀                │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

### 🏆 Achievement Unlocked!

**🎖️ Vectorization Wizard**

*You now wield the power of ufuncs — math at the speed of light!*

---

**Happy Coding! 🚀**

![Made with NumPy](https://img.shields.io/badge/Made%20with-NumPy-013243?style=flat&logo=numpy)
![ufuncs](https://img.shields.io/badge/ufuncs-Mastered-green?style=flat)
![Week 2](https://img.shields.io/badge/Week%202-In%20Progress-orange?style=flat)

</div>

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.