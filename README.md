# Driving the Transverse Ising Model with an Oscillating Field

  ## Introduction
There is always a first time for everything. In this case, the Ising model is the first mathematical formalism that could be exactly solved to explain phase transitions in physical systems. It provides us with the Hamiltonian consisting of the spin interactions of the system, which encompasses properties such as ferromagnetism and the Curie temperature. Moving into the quantum realm, the spin terms become Pauli-matrices 
$\ S^{(x,z)}$
and the classical treatment of the Ising model hence does not apply. The system’s Hamiltonian
$\ H $ 
becomes an operator as the following shows,



<p align="center">
$\ H = -qJ\sum_{\braket{ij}}S_i^zS_{j}^z - B_x\cos(\omega t)\sum_i S_i^x$
</p>

This is what we call as the Transverse Ising model, where J is the coupling term between the spins, B(t) represents the oscillating external magnetic field, and the notation
$\ \braket{ij}$
indicates a summation of the nearest-neighbor (NN) of the i-th spin site. This quantum model will enable us to explore the quantum phase transition (QPT) of system with different transverse field. In this case, we chose $\ B(t)$ to be $\ B_x\cos(\omega t)$ as the oscillating drive transverse field that affects the QPT. During the study, the following three properties of the transverse field would be tweaked and played around with the Amplitude $\ B_x$, frequency $\ \omega$, and the Polarization $\ \phi$. Our objective is then to see any phase transitions and symmetry breaking of the magnetization expectation values $\ M_z$ and $\ M_x$, as we play around with the three values mentioned above.


