# Specious Randomness Generator & χ² Randomness Tester

This repository implements the specious randomness construction and the double-sided χ² statistical test described in:

**Almlöf et al., "Creating and detecting specious randomness", EPJ Quantum Technology (2023).**

Specious randomness refers to binary sequences that appear random to traditional test suites (e.g., NIST SP 800-22) but are, in fact, artificially structured so that all possible *N-bit patterns* occur exactly once. These sequences pass NIST tests but fail the lower-tail χ² test because their n-gram frequencies are **too close** to uniform.

This project provides:

- A **specious random number generator** that builds complete number-system strings (all 2ⁿ patterns of length n).
- A **double-sided χ² statistical tester** that detects suspiciously uniform n-gram distributions.

---

## Features

### ✔ Specious Random Number Generator
- Generates a complete number-system sequence of length `N * 2^N`.
- Supports optional shuffling of the pattern order.
- Can automatically select an optimal `N` for a desired output length.
- Outputs 8-bit lines compatible with NIST SP 800-22.

### ✔ Double-Sided χ² Randomness Test
- Implements the χ² statistic for discrete uniform distributions (Eq. 18).
- Evaluates both:
  - **Upper critical bound** (traditional deviation)
  - **Lower critical bound** (Fisher-style detection of “too uniform” data)
- Uses SciPy where available; falls back to Gaussian approximation.
- Includes overlapping n-gram counting (default).

---

## Usage

### Generate Specious Randomness
```python
generate_specious_stream(
    N=16,
    outfile="specious_bits.txt",
    shuffle=True
)
