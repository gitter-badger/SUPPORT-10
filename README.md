<p align="center">
  <a href="http://nestjs.com/" target="blank"><img src="https://github.com/NICALab/SUPPORT/blob/main/logo-1.png" width="120" alt="SUPPORT Logo" /></a>
</p>

  <h3 align="center">SUPPORT, a self-supervised denoising method for voltage imaging data. </h3>

<p align="center">
<img alt="GitHub" src="https://img.shields.io/github/license/NICALab/SUPPORT">
<img alt="GitHub repo size" src="https://img.shields.io/github/repo-size/NICALab/SUPPORT">
<img alt="GitHub issues" src="https://img.shields.io/github/issues/NICALab/SUPPORT">
<img alt="GitHub Repo stars" src="https://img.shields.io/github/stars/NICALab/SUPPORT?style=social">
</p>

<p align="center"><a href="https://nicalab.github.io/SUPPORT/" target="_blank">Project page</a> | <a href="https://www.biorxiv.org/content/10.1101/2022.11.17.516709v1" target="_blank">Paper</a> | <a href="https://doi.org/10.5281/zenodo.7330257" target="_blank">Data</a>


<p align="center"><img src="thumbnail.png" width="80%"/></p>


## About SUPPORT
Here we present SUPPORT (**S**tatistically **U**nbiased **P**rediction utilizing s**P**ati**O**tempo**R**al information in imaging da**T**a), **a self-supervised denoising method** for **voltage imaging data**. SUPPORT is based on the insight that a pixel value in voltage imaging data is highly dependent on its spatially neighboring pixels in the same time frame even when its temporally adjacent frames do not provide useful information for statistical prediction. Such spatiotemporal dependency is captured and utilized to accurately denoise voltage imaging data in which the existence of the action potential in a time frame cannot be inferred by the information in other frames. We show, through simulation and experiments, that SUPPORT enables precise denoising of voltage imaging data while preserving the underlying dynamics in the scene. 

We also show that SUPPORT can be used for denoising **time-lapse fluorescence microscopy images** of Caenorhabditis elegans (C. elegans), in which the imaging speed is not faster than the locomotion of the worm, as well as **static volumetric images** of Penicillium and mouse embryos. SUPPORT is exceptionally compelling for denoising voltage imaging and time-lapse imaging data, and is even effective for denoising **calcium imaging data**.

For more details, please see the accompanying research publication "[Statistically unbiased prediction enables accurate denoising of voltage imaging data](https://www.biorxiv.org/content/10.1101/2022.11.17.516709v1)".

## System Requirements

### Hardware Requirements

`test_GUI` is designed to be run on a standard computer without large RAM. If the GPU is available, denoising process could be accelerated.

Starting with (Code) or running `train_GUI` require GPU with enough VRAM.

### Software Requirements

We tested on the following systems:

- Ubuntu 18.04
- Python 3.9
- Pytorch 1.13.0
- CUDA 11.7

## Installation

It could vary on your network speed, but the installation generally took less than 20 minutes.

1. Clone the repository
```
git clone git@github.com:NICALab/SUPPORT.git
```

2. Navigate into the cloned folder
```
cd ./SUPPORT
```

3. Create the conda environment
```
conda env create -f env.yml
```

4. Activate the conda environment
```
conda activate SUPPORT
```

5. Install Pytorch with **the version compatible with your OS and platform** from https://pytorch.org/get-started/locally/
```
conda install pytorch torchvision torchaudio pytorch-cuda=11.7 -c pytorch -c nvidia
```

## Getting Started (GUI)
**1. Denoise the data with pretrained networks**
```
python -m src.GUI.test_GUI
```
As the network is trained on different dataset of denoising,
for optimal performance, one might have to train the network.

For denoising data with size of (128, 128, 1200), it took about 30 seconds with one RTX 2080 Ti GPU.

**2. Train the network**

Will be updated soon.

## Getting Started (code)
**1. Train SUPPORT**
```
python -m src.train --exp_name mytest --noisy_data ./data/sample_data.tif --n_epochs 11 --checkpoint_interval 10
```
It will train a network using the sample data (For faster demo, the above code trains the network only for few iterations with small data).

For more options, please refer to the manual through the following code.
```
python -m src.train --help
```

**2. Inferece with SUPPORT**

After training the network, the trained model will be saved on `results/saved_models/mytest/model_X.pth`, where X is the epoch of training.

```
python -m src.test
```

It will save the denoised file on `results/images/mytest/denoised_X.tif`.

<div align="center"><img src="data/sample_data.png" width="20%"/><img src="data/denoised_10.png" width="20%"/></div>

Edit `src/test.py` file to change the path to infer with your own data and models.



## Data availability
Dataset for volumetric structured imaging of *penicillium* and calcium imaging of larval zebrafish can be downloaded from [Zenodo](https://doi.org/10.5281/zenodo.7330257).

## Contributors
We are happy to help any questions or requests.
Please contact to following authors to get in touch!
* Minho Eom (djaalsgh159@kaist.ac.kr)
* Seungjae Han (jay0118@kaist.ac.kr)

## Citation
Eom, M. et al. [Statistically unbiased prediction enables accurate denoising of voltage imaging data.](https://www.biorxiv.org/content/10.1101/2022.11.17.516709v1) Preprint at *bioRxiv* (2022).
```
@article {Eom2022SUPPORT,
	author = {Eom, Minho and Han, Seungjae and Kim, Gyuri and Cho, Eun-Seo and Sim, Jueun and Park, Pojeong and Lee, Kang-Han and Kim, Seonghoon and Rozsa, Marton and Svoboda, Karel and Choi, Myunghwan and Kim, Cheol-Hee and Cohen, Adam and Chang, Jae-Byum and Yoon, Young-Gyu},
	title = {Statistically unbiased prediction enables accurate denoising of voltage imaging data},
	elocation-id = {2022.11.17.516709},
	year = {2022},
	doi = {10.1101/2022.11.17.516709},
	publisher = {Cold Spring Harbor Laboratory},
	URL = {https://www.biorxiv.org/content/early/2022/11/18/2022.11.17.516709},
	eprint = {https://www.biorxiv.org/content/early/2022/11/18/2022.11.17.516709.full.pdf},
	journal = {bioRxiv}
}
```
