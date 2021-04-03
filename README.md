# Rodents Whole Brain fMRI Data Preprocessing Toolbox
This pipeline has been tested on 4 different fMRI whole brain group datasets of rodents with different imaging protocols and experimental conditions (3 rats groups and 1 mice group) to obtain reasonable FC maps and QPPs.

## I. Prerequisite software
1. FSL5.0, AFNI and ANTs--can be installed on a PC by following "SoftwareInstallation_fsl_afni_ants.txt"
2. PCNN3d toolbox in Matlab (optional for mice brain preprocessing, see below for details). 

## II. Main Pipeline
### Step1: run "PreprocessingScript_step1.sh"
#### 1. Slice time correction: optional for long TRs (e.g., TR>=1s)
#### 2. Motion correction: (motions are corrected to its mean)
    Generate 3 plots in each data folder, "EPI_mc_rot.png", "EPI_mc_trans.png", and "EPI_mc_disp.png". 
    One can use these 3 plots as a quality control of motions during the imaging session.
#### 3. Distortion correction using fsl topup: 
    a. Relign 1 reverse EPI scan to the 1st volume of the forward EPI data 
    b. Estimate the topup correction parameters (see the required topup parameter files in 3 below) 
    c. Apply topup correction
#### 4. Brain extraction: using fsl bet command    
### Step2: edit the extracted brain using fsleyes editing tool
    (optional) For the mouse data, the PCNN3d might do better job than `fsl bet` function in Step 1. One can run PCNN3d in Matlab for the mouse brain preprocessing. Then you can pick the best extrated brain for manual editing.
### Step3: run "PreprocessingScript_step2.sh"

## III. Data Folder 
Two data samples are provided, one for rat (./data_rat/) and one for mouse (./data_mouse/).

## IV. Library Folder 
### ./lib/tmp/: Templates
### ./lib/topup/: Topup parameter files
#### 1. Imaging acquisition parameter file, "datain_topup_\*.txt":   
The parameters totally depend on your imaging acquisition protocal (see [Ref](https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/topup/TopupUsersGuide#A--datain)). It's IMPORTANT to setup the correct parameters, as they significantly impact the final results. Two files are provided here, "datain_topup_mice.txt" for the mouse data sample, and "datain_topup_rat.txt" for the rat data sample.
#### 2. Image parameter configuration file, "\*.cnf": 
    b02b0.cnf: a generally applicable (default) configration file provided by fsl 
    EPI_topup_mice.cnf: a configration file optimized for the mouse data "data_mouse"
    EPI_topup_rat.cnf: a configration file optimized for the mouse data "data_rat"
The above 3 "\*.cnf" files are provided in the ./lib/topups/ folder. These parameters totally depend on your image (e.g., dimension, resolution, etc). 
  




