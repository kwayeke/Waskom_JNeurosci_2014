# Analysis repository for Waskom et al. (2014) J Neurosci

This repository contains code for the manuscript

Waskom, M.L., Kumaran, D., Gordon, A.M., Rissman, J., Wagner, A.D. (2014) Frontoparietal representations of task context support the flexible control of goal-directed cognition. *Journal of Neuroscience*. 

The code is contained within several IPython notebooks that performed the analyses and generated all figures used in the manuscript.

Authors
-------

- Michael L. Waskom
- Dharshan Kumaran
- Alan M. Gordon
- Jesse Rissman
- Anthony D. Wagner

Preprocessing
-------------

Two processing steps were performed outside the scope of the notebooks. First,
the anatomical image for each subject was processed using Freesurfer to
generate the cortical surface models. Specifically, the following command line
was used for each subject:

    recon-all -s $subject -all -3T

Additionally, the functional data were preproccesed with FSL, Freesurfer, and
Nipype using [lyman](http://stanford.edu/~mwaskom/software/lyman). The
processing used the experiment parameters in the `dksort.py` file included in
this repository and was performed with the following command line:

    run_fmri.py -s subjects.txt -w preproc reg -t -reg epi -unsmoothed

Once those commands have been executed, every analysis can be generated using
these notebooks.

Software Versions
-----------------

The versions of all Python packages that were installed when these analyses
were performed are contained in the `dependencies.txt` file.

To facilitate reproduction of these results, the minimum set of required
packages are contained in the `conda_requirements.txt` and
`pip_requirements.txt` files. These can be used to set up an analysis
environment using `conda` and `pip` respectively. Please note that an effort
was made for accuracy, but these files were created after the bulk of the
analyses had been run and cached.

Other software versions are recorded here:

### MRI Processing

- **Freesurfer**: 5.3
- **FSL**: 5.0

### R Packages

- **R**: 3.0.2
- **lme4**: 0.999999-2

### Lyman

Two different git snapshots of lyman correspond most directly to the analyses.

- [Preprocessing using `run_fmri.py`](https://github.com/mwaskom/lyman/tree/d1c4604bbc7973550175a7eaf1885ebb45774082)
- [Decoding analyses using `lyman.mvpa`](https://github.com/mwaskom/lyman/tree/983c721824d31859383c3b5c5b64569af2f8130e)


Analysis Notebooks
------------------

To reproduce the analyses in the manuscript, the notebooks should be executed
in the following order.

### Mask_Generation.ipynb

[Link to static notebook](http://nbviewer.ipython.org/github/WagnerLabPapers/Waskom_JNeurosci_2014/blob/master/Mask_Generation.ipynb)

Using the label files in `roi/`, warp the ROIs from group space to individual
subject sufaces and write binary masks in functional space.

### Event_Info_Generation.ipynb

[Link to static notebook](http://nbviewer.ipython.org/github/WagnerLabPapers/Waskom_JNeurosci_2014/blob/master/Event_Info_Generation.ipynb)

Read the `.mat` files generated by PsychToolBox and create

- a master `.csv` file with behavioral and design information and

- specific event files for the decoding analyses.

### Design_Figure.ipynb

[Link to static notebook](http://nbviewer.ipython.org/github/WagnerLabPapers/Waskom_JNeurosci_2014/blob/master/Design_Figure.ipynb)

This notebook generates the experimental design figure in the manuscript.

### ROI_Figure.ipynb

[Link to static notebook](http://nbviewer.ipython.org/github/WagnerLabPapers/Waskom_JNeurosci_2014/blob/master/ROI_Figure.ipynb)

This notebook generates the ROI figure in the manuscript. Unlike the other
notebooks, it requires [PySurfer](http://pysurfer.github.io).

### Behavioral_and_Decoding_Analyses.ipynb

[Link to static notebook](http://nbviewer.ipython.org/github/WagnerLabPapers/Waskom_JNeurosci_2014/blob/master/Behavioral_and_Decoding_Analyses.ipynb)

All of the actual analyses are contained within this notebook.

### Searchlight_Analysis.ipynb

[Link to static notebook](http://nbviewer.ipython.org/github/WagnerLabPapers/Waskom_JNeurosci_2014/blob/master/Searchlight_Analysis.ipynb)

The searchlight analysis is performed separately within this notebook and the
`process_searchlight.py` script.

Other Data
----------

### rois/

Freesurfer `.label` files defining the ROIs in common surface space. These
labels were created from files distributed by
[Freesurfer](http://ftp.nmr.mgh.harvard.edu/fswiki/CorticalParcellation_Yeo2011).

### figures/

Figures that are output by these notebooks.

### project.py

The lyman project file that was used to process the data.

### dksort.py

The lyman experiment file for preprocessing the fMRI data.

### subjects.txt

The subject codes used in the processing.

### dependencies.txt

A pip dependencies file that can be used to install a virtual environment with
software versions that were used for these analyses.

License 
-------

The code in this notebook is under a BSD (3-clause) license.
