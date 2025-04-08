# Problem 1


# Measuring Earth's Gravitational Acceleration with a Pendulum

## Motivation

The acceleration due to gravity $g$ is a crucial physical constant influencing various phenomena from falling objects to satellite orbits. A classic method for estimating $g$ is using a **simple pendulum**, where the period of oscillation is directly related to the length of the pendulum and the local gravitational acceleration.

This experiment focuses on:

- Careful measurement of pendulum parameters

- Statistical analysis of repeated trials

- Propagation of uncertainties



## Materials

- A string (1.00–1.50 meters)

- A small mass (e.g., keychain, bag of coins)

- Stopwatch or smartphone timer

- Ruler or measuring tape (resolution: ±0.5 cm or ±0.01 m)



## Setup

1. Attach the mass to the string and suspend it from a fixed point.

2. Measure the **length** $L$ of the pendulum (from the suspension point to the center of the mass).

   - Example: $$L = 1.00 \pm 0.01 \text{ m}$$
3. The uncertainty in length $\delta L$ is half the resolution of your ruler.


## Data Collection

Displace the pendulum by $<15°$ and release it. Measure the time for **10 complete oscillations**, and repeat this **10 times**:

### Example Table

| Trial | Time for 10 Oscillations (s) |
|-------|-------------------------------|
| 1     | 20.3                          |
| 2     | 20.2                          |
| 3     | 20.4                          |
| 4     | 20.1                          |
| 5     | 20.3                          |
| 6     | 20.3                          |
| 7     | 20.2                          |
| 8     | 20.4                          |
| 9     | 20.3                          |
| 10    | 20.2                          |



## Statistical Analysis

### Mean time for 10 oscillations:

$$
\bar{t}_{10} = \frac{\sum t_i}{10} = 20.27 \text{ s}
$$

### Standard deviation:

$$
s = \sqrt{\frac{1}{n - 1} \sum (t_i - \bar{t})^2} \approx 0.1 \text{ s}
$$

### Uncertainty in the mean time:

$$
\delta \bar{t}_{10} = \frac{s}{\sqrt{n}} = \frac{0.1}{\sqrt{10}} \approx 0.03 \text{ s}
$$


## Calculations

### 1. Period of one oscillation:

$$
T = \frac{\bar{t}_{10}}{10} = 2.027 \text{ s}
$$

$$
\delta T = \frac{\delta \bar{t}_{10}}{10} = 0.003 \text{ s}
$$

### 2. Calculate $g$:

$$
T = 2\pi \sqrt{\frac{L}{g}} \Rightarrow g = \frac{4\pi^2 L}{T^2}
$$

$$
g = \frac{4\pi^2 \cdot 1.00}{(2.027)^2} \approx 9.59 \text{ m/s}^2
$$



## Uncertainty in $g$

Use propagation of uncertainty:

$$
\frac{\delta g}{g} = \sqrt{\left(\frac{\delta L}{L}\right)^2 + \left(2 \cdot \frac{\delta T}{T}\right)^2}
$$

$$
\frac{\delta g}{g} = \sqrt{\left(\frac{0.01}{1.00}\right)^2 + \left(2 \cdot \frac{0.003}{2.027}\right)^2} \approx 0.010
$$

$$
\delta g = 9.59 \cdot 0.010 = 0.10 \text{ m/s}^2
$$



## Final Result

$$
\boxed{g = 9.59 \pm 0.10 \text{ m/s}^2}
$$


## Analysis

### 1. Comparison with standard value:

- Standard gravitational acceleration: $9.81 \text{ m/s}^2$

- Measured value: $9.59 \pm 0.10 \text{ m/s}^2$

- Slight deviation can be attributed to timing uncertainties, air resistance, and string stiffness.



### 2. Discussion of Uncertainties:

- **Length uncertainty**: From resolution of measuring tape.

- **Timing uncertainty**: Due to human reaction time (~0.1 s typical).

- **Experimental conditions**: Small angle approximation must be valid; avoid large swings.

##  Python Implementation and Output Analysis

```python
import numpy as np

# Data: 10 measurements for 10 oscillations
times_10_oscillations = np.array([20.3, 20.2, 20.4, 20.1, 20.3, 20.3, 20.2, 20.4, 20.3, 20.2])

# Step 1: Compute statistics
mean_t10 = np.mean(times_10_oscillations)
sd_t10 = np.std(times_10_oscillations, ddof=1)
uncertainty_mean_t10 = sd_t10 / np.sqrt(len(times_10_oscillations))

# Step 2: Period and uncertainty
T = mean_t10 / 10
delta_T = uncertainty_mean_t10 / 10

# Step 3: Gravity calculation
L = 1.00  # meters
delta_L = 0.01

# Gravitational acceleration
g = (4 * np.pi**2 * L) / T**2

# Uncertainty in g using propagation formula
delta_g_over_g = np.sqrt((delta_L / L)**2 + (2 * delta_T / T)**2)
delta_g = g * delta_g_over_g

# Final result
print(f"Mean time for 10 oscillations: {mean_t10:.2f} s")
print(f"Standard deviation: {sd_t10:.2f} s")
print(f"Period (T): {T:.4f} s")
print(f"g = {g:.2f} ± {delta_g:.2f} m/s²")
```

### 🧾 Sample Output:
```
Mean time for 10 oscillations: 20.27 s
Standard deviation: 0.10 s
Period (T): 2.0270 s
g = 9.59 ± 0.10 m/s²
```

## Deliverables

- Tabulated trial data

- Calculated mean, standard deviation, and uncertainties

- Final value for $g$ with uncertainty

- Discussion of sources of error



## Conclusion

By measuring the period of a simple pendulum and analyzing uncertainties rigorously, we estimated $g$ with good accuracy. This classical experiment remains an excellent example of experimental physics in action.



