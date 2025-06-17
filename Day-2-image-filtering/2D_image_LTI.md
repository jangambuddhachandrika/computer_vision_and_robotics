
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

In image processing, **horizontal**, **vertical**, and **gradient** filters are used for **edge detection**, **feature extraction**, and **enhancing details**. These filters work by convolving a kernel (matrix) with the image.

---

### 1. **Horizontal Filter**

Detects **horizontal edges** — i.e., changes in intensity **along rows** (left to right).

**Example Kernel (Sobel Horizontal):**

```text
[-1  -2  -1]
[ 0   0   0]
[ 1   2   1]
```

This emphasizes differences in pixel values **top to bottom**.

---

### 2. **Vertical Filter**

Detects **vertical edges** — i.e., changes in intensity **along columns** (top to bottom).

**Example Kernel (Sobel Vertical):**

```text
[-1   0   1]
[-2   0   2]
[-1   0   1]
```

This emphasizes differences **left to right**.

---

### 3. **Gradient Filter**

Combines both horizontal and vertical filters to detect the **overall edge strength and direction**.

**Gradient Magnitude** is typically computed as:

```python
G = sqrt(Gx² + Gy²)
```

Or approximated as:

```python
G ≈ |Gx| + |Gy|
```

Where:

* `Gx` = result of horizontal filter
* `Gy` = result of vertical filter

---

### Example with OpenCV (Python)

```python
import cv2
import numpy as np
from matplotlib import pyplot as plt

# Load grayscale image
img = cv2.imread('image.jpg', cv2.IMREAD_GRAYSCALE)

# Apply Sobel filters
sobel_x = cv2.Sobel(img, cv2.CV_64F, 1, 0, ksize=3)  # Horizontal
sobel_y = cv2.Sobel(img, cv2.CV_64F, 0, 1, ksize=3)  # Vertical

# Gradient magnitude
gradient = cv2.magnitude(sobel_x, sobel_y)

# Display
plt.subplot(1, 3, 1), plt.imshow(sobel_x, cmap='gray'), plt.title('Horizontal')
plt.subplot(1, 3, 2), plt.imshow(sobel_y, cmap='gray'), plt.title('Vertical')
plt.subplot(1, 3, 3), plt.imshow(gradient, cmap='gray'), plt.title('Gradient')
plt.show()
```

---
Yes — **horizontal (x) and vertical (y) filters are separable** in many cases, especially with common kernels like **Gaussian** and **Sobel**. A **separable filter** means a 2D filter can be expressed as the **outer product of two 1D filters**, significantly reducing computational cost.

---

### 🔹 What is a Separable Filter?

A 2D filter $K(x, y)$ is **separable** if:

$$
K(x, y) = f(x) \cdot g(y)
$$

So instead of convolving a 2D kernel, you do:

1. Convolve image with $f(x)$ along **rows**
2. Then convolve result with $g(y)$ along **columns**

This reduces:

* **Computation from O(n²)** to **O(2n)** per pixel for an $n \times n$ kernel

---

### 🔹 Example: Gaussian Filter

A 2D **Gaussian kernel** is separable:

$$
G(x, y) = G_x(x) \cdot G_y(y)
$$

#### 1D Gaussian (e.g., for σ=1):

```text
Gx = [1 2 1]
Gy = [1
      2
      1]
```

So the 2D kernel:

```text
[1 2 1]ᵀ * [1 2 1] = 
[
 [1 2 1]
 [2 4 2]
 [1 2 1]
]
```

You can apply horizontal then vertical 1D convolutions instead of a full 3x3 2D convolution.

---

### 🔹 Example: Sobel Filter (Separable!)

Sobel X:

$$
S_x = \begin{bmatrix}
-1 & 0 & 1 \\
-2 & 0 & 2 \\
-1 & 0 & 1
\end{bmatrix}
\quad = 
\begin{bmatrix}
1 \\
2 \\
1
\end{bmatrix}
\cdot
\begin{bmatrix}
-1 & 0 & 1
\end{bmatrix}
$$

So you can do:

* Horizontal convolution with `[-1 0 1]`
* Then vertical convolution with `[1 2 1]ᵗ`

---

### 🔹 OpenCV Example with Separable Gaussian

```python
import cv2
import numpy as np

img = cv2.imread('image.jpg', 0)

# Use 1D Gaussian
kernel_1d = cv2.getGaussianKernel(ksize=5, sigma=1)

# Apply horizontal then vertical
blur_horizontal = cv2.sepFilter2D(img, -1, kernel_1d, np.array([[1]]))  # Horizontal
blur = cv2.sepFilter2D(blur_horizontal, -1, np.array([[1]]), kernel_1d)  # Vertical
```

Or simply:

```python
blur = cv2.sepFilter2D(img, -1, kernel_1d, kernel_1d)
```

---

### ✅ Benefits of Separable Filters

* Faster computation
* Lower memory usage
* Mathematically equivalent to 2D convolution for separable kernels

---




