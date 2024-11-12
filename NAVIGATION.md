```mermaid
flowchart LR
A[MD: Peptidyl-Prolyl] ==> B[Metadynamics: cis-trans isomerization]
A[MD: Peptidyl-Prolyl] ==> C[Bias-Exchange: cis-trans isomerization]
D[PLUMED syntax] ==> B[Metadynamics: cis-trans isomerization]
D[PLUMED syntax] ==> C[Bias-Exchange: cis-trans isomerization]
B[Metadynamics: Peptidyl-Prolyl]==>E[WHAM: Free energy]
C[Bias-Exchange: Peptidyl-Prolyl]==>F[WHAM: Free energy]
B[Metadynamics: Peptidyl-Prolyl]==>H[FCAM: Free energy]
C[Bias-Exchange: Peptidyl-Prolyl]==>I[FCAM: Free energy]
G[Tutorial Instructions]
click D "tute" "A tutorial on the basic plumed syntax"
```
