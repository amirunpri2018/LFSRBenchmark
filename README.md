# LFSRBenchmark
An code integration and processed data collection for light field super-resolution resources with the benchmark paper [Light Field Super-Resolution: A Benchmark](http://openaccess.thecvf.com/content_CVPRW_2019/html/NTIRE/Cheng_Light_Field_Super-Resolution_A_Benchmark_CVPRW_2019_paper.html) (CVPRW2019).

## Datasets

We select two datasets that are widely used in light field researches for the benchmark evaluation.

1. The HCI dataset [1], it is a synthetic dataset synthesized by graphic software. Our used data is an early version of their public dataset which can't be found in their website. But you can download this repository for usage with referring to */data*.
2. The EPFL dataset [2], it is a real-world dataset captured by Lytro Illum camera. Due to the vignetting effect, we make a further rectification after calibration with the [Light Field Toolbox for MATLAB](http://dgd.vision/Tools/LFToolbox/). The rectification can be found in our supplementary document.

## Codes

We select four representative light field SR methods from three categories described in Related Work. Among them, GB [3] and RR [4] are implemented with the official codes while PRO [5] and LFCNN [6] are implemented by ourselves. Single image super resolution method VDSR [7] is also implemented by ourselves.

If you want to test these algorithms with other datasets, you can just change the data directories to your data directory.

### GB

GB is a graph-based framework for light field super-resolution. The official code can be found at [GB-official-code](https://github.com/rossimattia/light-field-super-resolution).

#### Requirements and dependencies

- MATLAB

#### Run

You can simply run the code in the MATLAB command window with the following commands:

```matlab
cd GB
graph_based_SR_on_EPFL
```

The above script can also be executed with the Run button in MATLAB edit mode. You can increase the parameter *poolSize* in the script graph_based_SR.m to accelerate the running. If your CPU resource is limited, you can decrease the pool size as well.

For more details about the code, we recommend you to the official code.

### RR

RR is a learning-based light field SR method with Principal Component Analysis (PCA) and Ridge Regression (RR). The official code can be found at [RR-official-code](https://github.com/rrfarr/LF-Editing).

#### Requirements and dependencies

- MATLAB

#### Run

You can simply run the code in the MATLAB command window with the following commands:

```matlab
cd RR
pca_rr_bm_for_EPFL
```

The above script can also be executed with the Run button in MATLAB edit mode. For more details, we recommend you to the comments inside the codes as well as the README file of the official code repository.

### PRO

PRO is a projection-based light field super-resolution method. The method is originated from [5] and implemented by ourselves.

#### Requirements and dependencies

- MATLAB

#### Run

You can simply run the code in the MATLAB command window with the following commands:

```matlab
cd PRO
projection_based_SR_on_EPFL_scale2
```

We recommend to run this script on Windows. With Linux OS such as Ubuntu, the script will get stuck due to some unknown configuration problems. The above script is used for scale 2, if you want to upsample the light field with scale 3, you should change the function *sr_projection_scale2* to *sr_projection_scale3*. Note that the input parameters of these two functions are not exactly the same, please pay some attention.

For the details of the implementation, please refer to the code or our supplementary document.

### LFCNN

LFCNN is the first CNN-based method which is published in ICCVW2015. The original LFCNN uses SRCNN structure as their backbone model, we upgrade the shallow SRCNN structure to the deep VDSR structure, which promotes LFCNN's performance for a fair comparison with single image VDSR.

#### Requirements and dependencies

- Caffe 1.0
- CUDA and Cudnn suited for Caffe 1.0
- MATLAB with pre-compiled matcaffe

#### Train

Please use the code under folder *data_generation* for test and training data generation at first. Then please change the directory for snapshots, logs, data path and the executable caffe tool in corresponding files in the directory *training_configs*.

#### Test

The test code is *LFCNN/test_code/test_LFCNN_to_whole_LF.m*, please change the folder path of matcaffe to your path and run the script in MATLAB command window.

#### Tips

Note that we used two relatively small datasets for training and testing, so we used Cross-Validation strategy. With more training data, LFCNN can achieve better performance.

### VDSR

VDSR is a representative CNN-based single image SR method without using any angular information. We train the network using the same training set as in [7]. The official code is implemented with MatConvNet, we implement it with Caffe 1.0.

#### Requirements and dependencies

- Caffe 1.0
- CUDA and Cudnn suited for Caffe 1.0
- MATLAB with pre-compiled matcaffe

#### Train

Please use the code under folder *data_generation* for test and training data generation at first. Then please change the directory for snapshots, logs, data path and the executable caffe tool in corresponding files in the directory *training_configs*.

#### Test

The test code is *VDSR/test_code/test_VDSR_whole_LF.m*, please change the folder path of matcaffe to your path and run the script in MATLAB command window.

## Reference

[1] S. Wanner, S. Meister, and B. Goldlucke. Datasets and benchmarks for densely sampled 4d light fields. In International Symposium on Vision Modeling and Visualization, 2013.

[2] M. Rerabek and T. Ebrahimi. New light field image dataset. In International Conference on Quality of Multimedia Experience (QoMEX), 2016.

[3] M. Rossi and P. Frossard. Graph-based light field super-resolution. In MMSP, 2017.

[4] R. A. Farrugia, C. Galea, and C. Guillemot. Super resolution of light field images using linear subspace projection of patch-volume. IEEE Journal of Selected Topics in Signal Processing, 11(7):1058-1071, 2017.

[5] C.-K. Liang and R. Ramamoorthi. A light transport framework for lenslet light field cameras. ACM Transactions on Graphics, 34(2):16:1-16:19, 2015.

[6] Y. Yoon, H. G. Jeon, D. Yoo, J. Y. Lee, and I. S. Kweon. Learning a deep convolutional network for light-field image super-resolution. In ICCVW, 2015.

[7] J. Kim, J. Kwon Lee, and K. Mu Lee. Accurate image super-resolution using very deep convolutional networks. In CVPR, 2016.

The citation of our benchmark paper:

```latex
@InProceedings{Cheng_2019_CVPR_Workshops,
author = {Cheng, Zhen and Xiong, Zhiwei and Chen, Chang and Liu, Dong},
title = {Light Field Super-Resolution: A Benchmark},
booktitle = {The IEEE Conference on Computer Vision and Pattern Recognition (CVPR) Workshops},
month = {June},
year = {2019}
}
```




