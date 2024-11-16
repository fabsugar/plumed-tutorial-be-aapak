# Bias exchange metadynamics simulation of the cis-trans isomerization of a Peptidyl-Prolyl Peptide

PLUMED input for a bias-exchange metadynamics simulation of the cis-trans isomerization in a Peptidyl-Prolyl peptide. The simulation utilizes two replicas, each applying a bias to one of the torsion angles, omega and psi, that describe the cis-trans transition at the proline peptide bond, along with the associated auxiliary conformational motion, respectively. Replica exchanges are attempted at regular intervals and accepted according to a Metropolis criterion, based on the biasing potentials of the replicas.
For running the bias exchange with two replicas we need 3 PLUMED files; one common (here we named it plumed_be-common.dat) and two other files for each metadynamics replica (plumed.0.dat and plumed.1.dat).![image](https://github.com/user-attachments/assets/67fa1f3b-0642-4fad-9426-0c85a683e6b8)


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
