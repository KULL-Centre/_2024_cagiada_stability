# _2024_cagiada_stability
# Predicting absolute protein folding stability using generative models

This repository contains Python code, [Jupyter](http://jupyter.org) Notebooks and used data for reproducing the work of the scientific paper `Predicting absolute protein folding stability using generative models` by M. Cagiada, S. Ovchinnikov and K. Lindorff-Larsen, 2023, biorxiv (1): 1–13. [https://doi.org/](https://doi.org/).

## Layout
- `stab_ESM-IF.ipynb` Jupyter Notebook to generate new stability prediction, it can be run using the Google Colaboratory system.
- `PAPER SI` Folder with all the data, notebook and figures used in the current version of the manuscript. The data are collected in different folders, describing which experimental dataset they are referrint to:
  - `exp_scores` folder with experimental data from Tsuboyama,2023 and Maxwell,2005.
  - `figures_SI` folder with the raw plots and figures generated via the pred_dG_SI notebook.
  - `fraser2009` folder with input structures and predictions for proteins from Fraser, et al. (2009).
  - `gruszka2015` folder with input structures and predictions for proteins from Gruszka, et al. (2015).
  - `maxwell2005` folder with input structures and predictions for proteins from Maxwell, et al. (2005).
  - `mello2004` ffolder with input structures and predictions for proteins from Mello, et al. (2004).
  - `non_2states_proteins` folder with input structures and predictions for non-two states folding proteins from the ProTherm DB.
  - `tsuboyama2023` folder with input structures and predictions for proteins from Tsuboyama, et al. (2023).
  - `wang2016` folder with input structures and predictions for proteins from Wang, et al. (2016).
  - `dG_pred_SI.ipynb` jupyter notebook to reproduce all the analysis and figures used in the manuscript

**N.B.: due to the large size of the dataset the Tsuboyama,2023 experimental results are not included in the Github repository, if you wish to download the dG_pred_notebook, please download the data from the [manuscript SI](https://www.nature.com/articles/s41586-023-06328-6) zenodo repository and move the `Tsuboyama2023_Dataset2_Dataset3_20230416.csv` file into the exp_score folder**
    
## Functional Model Notebook
### Usage
To run the Prediction Colaboratory Notebook, we suggest to open it in [Google Colaboratory](https://colab.research.google.com/), it can be open clicking [here](https://colab.research.google.com/github/KULL-Centre/_2022_functional-sites-cagiada/blob/main/Functional_site_model.ipynb).
To run the Notebook is necessary to follow different steps:
1 Run the cells with the PRELIMINARY OPERATIONS prefix, this will install all the dependencies and load the required functions to run the predictor.
2 Upload all the structure and additional information in the `DATA UPLOADING` cell. Specifically in required to:
  - set up a job name
  - upload an input structure (via download from AF2 DB or uploading from local storage).
  - add an alternative sequence for you target fold (optional). 
3 Run the `MODEL RUN` cell to return a absolute stability prediction. Fow a new prediction, the `PRELIMINARY OPERATIONS` must not be re-run and the new prediction is produced by simply  loading the new target protein information in the `DATA UPLOADING` cell and run the model again.
5 Run the cell `DOWNLOAD RESULTS`  to collect and download all the files produced during the current session.

### Input requirements:

- The input structure should be a predicted structure from AlphaFold2 if possible. This is necessary to ensure maximum prediction quality as ESM-IF has been trained using the backbone from AlphaFold2.

- The maximum size of proteins that can be used in the ESM-IF Colab implementation is 1023 residues, larger proteins cannot be treated at the moment.
  
-If an alternative sequence is provided, its length must match the length of the structure sequence.

### Output:

When a prediction is complete, the files associated with the run are stored in the `/content/outputs` folder. When the `DOWNLOAD RESULTS` cell is executed, all files are downloaded at once.

The output files stored for each run are
- the pdb used as input
- the fasta file of the query sequence
- the prediction output file

The output files will be label using the chosen `jobname`.

### Prediction file Format

The output csv file consists of two columns, where the wild-type amino acid probability for each position is reported, and then at the bottom both the $\Delta G$ as the sum of the wild-type probabilities and in kcal/mol are reported.
\\

>OUTPUT FILE EXAMPLE:

>For a target protein with 45 residues, the scores file should be formatted like this:

>Residue  Likelihood

>M1               0.4  
A2                0.2
D3                0.3  
C5                0.9   
..  
..  
Y45               0.3
dG_IF       201
dG_kcalmol  13

### Extra
#### License:

The source code and model's parameters are licensed under the permissive Apache Licence, Version 2.0.

#### Bugs:

For any bugs please report the issue on the project [Github](https://github.com/KULL-Centre/_2022_functional-sites-cagiada) or contact one of the listed authors in the connected [manuscript](https://doi.org/10.1038/s41467-023-39909-0).

#### Citing this work:

If you use our model please cite:

Cagiada, Matteo, Sergey Ovchinnikov, and Kresten Lindorff-Larsen. 2023. “Discovering Functionally Important Sites in Proteins.” Nature Communications 14 (1): 1–13. https://doi.org/10.1038/s41467-023-39909-0.
```

@ARTICLE{Cagiada2024-pe,
  title     = "Predicting absolute protein folding stability using generative models",
  author    = "Cagiada, Matteo and Ovchinnikov, Sergey and Lindorff-Larsen, Kresten",
  journal   = "",
  publisher = "",
  volume    =  ,
  year      =  2024,
  language  = "en"
}

```
