# Bi-dimensional metadynamics simulation of the cis-trans isomerization of a Prolyl Peptide

Input for PLUMED specifying a two-dimensional metadynamics simulation of the cis-trans isomerization in a Prolyl peptide. The collective variables are the dihedral angles omega and psi. Omega captures the cis-trans transition across the peptide bond, while psi serves as an auxiliary collective variable, aiding in the exploration and equilibration of the peptide's conformational space during the isomerization process.

```plumed
# set up the two torsion collective variables
omega: TORSION ATOMS=19,26,28,31
psi: TORSION ATOMS=27,31,39,41

#METAD activates metadynamics
#ARG indicates variables to enhance (omega & psi)
#PACE indicates frequency of Gaussian deposition is 1000 time step (2ps)
#HEIGHT indicates that height of the Gaussians is 0.5 kJ/mol
#SIGMA indicates the width of the Gaussians on omega and psi CVs, respectively
#FILE indicates the name of the file where the hills are stored

metad: METAD ARG=omega,psi PACE=1000 HEIGHT=0.2 SIGMA=0.17,0.24 FILE=HILLS

#print in other file the values of the CVS and the bias potential
#STRIDE frequency of output
#ARG things to print, omega, psi, metad.bias
#FILE, name of the file to output; COLVAR
#DUMPFORCES print applied forces to output; forces.dat

PRINT STRIDE=500 ARG=omega,psi,metad.bias FILE=COLVAR
DUMPFORCES ARG=omega,psi STRIDE=500 FILE=forces.dat
```
The numbers in the *keyword* ```ATOMS``` are the atom numbers that define the two torsion angles, omega and psi.

The *keyword* ```METAD``` directs *PLUMED* to perform a metadynamics calculation with a Gaussian height of ```HEIGHT=0.2``` and widths of ```SIGMA=0.17,0.24```. The vaules of ```SIGMA``` roughly correspond to the standard deviation of each torsion angle, as computed in unbiased simulations.

The line starting with ```PRINT``` instruct plumed to write collective variables and bias potential every 500 step to the file ```COLVAR```.
The line starting with ```DUMPFORCES``` instruct plumed to write the applied biasing forces on the collective variables,```omega,psi``` to the file ```forces.dat```. Writing these forces is useful for calculating the unbiased free energy using the force correction analysis method (FCAM, Marinelli et al. JCTC 2021, https://github.com/FCAM-NIH/FCAM). Detailed documentation on setup and analysis is provided on the Tutorial Instructions. 

