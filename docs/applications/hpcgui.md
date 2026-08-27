# HPC Application GUI — User Guide

The **HPC Application GUI**, developed by **C-DAC** for **PARAM Shavak**, provides an easy,
form-based way to run High Performance Computing applications without needing to know
Linux terminal commands, module load syntax, or SBATCH scripting. Users who are not
familiar with the command line can select an application, configure inputs through a
simple form, and submit jobs directly from the GUI.

This guide walks through the complete workflow, from launching the application to
viewing job output.

---



## 1. Launch the HPC Applications Window

When the tool is opened, the **HPC Applications** home screen is displayed, showing all
the HPC applications installed and available on the system (e.g. GROMACS, LAMMPS, NAMD,
WRF, OpenFOAM, NWChem, CP2K, HMMER, MUMmer, HPL, Quantum-ESPRESSO, and more).

- Use the **Search** bar to quickly find an application or package by name.
- Click on any application tile to open its dedicated interface.

!!! tip "No terminal needed"
    Every button on this screen leads to a guided form — users never need to type a
    Linux command to get started.

---

<img src="../../image/hpcgui01.png" alt="alt">
<p style="text-align: center;">Figure - CDAC HPC-GUI Interface .</p> 


## 2. Select the Application

Click the tile of the required application (for example, **LAMMPS**) to open its
dedicated page.

Each application page displays:

- The application logo/branding
- A **Back** button to return to the applications list
- A **Search** box to search dependent packages
- Two selection panels: **Select Version** and **Select Interface**

---
<img src="../../image/hpcgui02.png" alt="alt">
<p style="text-align: center;">Figure - Selected Lammps.</p>  



## 3. Select the Version

The **Select Version** panel lists all the versions of the application that are
installed on the cluster (multiple versions may be available side-by-side, e.g.
different compiler/toolchain builds).

- Click on a version entry to select it.
- Selecting a version also allows the user to **view its dependencies** — the compiler,
  libraries, and packages that version was built against — so the correct build can be
  chosen for the job.

---

<img src="../../image/hpcgui03.png" alt="alt">
<p style="text-align: center;">Figure - Available Multiple version .</p>  


## 4. Select the Interface: Terminal or GUI

The **Select Interface** panel offers two ways to run the application:

| Option | Description |
|---|---|
| **Use Terminal** | Opens a terminal pre-loaded with the selected application/version (for advanced users who prefer the command line). |
| **Use GUI** | Opens a guided configuration **form** — recommended for users unfamiliar with the command line. |

Click **Use GUI** to continue with the form-based workflow.

---

<img src="../../image/hpcgui04.png" alt="alt">
<p style="text-align: center;">Figure - Select the GUI - Terminal Interface </p>

## 5. Configure the Job (Form Interface)

Selecting **Use GUI** brings up a configuration form where the user can set up the job
without writing any script manually. Typical fields include:

- **Input File** — browse and select the input file required by the application.
- **Output File Location** — choose the folder/path where results should be written.
- **Job Parameters** — resource options such as number of nodes, tasks/cores, walltime,
  partition/queue, and any application-specific run-time flags.

Once the required fields are filled in, the GUI automatically generates a valid
**SBATCH script** in the background based on the selections.

---

<img src="../../image/hpcgui06.png" alt="alt">
<p style="text-align: center;">Figure - GUI Interfeace Add Parameters And Input Files </p>

## 6. Preview and Edit the SBATCH Script

Before submission, the GUI displays a **Preview** of the auto-generated SBATCH script.

- Review the script to confirm resource requests, input/output paths, and module loads.
- The script can be **edited/altered manually** in the preview pane if any custom change
  is needed.
- Save the changes if edits were made.

!!! note
    This gives advanced users full control while still letting beginners rely on the
    auto-generated defaults.

---

<img src="../../image/hpcgui07.png" alt="alt">
<p style="text-align: center;">Figure - Check the preview and edit if required  and save.</p>

## 7. Submit the Job

Once satisfied with the script:

1. Click **Execute / Submit** to submit the job to the scheduler.
2. On successful submission, the GUI displays the **Job ID** assigned by the scheduler.

---


<img src="../../image/hpcgui08.png" alt="alt">
<p style="text-align: center;">Figure - Select output folder path and the Submit  </p>

## 8. Monitor Job Status

Using the displayed **Job ID**, the user can check the job status directly from the GUI.
The status indicator will show one of the following:

- **Running**
- **Completed**
- **Failed**

---

<img src="../../image/hpcgui09.png" alt="alt">
<p style="text-align: center;">Figure - JobID displayed and status can be verified </p>

## 9. View Output and Error Files

Once the job finishes, two buttons become available:

- **Output File** — opens/displays the standard output (`.out`) generated by the job.
- **Error File** — opens/displays the standard error (`.err`) log, useful for
  troubleshooting failed jobs.

---


<img src="../../image/hpcgui10.png" alt="alt">
<p style="text-align: center;">Figure - Ouput File  </p>


## 10. Visualize Support (If Application Supports)

For applications that support visualization (e.g. molecular dynamics or CFD tools):

1. Click the **Visualization** option.
2. Add/select the output file to be rendered.


---


<img src="../../image/hpcgui11.png" alt="alt">
<p style="text-align: center;">Figure - Visualisation tool </p>

## 11. Visualize Results

3. The built-in visualization tool launches and renders the output for analysis directly

<img src="../../image/hpcgui12.png" alt="alt">
<p style="text-align: center;">Figure - Rendered Visualization Result </p>


## Applicability

This workflow is uniform across **all HPC applications** listed on the home screen
(GROMACS, LAMMPS, NAMD, WRF, OpenFOAM, NWChem, CP2K, HMMER, MUMmer, HPL,
Quantum-ESPRESSO, etc.) — every application has its own GUI page following the same
Version → Interface → Configure → Submit → Monitor → Output/Visualize pattern, ensuring
a consistent, easy-to-use experience for users regardless of HPC/Linux expertise.
