# Pymatgen Scripts

## Converting a conventional cell to primitve cell using pymatgen library on supercomputers

Write the below command in the terminal to load python module where pymatgen is installed

`module load anaconda3_2019`

Input file: input.py

```
#!/lfs/sware/anaconda3_2019/bin/python3
from pymatgen.core import Structure
from pymatgen.symmetry.analyzer import SpacegroupAnalyzer
str = Structure.from_file('TiN.vasp')
strPrim = str.get_primitive_structure()
strPrim.to(fmt='poscar', filename='TiNprimitive')
```

Use submission script because some jobs might take longer time.

Submission file: job.sh
```
#!/bin/bash
#PBS -o out
## Merge output and error files
#PBS -j oe
#PBS -k eod
#PBS -l walltime=00:59:59
## Select n nodes, each with n CPUs
#PBS -l select=1:ncpus=1
cd $PBS_O_WORKDIR
mpirun -np 1 /lfs/sware/anaconda3_2019/bin/python3 input.py > log
```

Submit the calculation
`qsub job.sh`
