---
title: "4. Nonadiabatic Dynamics and Trajectory Surface Hopping with Libra"
---

# 1. Setting up individual Jupyter kernel for using Libra on the OOD (Open On Demand)

## 1. Add this in your `.bashrc`:

```bash
module use /projects/academic/cyberwksp21/MODULES
module load libra_ava/devel
```

Restart your terminal or reload your `.bashrc`:

```bash
source ~/.bashrc
```

## 2. Activate libra environment and install jupyter kernel in user location:
```bash
conda activate libra 
python -m ipykernel install     --user     --name libra     --display-name "Python (libra)"
```

## 3. Update the `kernel.json` file in `/user/<your username>/.local/share/jupyter/kernels/libra` to be like this:


```bash
{
 "argv": [
  "/user/<your username>/.local/share/jupyter/kernels/libra/launcher.sh",
  "-f",
  "{connection_file}"
 ],
 "display_name": "Python (libra)",
 "language": "python",
 "metadata": {
  "debugger": true
 }
}
```

> Note: Replace `<your username>` with your actual user name e.g. `alexeyak`


# 4. Create the file `launcher.sh` in `/user/<your username>/.local/share/jupyter/kernels/libra` to be like this:

```bash
#!/bin/bash
# ======================================================
# HARD CLEAN (CRITICAL on CCR)
# ======================================================
unset PYTHONPATH
unset PYTHONHOME
unset EBPYTHONPREFIXES
# Prevent user site leakage
export PYTHONNOUSERSITE=1
# ======================================================
# Load module environment (ONLY ONE layer)
# ======================================================
module use /projects/academic/cyberwksp21/MODULES
module load libra_ava/devel
# ======================================================
# Activate Conda environment (must match module!)
# ======================================================
source /projects/academic/cyberwksp21/SOFTWARE/Conda/etc/profile.d/conda.sh
conda activate libra
# ======================================================
# Libra runtime libraries
# ======================================================
export LD_LIBRARY_PATH=/projects/academic/cyberwksp21/SOFTWARE/libra/_build/src:$LD_LIBRARY_PATH
# ======================================================
# Launch kernel
# ======================================================
exec /projects/academic/cyberwksp21/SOFTWARE/Conda/envs/libra/bin/python \
     -m ipykernel_launcher "$@"
```

And make it executable:

```bash
chmod +x .local/share/jupyter/kernels/libra/launcher.sh
```

# 5. Launch Jupyter on the OOD without any additional modules load needed

# 6. In the started Jupyter select "Python (libra)" kernel





