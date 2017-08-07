### dockerfiles 

Order of images:

1. root (using centos 7 base os);
2. clhep;
3. geant4;
4. mpich (built locally);
5. g4env (setting environment variables and building G4MPI);
6. g4app (modified version of [g4simple](https://github.com/legend-exp/g4simple) );

docker hub:

`docker pull nmtzwh/scistack`

usages:

```bash
# use the bash entry point to test
docker run -it --rm nmtzwh/scistack

# run the g4simple program with local directory mounted
docker run -it -v <path-to-input>:/input \
    nmtzwh/scistack \
    mpiexec -n 2 g4simple /input/run.mac

```

SLURM script for `shifter`:

```bash
#!/bin/bash
#SBATCH --image=docker:nmtzwh/scistack:latest
#SBATCH --nodes=1
#SBATCH --partition=debug
#SBATCH --constraint=haswell
#SBATCH --time=00:30:00
#SBATCH --volume="/global/project/<path-to-input>:/input;/global/project/<path-to-output>:/output"

srun -n 32 shifter g4simple /input/macro_input.mac
```


