# Conjclassts

**A Python Package for Enumerating Conjugacy Classes in Transformation Semigroups**

[![Python Version](https://img.shields.io/badge/python-3.7%2B-blue.svg)](https://www.python.org/downloads/)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![Status](https://img.shields.io/badge/status-active-success.svg)]()

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Documentation](#documentation)
  - [Full Transformation Semigroup](#1-full-transformation-semigroup)
  - [Partial One-to-One Transformation Semigroup](#2-partial-one-to-one-transformation-semigroup)
  - [Partial Transformation Semigroup](#3-partial-transformation-semigroup)
- [Mathematical Background](#mathematical-background)
- [Examples](#examples)
- [API Reference](#api-reference)
- [Contributing](#contributing)
- [Citation](#citation)
- [License](#license)
- [Contact](#contact)

## 🎯 Overview

`Conjclassts` is a specialized Python package designed for researchers and mathematicians working in **semigroup theory** and **algebraic combinatorics**. It provides efficient tools for enumerating and analyzing conjugacy classes in various transformation semigroups and their subsemigroups.

### Key Capabilities

- **Comprehensive Coverage**: Supports full, partial, and partial one-to-one transformation semigroups
- **Subsemigroup Analysis**: Handles order-preserving, order-reversing, order-decreasing, and contraction transformations
- **Conjugacy Classification**: Identifies and counts conjugacy classes using graph isomorphism
- **Special Elements**: Detects nilpotent and idempotent conjugacy classes
- **Visualization**: Graph-based representation of transformations using NetworkX

## ✨ Features

### 1. **Transformation Semigroup Types**
- Full Transformation Semigroup (𝒯ₙ)
- Partial One-to-One Transformation Semigroup (ℐₙ)
- Partial Transformation Semigroup (𝒫𝒯ₙ)

### 2. **Subsemigroup Variants**
For each transformation type, the package supports:
- Order-Preserving transformations
- Order-Preserving or Reversing transformations
- Order-Decreasing transformations
- Contraction transformations
- Combinations (e.g., Order-Preserving Contraction)

### 3. **Conjugacy Analysis**
- Automatic conjugacy class enumeration
- Nilpotent conjugacy class identification
- Idempotent conjugacy class identification
- Class size computation
- Graph isomorphism-based classification

## 📦 Installation

### Prerequisites
```bash
python >= 3.7
numpy
networkx
matplotlib
```

### Install from PyPI (Coming Soon)
```bash
pip install conjclassts
```

### Install from Source
```bash
git clone https://github.com/yourusername/conjclassts.git
cd conjclassts
pip install -r requirements.txt
pip install -e .
```

### Dependencies
```bash
pip install numpy networkx matplotlib itertools
```

## 🚀 Quick Start

```python
from conjclassts import FT_semigroup, conjugacy_class

# Generate full transformation semigroup for n=3
transformations = FT_semigroup(3)
print(f"Total transformations: {len(transformations)}")
# Output: Total transformations: 27

# Enumerate conjugacy classes
conjugacy_class(transformations)
# Output:
# Total Number of Conjugacy Classes: 7
# Class 1: 3 Elements
# List of Elements: [(1, 1, 1), (2, 2, 2), (3, 3, 3)]
# Idempotent Conjugacy Class 1 in Class 1: 3 Elements
# ...
```

## 📚 Documentation

### 1. Full Transformation Semigroup

The **Full Transformation Semigroup** 𝒯ₙ consists of all mappings from a finite set Xₙ = {1, 2, ..., n} to itself.

#### 1.1 Basic Full Transformation

```python
from conjclassts import FT_semigroup, conjugacy_class

# Generate all transformations for n=3
transformations = FT_semigroup(3)
print(f"Order |𝒯₃| = {len(transformations)}")  # Output: 27

# Example transformations (in two-line notation)
# (1, 2, 3) represents: 1→1, 2→2, 3→3
# (1, 1, 2) represents: 1→1, 2→1, 3→2
```

#### 1.2 Order-Preserving Full Transformation

Transformations satisfying: i ≤ j ⟹ α(i) ≤ α(j)

```python
from conjclassts import FT_semigroup, Order_Preserving_FT

transformations = FT_semigroup(3)
order_preserving = Order_Preserving_FT(3)
print(f"Order |𝒪₃| = {len(order_preserving)}")  # Output: 10

# Examples: (1,1,1), (1,1,2), (1,2,3), (2,3,3)
conjugacy_class(order_preserving)
```

#### 1.3 Order-Preserving or Reversing Full Transformation

```python
from conjclassts import Order_Preserving_Or_Reversing_FT

op_or_rev = Order_Preserving_Or_Reversing_FT(3)
print(f"Order |𝒪ℛ₃| = {len(op_or_rev)}")  # Output: 17

# Includes both increasing (1,2,3) and decreasing (3,2,1) patterns
```

#### 1.4 Order-Decreasing Full Transformation

Transformations satisfying: α(i) ≤ i for all i ∈ Xₙ

```python
from conjclassts import Order_Decreasing_FT

combinations = FT_semigroup(4)
order_decreasing = Order_Decreasing_FT(combinations)
print(f"Order |𝒪𝒟₄| = {len(order_decreasing)}")  # Output: 24
```

#### 1.5 Full Contraction Transformation

Lipschitz transformations with constant 1: |α(i) - α(j)| ≤ |i - j|

```python
from conjclassts import Contraction_FT

contractions = Contraction_FT(4)
print(f"Order |𝒞₄| = {len(contractions)}")  # Output: 68

# Example: (1,1,2,2) is a contraction
# Not a contraction: (1,3,1,3) because |3-1| > |2-1|
```

#### 1.6 Order-Preserving Full Contraction

```python
from conjclassts import Order_Preserving_Contraction_FT

op_contraction = Order_Preserving_Contraction_FT(3)
print(f"Order = {len(op_contraction)}")  # Output: 8
```

#### 1.7 Order-Preserving or Reversing Full Contraction

```python
from conjclassts import Order_Preserving_Or_Reversing_Contraction_FT

opr_contraction = Order_Preserving_Or_Reversing_Contraction_FT(3)
print(f"Order = {len(opr_contraction)}")  # Output: 13
```

#### 1.8 Order-Decreasing Full Contraction

```python
from conjclassts import Order_Decreasing_Contraction_FT

od_contraction = Order_Decreasing_Contraction_FT(FT_semigroup(3))
print(f"Order = {len(od_contraction)}")  # Output: 5
```

---

### 2. Partial One-to-One Transformation Semigroup

The **Partial One-to-One Transformation Semigroup** ℐₙ consists of all partial injective mappings. Undefined mappings are denoted by "-".

#### 2.1 Basic Partial One-to-One Transformation

```python
from conjclassts import P1T_semigroup

# Generate partial one-to-one transformations
transformations = P1T_semigroup(3)
print(f"Order |ℐ₃| = {len(transformations)}")  # Output: 34

# Examples:
# ('-', '-', '-'): all undefined
# (1, '-', 3): 1→1, 2→undefined, 3→3
# (2, 3, 1): 1→2, 2→3, 3→1 (bijection)
```

#### 2.2 Order-Preserving Partial One-to-One

```python
from conjclassts import Order_Preserving_P1T

op_p1t = Order_Preserving_P1T(P1T_semigroup(3))
print(f"Order = {len(op_p1t)}")  # Output: 20
```

#### 2.3 Order-Preserving or Reversing Partial One-to-One

```python
from conjclassts import Order_Preserving_Or_Reversing_P1T

opr_p1t = Order_Preserving_Or_Reversing_P1T(P1T_semigroup(3))
print(f"Order = {len(opr_p1t)}")  # Output: 30
```

#### 2.4 Order-Decreasing Partial One-to-One

```python
from conjclassts import Order_Decreasing_P1T

od_p1t = Order_Decreasing_P1T(P1T_semigroup(3))
print(f"Order = {len(od_p1t)}")  # Output: 15
```

#### 2.5 Partial One-to-One Contraction

```python
from conjclassts import Contraction_P1T

contraction_p1t = Contraction_P1T(P1T_semigroup(3))
print(f"Order = {len(contraction_p1t)}")  # Output: 26
```

#### 2.6 Order-Preserving Partial One-to-One Contraction

```python
from conjclassts import Order_Preserving_P1T, Contraction_P1T

p1t = P1T_semigroup(3)
contraction = Contraction_P1T(p1t)
op_contraction = Order_Preserving_P1T(contraction)
print(f"Order = {len(op_contraction)}")  # Output: 18
```

#### 2.7 Order-Preserving or Reversing Partial One-to-One Contraction

```python
from conjclassts import Order_Preserving_Or_Reversing_P1T, Contraction_P1T

p1t = P1T_semigroup(3)
contraction = Contraction_P1T(p1t)
opr_contraction = Order_Preserving_Or_Reversing_P1T(contraction)
print(f"Order = {len(opr_contraction)}")  # Output: 26
```

#### 2.8 Order-Decreasing Partial One-to-One Contraction

```python
from conjclassts import Order_Decreasing_P1T, Contraction_P1T

p1t = P1T_semigroup(3)
contraction = Contraction_P1T(p1t)
od_contraction = Order_Decreasing_P1T(contraction)
print(f"Order = {len(od_contraction)}")  # Output: 14
```

---

### 3. Partial Transformation Semigroup

The **Partial Transformation Semigroup** 𝒫𝒯ₙ consists of all partial mappings (not necessarily injective).

#### 3.1 Basic Partial Transformation

```python
from conjclassts import PT_semigroup

# Generate all partial transformations
transformations = PT_semigroup(3)
print(f"Order |𝒫𝒯₃| = {len(transformations)}")  # Output: 64

# Examples:
# (1, 1, 1): all map to 1
# ('-', 2, '-'): only 2 is defined, maps to 2
# (1, 2, 3): full transformation (bijection)
```

#### 3.2 Order-Preserving Partial Transformation

```python
from conjclassts import Order_Preserving_PT

op_pt = Order_Preserving_PT(PT_semigroup(3))
print(f"Order = {len(op_pt)}")  # Output: 38
```

#### 3.3 Order-Preserving or Reversing Partial Transformation

```python
from conjclassts import Order_Preserving_Or_Reversing_PT

opr_pt = Order_Preserving_Or_Reversing_PT(PT_semigroup(3))
print(f"Order = {len(opr_pt)}")  # Output: 54
```

#### 3.4 Order-Decreasing Partial Transformation

```python
from conjclassts import Order_Decreasing_PT

od_pt = Order_Decreasing_PT(PT_semigroup(3))
print(f"Order = {len(od_pt)}")  # Output: 24
```

#### 3.5 Partial Contraction Transformation

```python
from conjclassts import Contraction_PT

contraction_pt = Contraction_PT(PT_semigroup(3))
print(f"Order = {len(contraction_pt)}")  # Output: 50
```

#### 3.6 Order-Preserving Partial Contraction

```python
from conjclassts import Order_Preserving_PT, Contraction_PT

pt = PT_semigroup(3)
contraction = Contraction_PT(pt)
op_contraction = Order_Preserving_PT(contraction)
print(f"Order = {len(op_contraction)}")  # Output: 34
```

#### 3.7 Order-Preserving or Reversing Partial Contraction

```python
from conjclassts import Order_Preserving_Or_Reversing_PT, Contraction_PT

pt = PT_semigroup(3)
contraction = Contraction_PT(pt)
opr_contraction = Order_Preserving_Or_Reversing_PT(contraction)
print(f"Order = {len(opr_contraction)}")  # Output: 46
```

#### 3.8 Order-Decreasing Partial Contraction

```python
from conjclassts import Order_Decreasing_PT, Contraction_PT

pt = PT_semigroup(3)
contraction = Contraction_PT(pt)
od_contraction = Order_Decreasing_PT(contraction)
print(f"Order = {len(od_contraction)}")  # Output: 22
```

---

## 🔬 Mathematical Background

### Conjugacy in Transformation Semigroups

Two transformations α and β are **conjugate** if there exists a permutation γ in the symmetric group Sₙ such that:

β = γ⁻¹ ∘ α ∘ γ

This package uses **graph isomorphism** to determine conjugacy: transformations are conjugate if and only if their directed graphs (where i → α(i)) are isomorphic.

### Special Conjugacy Classes

#### Idempotent Elements
An element α is **idempotent** if α² = α. In transformation semigroups, idempotents fix their image pointwise.

#### Nilpotent Elements
An element α is **nilpotent** if αᵏ is a constant map for some k ≥ 1.

### Orders (Cardinalities)

| Semigroup | Notation | Order Formula |
|-----------|----------|---------------|
| Full Transformation | 𝒯ₙ | nⁿ |
| Partial One-to-One | ℐₙ | Σₖ₌₀ⁿ C(n,k)·k! |
| Partial Transformation | 𝒫𝒯ₙ | (n+1)ⁿ |
| Order-Preserving | 𝒪ₙ | C(2n-1, n) |
| Symmetric Group | Sₙ | n! |

---

## 💡 Examples

### Example 1: Complete Conjugacy Analysis

```python
from conjclassts import FT_semigroup, conjugacy_class

# Analyze full transformation semigroup
transformations = FT_semigroup(3)
conjugacy_class(transformations)
```

**Output:**
```
Total Number of Conjugacy Classes: 7

Class 1: 3 Elements
List of Elements: [(1, 1, 1), (2, 2, 2), (3, 3, 3)]
Idempotent Conjugacy Class 1 in Class 1: 3 Elements

Class 2: 6 Elements
List of Elements: [(1, 1, 2), (1, 3, 1), (2, 2, 1), (2, 3, 3), (3, 1, 3), (3, 2, 2)]

...

Total Number of Nilpotent Conjugacy Classes: 2
Total Number of Idempotent Conjugacy Classes: 3
```

### Example 2: Comparing Subsemigroups

```python
from conjclassts import *

n = 4

# Generate different subsemigroups
ft = FT_semigroup(n)
op_ft = Order_Preserving_FT(n)
opr_ft = Order_Preserving_Or_Reversing_FT(n)
c_ft = Contraction_FT(n)

print(f"Full Transformation: {len(ft)}")
print(f"Order-Preserving: {len(op_ft)}")
print(f"Order-Preserving/Reversing: {len(opr_ft)}")
print(f"Contraction: {len(c_ft)}")
```

**Output:**
```
Full Transformation: 256
Order-Preserving: 35
Order-Preserving/Reversing: 67
Contraction: 68
```

### Example 3: Visualizing Conjugacy Classes

```python
from conjclassts import P1T_semigroup, conjugacy_class
import networkx as nx
import matplotlib.pyplot as plt

# Generate and visualize
transformations = P1T_semigroup(3)
conjugacy_class(transformations)  # This will display graphs for each class
```

---

## 📖 API Reference

### Core Functions

#### `FT_semigroup(n)`
Generate all full transformations on n elements.
- **Parameters:** `n` (int) - size of the set
- **Returns:** list of tuples representing transformations
- **Example:** `FT_semigroup(3)` returns 27 transformations

#### `P1T_semigroup(n)`
Generate all partial one-to-one transformations.
- **Parameters:** `n` (int) - size of the set
- **Returns:** list of tuples (with '-' for undefined)
- **Example:** `P1T_semigroup(3)` returns 34 transformations

#### `PT_semigroup(n)`
Generate all partial transformations.
- **Parameters:** `n` (int) - size of the set
- **Returns:** list of tuples
- **Example:** `PT_semigroup(3)` returns 64 transformations

#### `conjugacy_class(tuples_list)`
Enumerate and analyze conjugacy classes.
- **Parameters:** `tuples_list` (list) - transformations to classify
- **Prints:** Complete conjugacy class analysis
- **Identifies:** Nilpotent and idempotent classes

### Filter Functions

#### `Order_Preserving_FT(n)` / `Order_Preserving_P1T(tuples)` / `Order_Preserving_PT(tuples)`
Filter for order-preserving transformations.

#### `Order_Preserving_Or_Reversing_FT(n)` / Similar for P1T and PT
Filter for order-preserving or order-reversing transformations.

#### `Order_Decreasing_FT(tuples)` / Similar for P1T and PT
Filter for order-decreasing transformations.

#### `Contraction_FT(n)` / `Contraction_P1T(tuples)` / `Contraction_PT(tuples)`
Filter for contraction transformations.

### Utility Functions

#### `compose(a, b)`
Compose two transformations: a ∘ b
- **Parameters:** `a`, `b` (tuples) - transformations
- **Returns:** tuple - composed transformation

#### `compute_nilpotent_idempotent(elements)`
Identify nilpotent and idempotent elements.
- **Parameters:** `elements` (list) - transformations
- **Returns:** tuple of (nilpotent_list, idempotent_list)

---

## 🤝 Contributing

We welcome contributions! Here's how you can help:

### Reporting Bugs
- Use the GitHub issue tracker
- Include Python version, package version, and minimal reproducible example

### Suggesting Enhancements
- Open an issue with the tag "enhancement"
- Describe the feature and its use case

### Pull Requests
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Development Setup
```bash
git clone https://github.com/ClintonKayoh/conjclassts.git
cd conjclassts
pip install -r requirements-dev.txt
pytest tests/
```

---

## 📝 Citation

If you use this package in your research, please cite:

```bibtex
@software{conjclassts2025,
  author = {Clinton Oluranran Kayoh},
  title = {Conjclassts: A Python Package for Enumerating Conjugacy Classes in Transformation Semigroups},
  year = {2025},
  url = {https://github.com/ClintonKayoh/conjclassts},
  version = {1.0.0}
}
```

### Related Publications
- Howie, J. M. (1995). *Fundamentals of Semigroup Theory*. Oxford University Press.
- Ganyushkin, O. & Mazorchuk, V. (2009). *Classical Finite Transformation Semigroups*. Springer.

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

```
MIT License

Copyright (c) 2025 Clinton Oluranran Kayoh

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction...
```

---

## 📧 Contact

**Clinton Oluranran Kayoh**
- GitHub: [@ClintonKayoh](https://github.com/ClintonKayoh)
- Email: kayohclinton@gmail.com
- Research Gate: [Clinton Kayoh](https://www.researchgate.net/profile/ClintonKayoh)

### Support
- 📮 Issues: [GitHub Issues](https://github.com/ClintonKayoh/conjclassts/issues)
- 💬 Discussions: [GitHub Discussions](https://github.com/ClintonKayoh/conjclassts/discussions)
- 📚 Documentation: [Read the Docs](https://conjclassts.readthedocs.io) (coming soon)

---

## 🙏 Acknowledgments

- NetworkX team for graph isomorphism algorithms
- The semigroup theory community for foundational research
- Contributors and users of this package

---

## 🗺️ Roadmap

### Version 1.1 (Planned)
- [ ] Performance optimizations for n > 5
- [ ] Parallel processing support
- [ ] Export results to LaTeX format
- [ ] Interactive visualization dashboard

### Version 1.2 (Future)
- [ ] Support for additional transformation types
- [ ] Green's relations computation
- [ ] Maximal subgroup identification
- [ ] Integration with SageMath

---

## 📊 Performance Notes

| n | 𝒯ₙ Size | Computation Time* |
|---|---------|-------------------|
| 3 | 27 | < 0.1s |
| 4 | 256 | ~1s |
| 5 | 3,125 | ~30s |
| 6 | 46,656 | ~15min |

*Times are approximate and depend on hardware

### Tips for Large n
- Use subsemigroup filters to reduce computation
- Consider caching results
- Use multiprocessing for independent computations

---

**Made with ❤️ for the algebraic combinatorics community**# Conjclassts
Python Package for Enumerating Conjugacy classes in Transformation Semigroups and Monoids
