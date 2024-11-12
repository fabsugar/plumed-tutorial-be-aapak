```mermaid
flowchart LR
A[MD: Peptidyl-Prolyl] ==> B[Metadynamics: Peptidyl-Prolyl]
A[MD: Peptidyl-Prolyl] ==> C[Bias-Exchange: Peptidyl-Prolyl]
D[PLUMED syntax] ==> B[Metadynamics: Peptidyl-Prolyl]
D[PLUMED syntax] ==> C[Bias-Exchange: Peptidyl-Prolyl]
B[Metadynamics: Peptidyl-Prolyl]==>E[WHAM: Free energy]
C[Bias-Exchange: Peptidyl-Prolyl]==>F[WHAM: Free energy]
B[Metadynamics: Peptidyl-Prolyl]==>H[FCAM: Free energy]
C[Bias-Exchange: Peptidyl-Prolyl]==>I[FCAM: Free energy]
G[Tutorial Instructions]==>A[MD: Peptidyl-Prolyl]
G[Tutorial Instructions]==>B[Metadynamics: Peptidyl-Prolyl]
G[Tutorial Instructions]==>C[Bias-Exchange: Peptidyl-Prolyl]
G[Tutorial Instructions]==>E[WHAM: Free energy]
G[Tutorial Instructions]==>F[WHAM: Free energy]
G[Tutorial Instructions]==>H[FCAM: Free energy]
G[Tutorial Instructions]==>I[FCAM: Free energy]
click D "tute" "A tutorial on the basic plumed syntax"
```
