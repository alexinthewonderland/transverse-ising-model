# Driving the Transverse Ising Model with an Oscillating Field

This repository consists of the following things:

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
$\ \ket{\psi (t)} = \sum_{j=1} \gamma_j\ \bra{\phi (t)}$
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
