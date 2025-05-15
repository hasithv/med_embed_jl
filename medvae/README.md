# Using MedVAE for embedding medical images

## Installation
First, create a conda environment and install the required packages. Note, the 3.10 Python version is required for medvae.
```bash
conda create -n medvae-env python=3.10
conda activate medvae-env
pip install torch jupyter numpy matplotlib
```
Then, install the medvae package.
```bash
git clone https://github.com/StanfordMIMI/MedVAE.git`
cd MedVAE
pip install -e .
```

## Usage

