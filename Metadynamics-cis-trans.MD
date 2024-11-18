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

# Bias exchange metadynamics simulation of the cis-trans isomerization of a Prolyl Peptide

PLUMED input for a bias-exchange metadynamics simulation of the cis-trans isomerization in a Prolyl peptide (see also that of a bi-dimensional metadynamics). The simulation utilizes two replicas, each applying a bias to one of the torsion angles, omega and psi, that describe the cis-trans transition at the proline peptide bond, along with the associated auxiliary conformational motion, respectively. Replica exchanges are attempted at regular intervals and accepted according to a Metropolis criterion, based on the biasing potentials of the replicas.
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
Two additional *PLUMED* files are required for each metadynamics replica, and these can be placed in separate folders where each replica is being run. These *PLUMED* files read the definitions of collective variables and other shared parameters from the common *PLUMED* file using the ```INCLUDE FILE``` *keyword*. The bias is applied to a single dihedral angle, with each replica biasing a different angle. The first *PLUMED* file performs metadynamics on the omega angle (```cv1```):

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
The second *PLUMED* file entails a metadynamics on the psi angle (```cv2```):

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
Both *PLUMED* files output the collective variables and biasing applied forces on those variables to the files ```COLVAR``` and ```forces.dat``` via the keywords ```PRINT``` and ```DUMPFORCES```, respectively. These files are useful for calculating the bi-dimensional free energy as a function of omega and psi, using the sampling of both replicas via the force correction analysis method (FCAM, Marinelli et al. JCTC 2021, https://github.com/FCAM-NIH/FCAM). Detailed documentation on setup and analysis is provided on the Tutorial Instructions. 
