# Bidimensional metadynamics simulation of the cis-trans isomerization of a Peptidyl-Prolyl Peptide

Input for PLUMED specifying a two-dimensional metadynamics simulation of the cis-trans isomerization in a Peptidyl-Prolyl peptide. The collective variables are the dihedral angles omega and psi. Omega captures the cis-trans transition across the peptide bond, while psi serves as an auxiliary collective variable, aiding in the exploration and equilibration of the peptide's conformational space during the isomerization process.

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
