# Code for 'Microscopic imprints of learned solutions in adaptive resistor networks'
**Marcelo Guzman, Felipe Martins**, Menachem Stern, and Andrea J. Liu

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.14680897.svg)](https://doi.org/10.5281/zenodo.14680897)

arXiv reference: [arXiv:2412.19356](https://arxiv.org/abs/2412.19356)

## Notebooks
   - The notebook named 'networkTrainingExample_paper.ipynb' creates an adaptive resistor circuit - the corresponding network strucutre, conductances, task description, etc. - and examplifies the training of a circuit for a regression task where the voltages at the output nodes follow a particular, pre-specified linear relation on the inputs. The trained circuit is saved in three files: two json and one csv. The information about the network structure - nodes, edges - are saved in '*graph.json', while information along training and hyperparameters are saved in '*global.json.' Finally, the conductances recorded along trained are saved in the '*.csv' file.
   - The notebook named 'examplePlottingRoutines.ipynb' takes in trained adaptive resistor circuits from the three file types created by the learning routine. It then produces the different kinds of plot shown in the paper. The calculation of key quantities defined in the paper like the Cost Hessian and its eigenspectrum and susceptibility tensor are demonstrated. The physical hessian along with the calculation of the response of the network to a particular input is natively implemented in the source code developed for the learning routines. For information about the algorithmic implementation of Persistence Homology refered to in the paper, see Rocks et. al: https://doi.org/10.1103/PhysRevResearch.2.033234


## Setup of Repo for Adaptive Resistor Circuits

1.1. Preliminaries for macOS: Install miniforge
   - Download https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-MacOSX-arm64.sh
   - Run the script
   - Open another shell and run
     ```bash
     bash Miniforge3-MacOSX-arm64.sh
     ```
   - Get data.
   
1.2. Clone a local copy of the repository:

```bash
git clone git@github.com:ftmartins/code_microscopic_imprints.git
```

1.3. Create the environment. Follow one of these two options depending on your computer.
   - **For Intel chips:** The main directory contains an environment.yml file for easily setting up a conda environment, named microscopic_imprints_learning_circuit, with all the package dependencies:
     ```bash
     conda env create --file=environment-intel.yml
     ```
     To activate the environment, run
     ```bash
     conda activate cl
     ```
   - **For M1/M2 chips:** We have to build numpy with the accelerator. (:warning: this is constantly evolving. New OS will get rid of these tricks. If you encounter any problem, please create an issue.)
     ```bash
     conda env create --file=environment-M1-M2.yml
     ```
     Activate the environment, install numpy using pip and set the pip to be recognized by further package installations:
     ```bash
     conda activate cl
     ```
     ```bash
     pip install --no-binary :all: numpy==1.24.3 --no-cache-dir
     ```
     Once numpy installed, run
     ```bash
     conda config --set pip_interop_enabled true
     ```

     check that numpy is using vecLib:
     ```bash
     >>> import numpy
     >>> numpy.show_config()
     ```
     If everything is right, you should see info like ```/System/Library/Frameworks/vecLib.framework/Headers``` printed.
     Then install the higher level dependencies.
     ```bash
     pip install -r requirements.txt --no-cache-dir
     ```

     (for more information see: https://gist.github.com/MarkDana/a9481b8134cf38a556cf23e1e815dafb)
