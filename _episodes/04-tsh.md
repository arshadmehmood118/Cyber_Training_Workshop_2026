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


## 4. Create the file `launcher.sh` in `/user/<your username>/.local/share/jupyter/kernels/libra` to be like this:

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

## 5. Launch Jupyter on the OOD without any additional modules load needed

## 6. In the started Jupyter select "Python (libra)" kernel


# 2. Starting tutorials

The Libra tutorials are available at [https://github.com/compchem-cybertraining/Tutorials_Libra](https://github.com/compchem-cybertraining/Tutorials_Libra)

it is advisable that you just clone this repository to your local working directory and go from there. 

## 1. Go to your working directory, e.g.:
```bash
cd /projects/academic/cyberwksp21/Students/alexeyak/libra_examples`
```

or go to your home directory: 
```
cd
```

## 2. Clone the Tutorials_Libra repository:

```bash
git clone https://github.com/compchem-cybertraining/Tutorials_Libra.git
```

## 3. Start your Jupyter app on the OOD and open the desired tutorial/example

## 4. Keep in mind that Jupyter app run on the OOD can "see" only your home directory. 
If you keep your examples elsewhere, e.g. on the `/projects/academic/cyberwksp21/Students/alexeyak`,

you need to create a symlink (symbolic link) to that directory in your home directory, e.g.:

```bash
cd
ln -s /projects/academic/cyberwksp21/Students/<my working folder> workshop
```

> Note: replace `<my working folder>` with the actual name

This will create a link (that would appear as a folder) in your home directory called `workshop`. It will point to the actual folder
located at `/projects/academic/cyberwksp21/Students/<my working folder>`

> WARNING: Link behaves the same way as the actual folder, so if you try to delete the link like this `rm -r workshop`, it will delete your actual tutorials folder.
  If you no longer need the link, use `rm workshop` (no `-r` option!)


# 3. Lesson plan

To be added 



