# Driving the Transverse Ising Model with an Oscillating Field

 ## Introduction
 
There is always a first time for everything. In this case, the Ising model is the first mathematical formalism that could be exactly solved to explain phase transitions in physical systems. It provides us with the Hamiltonian consisting of the spin interactions of the system, which encompasses properties such as ferromagnetism and the Curie temperature. Moving into the quantum realm, the spin terms become Pauli-matrices 
$\ S^{(x,z)}$
and the classical treatment of the Ising model hence does not apply. The system’s Hamiltonian
$\ H $ 
becomes an operator as the following shows,

<p align="center">
$\ \hat{H} = -qJ\sum_{\braket{ij}}S_i^zS_{j}^z - B_x\cos(\omega t)\sum_i S_i^x$
</p>

This is what we call as the Transverse Ising model, where J is the coupling term between the spins, B(t) represents the oscillating external magnetic field, and the notation
$\ \braket{ij}$
indicates a summation of the nearest-neighbor (NN) of the i-th spin site. This quantum model will enable us to explore the quantum phase transition (QPT) of system with different transverse field. In this case, we chose $\ B(t)$ to be $\ B_x\cos(\omega t)$ as the oscillating drive transverse field that affects the QPT. During the study, the following three properties of the transverse field would be tweaked and played around with the Amplitude $\ B_x$, frequency $\ \omega$, and the Polarization $\ \phi$. Our objective is then to see any phase transitions and symmetry breaking of the magnetization expectation values $\ M_z$ and $\ M_x$, as we play around with the three values mentioned above.

## Methods that I used
### Mean Field Theory
Due to the mathematical complication of the NN spin coupling summation, the Mean-Field theory (MFT) or approximation lets each spin to instead feel an average field that the nearest-neighbors spins produce. Hence, in our case, the nearest neighbor summation becomes a single site summation,

<p align="center">
$\ {\hat{H}}_{MF}=-qJM_z(t) {\sum_{i}^{N}} {\hat{S}}_i^z-B_x\cos{(\omega t)}\sum_{i=1}^{N}{\hat{S}}_i^x$
</p>

where $\ {\hat{H}}_{MF}$ is the mean field Hamiltonian and $\ qJM_z$ is our mean field with $\ q$ as the value of how many nearest neighbors the $\ i$-th has and $\ M_z(t)$ is the magnetization in the $\ z$-axis direction. The power of mean field approximation is seen above as it reduces a many-body problem into a two-level system with its approximation. The above mean-field Hamiltonian could be derived from the Gibbs-Bogoluibov Inequality, or you could take a different route using the variational principle.


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
 $\ \epsilon_j \ket{u_j (t)} = [\hat{h}_{MF}(t)-i \hbar \frac{d}{dt}] \ket{u_j (t)}$
 </p>
 

where <p>$\ \hat{h}_{MF}$</p> represents the Hamiltonian operator of a single spin site. We call 
$\ \hat{H}_{F}=[\hat{h}_{MF}(t)-i\hbar\frac{d}{dt}]\ket{u_j (t)}$ 

as the Floquet Hamiltonian which becomes an eigenvalue problem, where \epsilon_j as the eigenvalue or quasienergy and |u_j\left(t\right)\ket as the eigenvector or Floquet mode. We only pick the quasienergies within the range of -\frac{\pi}{\omega}\le\epsilon_j\le\frac{\pi}{\omega} also known as the first Brillouin zone. The eigenvalue problem would then be transformed into the Fourier space to solve the Floquet Modes from the \left(4N+2\right)\times(4N+2) Floquet Hamiltonian matrix where N is the Fourier series cutoff.



### Fixed Point Iteration

