# Results and Discussions
Through the Floquet theorem, to yield a periodical self-consistent solution of $\ M_z(t)$, the wavefunction should only consist of one Floquet mode. This is because a linear combined wavefunction with different quasienergies would produce a phase factor that annihilates the periodicity of the magnetization. Having this property, we first choose the smallest positive quasienergy and the result we obtained from the numerical iteration displays a damping of the average $\ M_z(t)$ over one period $\ \bar{M_z}$ with increasing $\ B_x$ as shown below.

<p align = "center">
  <img width="300" alt="image" src="https://user-images.githubusercontent.com/103773281/209478863-95d28fa2-d82e-40df-bd22-52747a46db9a.png">
  <img width="350" alt="image" src="https://user-images.githubusercontent.com/103773281/209478979-8e544ba3-3605-4d7a-ae42-c81f2887842f.png">


</p>

## Regarding Initial Guess
We only use $\ M_z(t) = 1$ as the initial guess due to its average expected energy to have the lowest value out of many initial guess. The following shows the graph of The Average Expectation Value of the Energy vs $\ B_x$ with different initial guesses of $\ M_z(t)$

<p align="center">
  
  <img width="400" alt="image" src="https://user-images.githubusercontent.com/103773281/209558372-6f72ae95-141a-4d5b-9aa8-c9fe8bfa9620.png">
  <img width="400" alt="image" src="https://user-images.githubusercontent.com/103773281/209496522-c288a0ce-3e37-4332-a82c-bc669f2f9964.png">
  
  </p>
  
More than the picture above, I also used many other initial guess where the amplitude of the $\ z$-axis magnetization must equal to 1 for physical reasons. Moreover, we use the previous iteration solution as the initial guess for the next $\ B_x$ that we want to study. For more details of how I performed the numerical iteration, it could be seen on the [README.md](https://github.com/alexinthewonderland/transverse-ising-model/blob/main/README.md) file at the very front under the "Iteration Method" part.


## Solving the Floquet Hamiltonian (Old Algorithm)
The following is the plot of the average magnetization in all three axis direction $\(\bar{M_x}, \bar{M_y}, \bar{M_z})$ which is obtained by solving the Floquet Hamiltonian as seen by the method used in the [Floquet Hamiltonian Python file](https://github.com/alexinthewonderland/transverse-ising-model/blob/main/Floquet%20Hamiltonian%20Method%20(Old%20Algorithm).ipynb)

<p align="center">
<img width="249" alt="image" src="https://user-images.githubusercontent.com/103773281/209479197-97a73587-9fe8-44f1-aee8-a641020c71db.png">
  </p>

## Integrating the time-evolution operator using QuTiP (New Algorithm)

<p align="center">
  
<img width="400" alt="image" src="https://user-images.githubusercontent.com/103773281/209568783-833c6fe0-fdd3-42b2-9dd7-b926263d8388.png">
  
  </p>

## Old VS New Algorithm
The following is the comparison of the $\ \bar{M_z}$ VS $\ B_x$ plot obtained by the two methods explained previously 

<p align="center">
  
<img width="252" alt="image" src="https://user-images.githubusercontent.com/103773281/209575808-36148f16-35d0-45dd-806d-a8bc9fdb9157.png">

  </p>

## Bloch Sphere Visualization
Due to the difficulty of imagining how the magnetization changes with time and also how different $\ B_x$ affects the system, I tried to track the path that the magnetization vector (here being $\ <\bar{M_x}, \bar{M_y}, \bar{M_z}>$ in a unit sphere which we call as the Bloch sphere.

## Winding Numbers
To classify one of the properties of each path (different $\ B_x$), 







