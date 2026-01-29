# 📅 DAY 7 – RANDOM NUMBERS & SIMULATION

> **"If you can simulate it, you can understand it."** — The power of synthetic data

![NumPy](https://img.shields.io/badge/NumPy-Day%207-013243?style=for-the-badge&logo=numpy)
![Python](https://img.shields.io/badge/Python-3.x-blue?style=for-the-badge&logo=python)
![Level](https://img.shields.io/badge/Level-Intermediate-yellow?style=for-the-badge)
![Week 1](https://img.shields.io/badge/Week%201-Complete!-success?style=for-the-badge)

---

## 🎯 Today's Goals

By the end of Day 7, you will:

| Goal | Description | Real-World Application |
|------|-------------|------------------------|
| 🎲 | Generate random data like real datasets | Create test data instantly |
| 🔬 | Simulate real-life situations | Model uncertainty & risk |
| 🤖 | Understand randomness in ML & DS | Train-test splits, initialization |

> 🎉 **Congratulations!** This is the final day of Week 1!

---

## 📚 Table of Contents

- [Step 1: Why Random Numbers Matter](#-step-1-why-random-numbers-matter)
- [Step 2: NumPy Random Basics](#-step-2-numpy-random-basics)
- [Step 3: Random Integers](#-step-3-random-integers)
- [Step 4: Setting Seed](#-step-4-set-seed-important-)
- [Step 5: Random Distributions](#-step-5-random-from-distributions)
- [Step 6: Real-Life Simulations](#-step-6-real-life-simulation-examples)
- [Step 7: Random Sampling](#-step-7-random-sampling)
- [Step 8: Case Study](#-step-8-mini-case-study--dice-roll-)
- [Practice Exercises](#-day-7-practice-fun-but-serious-)
- [Week 1 Checkpoint](#-week-1-checkpoint-)

---

## 🧠 Step 1: Why Random Numbers Matter?

### The Big Picture

> **Data Scientists don't always wait for data — they GENERATE it!**

Random numbers are the foundation of:

```
┌─────────────────────────────────────────────────────────────┐
│                 RANDOM NUMBERS ARE USED IN                  │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  🤖 Machine Learning                                        │
│     • Train/test splitting                                  │
│     • Weight initialization                                 │
│     • Data augmentation                                     │
│                                                             │
│  📊 Statistics & Simulation                                 │
│     • Monte Carlo methods                                   │
│     • Hypothesis testing                                    │
│     • Bootstrapping                                         │
│                                                             │
│  💰 Finance                                                 │
│     • Stock price modeling                                  │
│     • Risk analysis                                         │
│     • Portfolio simulation                                  │
│                                                             │
│  🎮 Games & Graphics                                        │
│     • Procedural generation                                 │
│     • AI decision making                                    │
│     • Physics simulations                                   │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### Real-World Examples

| Field | Use Case | Why Random? |
|-------|----------|-------------|
| 🤖 ML | Train-test split | Ensure unbiased evaluation |
| 📈 Finance | Stock simulation | Model market uncertainty |
| 🎓 Education | Generate test scores | Create realistic datasets |
| 🏥 Healthcare | Clinical trial simulation | Test before real trials |
| 🎲 Gaming | Dice rolls, card shuffles | Create unpredictability |

### The Power of Simulation

```
Real Data Collection:          Simulation:
┌─────────────────┐           ┌─────────────────┐
│ Collect 10,000  │           │ Generate 10,000 │
│ survey responses│           │ data points     │
│                 │           │                 │
│ Time: 6 months  │           │ Time: 0.001 sec │
│ Cost: $50,000   │           │ Cost: FREE      │
└─────────────────┘           └─────────────────┘
```

---

## 🎲 Step 2: NumPy Random Basics

### Setting Up

```python
import numpy as np
```

### Single Random Float (0 to 1)

```python
np.random.rand()
```

```python
# Output: 0.7432556483242135 (example)
```

### Random 1D Array

```python
np.random.rand(5)
```

```python
# Output: [0.234, 0.891, 0.123, 0.567, 0.445]
```

### Random 2D Array

```python
np.random.rand(3, 3)
```

```python
# Output:
# [[0.12, 0.45, 0.78],
#  [0.23, 0.56, 0.89],
#  [0.34, 0.67, 0.90]]
```

### Visual Understanding

```
np.random.rand(3, 4)

Generates a 3×4 matrix of random floats:

     Col0    Col1    Col2    Col3
    ┌───────┬───────┬───────┬───────┐
Row0│ 0.234 │ 0.567 │ 0.891 │ 0.123 │
    ├───────┼───────┼───────┼───────┤
Row1│ 0.456 │ 0.789 │ 0.012 │ 0.345 │
    ├───────┼───────┼───────┼───────┤
Row2│ 0.678 │ 0.901 │ 0.234 │ 0.567 │
    └───────┴───────┴───────┴───────┘

All values are in range [0, 1)
```

### Key Random Functions

| Function | Range | Use Case |
|----------|-------|----------|
| `np.random.rand(shape)` | [0, 1) | Probabilities, percentages |
| `np.random.randn(shape)` | Normal (μ=0, σ=1) | Standardized data |
| `np.random.random(shape)` | [0, 1) | Same as rand() |

### randn() vs rand()

```python
# rand() — Uniform distribution (0 to 1)
np.random.rand(5)
# [0.23, 0.78, 0.45, 0.12, 0.89]  All spread evenly

# randn() — Normal distribution (mean=0, std=1)
np.random.randn(5)
# [0.45, -1.23, 2.01, -0.34, 0.67]  Clustered around 0, can be negative
```

```
rand() Distribution:           randn() Distribution:
                               
    ████████████████               ████
    ████████████████              ██████
    ████████████████            ████████████
    ████████████████         ████████████████████
    ────────────────         ────────────────────────
    0              1         -3  -2  -1   0   1   2   3
    
    Uniform (flat)           Normal (bell curve)
```

---

## 🔢 Step 3: Random Integers

### Basic Integer Generation

```python
np.random.randint(1, 7)  # Single integer from 1 to 6
```

### Generate Multiple Integers

```python
np.random.randint(1, 7, size=10)
```

```python
# Output: [3, 6, 2, 5, 1, 4, 3, 6, 2, 1]
```

### 🎲 This is a Dice Simulation!

```
np.random.randint(1, 7, size=10)
                   ↓  ↓
               low=1  high=7 (exclusive)
               
Generates: 1, 2, 3, 4, 5, or 6

         🎲🎲🎲🎲🎲🎲🎲🎲🎲🎲
Result: [ 3  6  2  5  1  4  3  6  2  1 ]
```

### 2D Random Integers

```python
np.random.randint(0, 100, size=(3, 4))
```

```python
# Output:
# [[23, 67, 45, 89],
#  [12, 56, 78, 34],
#  [90, 11, 44, 77]]
```

### Important: High is Exclusive!

```python
np.random.randint(1, 10)   # Can produce: 1,2,3,4,5,6,7,8,9 (NOT 10!)
np.random.randint(0, 2)    # Can produce: 0 or 1 only (coin flip!)
```

### Parameters Explained

```python
np.random.randint(low, high, size)
                   ↓    ↓     ↓
             minimum  max+1  how many/shape
             
# Examples:
np.random.randint(1, 7, size=10)      # 10 dice rolls
np.random.randint(0, 100, size=(5,5)) # 5×5 matrix of 0-99
np.random.randint(1, 100)             # Single number 1-99
```

---

## 🔒 Step 4: Set Seed (IMPORTANT 🔒)

### The Problem: Randomness is... Random

```python
print(np.random.rand(3))  # [0.234, 0.567, 0.891]
print(np.random.rand(3))  # [0.123, 0.456, 0.789]  Different!
print(np.random.rand(3))  # [0.345, 0.678, 0.901]  Different again!
```

### The Solution: Seed

```python
np.random.seed(42)
print(np.random.rand(3))  # [0.374, 0.950, 0.731]

np.random.seed(42)
print(np.random.rand(3))  # [0.374, 0.950, 0.731]  SAME!

np.random.seed(42)
print(np.random.rand(3))  # [0.374, 0.950, 0.731]  SAME!
```

### 🧠 What is a Seed?

```
┌─────────────────────────────────────────────────────────────┐
│                    RANDOM SEED CONCEPT                      │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Seed = Starting point for random number generator          │
│                                                             │
│  Same seed → Same "random" sequence (every time!)           │
│                                                             │
│  ┌─────────────────────────────────────────────────────┐   │
│  │  seed(42) → 0.374, 0.950, 0.731, 0.598, 0.156...    │   │
│  │  seed(42) → 0.374, 0.950, 0.731, 0.598, 0.156...    │   │
│  │  seed(42) → 0.374, 0.950, 0.731, 0.598, 0.156...    │   │
│  └─────────────────────────────────────────────────────┘   │
│                                                             │
│  Different seed → Different sequence                        │
│                                                             │
│  ┌─────────────────────────────────────────────────────┐   │
│  │  seed(0)  → 0.548, 0.715, 0.602, 0.544, 0.423...    │   │
│  │  seed(1)  → 0.417, 0.720, 0.000, 0.302, 0.146...    │   │
│  │  seed(42) → 0.374, 0.950, 0.731, 0.598, 0.156...    │   │
│  └─────────────────────────────────────────────────────┘   │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### 🔥 Why Seed is CRITICAL in ML/DS

| Scenario | Without Seed | With Seed |
|----------|--------------|-----------|
| Train-test split | Different split each run | Same split every time |
| Model training | Different results | Reproducible results |
| Debugging | Can't reproduce bugs | Can reproduce exactly |
| Research papers | Others can't verify | Others get same results |
| Team collaboration | "Works on my machine" | Works for everyone |

### Real Example: Train-Test Split

```python
# ❌ Without seed — different split every run
from sklearn.model_selection import train_test_split
X_train, X_test = train_test_split(X, test_size=0.2)
# Run 1: Different data in train/test
# Run 2: Different data in train/test

# ✅ With seed — reproducible split
np.random.seed(42)
X_train, X_test = train_test_split(X, test_size=0.2, random_state=42)
# Run 1: Same split
# Run 2: Same split (identical!)
```

### Modern Way: Using Generator

```python
# New recommended approach (NumPy 1.17+)
rng = np.random.default_rng(seed=42)
rng.random(5)         # Random floats
rng.integers(1, 7, 10) # Random integers
```

---

## 📊 Step 5: Random from Distributions

### Understanding Distributions

```
Uniform Distribution:          Normal Distribution:
(Every value equally likely)   (Bell curve, most values near center)

Count                          Count
  │                              │        ████
  │ ██████████████████           │       ██████
  │ ██████████████████           │     ██████████
  │ ██████████████████           │   ██████████████
  │ ██████████████████           │ ████████████████████
  └───────────────────           └────────────────────────
    min          max               -3σ  -2σ  -1σ   μ   1σ   2σ   3σ
```

### Normal Distribution (Gaussian) 🔔

```python
np.random.normal(loc=50, scale=10, size=1000)
                  ↓       ↓         ↓
               mean   std dev    count
```

```python
# Generate 1000 exam marks (mean=70, std=15)
marks = np.random.normal(loc=70, scale=15, size=1000)

print(f"Mean: {marks.mean():.2f}")    # ≈ 70
print(f"Std: {marks.std():.2f}")      # ≈ 15
print(f"Min: {marks.min():.2f}")      # ≈ 20-30
print(f"Max: {marks.max():.2f}")      # ≈ 110-120
```

### Visual: Normal Distribution

```
np.random.normal(loc=70, scale=15, size=1000)

                         ████
                        ██████
                       ████████
                      ██████████
                    ██████████████
                  ████████████████████
                ██████████████████████████
             ████████████████████████████████
          ██████████████████████████████████████
    ─────────────────────────────────────────────────
    25   40   55   70   85   100  115
                    ↑
                  mean=70
                  
    68% of values within 1 std (55-85)
    95% of values within 2 std (40-100)
    99.7% of values within 3 std (25-115)
```

### 📌 Real-World Uses of Normal Distribution

| Application | Parameters | Example |
|-------------|------------|---------|
| Exam scores | mean=70, std=15 | Class performance |
| Heights | mean=170cm, std=10 | Population study |
| Measurement error | mean=0, std=0.1 | Sensor noise |
| Stock returns | mean=0.001, std=0.02 | Daily returns |
| IQ scores | mean=100, std=15 | By definition |

### Uniform Distribution

```python
np.random.uniform(low=10, high=20, size=10)
```

```python
# Output: [15.23, 12.45, 18.91, 10.34, 16.78, ...]
# All values equally likely between 10 and 20
```

### When to Use Which?

| Distribution | Use When |
|--------------|----------|
| **Uniform** | All values equally likely (dice, random selection) |
| **Normal** | Natural phenomena (heights, scores, errors) |
| **Binomial** | Count of successes (coin flips, defects) |
| **Poisson** | Count of events (arrivals, accidents) |

### Other Distributions

```python
# Binomial — number of successes in n trials
np.random.binomial(n=10, p=0.5, size=1000)  # 10 coin flips, 1000 times

# Poisson — events per time period
np.random.poisson(lam=5, size=1000)  # Average 5 events

# Exponential — time between events
np.random.exponential(scale=2, size=1000)  # Mean waiting time = 2
```

---

## 🧠 Step 6: Real-Life Simulation Examples

### 🎓 Example 1: Exam Marks Simulation

```python
np.random.seed(42)

# Simulate 100 students' exam marks
# Mean: 70, Standard Deviation: 10
marks = np.random.normal(70, 10, 100)

# Analyze
print(f"Class Average: {marks.mean():.2f}")
print(f"Highest Score: {marks.max():.2f}")
print(f"Lowest Score: {marks.min():.2f}")
print(f"Passing (≥50): {np.sum(marks >= 50)} students")
```

```python
# Output:
# Class Average: 70.45
# Highest Score: 95.23
# Lowest Score: 45.67
# Passing (≥50): 97 students
```

### 🪙 Example 2: Coin Toss Simulation

```python
# Simulate 20 coin tosses
tosses = np.random.choice(['Heads', 'Tails'], size=20)
print(tosses)
```

```python
# Output: ['Heads' 'Tails' 'Heads' 'Heads' 'Tails' ...]
```

```python
# Count results
unique, counts = np.unique(tosses, return_counts=True)
print(dict(zip(unique, counts)))
# {'Heads': 11, 'Tails': 9}
```

### 🎲 Example 3: Dice Rolling

```python
# Roll a die 1000 times
rolls = np.random.randint(1, 7, size=1000)

# Expected average = 3.5
print(f"Average roll: {rolls.mean():.2f}")  # ≈ 3.5

# Count each face
for face in range(1, 7):
    count = np.sum(rolls == face)
    print(f"Face {face}: {count} times ({count/10:.1f}%)")
```

```python
# Output:
# Average roll: 3.48
# Face 1: 162 times (16.2%)
# Face 2: 171 times (17.1%)
# Face 3: 165 times (16.5%)
# Face 4: 168 times (16.8%)
# Face 5: 167 times (16.7%)
# Face 6: 167 times (16.7%)
```

### 📈 Example 4: Stock Price Simulation

```python
np.random.seed(42)

# Simulate stock price movement
initial_price = 100
days = 252  # Trading days in a year
daily_returns = np.random.normal(0.001, 0.02, days)  # Mean 0.1%, Std 2%

# Calculate price path
prices = initial_price * np.cumprod(1 + daily_returns)

print(f"Starting price: ${initial_price}")
print(f"Final price: ${prices[-1]:.2f}")
print(f"Max price: ${prices.max():.2f}")
print(f"Min price: ${prices.min():.2f}")
```

### 🏥 Example 5: Patient Wait Time Simulation

```python
# Emergency room wait times (exponential distribution)
# Average wait: 30 minutes
wait_times = np.random.exponential(scale=30, size=500)

print(f"Average wait: {wait_times.mean():.1f} min")
print(f"Median wait: {np.median(wait_times):.1f} min")
print(f"Longest wait: {wait_times.max():.1f} min")
print(f"Patients waiting > 1 hour: {np.sum(wait_times > 60)}")
```

---

## 🔥 Step 7: Random Sampling

### Basic Sampling

```python
data = np.array([10, 20, 30, 40, 50])

# Sample 3 elements (with replacement by default)
np.random.choice(data, size=3)
```

```python
# Output: [30, 10, 30]  # 30 can appear twice!
```

### Sampling WITHOUT Replacement

```python
np.random.choice(data, size=3, replace=False)
```

```python
# Output: [40, 10, 30]  # Each element appears at most once
```

### Visual: With vs Without Replacement

```
Original: [10, 20, 30, 40, 50]

WITH Replacement (replace=True):
Pick 1: [10, 20, 30, 40, 50] → Choose 30 → Put it back!
Pick 2: [10, 20, 30, 40, 50] → Choose 30 again → Allowed!
Pick 3: [10, 20, 30, 40, 50] → Choose 10
Result: [30, 30, 10]  ← Duplicates possible

WITHOUT Replacement (replace=False):
Pick 1: [10, 20, 30, 40, 50] → Choose 30 → Remove it!
Pick 2: [10, 20, 40, 50] → Choose 10 → Remove it!
Pick 3: [20, 40, 50] → Choose 50
Result: [30, 10, 50]  ← No duplicates
```

### Weighted Sampling

```python
items = ['A', 'B', 'C']
probs = [0.7, 0.2, 0.1]  # A is 70% likely

samples = np.random.choice(items, size=1000, p=probs)

# Count
unique, counts = np.unique(samples, return_counts=True)
print(dict(zip(unique, counts)))
# {'A': 712, 'B': 198, 'C': 90}  ≈ 70%, 20%, 10%
```

### 📌 Real Use Cases for Sampling

| Use Case | Method | Example |
|----------|--------|---------|
| Train-test split | Without replacement | 80% train, 20% test |
| Bootstrap | With replacement | Statistical inference |
| Survey sampling | Without replacement | Select participants |
| Lottery | Without replacement | Draw winning numbers |
| Monte Carlo | With replacement | Simulation studies |

### Shuffling Arrays

```python
arr = np.array([1, 2, 3, 4, 5])

# In-place shuffle (modifies original)
np.random.shuffle(arr)
print(arr)  # [3, 1, 5, 2, 4]

# Return shuffled copy (original unchanged)
shuffled = np.random.permutation(arr)
```

---

## 🧠 Step 8: Mini Case Study – Dice Roll 🎲

### The Experiment

Let's verify the Law of Large Numbers with dice!

> **Law of Large Numbers:** As sample size increases, the sample mean approaches the expected value.

### Expected Value of a Fair Die

```
E(X) = (1 + 2 + 3 + 4 + 5 + 6) / 6 = 3.5
```

### Simulation

```python
np.random.seed(42)

# Roll dice different numbers of times
for n_rolls in [10, 100, 1000, 10000, 100000]:
    dice = np.random.randint(1, 7, size=n_rolls)
    mean = np.mean(dice)
    print(f"{n_rolls:>6} rolls: Mean = {mean:.4f}, Diff from 3.5: {abs(mean-3.5):.4f}")
```

### Output

```
    10 rolls: Mean = 3.4000, Diff from 3.5: 0.1000
   100 rolls: Mean = 3.5200, Diff from 3.5: 0.0200
  1000 rolls: Mean = 3.4890, Diff from 3.5: 0.0110
 10000 rolls: Mean = 3.5033, Diff from 3.5: 0.0033
100000 rolls: Mean = 3.4998, Diff from 3.5: 0.0002  ← Very close!
```

### Visual: Convergence to Expected Value

```
                Mean of Dice Rolls
    4.0 ─┤
        │   *
    3.8 ─┤       *
        │
    3.6 ─┤           *   
        │               *    *    *    *
    3.5 ─┤─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─  Expected Value
        │
    3.4 ─┤
        │
    3.2 ─┤
        └────────────────────────────────────
          10   100  1K   10K  100K  1M
                  Number of Rolls
```

### 😎 Statistics in Action!

This demonstrates:
1. **Randomness:** Small samples have high variance
2. **Convergence:** Large samples approach expected value
3. **Reliability:** More data = more accurate estimates

---

## 📝 DAY 7 PRACTICE (FUN BUT SERIOUS 🔴)

### Task 1: Dice Simulation

**Simulate 50 dice rolls and analyze:**

- [ ] Find the mean
- [ ] Find the maximum
- [ ] Count how many times 6 appeared

<details>
<summary>💡 Solution (Try First!)</summary>

```python
import numpy as np

np.random.seed(42)

# Simulate 50 dice rolls
dice_rolls = np.random.randint(1, 7, size=50)

print("Dice Rolls:", dice_rolls)
print(f"\nMean: {np.mean(dice_rolls):.2f}")
print(f"Maximum: {np.max(dice_rolls)}")
print(f"Times 6 appeared: {np.sum(dice_rolls == 6)}")

# Bonus: Distribution of all faces
print("\nDistribution:")
for face in range(1, 7):
    count = np.sum(dice_rolls == face)
    print(f"  Face {face}: {count} times ({count*2}%)")
```

```python
# Sample Output:
# Mean: 3.48
# Maximum: 6
# Times 6 appeared: 8
```

</details>

---

### Task 2: Student Marks Simulation

**Generate 100 student marks using normal distribution (mean=65, std=12):**

- [ ] Find the average
- [ ] Find the topper's marks
- [ ] Count students who failed (< 40)
- [ ] Count students with distinction (> 85)

<details>
<summary>💡 Solution (Try First!)</summary>

```python
import numpy as np

np.random.seed(42)

# Generate 100 student marks
marks = np.random.normal(loc=65, scale=12, size=100)

# Clip to realistic range (0-100)
marks = np.clip(marks, 0, 100)

print("Student Marks Simulation")
print("=" * 40)
print(f"Average: {np.mean(marks):.2f}")
print(f"Topper's marks: {np.max(marks):.2f}")
print(f"Lowest marks: {np.min(marks):.2f}")
print(f"\nFailed (< 40): {np.sum(marks < 40)} students")
print(f"Passed (≥ 40): {np.sum(marks >= 40)} students")
print(f"Distinction (> 85): {np.sum(marks > 85)} students")

# Grade distribution
print("\nGrade Distribution:")
print(f"  A (≥80): {np.sum(marks >= 80)}")
print(f"  B (70-79): {np.sum((marks >= 70) & (marks < 80))}")
print(f"  C (60-69): {np.sum((marks >= 60) & (marks < 70))}")
print(f"  D (50-59): {np.sum((marks >= 50) & (marks < 60))}")
print(f"  F (<50): {np.sum(marks < 50)}")
```

</details>

---

### Task 3: Thinking 🧠

**Question:** Why is setting a random seed important in Data Science?

<details>
<summary>💡 Answer</summary>

### Why Random Seed is Critical in Data Science:

#### 1. **Reproducibility**

```python
# Without seed: Different results every run
np.random.rand(3)  # [0.234, 0.567, 0.891]
np.random.rand(3)  # [0.123, 0.456, 0.789]  Different!

# With seed: Same results every run
np.random.seed(42)
np.random.rand(3)  # [0.374, 0.950, 0.731]  Always this!
```

#### 2. **Debugging**

```
Scenario: Your model has a bug, but results change each run.

Without seed:
Run 1: Error appears
Run 2: Error gone?!
Run 3: Different error?!

With seed:
Run 1: Error appears
Run 2: Same error → Can debug!
Run 3: Same error → Can verify fix!
```

#### 3. **Scientific Validity**

```
Research Paper Requirement:
"Others must be able to reproduce your results"

np.random.seed(42)  # Now anyone can get your exact results!
```

#### 4. **Fair Model Comparison**

```python
# Comparing two models fairly:
np.random.seed(42)
X_train, X_test = train_test_split(X)  # Split A

# Model 1 trained on Split A
model1.fit(X_train, y_train)

np.random.seed(42)  # Reset seed!
X_train, X_test = train_test_split(X)  # Same Split A

# Model 2 trained on SAME Split A (fair comparison!)
model2.fit(X_train, y_train)
```

#### 5. **Team Collaboration**

```
Team member 1: "My accuracy is 95%"
Team member 2: "Mine is 87% with same code!"

Problem: Different random splits!

Solution: Everyone uses seed(42)
Result: Everyone gets 95% ✓
```

### Summary Table

| Without Seed | With Seed |
|--------------|-----------|
| Different results each run | Same results every run |
| Can't debug random issues | Can reproduce exactly |
| Can't verify others' work | Full reproducibility |
| Unfair model comparison | Apples-to-apples comparison |
| "Works on my machine" | Works everywhere |

### Best Practice

```python
# At the start of every DS notebook/script:
import numpy as np
np.random.seed(42)  # Or any fixed number

# For multiple random operations:
rng = np.random.default_rng(42)  # Modern approach
```

</details>

---

### Task 4: Monte Carlo Pi Estimation 🥧

**Estimate π using random points!**

Concept:
- Generate random points in a square
- Count how many fall inside a circle
- π ≈ 4 × (points in circle / total points)

<details>
<summary>💡 Solution (Try First!)</summary>

```python
import numpy as np

np.random.seed(42)

def estimate_pi(n_points):
    # Generate random points in square [0,1] x [0,1]
    x = np.random.rand(n_points)
    y = np.random.rand(n_points)
    
    # Check if points are inside quarter circle (x² + y² ≤ 1)
    inside_circle = (x**2 + y**2) <= 1
    
    # Pi estimation
    pi_estimate = 4 * np.sum(inside_circle) / n_points
    
    return pi_estimate

# Test with different sample sizes
print("Monte Carlo Pi Estimation")
print("=" * 40)
print(f"Actual π: {np.pi:.6f}\n")

for n in [100, 1000, 10000, 100000, 1000000]:
    estimate = estimate_pi(n)
    error = abs(estimate - np.pi)
    print(f"n={n:>7}: π ≈ {estimate:.6f}, Error: {error:.6f}")
```

```python
# Output:
# Monte Carlo Pi Estimation
# ========================================
# Actual π: 3.141593
#
# n=    100: π ≈ 3.160000, Error: 0.018407
# n=   1000: π ≈ 3.144000, Error: 0.002407
# n=  10000: π ≈ 3.142000, Error: 0.000407
# n= 100000: π ≈ 3.139320, Error: 0.002273
# n=1000000: π ≈ 3.141752, Error: 0.000159
```

</details>

---

## 🚫 Today's Rules

| ❌ FORBIDDEN | ✅ REQUIRED |
|--------------|-------------|
| Memorizing random outputs | Understanding distributions |
| Ignoring seed | Always set seed for reproducibility |
| Skipping simulation thinking | Think in probabilities |
| Using loops for generation | Use NumPy random functions |

---

## 🔒 WEEK 1 CHECKPOINT 🎯

### 🎉 Congratulations!

You've completed **Week 1** of the NumPy Learning Series!

### Skills Acquired

```
┌─────────────────────────────────────────────────────────────┐
│                    WEEK 1 SKILLS UNLOCKED                   │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ✅ Day 1: Array Creation                                   │
│     • Create 1D and 2D arrays                               │
│     • Understand array properties                           │
│                                                             │
│  ✅ Day 2: Indexing & Slicing                               │
│     • Access any element confidently                        │
│     • Extract rows, columns, subsets                        │
│                                                             │
│  ✅ Day 3: Boolean Masking & Fancy Indexing                 │
│     • Filter data without loops                             │
│     • Use conditions for selection                          │
│                                                             │
│  ✅ Day 4: Reshaping & Memory                               │
│     • Change array shapes                                   │
│     • Understand view vs copy                               │
│                                                             │
│  ✅ Day 5: Math & Broadcasting                              │
│     • Vectorized operations                                 │
│     • Broadcasting rules                                    │
│                                                             │
│  ✅ Day 6: Aggregations & Axis                              │
│     • Summarize data (sum, mean, max, etc.)                 │
│     • Understand axis parameter                             │
│                                                             │
│  ✅ Day 7: Random Numbers & Simulation                      │
│     • Generate random data                                  │
│     • Simulate real-world scenarios                         │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### What You Can Now Do

| Task | You Can Now... |
|------|----------------|
| 📊 Data Creation | Create arrays of any shape |
| 🔪 Data Extraction | Slice and filter like a pro |
| ➕ Data Processing | Apply math operations without loops |
| 📈 Data Analysis | Calculate statistics efficiently |
| 🎲 Data Simulation | Generate realistic test data |
| 🐛 Debug | Understand memory and reproducibility |

### Self-Assessment Quiz

Answer these questions to verify your understanding:

1. **What's the difference between `view` and `copy`?**
2. **What does `axis=0` mean in a 2D array?**
3. **Why use `&` instead of `and` in boolean operations?**
4. **What does broadcasting allow?**
5. **Why is `np.random.seed()` important?**

<details>
<summary>Check Your Answers</summary>

1. **View shares memory (changes affect original), Copy is independent**
2. **axis=0 operates DOWN columns (gives result per column)**
3. **`&` is element-wise for arrays, `and` is for single values**
4. **Broadcasting lets NumPy operate on arrays of different shapes**
5. **Ensures reproducibility — same random numbers every run**

</details>

---

## 📊 Quick Reference Card

```python
# ═══════════════════════════════════════════════════════════
#                    RANDOM FLOATS
# ═══════════════════════════════════════════════════════════

np.random.rand()             # Single float [0, 1)
np.random.rand(5)            # 1D array of 5 floats
np.random.rand(3, 4)         # 3×4 array of floats
np.random.randn(5)           # Normal distribution (mean=0, std=1)

# ═══════════════════════════════════════════════════════════
#                    RANDOM INTEGERS
# ═══════════════════════════════════════════════════════════

np.random.randint(10)        # 0 to 9
np.random.randint(1, 7)      # 1 to 6 (dice)
np.random.randint(0, 100, 5) # 5 integers from 0-99
np.random.randint(1, 7, (3,3)) # 3×3 dice matrix

# ═══════════════════════════════════════════════════════════
#                    DISTRIBUTIONS
# ═══════════════════════════════════════════════════════════

np.random.normal(mean, std, size)     # Gaussian/Bell curve
np.random.uniform(low, high, size)    # Even spread
np.random.binomial(n, p, size)        # Success counts
np.random.poisson(lambda, size)       # Event counts

# ═══════════════════════════════════════════════════════════
#                    SAMPLING
# ═══════════════════════════════════════════════════════════

np.random.choice(arr, size)           # Random selection
np.random.choice(arr, size, replace=False)  # No duplicates
np.random.choice(arr, size, p=probs)  # Weighted selection
np.random.shuffle(arr)                # In-place shuffle
np.random.permutation(arr)            # Return shuffled copy

# ═══════════════════════════════════════════════════════════
#                    REPRODUCIBILITY
# ═══════════════════════════════════════════════════════════

np.random.seed(42)                    # Set seed (old way)
rng = np.random.default_rng(42)       # Generator (new way)
```

---

## 🔗 Navigation

| Previous | Current | Next |
|----------|---------|------|
| [Day 6: Aggregations & Axis](https://github.com/Saad-Shaikh095/30-Days-Numpy-for-Data-Science-/tree/main/Phase%201%20Foundations/Day%206%20Aggregations%20and%20Axis) | **Day 7: Random & Simulation** | [Week 2: Advanced NumPy](./WEEK2.md) |

---

<div align="center">

### 💡 Key Insight of Day 7

*"Random numbers aren't truly random in computing — they're pseudo-random, controlled by seeds. This is a feature, not a bug!"*

---

### 🏆 Week 1 Complete!

```
┌─────────────────────────────────────────────────────────────┐
│                                                             │
│   🎉 CONGRATULATIONS! 🎉                                    │
│                                                             │
│   You've completed Week 1 of NumPy Mastery!                 │
│                                                             │
│   Skills Unlocked:                                          │
│   ✅ Array Creation & Properties                            │
│   ✅ Indexing & Slicing                                     │
│   ✅ Boolean Masking & Fancy Indexing                       │
│   ✅ Reshaping & Memory Management                          │
│   ✅ Mathematical Operations & Broadcasting                 │
│   ✅ Aggregations & Axis Parameter                          │
│   ✅ Random Numbers & Simulation                            │
│                                                             │
│   You're now ready for Week 2: Advanced NumPy! 🚀           │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

### 🎖️ Achievement Unlocked!

**🏅 NumPy Apprentice**

*You've mastered the fundamentals of numerical computing with NumPy!*

---

**See you in Week 2! 🚀**

![Made with NumPy](https://img.shields.io/badge/Made%20with-NumPy-013243?style=flat&logo=numpy)
![Week 1](https://img.shields.io/badge/Week%201-Complete!-success?style=flat)
![Ready](https://img.shields.io/badge/Ready%20for-Week%202-blue?style=flat)

</div>

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.