# CS 598 - Deep Learning For Healthcare

This repository contains code, data, trained models, and results for the submission of team 57 (NetID's: austinw7, chp2, saxena9) for our course project.

## Original paper repository
https://github.com/sebbarb/time_aware_attention

## Environment
* Python Version: Python 3.11+
* Required Packages (no specific version requirements):
  * pandas
  * numpy
  * tqdm
  * torch
  * torchdiffeq
  * scipy
  * sklearn
  * tabulate

## Data
This project uses the MIMIC III dataset, specifically the following tables:
* ADMISSIONS
* CHARTEVENTS
* D_ITEMS
* DIAGNOSES_ICD
* ICUSTAYS
* OUTPUTEVENTS
* PATIENTS
* PRESCRIPTIONS
* PROCEDURES_ICD
* SERVICES

These tables are not uploaded to GH due to the requirement that only certified people should have access to it.  In addition to these tables, there are data sets generated by intermediate preprocessing steps before model training starts.  Some of those files are provided in this respository, but the larger files (> 25 MB) could not be uploaded here and can instead by generated upon running the code.  Lastly, a set of medical embeddings were provided in the original paper repository which are used to train three out of the 14 models referenced in the paper; those embeddings are in the data folder of this repository.

## Code
All code involved with preprocessing data sets, training, evaluating, and visualizing results are in the Jupyter notebook DL4H_Team_57.ipynb.  In order to run this notebook, the required packages must be installed and the MIMIC-III tables must be downloaded, uncompressed, and saved to a local directory in order to be used in the preprocessing steps, but other than that the notebook can be run in the order provided.  The notebook also contains a block of commented out invocations for training each model referenced in the original paper; these can be uncommented and run one by one, but are commented by default because the training output is provided in this repository and also because the training code takes much longer to run than any other part of the code.

## Trained Models
Information about trained models are in the /logdir directory of this repository.  Each model except for the baseline logistic regression has a subdirectory which contains a final_model.pt file which represents the trained model parameters and an epoch_times.npz file which contains information about runtime duration when training the model.  The final_model.pt file is used when evaluating the model against bootstrap samples.
Models trained are
* RNN (concatenated Δtime)
* RNN (concatenated Δtime) + Attention
* Attention (concatenated time)
* ODE + RNN + Attention
* ODE + Attention
* ODE + RNN    
* RNN (exp time decay) + Attention
* RNN (exp time decay)    
* RNN (ODE time decay)   
* RNN (ODE time decay) + Attention    
* MCE + RNN + Attention
* MCE + RNN
* MCE + Attention
* Logistic Regression

## Results
Evaluation results for each model are in the /results directory of this repository.  There is a pickle file for each model to capture the results that were collected for the full sample size. Each pickle file is used in the Jupyter notebook to display and compare against the original paper's findings in a nicely formatted table.
