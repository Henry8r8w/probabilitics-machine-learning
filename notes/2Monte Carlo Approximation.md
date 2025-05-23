## 🏃‍♂️ The Steps to Obtain Our Quantity of Interest

### Step 1: Generate $S_n$ from the distribution $X_1, \dots, X_n$

**Various Methods:**

1. Markov Chain Monte Carlo
2. Binomial sampling (e.g., Bernoulli process)

### Step 2: Approximate the empirical distribution of $\{f(x_s)\}_{s=1}^n$

Monte Carlo approximation:

* Originated in statistical physics during WWII
* Named after the famous Monte Carlo casino

The goal is to estimate **expected values**:

$$
\mathbb{E}[f(X)] = \int f(x) p(x)dx \approx \frac{1}{N} \sum_{s=1}^{N} f(x_s), \quad \text{where } x_s \sim p(x)
$$

**Also known as Monte Carlo Integration (canonical form)**

---

## 😜 The Advantage of Monte Carlo Over Grid-Based Numerical Integration

**Numerical integration** (e.g., Simpson's Rule, Trapezoidal Rule) evaluates $f(x)$ at fixed, uniform intervals. This wastes computation in areas where $p(x) \approx 0$.

**Monte Carlo integration**, by contrast:

* Samples according to $p(x)$
* Focuses computation in **high-probability** regions

> Monte Carlo's strength is its probabilistic perspective: sampling with importance weights. It scales well in high dimensions.

---

## 📘 Examples

### ∆ Example 1: Change of Variables the Monte Carlo Way

$$
y = f(x), \quad x \sim \text{Uniform}(-1, 1), \quad y = x^2
$$

Approximate $p(y)$ by drawing many samples $x_s \sim p(x)$, then compute $y_s = x_s^2$ and build a histogram.

### 🎤 Example 2: Estimating $\pi$ via Monte Carlo Integration

Function definition:

$$
f(x, y) = \begin{cases}
1 & \text{if } x^2 + y^2 \leq r^2 \\
0 & \text{otherwise}
\end{cases}
$$

We define:

$$
A = \int_{-r}^{r} \int_{-r}^{r} \mathbb{I}(x^2 + y^2 \leq r^2) \, dx \, dy
$$

Let $p(x) = p(y) = \frac{1}{2r} \Rightarrow p(x)p(y) = \frac{1}{4r^2}$

**Monte Carlo Integral:**

$$
A = (2r)^2 \iint f(x, y) p(x)p(y) \, dx \, dy \approx 4r^2 \cdot \frac{1}{S} \sum_{s=1}^S f(x_s, y_s)
$$

And finally:

$$
\pi \approx 4 \cdot \left( \frac{\mathrm{points\ inside\ circle}}{\mathrm{total\ samples}} \right)
$$

**Figures:**

![pi\_estimate\_convergence](https://github.com/Henry8r8w/machine-learning/blob/main/codes/monte%20carlo/outputs/processed/pi_estimate_convergence.png)

![codes/monte carlo/outputs/processed/rain_drop_plot.png](https://github.com/Henry8r8w/machine-learning/blob/main/codes/monte%20carlo/outputs/processed/rain_drop_plot.png)

---

### Example 3: Monte Carlo Accuracy (CLT Perspective)

If $\hat{\mu} = \frac{1}{S} \sum f(x_s)$, then:

$$
(\hat{\mu} - \mu) \sim \mathcal{N}\left(0, \frac{\sigma^2}{S}\right)
$$

Where:

$$
\sigma^2 = \mathbb{E}[f(X)^2] - \mathbb{E}[f(X)]^2 \approx \frac{1}{S} \sum_{s=1}^{S} (f(x_s) - \hat{\mu})^2
$$

And the 95% confidence interval is:

$$
P\left( \mu - 1.96 \cdot \frac{\hat{\sigma}}{\sqrt{S}} \leq \hat{\mu} \leq \mu + 1.96 \cdot \frac{\hat{\sigma}}{\sqrt{S}} \right) \approx 0.95
$$

---

## Reference

\[1] K. P. Murphy, *Probabilistic Machine Learning: An Introduction*, MIT Press, 2023


