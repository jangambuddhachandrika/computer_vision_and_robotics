
## ✅ 1. Discrete Image = 2D Discrete Signal

A **discrete image** is a **2D matrix**:

* Denoted as $f[m, n]$
* $m$: row index (vertical position)
* $n$: column index (horizontal position)
* Each value is a pixel intensity (e.g., 0–255 for grayscale)

---

## ✅ 2. Impulse in 2D (2D Delta Function)

The **2D impulse**, $\delta[m, n]$, is defined as:

$$
\delta[m, n] =
\begin{cases}
1, & m = 0, n = 0 \\
0, & \text{otherwise}
\end{cases}
$$

Think of it as an image where **only the center pixel is white (1)** and all others are black (0).

---

## ✅ 3. Linear Time-Invariant (LTI) Systems in 2D

A 2D **LTI system** satisfies:

### **Linearity**:

If input = $a f_1[m,n] + b f_2[m,n]$,
Then output = $a y_1[m,n] + b y_2[m,n]$

### **Shift Invariance**:

If shifting the input by $(m_0, n_0)$ shifts the output by the **same amount**, the system is shift-invariant.

---

## ✅ 4. Impulse Response Fully Characterizes 2D LTI System

Just like in 1D, a **2D LTI system is fully characterized by its impulse response $h[m, n]$**.

### 📌 That means:

If you know what output the system gives for the 2D impulse $\delta[m,n]$,
you can compute the output for **any input image** via **2D convolution**:

$$
y[m,n] = (f * h)[m,n] = \sum_{i} \sum_{j} f[i,j] \cdot h[m - i, n - j]
$$

---

## ✅ 5. Example: Box Blur Filter

Let’s say the system applies a **box blur** with kernel:

$$
h[m,n] = \frac{1}{9}
\begin{bmatrix}
1 & 1 & 1 \\
1 & 1 & 1 \\
1 & 1 & 1
\end{bmatrix}
$$

* This kernel **is the impulse response** of the system.
* Any image passed through this system gets convolved with $h[m,n]$.

---

## ✅ 6. How to Find the Impulse Response Practically

To **find the impulse response of a 2D system**:

1. Create an image with a 1 at the center and 0s elsewhere.
2. Pass this image through the system (filter, algorithm, etc.).
3. The output is the **impulse response $h[m,n]$**.

---

### 🧪 Python Code Example

```python
import numpy as np
import cv2
import matplotlib.pyplot as plt

# 7x7 impulse image
impulse = np.zeros((7, 7), dtype=np.float32)
impulse[3, 3] = 1.0

# Apply a Gaussian blur (LTI system)
h = cv2.GaussianBlur(impulse, (3, 3), sigmaX=1)

# Display impulse response
plt.imshow(h, cmap='gray')
plt.title("Impulse Response of 2D Gaussian Filter")
plt.colorbar()
plt.show()
```

---

## 🧠 Summary Table

| Concept              | Description                                                  |
| -------------------- | ------------------------------------------------------------ |
| Discrete Image       | 2D matrix of pixel values                                    |
| 2D Impulse           | Only one pixel is 1, all others are 0                        |
| 2D LTI System        | Linear + Shift Invariant; output computed via 2D convolution |
| Impulse Response $h$ | Output of the system when input is the 2D impulse            |
| System Output        | $y[m,n] = f[m,n] * h[m,n]$ — 2D convolution                  |


