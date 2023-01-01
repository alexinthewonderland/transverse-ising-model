Sorry, still under construction!
# Results and Discussions

## Static Transverse Field 
The following is the result when the Transverse Ising Model is applied by a static field instead of an oscillating one.

<p align = "center">
  <img width="300" alt="image" src="https://user-images.githubusercontent.com/103773281/209478863-95d28fa2-d82e-40df-bd22-52747a46db9a.png">
  <img width="300" alt="image" src="https://user-images.githubusercontent.com/103773281/210075963-3a8dfb40-0884-4600-a806-d806eea0a5ad.png">
    
  <p align = "center">
  <strong>Figure 1.</strong> The plot of $\ M_z$ VS $\ \frac{\Omega}{qJ}$ <strong>(Left)</strong> and the plot of $\ M_x$ VS $\ \frac{\Omega}{qJ}$ when the field applied is time-dependent or dynamic <strong>(Right)</strong> when the field applied is time-independent or static.
  </p>
  

</p>

We see that when $\ \frac{\Omega}{qJ} = 1$ , where $\ \Omega$ is the ampltiude of the static field, the magnetization in the $\ z$ -axis direction gets annihilated and stays $\ M_z=0$ with larger values of $\ \frac{\Omega}{qJ}$. On the other hand, for the magnetization in the $\ x$ -axis increases linearly until $\ \frac{\Omega}{qJ} = 1$ where $\ M_x$ reaches the value of 1 and stays at the same value when $\ \frac{\Omega}{qJ}$ gets bigger than 1. In the next part, we would now explore the result where the transverse field is now dynamic.


## Oscillating Transverse Field
Before any numerical calculations, it is importantly noted that through the Floquet theorem, to yield a periodical self-consistent solution of $\ M_z(t)$, the wavefunction should only consist of one Floquet mode. This is because a linear combined wavefunction with different quasienergies would produce a phase factor that annihilates the periodicity of the magnetization. 

### Solving the Floquet Hamiltonian (Old Algorithm)
The following is the plot of the average magnetization in all three axis direction $\(\bar{M_x}, \bar{M_y}, \bar{M_z})$ which is obtained by solving the Floquet Hamiltonian used in the [Floquet Hamiltonian Python file](https://github.com/alexinthewonderland/transverse-ising-model/blob/main/Floquet%20Hamiltonian%20Method%20(Old%20Algorithm).ipynb) Here, we are solving for the very large (ideally infinite) Floquet Hamiltonian matrix and then reverse engineeing it to obtain the self consistent value of $\ M_z(t)$ and its average over one period $\ \bar{M_z}$

Having this property, we first choose the smallest positive quasienergy, and the result we obtained from the numerical iteration displays a **damping** of the average $\ M_z(t)$ over one period $\ \bar{M_z}$ with increasing $\ B_x$ as shown below.

<p align="center">

<img width="400" alt="image" src="https://user-images.githubusercontent.com/103773281/209478979-8e544ba3-3605-4d7a-ae42-c81f2887842f.png">

</p>

However, this method experiences a branching problem when trying to solve for the converging floquet modes and quasienergies solution. This motivates us to use another method explained in the following section.

### Integrating the time-evolution operator using QuTiP (New Algorithm)
In this new method, instead of solving the Floquet Hamiltonian, we numerically integrate the time-evolution operator by the help of the [QuTiP library](https://qutip.org/docs/4.1/guide/dynamics/dynamics-floquet.html). This lets us avoid the branching problem when doing the numerical iteration and also eliminate of our worry with the high frequency uncertainty results when using the Floquet Hamiltonian method. The following discusses further about how we choose the initial guess and also its results.

#### Regarding Initial Guess Choice
It is observed that $\ M_z(t) = 1$ as the initial guess has the lowest average expected energy from other initial guesses as shown in the figure below. The following graph shows The Average Expectation Value of the Energy vs $\ B_x$ with different initial guesses of $\ M_z(t)$

<p align="center">
  
  <img width="400" alt="image" src="https://user-images.githubusercontent.com/103773281/209558372-6f72ae95-141a-4d5b-9aa8-c9fe8bfa9620.png">
  <img width="400" alt="image" src="https://user-images.githubusercontent.com/103773281/209496522-c288a0ce-3e37-4332-a82c-bc669f2f9964.png">
  
  </p>
  
Extending from the picture above, I also used many other initial guess where the amplitude of the $\ z$-axis magnetization must equal to 1 for physical reasons and yield a higher average energy than $\ M_z(t)=1$ as the initial guess. During the numerical iterations, we further use the previous iteration solution as the initial guess for the next $\ B_x$ that we want to study. For more details of how I performed the numerical iteration, it could be seen on the [README.md](https://github.com/alexinthewonderland/transverse-ising-model/blob/main/README.md) file at the very front under the "Iteration Method" part.


#### New Algorithm Results
The following is the result of the average magnetization VS $\ B_x$ by using QuTiP

<p align="center">
  
<img width="400" alt="image" src="https://user-images.githubusercontent.com/103773281/209568783-833c6fe0-fdd3-42b2-9dd7-b926263d8388.png">
  
  </p>
 
From the above plot it could be observed that there are certain $\ B_x$ regime where only $\ \bar{M_z}$ is non-zero while $\ \bar{M_y}$ and \ \bar{M_x}$ is zero. There are also other regime where only $\ \bar{M_y}$ is non-zero while the other magnetization from the other axes are zero. In contrast, the value of $\ \bar{M_x}$ is always zero for all $\ B_x$ value.

 
We could also compare the previous (old) method $\ \bar{M_z}$ VS $\ B_x$ plot with the new algorithm as the following shows.

<p align="center">
  
<img width="400" alt="image" src="https://user-images.githubusercontent.com/103773281/209575808-36148f16-35d0-45dd-806d-a8bc9fdb9157.png">

  </p>
  
It could be seen that both algorithms does not give out the same exact plots, however, they both show a damping kind of characteristics for $\ \bar{M_z}$ when we increase the value of $\ B_x$. From here on, we would always use the new method due to its reliableness and robustness.


Furthermore, looking at the "amplitude" of the average magnetization also gives us interesting characteristics as the following shows.

<p align="center">
  
  <img width="400" alt="image" src="https://user-images.githubusercontent.com/103773281/209577905-663cd1b6-f33c-43cb-a263-13f5bf24cc67.png">

</p>

From the above plot, we hypothesize that the point where the amplitude of the average magnetization goes to zero indicates that the path as a functino of time of the average magnetization vector is a global path, meaning that it would cross a greater circle on the Bloch Sphere shown in the next section. Studying around this hypotheses would be one of our next big steps for the project.


#### Bloch Sphere Visualization
Due to the difficulty of imagining how the magnetization changes with time and also how different $\ B_x$ affects the system, I tried to track the path that the magnetization vector (here being $\ <\bar{M_x}, \bar{M_y}, \bar{M_z}>$ in a unit sphere which we call as the Bloch sphere.

<p align="center">

<img width="400" src="https://user-images.githubusercontent.com/103773281/210174076-1235e594-8e5e-4512-91df-276e5c038791.gif" />
<img width="400" src="https://user-images.githubusercontent.com/103773281/210174116-0a010988-28f2-4ff8-b0b1-fedfafb41303.gif" />
<img width="400" src="https://user-images.githubusercontent.com/103773281/210174102-f894a1ff-ea10-4395-98b4-5033e9b74905.gif" />
<img width="400" src="https://user-images.githubusercontent.com/103773281/210160073-d82f4c72-d0cf-4788-9f6a-d446da25408c.gif" />


<p align="center">
  A motion of the average magnetization vector inside of a Bloch sphere for when $\ B_x = 0.1$, $\ B_x = 2.0$, $\ B_x = 10.8$, and $\ B_x = 13.7$
</p>

 </p>

Here we only show a couple of the motion on the Bloch sphere for a few $\ B_x$ value since the motion itself might not be that useful to interpret (at least I don't have any idea currently). The real usefulness comes when we project the path to a 2D plane from one of the axes $\ (x, y, z)$ and try to calculate numerically the winding number of the projected path. This is what we will discuss in the next section.

#### Winding Numbers
To classify one of the properties of each path (different $\ B_x$), we use the following definition of the winding numbers explained in this [wikipedia](https://en.wikipedia.org/wiki/Winding_number) (for details could be seen in the frontpage [README.md](https://github.com/alexinthewonderland/transverse-ising-model/blob/main/README.md) file.

From the simulations, it is observed that the angle you project the path of the magnetization vs time in the bloch sphere determines whether the winding number is a unity or none (1 or 0). When a certain $\ B_x$ yields a none zero $\ \bar{M_z}$ then the winding the number projected from the $\ z$-axis equals to 1, while all the other projections yield a zero winding number. In contrast, when $\ \bar{M_y}$ dominates the average magnetization of the system, then the winding number projected from the $\ y$-axis is 1 while all the other projections gives us a zero winding number. A few of the result could be shown below with its projected path also visualized.





