

---

# 📚 Discrete-Time Signal Processing

---

## 1. 📈 Discrete-Time Signals

### 1.1 Definition

A **discrete-time signal** is a sequence of values defined only at integer times.
It is denoted as $x[n]$, where $n \in \mathbb{Z}$ is an integer index.

### 1.2 Common Discrete-Time Signals

* **Unit Impulse**: $\delta[n] = \begin{cases} 1 & n = 0 \\ 0 & n \neq 0 \end{cases}$
* **Unit Step**: $u[n] = \begin{cases} 1 & n \ge 0 \\ 0 & n < 0 \end{cases}$
* **Exponential**: $x[n] = a^n$, for $a \in \mathbb{R}$
* **Sinusoidal**: $x[n] = \sin(\omega n + \phi)$

### 1.3 Signal Operations

* **Time Shifting**: $x[n - n_0]$
* **Time Reversal**: $x[-n]$
* **Scaling**: $a \cdot x[n]$
* **Addition**: $x[n] + y[n]$

---

## 2. 🧠 Discrete-Time Systems

### 2.1 System Properties

* **Linearity**: Additivity + Homogeneity
* **Time Invariance**: $x[n - n_0] \rightarrow y[n - n_0]$
* **Causality**: Output depends only on current and past inputs
* **Stability**: BIBO (Bounded Input → Bounded Output)
* **Memory**: Memoryless if output at time $n$ depends only on input at $n$

### 2.2 Linear Time-Invariant (LTI) Systems

An LTI system is fully described by its **impulse response** $h[n]$.

---

## 3. 🔁 Convolution (Time-Domain Analysis)

For an LTI system with impulse response $h[n]$, the output $y[n]$ for input $x[n]$ is:

$$
y[n] = (x * h)[n] = \sum_{k = -\infty}^{\infty} x[k] \cdot h[n - k]
$$

### 3.1 Properties of Convolution

* Commutative: $x * h = h * x$
* Associative: $x * (h_1 * h_2) = (x * h_1) * h_2$
* Distributive: $x * (h_1 + h_2) = x * h_1 + x * h_2$

---

## 4. ⚙️ Z-Transform (System Analysis in z-domain)

### 4.1 Definition

The Z-transform of a discrete-time signal $x[n]$ is:

$$
X(z) = \sum_{n=-\infty}^{\infty} x[n] z^{-n}
$$

### 4.2 Region of Convergence (ROC)

* Set of $z$ values for which the sum converges.
* Important for **stability** and **causality** analysis.

### 4.3 Properties

* Linearity
* Time shift: $x[n - k] \leftrightarrow z^{-k} X(z)$
* Convolution in time ⇔ Multiplication in z-domain

### 4.4 Inverse Z-Transform Techniques

* Long division
* Power series expansion
* Residue method (partial fractions)

### 4.5 Transfer Function

For system with impulse response $h[n]$:

$$
H(z) = \frac{Y(z)}{X(z)} = Z\{h[n]\}
$$

---

## 5. 📊 Frequency Analysis of Signals

### 5.1 Discrete-Time Fourier Transform (DTFT)

$$
X(e^{j\omega}) = \sum_{n=-\infty}^{\infty} x[n] e^{-j\omega n}
$$

* Continuous in frequency $\omega$
* Periodic with period $2\pi$

### 5.2 Discrete Fourier Transform (DFT)

Used when signal is **finite** and **periodic**:

$$
X[k] = \sum_{n=0}^{N-1} x[n] e^{-j2\pi kn/N}, \quad k = 0,1,\dots,N-1
$$

* Can be computed efficiently using **FFT (Fast Fourier Transform)**

### 5.3 Properties of DFT

* Linearity
* Time shifting
* Convolution theorem (circular convolution)

---

## 6. 🔉 Digital Filter Design

### 6.1 Filter Types

* **FIR (Finite Impulse Response)**: $h[n] = 0$ for $n > M$
* **IIR (Infinite Impulse Response)**: Infinite duration due to feedback

### 6.2 FIR Design (Windowing Method)

1. Design ideal filter in frequency domain
2. Take inverse DTFT to get $h[n]$
3. Apply a window (Hamming, Hanning, Blackman) to truncate

### 6.3 IIR Filter Design

* Use analog prototype (Butterworth, Chebyshev)
* Transform to digital using:

  * Bilinear transform
  * Impulse invariance

### 6.4 Filter Specifications

* **Passband** and **Stopband**
* **Cutoff Frequency**
* **Ripple** and **Attenuation**
* Trade-offs between transition width and ripple

---

## 7. 🧪 DSP Applications

* Audio & speech processing
* Radar and sonar
* Image processing
* Communication systems
* Biomedical signal analysis (ECG, EEG)

---

### 🔚 Summary Table

| Concept       | Time-Domain    | Frequency-Domain | Z-Domain        |
| ------------- | -------------- | ---------------- | --------------- |
| Signal        | $x[n]$         | $X(e^{j\omega})$ | $X(z)$          |
| System        | $h[n]$         | $H(e^{j\omega})$ | $H(z)$          |
| Analysis Tool | Convolution    | Multiplication   | Multiplication  |
| Output        | $y[n] = x * h$ | $Y = X \cdot H$  | $Y = X \cdot H$ |

---

