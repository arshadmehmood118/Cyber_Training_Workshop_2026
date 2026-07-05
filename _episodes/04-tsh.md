---
title: "4. Nonadiabatic Dynamics and Trajectory Surface Hopping with Libra"
---

# 1. Setting up individual Jupyter kernel for using Libra on the OOD (Open On Demand)

## 1.1. Add this in your `.bashrc`:

```bash
module use /projects/academic/cyberwksp21/MODULES
module load libra_ava/devel
```

Restart your terminal or reload your `.bashrc`:

```bash
source ~/.bashrc
```

## 1.2. Activate libra environment and install jupyter kernel in user location:
```bash
conda activate libra 
python -m ipykernel install     --user     --name libra     --display-name "Python (libra)"
```

## 1.3. Update the `kernel.json` file in `/user/<your username>/.local/share/jupyter/kernels/libra` to be like this:


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


## 1.4. Create the file `launcher.sh` in `/user/<your username>/.local/share/jupyter/kernels/libra` to be like this:

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

## 1.5. Launch Jupyter on the OOD without any additional modules load needed

## 1.6. In the started Jupyter select "Python (libra)" kernel


# 2. Starting tutorials

The Libra tutorials are available at [https://github.com/compchem-cybertraining/Tutorials_Libra](https://github.com/compchem-cybertraining/Tutorials_Libra)

it is advisable that you just clone this repository to your local working directory and go from there. 

## 2.1. Go to your working directory, e.g.:
```bash
cd /projects/academic/cyberwksp21/Students/alexeyak/libra_examples`
```

or go to your home directory: 
```
cd
```

## 2.2. Clone the Tutorials_Libra repository:

```bash
git clone https://github.com/compchem-cybertraining/Tutorials_Libra.git
```

## 2.3. Start your Jupyter app on the OOD and open the desired tutorial/example

## 2.4. Keep in mind that Jupyter app run on the OOD can "see" only your home directory. 
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

## 3.1. Abstract model Hamiltonians (morning session)

### 3.1.1. Abstract (model Hamiltonian) NA-MD: 

 - **General NAMD:** 6_dynamics/1_trajectory_based/10_model_many_methods
 - **FMO example:** 6_dynamics/1_trajectory_based/12_model_spin_boson_fmo

### 3.1.2. Exact dynamics with PyTorch: 

 - **1D, 1 state:** 6_dynamics/4_wavepackets/6_soft_with_pytorch/1_single_state
 - **1D, multiple states:** /6_dynamics/4_wavepackets/6_soft_with_pytorch/2_multiple_states


## 3.2. Atomistic Hamiltonians (afternoon session)

### 3.2.1. Maing course: NBRA workflow with CP2K

 - **Step 1: adiabatic MD**  11_program_specific_methods/3_cp2k_methods/6_hpc_namd_workflow/1_step1
 - **Step 2: single-particle time-overlaps**  11_program_specific_methods/3_cp2k_methods/6_hpc_namd_workflow/2_step2
 - **Step 3: TD-DFT time-overlaps**  11_program_specific_methods/3_cp2k_methods/6_hpc_namd_workflow/3_step3
 - **Step 4: NBRA NA-MD** 6_dynamics/2_nbra_workflows/9_step4

### 3.2.2. Additional modules 

#### A. Computing time-overlaps

 - **Advanced Step 3 with CP2K:** 11_program_specific_methods/3_cp2k_methods/5_namd_workflow
 - **Steps 2 and 3 for DFTB+:** 11_program_specific_methods/4_dftbplus_methods/3_workflow
 - **Steps 2 and 3 for MOPAC:** 

    - 11_program_specific_methods/5_mopac_methods/1_initial_tutorial
    - 11_program_specific_methods/5_mopac_methods/2_using_active_spaces
     
#### B. Pre-NAMD analysis

 - **Time-resolved energies and influence spectra/spectral densities:** 11_program_specific_methods/3_cp2k_methods/3_time_resolved_energies
 - **Composition of excited states in therms of determinants:** 11_program_specific_methods/3_cp2k_methods/4_excitation_analysis

#### C. Running NA-MD
 
 - **Additional example of NBRA run:** 6_dynamics/2_nbra_workflows/10_generic_step3_4/1_Example1
 - **Non-NBRA example with DFTB+:** 11_program_specific_methods/4_dftbplus_methods/4_non_nbra_workflow


#### D. Post-NAMD analysis 

 - **Plotting TRPES:** 6_dynamics/2_nbra_workflows/18_plotting_trpes


# 4. Presentations and Videorecordings

## 4.1. Thursday, July 9, Morning

[Presentation](../files/Akimov/2026_July9-parts-1-3.pdf)

[Presentation](../files/Akimov/2026_July9-part4.pdf)







