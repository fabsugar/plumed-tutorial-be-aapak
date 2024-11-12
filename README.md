# Setting Up and Analyzing Bias-Exchange Metadynamics Simulations: the case of cis-trans isomerization of Peptidyl-Prolyl Peptides

This repository includes the required files and documentation to follow the tutorial on setting up and analyzing molecular dynamics, metadynamics and bias-exchange metadynamics simulations, specifically focusing on the cis-trans isomerization of peptidyl-prolyl peptides.
A tutorial step by step description is provided in the document: https://github.com/fabsugar/plumed-tutorial-be-aapak/blob/main/protocol1_md-meta-be.pdf.

The file `tutorial_files.zip` contain the necessary input files to perform the tutorial. It can be unpacked via `unzip tutorial_files.zip`. After unpacking, you'll find a folder with three separate files, each corresponding to a different step of the tutorial: 1) MD setup:`practical1.zip`, 2) Metadynamics and bias exchange setup:`practical2.zip`, 3) Convergence and Free energy analysis:`practical3.zip`.

```mermaid
flowchart LR
A[MD: Peptidyl-Prolyl] ==> B[Metadynamics: cis-trans isomerization]
A[MD: Peptidyl-Prolyl] ==> C[Bias-Exchange: cis-trans isomerization]
D[PLUMED syntax] ==> B[Metadynamics: cis-trans isomerization]
D[PLUMED syntax] ==> C[Bias-Exchange: cis-trans isomerization]
B[Metadynamics: cis-trans isomerization]==>E[WHAM: Free energy]
C[Bias-Exchange: cis-trans isomerization]==>F[WHAM: Free energy]
B[Metadynamics: cis-trans isomerization]==>H[FCAM: Free energy]
C[Bias-Exchange: cis-trans isomerization]==>I[FCAM: Free energy]
G[Tutorial Instructions]
L[Tutorial Files]
click E "https://github.com/metagui/metagui3" "metagu3: VMD plugin for cluster and free energy analysis (Giorgino et al. Comp Phys Comm 2017)"
click F "https://github.com/metagui/metagui3" "metagu3: VMD plugin for cluster and free energy analysis (Giorgino et al. Comp Phys Comm 2017)"
click H "https://github.com/FCAM-NIH/FCAM" "FCAM: free energy calculation based on mean forces (Marinelli et al. JCTC 2021)"
click I "https://github.com/FCAM-NIH/FCAM" "FCAM: free energy calculation based on mean forces (Marinelli et al. JCTC 2021)"
click D "http://www.plumed-tutorials.org/lessons/21/001/data/NAVIGATION.html" "A tutorial on the basic plumed syntax"
click G "https://github.com/fabsugar/plumed-tutorial-be-aapak/blob/main/protocol1_md-meta-be.pdf" "Tutorial Instructions"
click L "https://github.com/fabsugar/plumed-tutorial-be-aapak/blob/main/tutorial_files.zip" "tutorial files"
```


