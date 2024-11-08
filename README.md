# MASS

*MASS* is a deep learning framework for multi-species RNA modification analyses by integrating RNA modification data from multiple species. This is an instruction of predicting RNA modification using *MASS*.

## Dependencies

This repository has been tested on Ubuntu 16.04. We strongly recommend you to have [Anaconda3](https://www.anaconda.com/distribution/) installed, which contains most of required packages for running this model.

### Must installed packages or softwares

- tensorflow  1.8.0

- tensorlayer 1.10.1

- pandas 0.12.0

- [CD-HIT](http://weizhongli-lab.org/cd-hit/)

## Data Preparation

- Download complete data from the [RMBase 2.0](http://rna.sysu.edu.cn/rmbase/) or [ENSEMBL](http://www.ensembl.org), and unzip these data to `./data/YOUR_DATA_NAME`.
- You can preprocess your own data with `./src/pocessing_pipeline.py`, and move the processed data to `./data/YOUR_DATA_NAME`.
- For the training process, you should store positive samples in `data/YOU_DATA_NAME/positive_samples/train` and negative samples in `./data/YOUR_DATA_NAME/negative_samples/train`.

## Get Started

### Test with pre-trained models
- The trained multi-speices model were stored in `./checkpoint`
- You can run the script `./src/main.py` to generate prediction on test data, and the results will be stored in `./predict_result`. It will also report AUPRC and AUPR based on the given data and label. Sample code:
```bash
cd src
python main.py --name mass --data full_data --sn 8 --mode test --fold 0 --gpu 0
```
Noticed NEG_POS_RATIO have to be set at src/main.py (defult is neg:pos = 100:1), if all negative samples are tested then no more samples will be tested.

### Train new models

- You can also train mass with you own data:

```bash
cd src
python main.py --name mass --data full_data --sn 8 --mode train --gpu 0
```
## Utility files

*data2fa.py* is used to convert dataset into fasta format

*main.py* is the main function that has the following arguments:
 
 - --name: experiment name
 - --gpu: gpu id, currently MASS can only run on single GPU
 - --data: data source for trainning for 
 - --sn: number of species
 - --fold:  index for species in `./src/config.sample_names`

