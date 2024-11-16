# Bias exchange metadynamics simulation of the cis-trans isomerization of a Peptidyl-Prolyl Peptide

PLUMED input for a bias-exchange metadynamics simulation of the cis-trans isomerization in a Peptidyl-Prolyl peptide. The simulation utilizes two replicas, each applying a bias to one of the torsion angles, omega and psi, that describe the cis-trans transition at the proline peptide bond, along with the associated auxiliary conformational motion, respectively. Replica exchanges are attempted at regular intervals and accepted according to a Metropolis criterion, based on the biasing potentials of the replicas.
The setup entails one common *PLUMED* file specifing the two torsional angles, omega and psi, and the ```RANDOM_EXCHANGES``` *keyword* instructing *PLUMED* to make exchanges between randomly chosen replicas:  

```plumed
# randomize the exchange (not between consecutive indeces, here just 2 replicas, so it is not relevant)
RANDOM_EXCHANGES
# set up the two torsion collective variables 
# omega (use cv1 so it will be compatible with the METAGUI analysis plugin)
cv1: TORSION ATOMS=19,26,28,3
# psi (use cv1 so it will be compatible with the METAGUI analysis plugin)
cv2: TORSION ATOMS=27,31,39,41
```
Two additional *PLUMED* files are required for each metadynamics replica, and these can be placed in separate folders where each replica is being run. These *PLUMED* files read the definitions of collective variables and other shared parameters from the common PLUMED file using the ```INCLUDE FILE``` *keyword*. The bias is applied to a single dihedral angle, with each replica biasing a different angle. The first PLUMED file performs metadynamics on the omega angle (```cv1```):

```plumed
INCLUDE FILE=../plumed_be-common.dat

#METAD activates metadynamics
#ARG indicates variables to enhance (omega & psi)
#PACE indicates frequency of Gaussian deposition is 1000 time step (2ps)
#HEIGHT indicates that height of the Gaussians is 0.2 kJ/mol
#SIGMA indicates the width of the Gaussians on the biased cv, respectively

be: METAD ARG=cv1 PACE=1000 HEIGHT=0.2 SIGMA=0.17

#print in other file the values of the CVS and the bias potential
#STRIDE frequency of output
#ARG things to print, omega, psi
#FILE, name of the file to output; COLVAR

PRINT STRIDE=500 ARG=cv1,cv2 FILE=COLVAR
DUMPFORCES ARG=cv1,cv2 STRIDE=500 FILE=forces.dat
```
The second *PLUMED* file entails a metadynamics on the psi angle (```cv2```)::

```plumed
INCLUDE FILE=../plumed_be-common.dat

#METAD activates metadynamics
#ARG indicates variables to enhance (omega & psi)
#PACE indicates frequency of Gaussian deposition is 1000 time step (2ps)
#HEIGHT indicates that height of the Gaussians is 0.2 kJ/mol
#SIGMA indicates the width of the Gaussians on the biased cv, respectively

be: METAD ARG=cv2 PACE=1000 HEIGHT=0.2 SIGMA=0.24

#print in other file the values of the CVS and the bias potential
#STRIDE frequency of output
#ARG things to print, omega, psi
#FILE, name of the file to output; COLVAR

PRINT STRIDE=500 ARG=cv1,cv2 FILE=COLVAR
DUMPFORCES ARG=cv1,cv2 STRIDE=500 FILE=forces.dat
```
Both *PLUMED* files write the collective variables and the applied forces in the files ```COLVAR``` and ```forces.dat``` via the keywords 

