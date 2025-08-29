# DSSP Analysis Through Trejectory using MDtraj and Matplotlib

A Python code for analyzing secondary structure and solvent accessible surface area (SASA) from molecular dynamics trajectories using DSSP algorithm. Plese see the Colab code for a streamlined application.

## Features

- **Secondary Structure Analysis**: DSSP-based assignment with temporal evolution tracking
- **SASA Calculations**: Shrake-Rupley algorithm for solvent accessibility analysis  
- **Time Series Visualization**: Plot secondary structure and SASA changes over simulation time
- **Statistical Analysis**: Automated calculation of averages, correlations, and distributions

## Installation

### Prerequisites

```bash
conda create -n dssp-analysis python=3.8
conda activate dssp-analysis
```

### Required packages

```bash
conda install -c conda-forge mdtraj numpy matplotlib
# or
pip install mdtraj numpy matplotlib
```

## Quick Start

### Basic DSSP Analysis

```python
import mdtraj as md
import numpy as np
import matplotlib.pyplot as plt

# Load trajectory
traj = md.load('trajectory.xtc', top='topology.tpr')

# Compute secondary structure
dssp = md.compute_dssp(traj, simplified=True)

# Calculate helix content over time
helix_content = (dssp == 'H').sum(axis=1)
time_ns = traj.time / 1000.0

# Plot results
plt.plot(time_ns, helix_content)
plt.xlabel('Time (ns)')
plt.ylabel('Number of Helical Residues')
plt.show()
```

### SASA Analysis

```python
# Calculate SASA
sasa = md.shrake_rupley(traj, probe_radius=0.14, n_sphere_points=960)
total_sasa = sasa.sum(axis=1)

# Plot SASA over time
plt.plot(time_ns, total_sasa)
plt.xlabel('Time (ns)')
plt.ylabel('Total SASA (nm²)')
plt.show()
```



## Acknowledgments

- [MDTraj](https://mdtraj.org/) for trajectory analysis capabilities
- [DSSP](https://swift.cmbi.umcn.nl/gv/dssp/) algorithm by Kabsch & Sander
- [Shrake-Rupley](https://doi.org/10.1016/0022-2836(73)90011-9) algorithm for SASA calculations
