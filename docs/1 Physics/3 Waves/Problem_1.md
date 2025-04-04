# Problem 1
# Interference Patterns on a Water Surface

## Introduction
This report focuses on the interference of surface water waves originating from multiple coherent point sources. These sources are placed at the vertices of a regular polygon, ensuring symmetrical spacing and uniform conditions for wave propagation. 

The primary objective is to analyze how the superposition of such waves forms complex interference patterns, and to understand the role of geometrical arrangements and wave parameters in shaping these patterns.

The simulation is developed in Python using numerical techniques and graphical visualization. By plotting the resultant displacement of the water surface, we can clearly distinguish between areas of constructive and destructive interference and study their symmetry.

### Geometrical Configuration of Sources

```python
import matplotlib.pyplot as plt
import numpy as np

n_sources = 4
radius = 2
angles = np.linspace(0, 2*np.pi, n_sources, endpoint=False)
x_coords = radius * np.cos(angles)
y_coords = radius * np.sin(angles)

fig, ax = plt.subplots(figsize=(6,6))
ax.scatter(x_coords, y_coords, color='red', label='Sources')
for i, (x, y) in enumerate(zip(x_coords, y_coords)):
    ax.text(x + 0.1, y + 0.1, f"S{i+1}", fontsize=12)

circle = plt.Circle((0, 0), radius, color='blue', fill=False, linestyle='--', alpha=0.5)
ax.add_patch(circle)
ax.set_xlim(-3, 3)
ax.set_ylim(-3, 3)
ax.set_aspect('equal')
ax.grid(True)
ax.legend()
plt.title('Wave Sources Positioned on a Square')
plt.show()
```
![wave-sources-positioned-on-a-square](Unknown-3.png)

- All sources are coherent and monochromatic (same wavelength, frequency, and amplitude).

- Waves propagate as circular wavefronts from each source.

- The water surface displacement is calculated using the principle of linear superposition.

- Simulation is conducted in 2D space on a uniform grid.

## Mathematical Background
The displacement $u\vec{r}$, t at position $\vec{r}$ and time $t$ due to a single wave source at position $\vec{r}_0$ is given by:

$$u(\vec{r}, t) = A \sin(k|\vec{r} - \vec{r}_0| - \omega t + \phi)$$

Where:
- $A$: Amplitude of the wave

- $k = \frac{2\pi}{\lambda}$: Wave number, $\lambda$ is the wavelength

- $\omega = 2\pi f$: Angular frequency, $f$ is the frequency

- $\phi$: Initial phase

- $|\vec{r} - \vec{r}_0|$: Distance from the source to point $\vec{r}$

The total displacement from multiple sources is:

$$u_{total}(\vec{r}, t) = \sum_{i=1}^{N} A \sin(k|\vec{r} - \vec{r}_i| - \omega t + \phi)$$

Where $N$ is the number of sources.

## Implementation in Python

### Imports
```python
import numpy as np
import matplotlib.pyplot as plt
```

### Parameters
```python
A = 1.0                # Amplitude
wavelength = 2.0       # Wavelength (lambda)
k = 2 * np.pi / wavelength  # Wave number
f = 1.0                # Frequency
omega = 2 * np.pi * f      # Angular frequency
phi = 0.0              # Initial phase
```

### Simulation Grid
```python
x = np.linspace(-5, 5, 500)
y = np.linspace(-5, 5, 500)
X, Y = np.meshgrid(x, y)
t = 0  # Time snapshot (can vary this for animation)
```

### Polygon Source Placement
```python
n_sources = 4  # Change to 3, 5, etc. for other polygons
radius = 2.0  # Distance from center to each source
angles = np.linspace(0, 2 * np.pi, n_sources, endpoint=False)
sources = [(radius * np.cos(a), radius * np.sin(a)) for a in angles]
```

### Superposition of Waves
```python
Z_total = np.zeros_like(X)
for (x0, y0) in sources:
    r = np.sqrt((X - x0)**2 + (Y - y0)**2)
    Z = A * np.sin(k * r - omega * t + phi)
    Z_total += Z
```

### Visualization of Interference Pattern
```python
plt.figure(figsize=(10, 8))
plt.contourf(X, Y, Z_total, levels=200, cmap='RdBu')
plt.colorbar(label='Displacement')
plt.title(f'Interference Pattern from {n_sources}-Sided Polygon Configuration')
plt.xlabel('x position')
plt.ylabel('y position')
plt.axis('equal')
plt.grid(True, linestyle='--', alpha=0.5)
plt.show()
```

![interference-pattern](Unknown-4.png)

## Observations and Analysis
- **Constructive Interference:** Occurs where wave peaks align, resulting in higher displacement amplitudes. These appear as bright or dark concentric lines in the plot.

- **Destructive Interference:** Occurs where a wave peak meets a trough from another wave, canceling each other out. These regions appear as transition zones.

- **Symmetry and Pattern:** The interference pattern reflects the geometric symmetry of the polygon. A square shows fourfold rotational symmetry.

## Possible Extensions
- Animate the wave pattern over time by varying `t`

- Use other polygons (triangle, pentagon, hexagon) and compare their patterns

- Change phase differences between sources for more complex interactions

- Add damping or nonlinear effects for more realism

## Conclusion
This simulation effectively visualizes how waves from multiple sources interact on a water surface. By leveraging symmetry and wave superposition, we gain a clearer understanding of the principles of interference and the beauty of wave physics in two dimensions.
