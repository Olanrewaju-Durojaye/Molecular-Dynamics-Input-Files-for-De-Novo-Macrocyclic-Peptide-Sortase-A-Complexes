================================================================================
GROMACS INPUT FILES FOR SORTASE A–MACROCYCLIC PEPTIDE MD SIMULATIONS
================================================================================

Repository title:
Molecular Dynamics Input Files for De Novo Macrocyclic Peptide–Sortase A
Complexes

--------------------------------------------------------------------------------
1. OVERVIEW
--------------------------------------------------------------------------------

This repository contains the starting coordinate files, molecular topologies,
position-restraint files, and GROMACS run-parameter files used for all-atom
molecular dynamics (MD) simulations of three de novo macrocyclic peptide
binder candidates in complex with Staphylococcus aureus Sortase A (SrtA):

    SMP01
    SMP41
    SMP103

The files are provided to facilitate reproducibility of the molecular dynamics
simulation setup and to allow direct inspection of the molecular topology of
each peptide–protein complex.

Each system is stored in a separate directory and contains the corresponding
starting structures, GROMACS topology files, and simulation parameter files.


--------------------------------------------------------------------------------
2. DIRECTORY STRUCTURE
--------------------------------------------------------------------------------

SrtA_macrocyclic_peptide_MD_inputs/
|
|-- README.txt
|
|-- SMP01/
|   |-- SMP01.pdb
|   |-- SMP01_processed.gro
|   |-- SMP01_solv_ions.gro
|   |-- topol.top
|   |-- topol_Protein_chain_A.itp
|   |-- topol_Protein_chain_B.itp
|   |-- posre_Protein_chain_A.itp
|   |-- posre_Protein_chain_B.itp
|   |-- minim.mdp
|   |-- ions.mdp
|   |-- nvt.mdp
|   |-- npt.mdp
|   `-- md.mdp
|
|-- SMP41/
|   |-- SMP41.pdb
|   |-- SMP41_processed.gro
|   |-- SMP41_solv_ions.gro
|   |-- topol.top
|   |-- topol_Protein_chain_A.itp
|   |-- topol_Protein_chain_B.itp
|   |-- posre_Protein_chain_A.itp
|   |-- posre_Protein_chain_B.itp
|   |-- minim.mdp
|   |-- ions.mdp
|   |-- nvt.mdp
|   |-- npt.mdp
|   `-- md.mdp
|
`-- SMP103/
    |-- SMP103.pdb
    |-- SMP103_processed.gro
    |-- SMP103_solv_ions.gro
    |-- topol.top
    |-- topol_Protein_chain_A.itp
    |-- topol_Protein_chain_B.itp
    |-- posre_Protein_chain_A.itp
    |-- posre_Protein_chain_B.itp
    |-- minim.mdp
    |-- ions.mdp
    |-- nvt.mdp
    |-- npt.mdp
    `-- md.mdp


--------------------------------------------------------------------------------
3. SYSTEM DESCRIPTION
--------------------------------------------------------------------------------

Each simulated system consists of Staphylococcus aureus Sortase A in complex
with one of three de novo-designed macrocyclic peptide binder candidates:
SMP01, SMP41, or SMP103.

Within the GROMACS topology:

    Protein chain A = Sortase A
    Protein chain B = macrocyclic peptide

The three peptide–protein complexes were treated using the same general
molecular dynamics preparation and simulation workflow to permit direct
comparison among the systems.


--------------------------------------------------------------------------------
4. MACROCYCLIC PEPTIDE TOPOLOGY
--------------------------------------------------------------------------------

SMP01, SMP41, and SMP103 were modeled as head-to-tail macrocyclic peptides.
The cyclic connectivity is explicitly encoded in the corresponding
topol_Protein_chain_B.itp file for each system.

In each peptide topology, atom 1 corresponds to the backbone nitrogen (N) of
the first peptide residue, whereas the indicated terminal atom corresponds to
the backbone carbonyl carbon (C) of the final peptide residue. The [ bonds ]
section explicitly connects these atoms as follows:


System: SMP01
Peptide residues: Gly207-Lys218
First-residue atom: Gly207:N (atom 1)
Last-residue atom:  Lys218:C (atom 177)
Cyclization bond:   1  177  1


System: SMP41
Peptide residues: Thr207-Gly219
First-residue atom: Thr207:N (atom 1)
Last-residue atom:  Gly219:C (atom 188)
Cyclization bond:   1  188  1


System: SMP103
Peptide residues: Met207-Val219
First-residue atom: Met207:N (atom 1)
Last-residue atom:  Val219:C (atom 189)
Cyclization bond:   1  189  1


These explicit N-to-C bonded topology entries define the head-to-tail
cyclization used during the molecular dynamics simulations. The corresponding
topology files additionally contain bonded terms spanning the cyclization
junction, including dihedral and CMAP terms, confirming that the cyclic
connectivity was incorporated into the bonded peptide topology rather than
being represented solely by spatial proximity of the terminal residues.

Molecular connectivity in GROMACS is defined by the topology. Therefore, the
corresponding topol_Protein_chain_B.itp files provide the primary reproducible
evidence for the macrocyclic representation employed in the simulations.

For direct verification, the relevant entries can be found in the [ bonds ]
section of:

    SMP01/topol_Protein_chain_B.itp
    SMP41/topol_Protein_chain_B.itp
    SMP103/topol_Protein_chain_B.itp

The respective head-to-tail bond entries are:

    SMP01:     1  177  1
    SMP41:     1  188  1
    SMP103:    1  189  1


--------------------------------------------------------------------------------
5. DESCRIPTION OF THE PROVIDED FILES
--------------------------------------------------------------------------------

A. Starting coordinate files
----------------------------

<SYSTEM>.pdb

    Initial peptide–Sortase A complex used for preparation of the corresponding
    molecular dynamics system.

<SYSTEM>_processed.gro

    GROMACS-processed coordinate structure generated during system preparation.

<SYSTEM>_solv_ions.gro

    Solvated and ionized coordinate structure used prior to subsequent energy
    minimization and equilibration.

Here, <SYSTEM> corresponds to SMP01, SMP41, or SMP103.


B. Molecular topology files
---------------------------

topol.top

    Master GROMACS topology file for the corresponding peptide–Sortase A
    simulation system.

topol_Protein_chain_A.itp

    Molecular topology of Sortase A (protein chain A).

topol_Protein_chain_B.itp

    Molecular topology of the corresponding macrocyclic peptide (protein
    chain B). This file contains the bonded molecular connectivity used for
    the peptide during the simulation.

posre_Protein_chain_A.itp

    Position-restraint topology for Sortase A.

posre_Protein_chain_B.itp

    Position-restraint topology for the macrocyclic peptide.


C. GROMACS run-parameter files
------------------------------

minim.mdp

    Parameters used for energy minimization.

ions.mdp

    Parameters used during preparation of the solvated/ionized system.

nvt.mdp

    Parameters used for NVT equilibration.

npt.mdp

    Parameters used for NPT equilibration.

md.mdp

    Parameters used for the production all-atom molecular dynamics simulation.


--------------------------------------------------------------------------------
6. FORCE FIELD AND SIMULATION SOFTWARE
--------------------------------------------------------------------------------

The molecular dynamics simulations were performed using GROMACS with the
CHARMM36 force field (charmm36-jul2021.ff).

The exact GROMACS version, CHARMM36 distribution/version, water model,
temperature, pressure, integration timestep, equilibration protocol, production
simulation duration, and other simulation parameters are also described in the
corresponding manuscript and are additionally specified where applicable in
the supplied .mdp and topology files.


--------------------------------------------------------------------------------
7. REPRODUCIBILITY
--------------------------------------------------------------------------------

The files in this repository are intended to provide the small, human-readable
input files necessary to inspect and reproduce the molecular dynamics system
preparation.

In particular, the repository enables inspection of:

    1. the starting coordinates of each peptide–Sortase A complex;
    2. the molecular topology assigned to Sortase A;
    3. the molecular topology assigned to each macrocyclic peptide;
    4. the covalent peptide connectivity used during MD;
    5. the position-restraint definitions; and
    6. the GROMACS parameters used for minimization, equilibration, and
       production MD.

Large trajectory files generated from the production simulations are archived
separately in Zenodo because of their substantially larger file sizes.


--------------------------------------------------------------------------------
8. LARGE TRAJECTORY DATA
--------------------------------------------------------------------------------

The production molecular dynamics trajectory files (.xtc) are not included
in this repository.

These files are deposited separately in Zenodo:

    Zenodo DOI: TO BE ADDED

The Zenodo deposition contains the trajectory data associated with the
simulations reported in the manuscript.


--------------------------------------------------------------------------------
9. ASSOCIATED PUBLICATION
--------------------------------------------------------------------------------

These files accompany the manuscript:

SMP103: a de novo-engineered macrocyclic peptide binder candidate targeting the virulence-associated transpeptidase Sortase A

Authors:

Olanrewaju Ayodeji Durojaye, Soukayna Baammi, Mohamed Moussaoui, Salaheddine EL HADAD, Loubna ALIMOUSSA, Rachid BENHIDA, Rachid Daoud,

Journal:
    
    Results in Engineering

DOI:
    (To be added)


--------------------------------------------------------------------------------
10. CITATION
--------------------------------------------------------------------------------

If these simulation input files or trajectory data are used in subsequent
work, please cite the associated publication and the corresponding Zenodo
dataset.

Publication citation:
    (To be added)

Zenodo dataset:
    (To be added)


--------------------------------------------------------------------------------
11. CONTACT
--------------------------------------------------------------------------------

For questions concerning the simulation setup or deposited files, please
contact:

Corresponding authors: Olanrewaju Ayodeji Durojaye/Rachid Doaud
    
Institution: Chemical and Biochemical Sciences, Green Process Engineering, University Mohammed VI Polytechnic, 43150 Ben Guerir, Morocco

Email: olanrewaju.ayodeji-durojaye-ext@um6p.ma; rachid.daoud@um6p.ma


--------------------------------------------------------------------------------
12. DATA AVAILABILITY
--------------------------------------------------------------------------------

The small molecular dynamics input files required to inspect and reproduce
the simulation setup, including starting coordinates, GROMACS molecular
topologies, position-restraint files, and run-parameter files, are publicly
available in this repository.

================================================================================
