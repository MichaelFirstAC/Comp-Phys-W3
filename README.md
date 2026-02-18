# Assignment 3: Accuracy and Speed
[cite_start]**Course:** Computational Physics (SCIE6063001)   
[cite_start]**Topic:** Week 3 - Numerical Accuracy and Algorithm Speed [cite: 2]

---

## Exercise 1.1: Decimal to Binary Conversion
[cite_start]*Convert the following to binary format (up to 17 digits after the decimal point):* [cite: 3, 4]

1. [cite_start]**20.25** [cite: 4]
   - Integer ($20$): $10100$
   - Fraction ($0.25$): $0.25 \times 2 = 0.5 (0)$, $0.5 \times 2 = 1.0 (1)$
   - [cite_start]**Result:** $10100.01_2$ [cite: 4]

2. [cite_start]**0.3** [cite: 5]
   - $0.3 \times 2 = 0.6$ (0)
   - $0.6 \times 2 = 1.2$ (1)
   - $0.2 \times 2 = 0.4$ (0)
   - $0.4 \times 2 = 0.8$ (0)
   - $0.8 \times 2 = 1.6$ (1) ... (repeats 0011)
   - [cite_start]**Result:** $0.01001100110011001_2$ (at 17 digits) [cite: 4, 5]

3. [cite_start]**0.1 + 0.1 + 0.1** [cite: 5]
   - [cite_start]Binary $0.1 \approx 0.00011001100110011_2$ [cite: 4, 5]
   - [cite_start]Adding these separately highlights floating-point precision errors inherent in binary systems. [cite: 5]

---

## Exercise 1.2: Base-10 to Binary Program
[cite_start]*A Python function to convert any decimal to binary:* [cite: 6, 7]

```python
def decimal_to_binary(n, precision=17):
    integer_part = bin(int(n)).replace("0b", "")
    fractional_part = n - int(n)
    res = []
    for _ in range(precision):
        fractional_part *= 2
        bit = int(fractional_part)
        res.append(str(bit))
        fractional_part -= bit
    return f"{integer_part}.{''.join(res)}"
``` [cite: 7]

---

## Exercise 1.3: IEEE 754 Representation
[cite_start]*Representing 1025.625:* [cite: 8, 9]

- [cite_start]**Single Precision (32-bit):** [cite: 9]
  - Sign: `0` (Positive)
  - Exponent: `10001001` (137 in decimal)
  - Fraction: `00000000011010000000000`
- [cite_start]**Double Precision (64-bit):** [cite: 9]
  - Sign: `0`
  - Exponent: `10000001001` (1033 in decimal)
  - Fraction: `00000000011010000000...000`

---

## Exercise 1.4: Selection Sort Benchmark
[cite_start]*Implementing Selection Sort to find N where runtime > 1 minute.* [cite: 10, 11, 12]



```python
import time

def selection_sort(arr):
    n = len(arr)
    for i in range(n):
        min_idx = i
        for j in range(i+1, n):
            if arr[j] < arr[min_idx]:
                min_idx = j
        arr[i], arr[min_idx] = arr[min_idx], arr[i]

# Testing for N
N = 30000 # Example starting N
start = time.time()
selection_sort(list(range(N, 0, -1)))
print(f"Time for N={N}: {time.time() - start}s")
``` [cite: 11, 12, 13]

---

## Exercise 1.5: Matrix Multiplication Complexity
[cite_start]*Plotting running times for NxN matrix multiplication ($0 < N \le 1000$).* [cite: 14, 15]



```python
import time
import matplotlib.pyplot as plt
import numpy as np

[cite_start]sizes = range(10, 1001, 10) [cite: 15]
times = []

for n in sizes:
    A = np.random.rand(n, n)
    B = np.random.rand(n, n)
    start = time.time()
    # Using nested loops or np.dot for comparison
    C = np.dot(A, B) 
    times.append(time.time() - start)

plt.plot(sizes, times)
plt.xlabel('N (Matrix Size)')
plt.ylabel('Time (seconds)')
plt.title('Matrix Multiplication Running Time')
plt.show()
[cite_start]``` [cite: 15, 16]

---

## Exercise 1.6: Numerical Integration
[cite_start]*Calculating the integral from textbook exercise 4.4 (p. 138) with precision $10^{-10}$.* [cite: 17, 18, 19]

- [cite_start]**Requirement:** Precision up to $1e-10$. [cite: 19]
- [cite_start]**Method:** Adaptive Simpson’s Rule or Gaussian Quadrature is recommended to achieve this level of accuracy with fewer iterations. [cite: 19]
