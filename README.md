# Assignment 3: Accuracy and Speed
**Course:** Computational Physics (SCIE6063001)   
**Topic:** Week 3 - Numerical Accuracy and Algorithm Speed

---

## Exercise 1.1: Decimal to Binary Conversion
*Convert the following to binary format (up to 17 digits after the decimal point):*

1. **20.25** 
   - Integer ($20$): $10100$
   - Fraction ($0.25$): $0.25 \times 2 = 0.5 (0)$, $0.5 \times 2 = 1.0 (1)$
   - **Result:** $10100.01_2$ 

2. **0.3**
   - $0.3 \times 2 = 0.6$ (0)
   - $0.6 \times 2 = 1.2$ (1)
   - $0.2 \times 2 = 0.4$ (0)
   - $0.4 \times 2 = 0.8$ (0)
   - $0.8 \times 2 = 1.6$ (1) ... (repeats 0011)
   - **Result:** $0.01001100110011001_2$ (at 17 digits) 

3. **0.1 + 0.1 + 0.1**
   - Binary $0.1 \approx 0.00011001100110011_2$
   - Adding these separately highlights floating-point precision errors inherent in binary systems.

---

## Exercise 1.2: Base-10 to Binary Program
*A Python function to convert any decimal to binary:* 

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
```

---

## Exercise 1.3: IEEE 754 Representation
*Representing 1025.625:* 

- **Single Precision (32-bit):** 
  - Sign: `0` (Positive)
  - Exponent: `10001001` (137 in decimal)
  - Fraction: `00000000011010000000000`
- **Double Precision (64-bit):** 
  - Sign: `0`
  - Exponent: `10000001001` (1033 in decimal)
  - Fraction: `00000000011010000000...000`

---

## Exercise 1.4: Selection Sort Benchmark
*Implementing Selection Sort to find N where runtime > 1 minute.*



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
``` 

---

## Exercise 1.5: Matrix Multiplication Complexity
*Plotting running times for NxN matrix multiplication ($0 < N \le 1000$).*



```python
import time
import matplotlib.pyplot as plt
import numpy as np

sizes = range(10, 1001, 10)
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
```

---

## Exercise 1.6: Numerical Integration
*Calculating the integral from textbook exercise 4.4 (p. 138) with precision $10^{-10}$.* 

- **Requirement:** Precision up to $1e-10$. 
- **Method:** Adaptive Simpson’s Rule or Gaussian Quadrature is recommended to achieve this level of accuracy with fewer iterations.
