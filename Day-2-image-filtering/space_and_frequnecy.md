The concepts of **space domain** and **frequency domain** relate to how signals (including images) are represented, processed, and analyzed. The **canonical basis** in each domain refers to a set of vectors or functions that form the "building blocks" for signals in that domain.

---

## 🧭 Summary

| Domain        | Canonical Basis                  | Intuition                                              |
| ------------- | -------------------------------- | ------------------------------------------------------ |
| **Spatial**   | Impulse basis (delta functions)  | Each basis represents a value at one pixel or location |
| **Frequency** | Sinusoids / Complex exponentials | Each basis represents a global frequency component     |

---

## 📌 1. **Space Domain (Spatial Canonical Basis)**

### Basis: **Kronecker delta / Unit impulse**

In 1D:

$$
\delta[n - k] = \begin{cases}
1 & \text{if } n = k \\
0 & \text{otherwise}
\end{cases}
$$

In 2D images:

* Each image can be viewed as a **sum of pixel-wise delta functions**.
* Each basis image has a value of **1 at one pixel** and **0 elsewhere**.

This is the **canonical basis in space**:

* Easy to interpret
* Localized — represents **individual pixels**

---

## 📌 2. **Frequency Domain (Fourier Canonical Basis)**

### Basis: **Complex exponentials / Sinusoids**

In 1D:

$$
e^{j2\pi fn}
$$

In 2D (images):

$$
e^{j2\pi(ux + vy)}
$$

These are the basis functions used in the **Discrete Fourier Transform (DFT)**.

Every image can be represented as a **weighted sum of sinusoids** with varying frequencies and orientations:

* These are **global** — they span the entire image.
* Represent how much of each frequency is present.

---

### 🎯 Why "Canonical"?

A **canonical basis** is:

* Complete (you can represent any signal using it)
* Linearly independent
* Natural to the domain

In:

* **Spatial domain** → Canonical basis = **unit impulses**
* **Frequency domain** → Canonical basis = **Fourier basis (sinusoids)**

---

## 📊 Analogy

| Concept      | Spatial Basis        | Frequency Basis              |
| ------------ | -------------------- | ---------------------------- |
| Vector space | Unit vectors $e_i$   | Fourier basis $e^{j2\pi fn}$ |
| Image        | Pixels               | Frequencies                  |
| Operation    | Convolution          | Multiplication in frequency  |
| Locality     | Local (single pixel) | Global (entire image)        |

---

## 📎 Applications

* **Image compression** (JPEG uses DCT – a frequency basis)
* **Filtering**: Spatial filters (like Gaussian) vs frequency filters (low-pass, high-pass)
* **Signal reconstruction** from basis components

---

