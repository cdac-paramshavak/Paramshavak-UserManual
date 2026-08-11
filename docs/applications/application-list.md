## HPC Applications Overview

The HPC environment includes a comprehensive collection of software for
parallel computing, molecular dynamics, computational chemistry, materials
science, computational fluid dynamics, weather modeling, bioinformatics, and
scientific visualization.

## Installed HPC Applications

| Software | Category | Description and Purpose |
|---|---|---|
| **Slurm** | Job Scheduler | Slurm is an HPC workload manager used to schedule and manage jobs across compute nodes. It allocates CPUs, memory, GPUs, and other resources according to job requirements. It also provides job queuing, monitoring, accounting, and resource management. |
| **OpenMPI** | MPI | OpenMPI is an implementation of the Message Passing Interface (MPI) standard used for distributed-memory parallel computing. It enables processes running across multiple CPU cores and compute nodes to communicate efficiently. It is commonly used with scientific applications such as GROMACS, LAMMPS, WRF, and OpenFOAM. |
| **Intel oneAPI Compilers** | Compiler | Intel oneAPI Compilers provide optimized C/C++ and Fortran compilers for HPC and scientific applications. They support compiler optimizations, vectorization, and architecture-specific performance improvements. They are commonly used to build and optimize HPC applications for Intel processors. |
| **Intel oneAPI MPI** | MPI | Intel oneAPI MPI is an MPI implementation optimized for Intel-based HPC environments. It provides high-performance communication between parallel processes running on the same or multiple compute nodes. It can be used with applications such as GROMACS, LAMMPS, WRF, CP2K, and Quantum ESPRESSO. |
| **GROMACS** | Molecular Dynamics | GROMACS is a high-performance molecular dynamics package mainly used for simulating biological molecules and molecular systems. It is widely used for protein, DNA, RNA, lipid, and protein-ligand simulations. GROMACS supports MPI, OpenMP, CPU, GPU, and multi-node HPC execution. |
| **LAMMPS** | Molecular Dynamics | LAMMPS (Large-scale Atomic/Molecular Massively Parallel Simulator) is used to simulate atoms, molecules, and materials. It is widely applied to metals, alloys, polymers, graphene, crystals, nanomaterials, and other atomistic systems. LAMMPS is highly parallel and can utilize MPI, GPUs, and large HPC clusters. |
| **NAMD** | Molecular Dynamics | NAMD is a parallel molecular dynamics application designed primarily for large biomolecular systems. It is used for studying proteins, DNA, RNA, membranes, and protein-ligand interactions. NAMD supports large-scale CPU/GPU and multi-node HPC simulations. |
| **OpenFOAM** | CFD | OpenFOAM is an open-source Computational Fluid Dynamics (CFD) framework used to simulate fluid flow and engineering problems. It supports applications such as aerodynamics, heat transfer, combustion, turbulence, and multiphase flow. Large simulations can be distributed across HPC nodes using MPI and Slurm. |
| **WRF** | Weather Modeling | WRF (Weather Research and Forecasting Model) is a numerical weather prediction and atmospheric research model. It is used for weather forecasting, climate studies, rainfall prediction, cyclone modeling, wind analysis, and atmospheric research. WRF is computationally intensive and is commonly executed using MPI on HPC clusters. |
| **NWChem** | Quantum Chemistry | NWChem is a high-performance computational chemistry package used for quantum-mechanical and molecular calculations. It can calculate molecular structures, electronic properties, chemical reactions, and other molecular characteristics. NWChem supports parallel execution and is suitable for large-scale HPC calculations. |
| **ABINIT** | Materials Science | ABINIT is an open-source software suite used for first-principles calculations of materials. It is primarily used to study electronic structures, crystal properties, phonons, optical properties, and material behavior using quantum-mechanical methods. ABINIT supports parallel execution and is suitable for HPC-based materials research. |
| **CP2K** | Quantum Chemistry | CP2K is a quantum chemistry and atomistic simulation package designed for large molecular and materials systems. It is widely used for Density Functional Theory (DFT), molecular dynamics, materials science, surface chemistry, and energy-material research. CP2K supports MPI and OpenMP-based parallel execution on HPC systems. |
| **HMMER** | Bioinformatics | HMMER is a bioinformatics software package used to search biological sequence databases using profile Hidden Markov Models. It is commonly used for protein family identification, domain detection, genome annotation, and functional analysis. HPC resources can accelerate searches against very large biological sequence databases. |
| **MUMmer** | Bioinformatics | MUMmer is a bioinformatics package designed for fast comparison and alignment of large DNA sequences and genomes. It is used for whole-genome comparison, genome alignment, assembly validation, mutation analysis, and comparative genomics. It is particularly useful when processing large genomic datasets. |
| **Quantum ESPRESSO** | Quantum Materials | Quantum ESPRESSO is an open-source suite for quantum-mechanical simulations of materials, primarily based on Density Functional Theory (DFT). It is used for electronic structure, crystal properties, phonon calculations, surface science, semiconductors, and nanomaterials. Its computational workloads can be distributed across HPC nodes using MPI. |
| **VMD** | Visualization | VMD (Visual Molecular Dynamics) is a molecular visualization and analysis application used to examine structures and simulation trajectories. It is commonly used with molecular dynamics results generated by GROMACS and NAMD. VMD provides tools for molecular visualization, trajectory analysis, structure inspection, and molecular surface analysis. |
| **OVITO** | Visualization | OVITO (Open Visualization Tool) is a scientific visualization and analysis application primarily used for atomistic and materials simulation data. It can visualize trajectories and analyze structures, defects, dislocations, grain boundaries, and particle behavior. OVITO is particularly useful for analyzing results generated by LAMMPS and other molecular dynamics applications. |

---

## Application Categories

The installed HPC applications can be grouped according to their scientific
and computational purpose.

| Category | Applications | Main Purpose |
|---|---|---|
| **HPC Management** | Slurm | Job scheduling, resource allocation, monitoring, and accounting |
| **Parallel Computing** | OpenMPI, Intel oneAPI MPI | Parallel process execution and inter-node communication |
| **Compiler** | Intel oneAPI Compilers | Compilation and optimization of HPC applications |
| **Molecular Dynamics** | GROMACS, LAMMPS, NAMD | Molecular, atomic, biomolecular, and materials simulations |
| **Computational Fluid Dynamics** | OpenFOAM | Fluid flow, heat transfer, combustion, and engineering simulations |
| **Weather Modeling** | WRF | Weather forecasting and atmospheric simulations |
| **Quantum Chemistry** | NWChem, CP2K | Quantum chemistry, molecular calculations, and DFT |
| **Materials Science** | ABINIT, Quantum ESPRESSO, CP2K | First-principles, electronic structure, and material simulations |
| **Bioinformatics** | HMMER, MUMmer | Protein, DNA, genome, and sequence analysis |
| **Visualization** | VMD, OVITO | Visualization and analysis of molecular and materials simulations |

---
