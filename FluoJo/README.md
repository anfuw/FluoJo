# FluoJo: 3D Spatial Gating & Z-Correction Tool

An interactive Python, Panel, and Bokeh-based toolkit for the spatial quantification and gating of Cellpose masks from whole-mount embryo imaging. 

Inspired by traditional flow cytometry analysis but built for immunofluorescence data, FluoJo processes 3D Cellpose masks to threshold immunofluorescence and select cells in an interactive workspace with real-time 3D display of cell selection.

## Features
1. **Z-Depth Intensity Correction:** Automatically uses a robust Huber Regressor to correct for fluorescence signal attenuation deep within tissue (Z-axis scattering).
2. **Interactive 2D/3D Gating:** A Jupyter-based interactive dashboard to draw lasso/polygon gates on 2D feature plots. Gatings can be saved for further sub-gating.
3. **Live 3D Mapping:** Selections made in 2D plots are instantly projected onto a 3D map (Centroid X, Y, Z) of the tissue.
4. **Co-positivity Tracking:** Automatically calculates subset overlaps and outputs detailed analysis CSVs alongside bundled interactive HTML layouts of your workspace.

## Installation

We recommend using [Miniconda](https://docs.conda.io/en/latest/miniconda.html) or Anaconda to manage dependencies.

1. Clone this repository to your local machine:
   ```bash
   git clone https://github.com/anfuw/FluoJo.git
   cd FluoJo
   ```

2. Create the required environment from the provided .yml file:
   ```bash
   conda env create -f environment.yml
   ```

3. Activate the environment:
   ```bash
   conda activate fluojo-env
   ```

## Usage

1. Prepare Your Data
Ensure your Cellpose output files are placed in a folder named Cellpose_output in the root directory.
The script expects pairs of files with the following suffixes by default:

   corrected.csv

   proce3Dflow__cellposed_filtered_cp_masks.tif

You can change the the input folder name and pairs of file suffixes as you wish and modify the notebook/script accordingly.

2. Run the Z-Correction Preprocessing
Open notebooks/01_prep_cellpose_csv.ipynb. This notebook will read your raw summary CSVs, apply the Huber Regressor to correct for Z-depth decay, and save new _corrected.csv files into your data directory.
Note that you would need to modify this script for your customised inputs, and make sure that output files have the same suffix as you specify in the 02_FluoJo-bokeh.ipynb. By default, this will be 'corrected.csv'.

3. Launch the FluoJo Dashboard
Open notebooks/02_FluoJo_dashboard.ipynb. Run the cells to launch the Panel interface.

Select your pre-processed file pair from the dropdown.

Add 1D or 2D plots to define populations.

Save your gates and export the layout to generate a summary CSV and an interactive HTML report in the interactive_quantification_results/ folder.