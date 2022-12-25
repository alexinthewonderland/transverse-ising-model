# Results and Discussions
Through the Floquet theorem, to yield a periodical self-consistent solution of $\ M_z(t)$, the wavefunction should only consist of one Floquet mode. This is because a linear combined wavefunction with different quasienergies would produce a phase factor that annihilates the periodicity of the magnetization. Having this property, we first choose the smallest positive quasienergy and the result we obtained from the numerical iteration displays a damping of the average $\ M_z(t)$ over one period $\ \bar{M_z}$ with increasing $\ B_x$ as shown below.

<p align = "center">
  <img width="300" alt="image" src="https://user-images.githubusercontent.com/103773281/209478863-95d28fa2-d82e-40df-bd22-52747a46db9a.png">
  <img width="350" alt="image" src="https://user-images.githubusercontent.com/103773281/209478979-8e544ba3-3605-4d7a-ae42-c81f2887842f.png">


</p>

## Regarding Initial Guess
We only use $\ M_z(t) = 1$ as the initial guess due to its average expected energy to have the lowest value out of many initial guess. The following shows the graph of The Average Expectation Value of the Energy vs $\ B_x$ with different initial guesses of $\ M_z(t)$

## Solving the Floquet Hamiltonian (Old Algorithm)
<img width="249" alt="image" src="https://user-images.githubusercontent.com/103773281/209479197-97a73587-9fe8-44f1-aee8-a641020c71db.png">

## Integrating the time-evolution operator using QuTiP (New Algorithm)
<img width="249" alt="image" src="https://user-images.githubusercontent.com/103773281/209479274-ede56829-d067-48ea-bc65-2565216a4c34.png">







