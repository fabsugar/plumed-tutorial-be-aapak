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
Two additional *PLUMED* files are required for each metadynamics replica, and these can be placed in separate folders where each replica is being run
