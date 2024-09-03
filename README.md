# roots_finding


Multidimensional root-finding algorithms are methods used to find the roots of a system of nonlinear equations in multiple dimensions. Given a system of n nonlinear equations with n unknowns, the goal is to find a vector x such that:
f(x) = 0
Where f(x) is a vector-valued function:
f(x) = [f_1(x_1, x_2, ..., x_n), f_2(x_1, x_2, ..., x_n), ..., f_n(x_1, x_2, ..., x_n)]
Here, x = [x_1, x_2, ..., x_n] is the vector of unknowns.


1. Newton's Method for Multidimensional Systems
Newton's method is an iterative approach for solving systems of nonlinear equations. It is a generalization of the Newton-Raphson method for scalar equations to multiple dimensions.

Jacobian Matrix: Compute the Jacobian matrix J_f(x) of the system, which contains all the first partial derivatives of the functions with respect to the unknowns:
J_f(x) = [∂f_1/∂x_1   ∂f_1/∂x_2  ...  ∂f_1/∂x_n]
         [∂f_2/∂x_1   ∂f_2/∂x_2  ...  ∂f_2/∂x_n]
         [ ...          ...           ...     ]
         [∂f_n/∂x_1   ∂f_n/∂x_2  ...  ∂f_n/∂x_n]
         
Iterative Update: Starting from an initial guess x_0, update the guess using:
x_(k+1) = x_k - J_f(x_k)^(-1) * f(x_k)
Where J_f(x_k)^(-1) is the inverse of the Jacobian matrix evaluated at x_k.

Convergence: Repeat the process until the change in x between iterations is smaller than a specified tolerance:
||x_(k+1) - x_k|| < tol
If the method converges, x_(k+1) will be the root of the system.

Pros:
Fast convergence, especially when the initial guess is close to the root.
High accuracy.

Cons:
Requires computation of the Jacobian matrix, which can be complex and computationally expensive for large systems.
Can fail if the Jacobian is singular or near-singular.


2. Broyden's Method
Broyden's method is a quasi-Newton method that approximates the Jacobian matrix and updates it iteratively, rather than computing it explicitly at each step.

Initial Approximation: Start with an initial guess x_0 and an initial approximation to the Jacobian matrix, often taken as the identity matrix B_0.

Iterative Update: At each iteration, update the guess using:
x_(k+1) = x_k - B_k^(-1) * f(x_k)
Where B_k is the approximation of the Jacobian matrix at iteration k.

Jacobian Update: Instead of recalculating the Jacobian, update B_k using the Broyden rank-1 update formula:
B_(k+1) = B_k + (y_k - B_k * delta_x_k) * delta_x_k^T / (delta_x_k^T * delta_x_k)
Where:
y_k = f(x_(k+1)) - f(x_k)
delta_x_k = x_(k+1) - x_k
Convergence: Similar to Newton's method, the process continues until the change in x is below a certain tolerance.

Pros:
Avoids explicit computation of the Jacobian, which can be advantageous for large systems.
Efficient when the Jacobian is expensive to compute.

Cons:
May converge slower than Newton's method.
Requires good initial guess and careful handling of the Jacobian approximation.
