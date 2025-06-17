

### ✅ Statement:

> A **discrete-time LTI system** is **completely characterized** by its **impulse response $h[n]$**.
> This means: **If you know the system’s response to a unit impulse**, you can compute its response to **any arbitrary input signal** using **convolution**.

---

### 🔍 Why?

The key ideas are:

1. **Linearity** allows us to break any input signal into a sum of scaled and shifted impulses.
2. **Time Invariance** ensures that if the response to $\delta[n]$ is $h[n]$, then the response to $\delta[n - k]$ is $h[n - k]$.

---

### 📦 Impulse Decomposition of Input

Any signal $x[n]$ can be written as:

$$
x[n] = \sum_{k = -\infty}^{\infty} x[k] \cdot \delta[n - k]
$$

Now, due to linearity and time invariance, the system's response to this input is:

$$
y[n] = \sum_{k = -\infty}^{\infty} x[k] \cdot h[n - k]
$$

This is the **convolution** of $x[n]$ with $h[n]$:

$$
y[n] = (x * h)[n]
$$

---

### 🔁 Convolution is the Core Operation

So, once you know $h[n]$, you don’t need to know how the system behaves on other inputs — you can compute the output to **any** input $x[n]$ via:

$$
y[n] = \sum_{k = -\infty}^{\infty} x[k] \cdot h[n - k]
$$

---

### 🧠 Interpretation:

* The **impulse response acts like a fingerprint** for the system.
* Knowing it means you know **everything** about how the system reacts to signals.
* This is why engineers focus on measuring or designing $h[n]$ when working with DSP systems.



## 🔢 Example

Let’s say we have:

### 1. Input signal:

$$
x[n] = [1, 2, 3] \quad \text{(defined at } n = 0, 1, 2 \text{)}
$$

### 2. Impulse response:

$$
h[n] = [1, -1] \quad \text{(defined at } n = 0, 1 \text{)}
$$

---

## 🔁 Convolution Formula:

$$
y[n] = \sum_{k=-\infty}^{\infty} x[k] \cdot h[n - k]
$$

Since $x[n]$ is nonzero for $n = 0, 1, 2$, and $h[n]$ is nonzero for $n = 0, 1$, the output $y[n]$ will be defined for:

$$
n = 0 \text{ to } (2 + 1) = 3
$$

---

## 🧮 Step-by-Step Convolution:

Let’s compute $y[0], y[1], y[2], y[3]$:

---

### ✅ $y[0]$

$$
y[0] = x[0] \cdot h[0] = 1 \cdot 1 = 1
$$

---

### ✅ $y[1]$

$$
y[1] = x[0] \cdot h[1] + x[1] \cdot h[0] = 1 \cdot (-1) + 2 \cdot 1 = -1 + 2 = 1
$$

---

### ✅ $y[2]$

$$
y[2] = x[1] \cdot h[1] + x[2] \cdot h[0] = 2 \cdot (-1) + 3 \cdot 1 = -2 + 3 = 1
$$

---

### ✅ $y[3]$

$$
y[3] = x[2] \cdot h[1] = 3 \cdot (-1) = -3
$$

---

## 📦 Final Output:

$$
y[n] = [1, 1, 1, -3]
$$

---

## 🧠 Summary:

The output was computed **only using the impulse response** and the **input signal** via convolution.
This demonstrates how an **LTI system is fully characterized by its impulse response**.


