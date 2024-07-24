# SwinSF: Image Reconstruction from Spatial-Temporal Spike Streams

Welcome to the **SwinSF** project! This repository contains the implementation of the **Swin Spikeformer (SwinSF)** model, as described in the paper ["Image Reconstruction from Spatial-Temporal Spike Streams"](http://arxiv.org/abs/2407.15708). SwinSF is designed to reconstruct high-quality images from spike streams generated by spike cameras, which are particularly useful for high-speed imaging where motion blur is a challenge.

## Table of Contents

- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Datasets](#datasets)
- [Training](#training)
- [Testing](#testing)
- [Model Weights](#model-weights)
- [Citation](#citation)


## Getting Started

### Prerequisites

Before you begin, ensure you have met the following requirements:
- Python 3.6.13
- PyTorch 1.10.0+cu113
- Other dependencies as listed in `requirements.txt`

You can install the required packages using pip:

```bash
pip install -r requirements.txt
```
### Datasets

To begin with the SwinSF project, you will need to download the datasets from Baidu Wangpan () to the datasets directory.

- **spike-reds**: A simulated dataset with ground truth, 250x400 pixels, from the paper "spk2imgnet".
- **spike-X4K**: A simulated dataset created for this project, with ground truth, 1000x1000 pixels.
- **spike-classA**: A dataset captured by a spike camera from the Peking University team, 250x400 pixels, without ground truth.

## Training

To train the SwinSF model on the reds dataset, use the following command:
```bash
python train.py --data_mode 250 --dataset_path ./datasets/spike_reds --device cuda:0
```
For the X4K dataset, use:
```bash
python train.py --data_mode 1000 --dataset_path ./datasets/spike_x4k --device cuda:0
```
To train using multiple GPUs, add the --device_ids 01 option (make sure the first device in device_ids matches the --device setting). For CPU training, simply use --device cpu.

Training weights will be automatically saved to the checkpoint directory.

## Testing

To test the model and save the reconstructed images for the reds dataset, use:
```bash
python test.py --data_mode 250 --dataset_path ./datasets/spike_reds --device cuda:0 --load_model /path/to/training/parameters --save_image True --save_path /path/to/save/images
```
For the X4K dataset:
```bash
python test.py --data_mode 1000 --dataset_path ./datasets/spike_x4k --device cuda:0 --load_model /path/to/training/parameters --save_image True --save_path /path/to/save/images
```
And for the classA dataset:
```bash
python test.py --data_mode 250 --dataset_path ./datasets/classA --device cuda:0 --load_model /path/to/training/parameters --save_image True --save_path /path/to/save/images
```

## Model Weights
We provide pre-trained weights for two resolutions, which can be downloaded from Baidu Wangpan(). Please note that the reds and classA datasets are not created by our team, so please contact the original authors to download them.

## Citation
If you find our work useful for your research, please consider citing our paper:
```
@article{jiang2024swinsf,
  title={Image Reconstruction from Spatial-Temporal Spike Streams},
  author={Jiang, Liangyan and others},
  journal={arXiv preprint arXiv:2407.15708},
  year={2024}
}
```