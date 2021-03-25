# Dual-Channel Combiner Network (DCCN)

## Input data
The 100 files in BOX (``EX_NLA_SEC_Analysis(ASA)/Dialysis/data/dataset_preprocess/``).

## Steps
* Put the input 100 files in ``data/``.
* Run ``prep.py`` to preprocess the data.
* Run ``train.py`` to train the model, and generate figures of the results (``fig/``).
* Run ``train_std.py`` to train the model multiple times, and generate average results with standard deviations.

## Setting
* Random / temporal scenario: ``train.py`` (line 94) and ``train_std.py`` (line 90).
* window size: ``train.py`` (line 33) and ``train_std.py`` (line 33).
* training ratio: ``train.py`` (line 34) and ``train_std.py`` (line 34).

## Parameters
Set model parameters at lines 25 - 32 in ``train.py`` and ``train_std.py``:
* hiddims_temp: dimensions of the hidden representations of the temporal channel
* hiddims_stat: dimensions of the hidden representations of the static channel
* dropout_rate: drop out rate
* lr: learning rate
* epochs: total number of epochs
* batchsz: batch size
* lmd: a hyperparameter that controls the regularization on model parameters
* runtime: the number of runs of the algorithm

## Model input format
* x_temp: shape=(batch, len, dim_temp), batch is the batch size, len is the maximal length of sequence, dim_temp is the dimensionality of temporal features
* x_temp_len: shape=(batch,), each value is the actual length of each sequence
* x_stat: shape=(batch, dim_stat), dim_stat is the dimensionality of the static features

## Model output format
* logit: shape=(batch, 1), each value is the prediction on the event at next time step, if sigmoid is on, each value is a probability (line 219 in ``model.py``)

## Requirement
* matplotlib==3.0.2
* numpy==1.17.4
* pandas==0.23.0
* scikit-learn==0.21.3
* sklearn==0.0
* torch==1.3.0
