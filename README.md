# Library-for-VI-problems

This is a library of variational inequality problems. Implemented are two commonly used problem classes; matrix games and constrained optimization.

## Getting Started

The library is relatively easy to setup as long as the prerequistes are all installed. There are two .ipynb files that exist to demonstrate importing, creating the problem and using the solvers from "solvers.py" to create graphs. One is for constrained optimization the other for matrix games. If the usage of certain functions is not clear the description is easily available by typing '?' before the function name, such as for example for "mg_problem":
```
? mg_problem
```

### Prerequisites

To run the library there are a few packages that need to be downloaded:
- [numpy](https://numpy.org/install/) 
- [scipy](https://scipy.org/install.html) 
- [autograd](https://github.com/HIPS/autograd) 
- [pytables](https://www.pytables.org/usersguide/installation.html) 
- [networkx](https://networkx.github.io/documentation/stable/install.html) 
- [matplotlib](https://matplotlib.org/users/installing.html) 

### Importing

To import the matrix games problem:
```
from vilib.matrix_games.base import mg_problem
```
for certain other functions of the matrix games problem:
```
from vilib.matrix_games.generate import*
```

To import the constrained optimization problem:
```
from vilib.constrained_optimization.base import co_problem
```
to create QCQP problems call:
```
from vilib.constrained_optimization.generate import*
```

## Example
### Matrix Games
```
dimN = 30
dimM = 30
proximal_name = "simplex"

prob = mg_problem("rand", proximal_name, (dimN, dimM), "plusuniform")
F_mg, J_mg, prox_g_mg = prob.get_parameters()
```
### Constrained Optimization (QCQP)
```
dimX = 20
dimY = 5
dimU = 0
proj = get_projector("simplex")

q0, p, q, r, A, b = randQCQP(dimX,dimY, proj,True,"uniform", False, dimU)
fx, hx, gradf, gradh, hx_opt = toQCQP(p, q, r)
prob = co_problem(fx, (dimX, dimY), hx_opt, proj, gradf, gradh, True, A, b)

x = np.ones(dimX+dimY+dimU)
F_co, J_co, prox_co = prob.get_parameters(False)
```
