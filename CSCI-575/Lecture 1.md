# 8/25 Lecture 1

### Quantum computing and quantum cryptography

#### Lecture unit 1: Classical versus quantum model of computation

##### What is the course about?

Quantum computing refers to computation based on quantum mechanical principles.
Proposed in 1980s and investigated primarily from a theoretical perspective for several decades, quantum computing has emerged as a prominent research area with tremendous potential for practical applications.
In this introductory course to quantum computing our exploration will be guided by the following questions:

- What are the quantum mechanical principles as they apply to computation and cryptography?
- How is quantum computation different from classical computation?
- What does it take to realize quantum computation? (light)

**Textbook**: *Quantum Computation and Quantum Information*, Michael A. Nielsen and Issac L. Chung, Cambridge

- Preface to the 10th edition
- The most successful and the most mysterious scientific theory.
- Applications: from polymers to semiconductors; from superfluids to superconductors; models of particle physics,
- New perspective from computer and information science: Quantum systems as systems that can be designed

##### Outline

- From bit to qubit
- Quantum mechanical worldview, quantum states, operators, entanglement, EPR pairs, quantum key distribution
- Quantum gates, quantum teleportation
- Quantum algorithms, quantum Fourier transformation

##### What is in a bit?

- Bit - basic unit of (digital) information
- In a computer (or any computing device), bits of information (bytes, mega-, giga-bytes) are stored - physically, and processed /computed.
- Each bit takes values in {0,1} - mathematically speaking.
- A classical bit at any time is either in state 0 or in state 1.
- Read - without changing the state (hence can copy)

---

- At a microscopic level of a particle, such as an electron or a photon, the concept of a state in the classical sense becomes problematic.

- The idea that a particle is found in a state (energy, momentum, position, spin) at any moment is problematic. (Double-slit experiment (wave-particle), Stern-Gerlach experiment (1.5))
- The spin of a particle as one or several bits of information? (7.6.1 p.310) When measured
  - The spin of a particle is either integer or a half integer
  - Photon (a boson) has spin 1 or -1
  - Electron (a fermion) has spin 1/2 (up) or 1½ (down).
  - Not the case that the spin is either 1 or -1 (1/2 or -1/2) at any moment - problematic if we assume so.

---

- Spin -- what is it?

  - Box 7.6, p. 301; Box 7.7, p. 310

  - An intrinsic property of particles, related to angular momentum (suggesting the idea of a particle rotating around an axis)

  - Bosons (integer spins) and fermions (half-integer spins)

  - Photon has spin ±1 when measured (spin measurement).