How does one implement the Finite Elements Method for solving the wave equation and biharmonic equation numerically?

# Biharmonic Wave Equation in Mathematica

A numerical solution for the biharmonic wave equation using finite difference methods in Mathematica.

## Overview

This notebook solves the Biharmonic wave equation, which models the vibration of thin plates and beams. The biharmonic equation is a fourth-order partial differential equation. 

## Mathematical Formulation

We guess that the solution $U(x,y)$ is a sum of basis functions:


$$U = \sum_{i,j} U_{i,j} N_{i,j} \tag{Sum of Basis Functions} $$

Given the wave equation, we isolate the term $\nabla^2 U = -F$. Integrating both sides against basis functions $\nu = N_{i,j}$, we find

$$\left( \sum_{k,l} \int_{[0,1]\times[0,1]} \nabla N_{i,j} \cdot \nabla N_{k,l} dA \right) U_{k,l} = - \int_{[0,1]\times[0,1]} F(x,y) N_{i,j} dA$$

We integrate and solve for $U_{i,j}$, and time propagate using the \emph{Finite Difference Method} for $\frac{\partial^2}{\partial t^2}$.

$$N_{i,j}(x,y) = N_{i}(x) N_{j}(y) \qquad N_j(x)= \begin{cases} \dfrac{x - x_{j-1}}{x_j - x_{j-1}}, & x_{j-1} \le x \le x_j, \\[8pt] \dfrac{x_{j+1} - x}{x_{j+1} - x_j}, & x_j \le x \le x_{j+1}, \\[8pt] 0, & \text{otherwise.} \end{cases}$$

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

<img width="379" height="253" alt="Screenshot 2025-11-19 at 11 58 28" src="https://github.com/user-attachments/assets/25987de4-ec21-4560-9605-3458674c0ef6" />

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

### Initial Conditions

The notebook implements a **Gaussian initial displacement**:

Initial velocity is typically set to zero:
$$\frac{\partial u}{\partial t}(x, y, 0) = 0$$


https://github.com/user-attachments/assets/c514439c-c701-4b79-bc67-cf36bcbfc111


https://github.com/user-attachments/assets/9e61a308-4774-4dd7-9bae-064bbfb1f766


https://github.com/user-attachments/assets/5837cf40-9c15-414c-b5f2-cb96bbb94266


## License

MIT License - Feel free to use and modify for your research and applications.

## Contributing

Contributions are welcome! Please feel free to submit pull requests or open issues for bugs and feature requests.

## Author

Numerical solution implementation for the 2D Euler-Bernoulli biharmonic wave equation.

---

**Note**: This README provides a comprehensive mathematical and implementation overview. Refer to the Jupyter notebook for the complete working code and detailed examples.
