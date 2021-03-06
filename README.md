# Split Stepo Fourier Method

This project is using SSFM implementation by: [Algorithm-Archive](https://github.com/algorithm-archivists/algorithm-archive) on Python 3.7.5 64bit

It adds initialization variables and a cool graphics for analyze different views

## Getting Started

You just need to copy the project to your machine for testing

### Prerequisites

Just type as following:

```
pip install numpy
pip install matplotlib
```

## Execution 

The default equation is 


<!-- $$
i\frac{\partial \psi}{\partial t}=-\frac{\partial^2 \psi}{\partial x^2}+0.5(x-x_0)^2
$$ --> 

<div align="center"><img src="https://render.githubusercontent.com/render/math?math=i%5Cfrac%7B%5Cpartial%20%5Cpsi%7D%7B%5Cpartial%20t%7D%3D-%5Cfrac%7B%5Cpartial%5E2%20%5Cpsi%7D%7B%5Cpartial%20x%5E2%7D%2B0.5(x-x_0)%5E2%0D"></div>

with initial condition:

<!-- $$
e^{-(x- x_0)^2/2}
$$ --> 

<div align="center"><img src="https://render.githubusercontent.com/render/math?math=e%5E%7B-(x-%20x_0)%5E2%2F2%7D%0D"></div>






### Equation changing

You can change equations by defining your Linear and nonlinear part
In this case:

#### Linear part
<!-- $$
L=-\frac{\partial^2 \psi}{\partial x^2}
$$ --> 

<div align="center"><img src="https://render.githubusercontent.com/render/math?math=L%3D-%5Cfrac%7B%5Cpartial%5E2%20%5Cpsi%7D%7B%5Cpartial%20x%5E2%7D%0D"></div>





And is located on this line, where $k^2$ is the fourier transformation of the derivative
```
opr.K = np.exp(-0.5 * (par.k ** 2) * par.dt * 1j)
```

If you want to compute:
<!-- $$
i\frac{\partial \psi}{\partial t} = -\frac{\partial^2 \psi}{\partial x^2}+\frac{\partial \psi}{\partial x} +0.5(x-x_0)^2
$$ --> 

<div align="center"><img src="https://render.githubusercontent.com/render/math?math=i%5Cfrac%7B%5Cpartial%20%5Cpsi%7D%7B%5Cpartial%20t%7D%20%3D%20-%5Cfrac%7B%5Cpartial%5E2%20%5Cpsi%7D%7B%5Cpartial%20x%5E2%7D%2B%5Cfrac%7B%5Cpartial%20%5Cpsi%7D%7B%5Cpartial%20x%7D%20%2B0.5(x-x_0)%5E2%0D"></div>





The new nonlinear part will be:
<!-- $$
L = -\frac{\partial^2 \psi}{\partial x^2} + \frac{\partial \psi}{\partial x}
$$ --> 

<div align="center"><img src="https://render.githubusercontent.com/render/math?math=L%20%3D%20-%5Cfrac%7B%5Cpartial%5E2%20%5Cpsi%7D%7B%5Cpartial%20x%5E2%7D%20%2B%20%5Cfrac%7B%5Cpartial%20%5Cpsi%7D%7B%5Cpartial%20x%7D%0D"></div>



And the changes must be like 

```
opr.K = np.exp(-0.5 * (par.k ** 2 - 1j*par.k) * par.dt * 1j)
```

#### Nonlinear Part

Nonlinear changes are of the form:
<!-- $$
N = 0.5(x-x_0)^2
$$ --> 

<div align="center"><img src="https://render.githubusercontent.com/render/math?math=N%20%3D%200.5(x-x_0)%5E2%0D"></div>


and its implementation is located on

```
opr.V = 0.5 * (par.x - voffset) ** 2
```

If you want to compute:
<!-- $$
i\frac{\partial \psi}{\partial t} = -\frac{\partial^2 \psi}{\partial x^2}+|\psi|^2
$$ --> 

<div align="center"><img src="https://render.githubusercontent.com/render/math?math=i%5Cfrac%7B%5Cpartial%20%5Cpsi%7D%7B%5Cpartial%20t%7D%20%3D%20-%5Cfrac%7B%5Cpartial%5E2%20%5Cpsi%7D%7B%5Cpartial%20x%5E2%7D%2B%7C%5Cpsi%7C%5E2%0D"></div>






you just need to change:

```
opr.V =   np.abs((opr.wfc)) ** 2
```

### Visualization

Two panel will show the solution allowing to see it on different perspectives

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details