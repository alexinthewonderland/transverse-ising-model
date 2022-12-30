Sorry, still under construction!
# Results and Discussions

## Static Transverse Field 
The following is the result when the Transverse Ising Model is applied by a static field instead of an oscillating one.

<p align = "center">
  <img width="300" alt="image" src="https://user-images.githubusercontent.com/103773281/209478863-95d28fa2-d82e-40df-bd22-52747a46db9a.png">
  <img width="300" alt="image" src="https://user-images.githubusercontent.com/103773281/210075963-3a8dfb40-0884-4600-a806-d806eea0a5ad.png">
    
  <p align = "center">
  <strong>Figure 1.</strong> The plot of $\ M_z$ VS $\ B_x$ <strong>(Left)</strong> and the plot of $\ M_x$ VS $\ B_x$ when the field applied is time-dependent or dynamic <strong>(Right)</strong> when the field applied is time-independent or static.
  </p>
  

</p>

We see that when $\ \frac{B_x}{qJ} = 1$ the magnetization in the $\ z$ -axis direction gets annihilated and stays $\ M_z=0$ with larger values of $\ \frac{B_x}{qJ}$. On the other hand, for the magnetization in the $\ x$ -axis increases linearly until $\ \frac{B_x}{qJ} = 1$ where $\ M_x$ reaches the value of 1 and stays at the same value when $\ \frac{B_x}{qJ}$ gets bigger than 1. In the next part, we would now explore the result where the transverse field is now dynamic.


## Oscillating Transverse Field
Before any numerical calculations, it is importantly noted that through the Floquet theorem, to yield a periodical self-consistent solution of $\ M_z(t)$, the wavefunction should only consist of one Floquet mode. This is because a linear combined wavefunction with different quasienergies would produce a phase factor that annihilates the periodicity of the magnetization. 

### Regarding Initial Guess
It is observed that $\ M_z(t) = 1$ as the initial guess has the lowest average expected energy from other initial guesses as shown in the figure below. The following graph shows The Average Expectation Value of the Energy vs $\ B_x$ with different initial guesses of $\ M_z(t)$

<p align="center">
  
  <img width="400" alt="image" src="https://user-images.githubusercontent.com/103773281/209558372-6f72ae95-141a-4d5b-9aa8-c9fe8bfa9620.png">
  <img width="400" alt="image" src="https://user-images.githubusercontent.com/103773281/209496522-c288a0ce-3e37-4332-a82c-bc669f2f9964.png">
  
  </p>
  
Extending from the picture above, I also used many other initial guess where the amplitude of the $\ z$-axis magnetization must equal to 1 for physical reasons. During the numerical iterations, we further use the previous iteration solution as the initial guess for the next $\ B_x$ that we want to study. For more details of how I performed the numerical iteration, it could be seen on the [README.md](https://github.com/alexinthewonderland/transverse-ising-model/blob/main/README.md) file at the very front under the "Iteration Method" part.

Having this in mind, there are now two methods that is used in solving this problem. I call the **Old Algorithm** to be the method finds the solution through the infinitely large dimension Floquet Hamiltonian, while the **New Algorithm** to be the method where the time evolution operator is instead numerically integrated using the Python library for quantum dynamics, namely [QuTiP](https://qutip.org/docs/4.1/guide/dynamics/dynamics-floquet.html).


### Solving the Floquet Hamiltonian (Old Algorithm)
The following is the plot of the average magnetization in all three axis direction $\(\bar{M_x}, \bar{M_y}, \bar{M_z})$ which is obtained by solving the Floquet Hamiltonian as seen by the method used in the [Floquet Hamiltonian Python file](https://github.com/alexinthewonderland/transverse-ising-model/blob/main/Floquet%20Hamiltonian%20Method%20(Old%20Algorithm).ipynb)

<p align="center">
<img width="249" alt="image" src="https://user-images.githubusercontent.com/103773281/209479197-97a73587-9fe8-44f1-aee8-a641020c71db.png">
  </p>

### Integrating the time-evolution operator using QuTiP (New Algorithm)

<p align="center">
  
<img width="400" alt="image" src="https://user-images.githubusercontent.com/103773281/209568783-833c6fe0-fdd3-42b2-9dd7-b926263d8388.png">
  
  </p>

### Old VS New Algorithm
The following is the comparison of the $\ \bar{M_z}$ VS $\ B_x$ plot obtained by the two methods explained previously 

<p align="center">
  
<img width="252" alt="image" src="https://user-images.githubusercontent.com/103773281/209575808-36148f16-35d0-45dd-806d-a8bc9fdb9157.png">

  </p>
  
We could see that both algorithms yield a damping characteristics as we increase the value of $\ B_x$ into larger and larger value, however, the plot are not exactly the same.

Having this property, we first choose the smallest positive quasienergy, and the result we obtained from the numerical iteration displays a **damping** of the average $\ M_z(t)$ over one period $\ \bar{M_z}$ with increasing $\ B_x$ as shown below.

<p align="center">

<img width="350" alt="image" src="https://user-images.githubusercontent.com/103773281/209478979-8e544ba3-3605-4d7a-ae42-c81f2887842f.png">

</p>

From here onwards, we would use the New Algorithm which numerically integrates the time-evolution operator to find the self-consistent solution of the magnetizations. This is achieved through the library in Python called [QuTiP](https://qutip.org/docs/4.1/guide/dynamics/dynamics-floquet.html). This is because the fact that 

### Total Magnetization
<p align="center">
  
  <img width="500" alt="image" src="https://user-images.githubusercontent.com/103773281/209577905-663cd1b6-f33c-43cb-a263-13f5bf24cc67.png">
  <img width="333" alt="image" src="https://user-images.githubusercontent.com/103773281/209579961-fb369145-f3c2-4d39-813f-359a35d1be29.png">

</p>


### Bloch Sphere Visualization
Due to the difficulty of imagining how the magnetization changes with time and also how different $\ B_x$ affects the system, I tried to track the path that the magnetization vector (here being $\ <\bar{M_x}, \bar{M_y}, \bar{M_z}>$ in a unit sphere which we call as the Bloch sphere.

<p align="center">
![DDC8C45F-43EB-4D95-A0A2-D01A9949EA30_1_102_o](https://user-images.githubusercontent.com/103773281/209582578-5fb9b0c9-58fa-43e2-b1cb-d16c191cd539.jpeg)
 </p>


### Winding Numbers
To classify one of the properties of each path (different $\ B_x$), we use the following definition of the winding numbers explained in this [wikipedia](https://en.wikipedia.org/wiki/Winding_number) (for details could be seen in the frontpage [README.md](https://github.com/alexinthewonderland/transverse-ising-model/blob/main/README.md) file.

From the simulations, it is observed that for all cases 









