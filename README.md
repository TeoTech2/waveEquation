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

### Initial Conditions

The notebook implements a **Gaussian initial displacement**:

$$u(x, y, 0) = A \exp\left(-\frac{(x-x_0)^2 + (y-y_0)^2}{2\sigma^2}\right)$$

where:
- $A$ is the amplitude
- $(x_0, y_0)$ is the center position
- $\sigma$ is the standard deviation (width)

Initial velocity is typically set to zero:
$$\frac{\partial u}{\partial t}(x, y, 0) = 0$$

## License

MIT License - Feel free to use and modify for your research and applications.

## Contributing

Contributions are welcome! Please feel free to submit pull requests or open issues for bugs and feature requests.

## Author

Numerical solution implementation for the 2D Euler-Bernoulli biharmonic wave equation.

---

**Note**: This README provides a comprehensive mathematical and implementation overview. Refer to the Jupyter notebook for the complete working code and detailed examples.
