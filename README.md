# 2D Euler-Bernoulli Biharmonic Wave Equation Solver

A numerical solution for the biharmonic wave equation using finite difference methods in Python.

## Overview

This notebook solves the **2D Euler-Bernoulli biharmonic wave equation**, which models the vibration of thin plates and beams. The biharmonic equation is a fourth-order partial differential equation that appears in elasticity theory and structural mechanics.

## Mathematical Formulation

### The Biharmonic Wave Equation

The equation we solve is:

$$\frac{\partial^2 u}{\partial t^2} + \nabla^4 u = 0$$

where:
- $u(x, y, t)$ is the displacement field
- $\nabla^4$ is the biharmonic operator (Laplacian of the Laplacian)
- $t$ is time

In 2D Cartesian coordinates, the biharmonic operator is:

$$\nabla^4 u = \frac{\partial^4 u}{\partial x^4} + 2\frac{\partial^4 u}{\partial x^2 \partial y^2} + \frac{\partial^4 u}{\partial y^4}$$

### Physical Interpretation

This equation describes:
- Vibrations of thin elastic plates
- Beam deflections under dynamic loading
- Structural mechanics problems
- Microelectromechanical systems (MEMS)

The biharmonic operator accounts for bending stiffness, making this equation more physically realistic than the standard wave equation for thin structures.

## Numerical Method

### Discretization Scheme

The solution uses a **finite difference method** on a uniform grid:

**Spatial Grid:**
- Domain: $[0, L_x] \times [0, L_y]$
- Grid points: $N_x \times N_y$
- Spacing: $\Delta x$, $\Delta y$

**Temporal Discretization:**
- Time step: $\Delta t$
- Total time: $T$
- Number of steps: $N_t$

### Finite Difference Approximations

**Biharmonic Operator (4th order spatial derivatives):**

For the $x$-direction fourth derivative:
$$\frac{\partial^4 u}{\partial x^4} \approx \frac{u_{i-2,j} - 4u_{i-1,j} + 6u_{i,j} - 4u_{i+1,j} + u_{i+2,j}}{\Delta x^4}$$

For the mixed derivative:
$$\frac{\partial^4 u}{\partial x^2 \partial y^2} \approx \frac{1}{\Delta x^2 \Delta y^2}[u_{i-1,j-1} - 2u_{i-1,j} + u_{i-1,j+1} - 2u_{i,j-1} + 4u_{i,j} - 2u_{i,j+1} + u_{i+1,j-1} - 2u_{i+1,j} + u_{i+1,j+1}]$$

**Time Integration:**
Using a second-order central difference scheme:
$$\frac{\partial^2 u}{\partial t^2} \approx \frac{u^{n+1} - 2u^n + u^{n-1}}{\Delta t^2}$$

### Algorithm Structure

1. **Initialize** the spatial grid and time parameters
2. **Set initial conditions** for displacement $u(x,y,0)$ and velocity $\frac{\partial u}{\partial t}(x,y,0)$
3. **Apply boundary conditions** (typically clamped or simply supported)
4. **Time-stepping loop:**
   - Compute biharmonic operator on interior points
   - Update solution using finite difference scheme
   - Enforce boundary conditions
   - Advance to next time step
5. **Visualize** results at various time snapshots

## Implementation Details

### Parameters

```python
# Spatial domain
Lx, Ly = 1.0, 1.0          # Domain size
Nx, Ny = 50, 50            # Grid points

# Material properties
D = 1.0                     # Flexural rigidity

# Time parameters
dt = 0.001                  # Time step
T = 2.0                     # Total simulation time
```

### Initial Conditions

The notebook implements a **Gaussian initial displacement**:

$$u(x, y, 0) = A \exp\left(-\frac{(x-x_0)^2 + (y-y_0)^2}{2\sigma^2}\right)$$

where:
- $A$ is the amplitude
- $(x_0, y_0)$ is the center position
- $\sigma$ is the standard deviation (width)

Initial velocity is typically set to zero:
$$\frac{\partial u}{\partial t}(x, y, 0) = 0$$

### Boundary Conditions

The implementation supports:
- **Clamped boundaries**: $u = 0$ and $\frac{\partial u}{\partial n} = 0$
- **Simply supported**: $u = 0$ and $\nabla^2 u = 0$

## Features

- ✅ 2D biharmonic wave equation solver
- ✅ Flexible initial conditions
- ✅ Multiple boundary condition options
- ✅ Real-time visualization of wave propagation
- ✅ 3D surface plots and animations
- ✅ Energy conservation monitoring
- ✅ Stability analysis tools

## Usage

### Basic Example

```python
import numpy as np
import matplotlib.pyplot as plt

# Define parameters
Nx, Ny = 50, 50
Lx, Ly = 1.0, 1.0
dx = Lx / (Nx - 1)
dy = Ly / (Ny - 1)
dt = 0.001

# Initialize grid
x = np.linspace(0, Lx, Nx)
y = np.linspace(0, Ly, Ny)
X, Y = np.meshgrid(x, y)

# Set initial condition (Gaussian)
u = np.exp(-((X - 0.5)**2 + (Y - 0.5)**2) / 0.01)

# Run simulation
# (see notebook for complete implementation)
```

### Visualization

The notebook includes:
- 2D contour plots of the displacement field
- 3D surface plots showing the plate deflection
- Time evolution animations
- Cross-sectional views

## Results

The solver produces:
1. **Displacement field** $u(x, y, t)$ at each time step
2. **Wave propagation** visualization showing how disturbances travel through the plate
3. **Energy analysis** to verify conservation properties
4. **Frequency domain analysis** of the vibration modes

### Example Output

The simulation shows:
- Initial disturbance creates waves that propagate outward
- Reflections from boundaries create interference patterns
- Energy disperses throughout the domain
- System exhibits characteristic biharmonic behavior with dispersive wave propagation

## Stability Considerations

For numerical stability, the **CFL (Courant-Friedrichs-Lewy) condition** must be satisfied:

$$\Delta t \leq C \cdot \min(\Delta x^2, \Delta y^2)$$

where $C$ is a stability constant dependent on the discretization scheme.

## Applications

This solver can be applied to:
- **Structural Engineering**: Plate vibration analysis
- **MEMS Design**: Microstructure resonator modeling
- **Acoustics**: Sound radiation from plates
- **Material Science**: Dynamic response of thin films
- **Civil Engineering**: Floor vibration analysis

## Dependencies

```python
numpy          # Numerical computations
matplotlib     # Plotting and visualization
scipy          # Optional: for advanced numerical methods
```

## Installation

```bash
pip install numpy matplotlib scipy
```

## References

- Timoshenko, S., & Woinowsky-Krieger, S. (1959). *Theory of Plates and Shells*
- Reddy, J.N. (2006). *Theory and Analysis of Elastic Plates and Shells*
- LeVeque, R.J. (2007). *Finite Difference Methods for Ordinary and Partial Differential Equations*

## Mathematical Background

### Biharmonic Operator Properties

The biharmonic operator $\nabla^4$ has several important properties:

1. **Fourth-order elliptic operator**: Requires two boundary conditions on each boundary
2. **Self-adjoint**: Leads to symmetric coefficient matrices
3. **Positive definite**: Ensures stability of equilibrium solutions
4. **Dispersion relation**: $\omega^2 = k^4$ for plane waves

### Energy Functional

The total energy of the system is:

$$E(t) = \frac{1}{2}\int_\Omega \left[\left(\frac{\partial u}{\partial t}\right)^2 + (\nabla^2 u)^2\right] dA$$

This energy should be conserved in the absence of damping.

## Advanced Features

### Modal Analysis

The eigenvalue problem for the biharmonic operator:

$$\nabla^4 \phi_n = \lambda_n \phi_n$$

yields natural frequencies:

$$\omega_n = \sqrt{\lambda_n}$$

### Damping

To include damping, modify the equation:

$$\frac{\partial^2 u}{\partial t^2} + \gamma\frac{\partial u}{\partial t} + \nabla^4 u = 0$$

where $\gamma$ is the damping coefficient.

## License

MIT License - Feel free to use and modify for your research and applications.

## Contributing

Contributions are welcome! Please feel free to submit pull requests or open issues for bugs and feature requests.

## Author

Numerical solution implementation for the 2D Euler-Bernoulli biharmonic wave equation.

---

**Note**: This README provides a comprehensive mathematical and implementation overview. Refer to the Jupyter notebook for the complete working code and detailed examples.
