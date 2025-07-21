
---

# MPIN Strength Checker

A Python-based utility to evaluate the strength of 4-digit and 6-digit Mobile Personal Identification Numbers (MPINs) using pattern recognition and demographic information.

> **Author**: Aryan Sharma
> **Note**: This project is for educational purposes only and does not collect or store any personal data.

---

## Table of Contents

* [Features](#features)
* [How It Works](#how-it-works)
* [Assumptions](#assumptions)
* [File Structure](#file-structure)
* [How to Run](#how-to-run)
* [Test Cases](#test-cases)
* [Usage Examples](#usage-examples)

---

## Features

This project consists of two main Python notebooks for analyzing MPIN strength:

1. **`AryanSharma(4 digit MPIN).ipynb`**

   * **Part A** – Basic MPIN check against common 4-digit values.
   * **Parts B & C** – Enhanced checks using demographic information:

     * Self Date of Birth (DOB)
     * Spouse DOB
     * Wedding Anniversary
   * Returns whether the MPIN is `WEAK` or `STRONG` with a list of reasons for weakness (e.g., `["commonly_used", "self_DOB"]`).

2. **`AryanSharma(6 digit MPIN).ipynb`**

   * **Part D** – Extension of the above logic for 6-digit MPINs.
   * Includes demographic and common pattern checks.

3. **Test Suite**

   * Each notebook contains **20+ test cases** covering valid, weak, and invalid MPINs.

---

## How It Works

MPINs are evaluated based on:

### 1. Common Patterns

Compared against a predefined list of frequently used MPINs.

### 2. Demographic Association

Checks whether the MPIN includes patterns from:

* Self Date of Birth
* Spouse DOB
* Anniversary Date

Supported formats include:

* `DDMM`, `MMDD`, `YYMMDD`, `YYYYMMDD`, etc.

---

## Assumptions

* **Common MPINs**: Maintained in internal lists and can be manually updated.
* **Date Input Format**: Should be `YYYY-MM-DD`. Invalid or empty entries are ignored.
* **MPIN Format**:

  * Must be exactly 4 or 6 digits.
  * Any other length or non-numeric format returns an `"INVALID"` result.

---

## File Structure

```
.
├── AryanSharma(4 digit MPIN).ipynb      # 4-digit MPIN strength logic and tests
└── AryanSharma(6 digit MPIN).ipynb      # 6-digit MPIN strength logic and tests
```

---

## How to Run

### 1. Prerequisites

* Python 3.x
* Jupyter Notebook or Jupyter Lab

### 2. Installation

```bash
pip install jupyter
```

### 3. Run the Notebooks

```bash
jupyter notebook
```

* Open the `.ipynb` file from your browser.
* Run cells using `Shift + Enter`, or use `Run All` from the menu.

---

## Test Cases

Each notebook includes at least 20 test cases validating:

* Common weak MPINs (e.g., `1234`, `1111`, `123456`)
* MPINs matching user DOBs or anniversaries
* Strong MPINs with no pattern matches
* Invalid formats (wrong length, non-digits)

Example Output:

```python
{'strength': 'WEAK', 'reasons': ['commonly_used']}
```

---

## Usage Examples

### 4-Digit MPIN

```python
mpin1 = "1234"
demographics1 = {"dob_self": "", "dob_spouse": "", "anniversary": ""}
result1 = check_mpin_strength(mpin1, **demographics1)
# Output: {'strength': 'WEAK', 'reasons': ['commonly_used']}
```

```python
mpin2 = "0102"
demographics2 = {"dob_self": "1990-02-01", "dob_spouse": "", "anniversary": ""}
result2 = check_mpin_strength(mpin2, **demographics2)
# Output: {'strength': 'WEAK', 'reasons': ['self_DOB']}
```

### 6-Digit MPIN

```python
mpin3 = "789012"
demographics3 = {"dob_self": "1985-01-01", "dob_spouse": "1986-02-02", "anniversary": "2010-03-03"}
result3 = check_mpin_strength(mpin3, **demographics3)
# Output: {'strength': 'STRONG', 'reasons': []}
```

```python
mpin4 = "030310"
demographics4 = {"anniversary": "2010-03-03"}
result4 = check_mpin_strength(mpin4, dob_self="", dob_spouse="", **demographics4)
# Output: {'strength': 'WEAK', 'reasons': ['anniversary_date']}
```

---
