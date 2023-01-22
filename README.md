# Driving the Transverse Ising Model with an Oscillating Field

This repository consists of the following things (Sorry if it is still a bit messy!):

* [old-algo.ipynb](https://github.com/alexinthewonderland/transverse-ising-model/blob/main/old-algo.ipynb) is a Jupyter Notebook file that contains the code to find the phase diagram of the transverse ising system, visualizing the dynamics on a Bloch sphere, and also calculating the winding number using the old algorithm which finds the self-consistent solution using the Floquet Hamiltonian.
* [qutip-algo.ipynb](https://github.com/alexinthewonderland/transverse-ising-model/blob/main/qutip-algo.ipynb). A Jupter Notebook file that is similar in usage as the [old-algo.ipynb](https://github.com/alexinthewonderland/transverse-ising-model/blob/main/old-algo.ipynb) but uses QuTiP to find the self-consistent solution for the phase diagram and other properties.
* [old-vs-qutip-algo.ipynb](https://github.com/alexinthewonderland/transverse-ising-model/blob/main/old-vs-qutip-algo.ipynb). This file combined the two above files into one file for comparison purposes of each algorithm's result.
* [Results]() folder. This folder contains the result that I obtained with its figures and videos from both the old and new algorithm. More details could be seen inside the folder.
* [project-presentation.pptx](https://github.com/alexinthewonderland/transverse-ising-model/blob/main/project-presentation.pptx). Since the README.md file is not perfect/complete yet, I uploaded a presentation that I gave around November last year to give some idea about the project if the description in this GitHub is confusing. Apologize for the inconvenience!


 ## Introduction
 
There is always a first time for everything. In this case, the Ising model is the first mathematical formalism that could be exactly solved to explain phase transitions in physical systems. It provides us with the Hamiltonian consisting of the spin interactions of the system, which encompasses properties such as ferromagnetism and the Curie temperature. Moving into the quantum realm, the spin terms become Pauli-matrices 
$\ S^{(x,z)}$
and the classical treatment of the Ising model hence does not apply. The system’s Hamiltonian
$\ H $ 
becomes an operator as the following shows,

<p align="center">
$\ \hat{H} = -qJ\sum_{\braket{ij}}S_i^zS_{j}^z - B(t) \sum_i S_i^x$
</p>

This is what we call as the Transverse Ising model, where J is the coupling term between the spins, B(t) represents the oscillating external magnetic field, and the notation
$\ \braket{ij}$
indicates a summation of the nearest-neighbor (NN) of the i-th spin site. This quantum model will enable us to explore the quantum phase transition (QPT) of system with different transverse field. In this case, we chose $\ B(t)$ to be $\ B_x\cos(\omega t)$ as the oscillating drive transverse field that affects the QPT. During the study, the following three properties of the transverse field would be tweaked and played around with the Amplitude $\ B_x$, frequency $\ \omega$, and the Polarization $\ \phi$. Our objective is then to see any phase transitions and symmetry breaking of the magnetization expectation values $\ M_z$, $\ M_x$, and $\ M_y$, as we play around with the three values mentioned above. To achieve this, the following methods and formalisms are used.

## Methods that I used
### Mean Field Theory
Due to the mathematical complication of the NN spin coupling summation, the Mean-Field theory (MFT) or approximation lets each spin to instead feel an average field that the nearest-neighbors spins produce. Hence, in our case, the nearest neighbor summation becomes a single site summation,

<p align="center">
$\ {\hat{H}}_{MF}=-qJM_z(t) {\Sigma_{i=1}^{N}} {\hat{S}}_i^z-B_x\cos{(\omega t)}\Sigma_{i=1}^{N}{\hat{S}}_i^x$
</p>

where $\ \hat{H_{MF}}$ is the mean field Hamiltonian and $\ qJM_z$ is our mean field with $\ q$ as the value of how many nearest neighbors the $\ i$-th has and $\ M_z(t)$ is the magnetization in the $\ z$-axis direction. The power of mean field approximation is seen above as it reduces a many-body problem into a two-level system with its approximation. The above mean-field Hamiltonian could be derived from the Gibbs-Bogoluibov Inequality, or you could take a different route using the variational principle.



### Floquet Formalism
Having a time-dependent but periodic Hamiltonian implies that the usual stationary state as an eigenvalue problem does not apply. This is where the Floquet formalism comes to the rescue. The Floquet formalism transforms the initial time-dependence from the coefficients to the eigenfunction in which they are periodical in time. The wavefunction could be written as a linear combination of the time-evolution operator eigenfunctions,


<p align = "center">          
$\ \ket{\psi (t)} = \sum_{j=1} \gamma_j\ \ket{\phi (t)}$
  </p>
         

Here, we invoke the Floquet theorem, in which we could write down $\ \ket{\phi_j (t)}$ as,

<p align="center">
$\ \ket{\phi_j (t)} = e^{-i\epsilon_j t} \ket{u_j(t)}$ 
with 
$\ \ket{u_j (t)} = \ket{u_j (t+T)}$,
  </p>
  
where 
$\ \epsilon_j$ and $\ \ket{u_j (t)}$ 
are the $\ j$-th quasienergy and Floquet mode, respectively. Substituting it to the time-dependent Schrödinger equation will get us, 	

<p align="center">
 $\ \epsilon_j \ket{u_j (t)} = [\hat{h_{MF}}(t)-i \hbar \frac{d}{dt}] \ket{u_j (t)}$
 </p>
 

where $\ \hat{h_{MF}}$ represents the Hamiltonian operator of a single spin site. We call 
$\ \hat{H_F}=\[\hat{h_{MF}}(t)-i\hbar\frac{d}{dt}\]\ket{u_j (t)}$ 
as the Floquet Hamiltonian which becomes an eigenvalue problem, where $\ \epsilon_j$  as the eigenvalue or quasienergy and $\ \ket{u_j (t)}$ as the eigenvector or Floquet mode. We only pick the quasienergies within the range of $\ -\frac{\pi}{\omega}\le\epsilon_j\le\frac{\pi}{\omega}$ also known as the first Brillouin zone. The eigenvalue problem would then be transformed into the Fourier space to solve the Floquet Modes from the $\ \(4N+2)\times(4N+2)$ Floquet Hamiltonian matrix where $\ N$ is the Fourier series cutoff.



### Fixed Point Iteration

To obtain the self-consistent value of $\ M_z (t)$, we assume first that $\ M_z(t)$ itself is periodical with the same period $\ T = \frac{2\pi}{\omega}$ as the driving field. The z-axis magnetization $\ M_z$ is then transformed into the Fourier space where the objective is solving the Fourier coefficients $\ \hat{C}$ by performing numerical iteration similar as the Gauss-Seidel method using the Successive Under/Over Relaxation (SUR/SOR).

## Current Results and Analysis

### Static Transverse Field 
The following is the result when the Transverse Ising Model is applied by a static field instead of an oscillating one.

<p align = "center">
  <img width="300" alt="image" src="https://user-images.githubusercontent.com/103773281/209478863-95d28fa2-d82e-40df-bd22-52747a46db9a.png">
  <img width="300" alt="image" src="https://user-images.githubusercontent.com/103773281/210075963-3a8dfb40-0884-4600-a806-d806eea0a5ad.png">
    
  <p align = "center">
  <strong>Figure 1.</strong> The plot of $\ M_z$ VS $\ \frac{\Omega}{qJ}$ <strong>(Left)</strong> and the plot of $\ M_x$ VS $\ \frac{\Omega}{qJ}$ when the field applied is time-dependent or dynamic <strong>(Right)</strong> when the field applied is time-independent or static.
  </p>
  

</p>

We see that when $\ \frac{\Omega}{qJ} = 1$ , where $\ \Omega$ is the ampltiude of the static field, the magnetization in the $\ z$ -axis direction gets annihilated and stays $\ M_z=0$ with larger values of $\ \frac{\Omega}{qJ}$. On the other hand, for the magnetization in the $\ x$ -axis increases linearly until $\ \frac{\Omega}{qJ} = 1$ where $\ M_x$ reaches the value of 1 and stays at the same value when $\ \frac{\Omega}{qJ}$ gets bigger than 1. In the next part, we would now explore the result where the transverse field is now dynamic.


### Oscillating Transverse Field

Before any numerical calculations, it is importantly noted that through the Floquet theorem, to yield a periodical self-consistent solution of $\ M_z(t)$, the wavefunction should only consist of one Floquet mode. This is because a linear combined wavefunction with different quasienergies would produce a phase factor that annihilates the periodicity of the magnetization.


#### Regarding Initial Guess Choice
It is observed that $\ M_z(t) = 1$ using QuTiP (will be explained below) as the initial guess has the lowest average expected energy from other initial guesses as shown in the figure below. The following graph shows The Average Expectation Value of the Energy vs $\ B_x$ with different initial guesses of $\ M_z(t)$


<p align="center">
  
  <img width="400" alt="image" src="https://user-images.githubusercontent.com/103773281/209558372-6f72ae95-141a-4d5b-9aa8-c9fe8bfa9620.png">
  <img width="400" alt="image" src="https://user-images.githubusercontent.com/103773281/209496522-c288a0ce-3e37-4332-a82c-bc669f2f9964.png">
  
  <p align="center">
  <strong>Figure 2. </strong>
  </p>
  
  </p>
  
Extending from the picture above, I also used many other initial guess where the amplitude of the $\ z$-axis magnetization must equal to 1 for physical reasons and yield a higher average energy than $\ M_z(t)=1$ as the initial guess. During the numerical iterations, we further use the previous iteration solution as the initial guess for the next $\ B_x$ that we want to study, so the initial guess of the $\ i+1$-th Bx follows the previous $\ i$-th Bx converging solution. 


#### Solving the Floquet Hamiltonian (Old Algorithm)
The following is the plot of the average magnetization in all three axis direction $\(\bar{M_x}, \bar{M_y}, \bar{M_z})$ which is obtained by solving the Floquet Hamiltonian used in the [Floquet Hamiltonian Python file](https://github.com/alexinthewonderland/transverse-ising-model/blob/main/Floquet%20Hamiltonian%20Method%20(Old%20Algorithm).ipynb) Here, we are solving for the very large (ideally infinite) Floquet Hamiltonian matrix and then reverse engineeing it to obtain the self consistent value of $\ M_z(t)$ and its average over one period $\ \bar{M_z}$

Having this property, we first choose the smallest positive quasienergy, and the result we obtained from the numerical iteration displays a **damping** of the average $\ M_z(t)$ over one period $\ \bar{M_z}$ with increasing $\ B_x$ as shown below.

<p align="center">

<img width="423" alt="image" src="https://user-images.githubusercontent.com/103773281/213920294-0724c04a-46c4-4977-ac30-54bb9982a235.png">

 <p align="center">
<strong>Figure 3.</strong>The plot that shows how the average magnetization changes with the value of $\ B_x$ using the Old Algorithm. Note that the orange line and the blue line overlap with each other since both have the same value for all $\ B_x$, which is 0.
</p>

</p>

From the above plot, we could also see that both $\ bar{M_x}$ and $\ bar{M_y}$ averages to zero for all of $\ B_x$, which makes sense since our driving oscillating field oscillates in a cosine manner that averages its magnitude to zero within one period. Nonetheless, we see that there are actually another solution during the numerical iteration, and this is shows below using QuTiP or as I call it the New Algorithm.

#### Integrating the time-evolution operator using QuTiP (New Algorithm)
In this new method, instead of solving the Floquet Hamiltonian, we numerically integrate the time-evolution operator by the help of the [QuTiP library](https://qutip.org/docs/4.1/guide/dynamics/dynamics-floquet.html). This lets us to eliminate of our worry with the high frequency uncertainty results if one uses the Floquet Hamiltonian method. 

The following is the result of the average magnetization VS $\ B_x$ by using QuTiP,

<p align="center">
  
<img width="400" alt="image" src="https://user-images.githubusercontent.com/103773281/209568783-833c6fe0-fdd3-42b2-9dd7-b926263d8388.png">

<p align="center">
<strong>Figure 4.</strong>
</p>
  
  </p>
 
From the above plot it could be observed that there are certain $\ B_x$ regime where only $\ \bar{M_z}$ is non-zero while $\ \bar{M_y}$ and \ \bar{M_x}$ is zero. There are also other regime where only $\ \bar{M_y}$ is non-zero while the other magnetization from the other axes are zero. In contrast, the value of $\ \bar{M_x}$ is always zero for all $\ B_x$ value. We also observe the same kind of damping to the system on average as we increase the value of $\ B_x$ as the Old Algorithm also does.

Nonetheless, this new result is starkingly different with the result obtained from the Old Algorithm using the Floquet Hamiltonian. However, further investigation showed us that this difference is due to two possible solutions from the numerical iteration as showin in the figure below. 

<p align="center">

<img width="400" alt="image" src="https://user-images.githubusercontent.com/103773281/213931943-ef001a90-5fe7-4bcf-9114-2a37d220fb79.png">

<p align="center">
<strong>Figure 5.</strong> Plot of +ve quasienergy VS $\ B_x$ with two different algorithms (the orange and blue plots), and on the lower part of the plot contains the plot of average magnetization in the $\ z$-axis for both algorithms as well as a function of $\ B_x$.
</p>

</p>

The above plot shows that there are some regions where the numerical iteration gives us the same quasienergy result for both algorithms, however, there are also some regions where suddenly the quasienergy values differs from one another. Looking further into the regions with different quasienergies, it is observed that the average Mz value are also different from one another, while when the quasienergy values are the same, the values of the average Mz is also the same. This invites us to conclude that there are two solutions possible during the numerical calculations. <strong>As a future plan</strong>, I would like to try to compare the average energy over one period value using both algorithms in those regions where the quasienergy solution differs.

  

Furthermore, looking at the "amplitude" of the average magnetization also gives us interesting characteristics as the following shows.

<p align="center">
  
  <img width="400" alt="image" src="https://user-images.githubusercontent.com/103773281/209577905-663cd1b6-f33c-43cb-a263-13f5bf24cc67.png">
  
  <p align="center">
  <strong>Figure 6.</strong>
  </p>

</p>

From the above plot, we hypothesize that the point where the amplitude of the average magnetization goes to zero indicates that the path as a functino of time of the average magnetization vector is a global path, meaning that it would cross a greater circle on the Bloch Sphere shown in the next section. Studying around this hypotheses would be one of our next big steps for the project.


##### Bloch Sphere Visualization
Due to the difficulty of imagining how the magnetization changes with time and also how different $\ B_x$ affects the system, I tried to track the path that the magnetization vector (here being $\ <\bar{M_x}, \bar{M_y}, \bar{M_z}>$ in a unit sphere which we call as the Bloch sphere.

<p align="center">

<img width="400" src="https://user-images.githubusercontent.com/103773281/210174076-1235e594-8e5e-4512-91df-276e5c038791.gif" />
<img width="400" src="https://user-images.githubusercontent.com/103773281/210174116-0a010988-28f2-4ff8-b0b1-fedfafb41303.gif" />
<img width="400" src="https://user-images.githubusercontent.com/103773281/210174102-f894a1ff-ea10-4395-98b4-5033e9b74905.gif" />
<img width="400" src="https://user-images.githubusercontent.com/103773281/210160073-d82f4c72-d0cf-4788-9f6a-d446da25408c.gif" />


<p align="center">
  <strong>Figure 7. </strong>A motion of the average magnetization vector inside of a Bloch sphere for when $\ B_x = 0.1$, $\ B_x = 2.0$, $\ B_x = 10.8$, and $\ B_x = 13.7$
</p>

 </p>

Here we only show a couple of the motion on the Bloch sphere for a few $\ B_x$ value since the motion itself might not be that useful to interpret (at least I don't have any idea currently). The real usefulness comes when we project the path to a 2D plane from one of the axes $\ (x, y, z)$ and try to calculate numerically the winding number of the projected path. This is what we will discuss in the next section.

##### Winding Numbers
To classify one of the properties of each path (different $\ B_x$), we use the following definition of the winding numbers explained in this [wikipedia](https://en.wikipedia.org/wiki/Winding_number) article (more details coming!).

From the simulations, it is observed that the angle you project the path of the magnetization vs time in the bloch sphere determines whether the winding number is a unity or none (1 or 0). When a certain $\ B_x$ yields a none zero $\ \bar{M_z}$ then the winding the number projected from the $\ z$-axis equals to 1, while all the other projections yield a zero winding number. In contrast, when $\ \bar{M_y}$ dominates the average magnetization of the system, then the winding number projected from the $\ y$-axis is 1 while all the other projections gives us a zero winding number. A few of the result could be shown below with its projected path also visualized.



## Note

If you found any mistakes or questions that you would like to assert, feel free to contact me on makurniawan@connect.ust.hk, I am more than happy to reply and fix it!



