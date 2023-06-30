## Overview
The fifth-generation Tencent Cloud CVM instances (including  S6, S5, M5, C4, IT5, D3, etc.) all come with the 2nd generation Intel<sup>®</sup> Xeon<sup>®</sup> scalable processor Cascade Lake. These instances provides more instruction sets and features, which can accelerate the artificial intelligence (AI) applications. The integrated hardware enhancement technology, like Advanced Vector Extensions 512 (AVX-512), can boost the parallel computing performance for AI inference and produce a better deep learning result.

This document describes how to use AVX-512 on S5 and M5 CVM instances to accelerate AI application.

## Recommended Models[](id:RecommendedSelection)
Tencent Cloud provides various types of CVMs for different application development. The [Standard S6](https://intl.cloud.tencent.com/document/product/213/11518)、[Standard S5](https://intl.cloud.tencent.com/document/product/213/11518) and [Memory Optimized M5](https://intl.cloud.tencent.com/document/product/213/11518) instance types come with the 2nd generation Intel<sup>®</sup> Xeon<sup>®</sup> processor and support Intel<sup>®</sup> DL Boost, making them suitable for machine learning or deep learning. The recommended configurations are as follows:
<table>
<tr>
<th>Scenario</th><th>Instance Specifications</th>
</tr>
<tr>
<td>Deep learning training platform</td>
<td>84vCPU Standard S5 or 48vCPU Memory Optimized M5</td>
</tr>
<tr>
<td>Deep learning inference platform</td>
<td>8/16/24/32/48vCPU Standard S5 or Memory Optimized M5</td>
</tr>
<tr>
<td>Deep learning training or inference platform</td>
<td>48vCPU Standard S5 or 24vCPU Memory Optimized M5</td>
</tr>
</table>

 ## Advantages
Running the workloads for machine learning or deep learning on Intel<sup>®</sup> Xeon<sup>®</sup> scalable processors has the following advantages:
- Suitable for processing 3D-CNN topologies used in scenarios such as big-memory workloads, medical imaging, GAN, seismic analysis, gene sequencing, etc.
- Flexible core support simply using the `numactl` command, and applicable to small-scale online inference.
- Powerful ecosystem to directly perform distributed training on large clusters, without the need for a large-scale architecture containing additional large-capacity storage and expensive caching mechanisms.
- Support for many workloads (such as HPC, BigData, and AI) in a single cluster to deliver better TCO.
- Support for SIMD acceleration to meet the computing requirements of various deep learning applications.
- The same infrastructure for direct training and inference.

## Directions
### Creating an instance
Create an instance as instructed in [Creating Instances via CVM Purchase Page](https://intl.cloud.tencent.com/document/product/213/4855). Select a [recommended model](#RecommendedSelection) that suits your actual use case.
![](https://main.qcloudimg.com/raw/ceb104790caba9f281f4515f00d32585.png)

>?For more information on instance specifications, see [Instance Types](https://intl.cloud.tencent.com/document/product/213/11518).

### Logging in to the instance
1. [Log in to a Linux instance using standard login method](https://intl.cloud.tencent.com/document/product/213/5436).

### Deploying a platform
Deploy an AI platform as instructed below to perform the machine learning or deep learning task:
<dx-accordion>
::: Sample 1: optimizing the deep learning framework TensorFlow* with Intel<sup>®</sup>
PyTorch and IPEX on the 2nd generation Intel <sup>®</sup> Xeon<sup>®</sup> scalable processor Cascade Lake will automatically optimize AVX-512 instructions to maximize the computing performance.

TensorFlow\* is a widely-used large-scale machine learning and deep learning framework. You can improve the instance training and inference performance as instructed in the sample below. More information about the framework, see [Intel<sup>®</sup> Optimization for TensorFlow\* Installation Guide](https://software.intel.com/content/www/us/en/develop/articles/intel-optimization-for-tensorflow-installation-guide.html). Follow these steps:

#### Deploying the TensorFlow\* framework
1. Install Python in the CVM instance. This document uses Python 3.7 as an example.
2. Run the following command to install the Intel<sup>®</sup> optimized TensorFlow\* intel-tensorflow.
<dx-alert infotype="explain" title="">
The **version 2.4.0 or later** is recommended to obtain the latest features and optimization.
</dx-alert>
```
pip install intel-tensorflow
```

#### Setting runtime parameters
Choose one of the following two runtime interfaces to optimize runtime parameters as needed. For more information about the optimization settings, see [General Best Practices for Intel<sup>®</sup> Optimization for TensorFlow](https://github.com/IntelAI/models/blob/master/docs/general/tensorflow/GeneralBestPractices.md).
 - **Batch inference**: measures how many input tensors can be processed per second with batches of size greater than one. Typically, for batch inference, optimal performance is achieved by exercising all the physical cores on a CPU socket.
 - **On-line Inference**: (also called real-time inference) is a measurement of the time it takes to process a single input tensor, i.e. a batch of size one. In a real-time inference scenario, optimal throughput is achieved by running multiple instances concurrently.

Follow the steps below:
1. Run the following command to obtain the number of physical cores in the system.
```
lscpu | grep "Core(s) per socket" | cut -d':' -f2 | xargs
```
2. Set the optimization parameters using either method:
 - Set the runtime parameters. Add the following configurations in the environment variable file:
``` 
 export OMP_NUM_THREADS= # <physicalcores>
 export KMP_AFFINITY="granularity=fine,verbose,compact,1,0"
 export KMP_BLOCKTIME=1
 export KMP_SETTINGS=1
 export TF_NUM_INTRAOP_THREADS= # <physicalcores>
 export TF_NUM_INTEROP_THREADS=1
 export TF_ENABLE_MKL_NATIVE_FORMAT=0
```
 - Add the environment variables to codes. Add the following configurations to the running Python codes.
```
import os
os.environ["KMP_BLOCKTIME"] = "1"
os.environ["KMP_SETTINGS"] = "1"
os.environ["KMP_AFFINITY"]= "granularity=fine,verbose,compact,1,0"
if FLAGS.num_intra_threads > 0:
    os.environ["OMP_NUM_THREADS"]= # <physical cores>
os.environ["TF_ENABLE_MKL_NATIVE_FORMAT"] = "0"
config = tf.ConfigProto()
config.intra_op_parallelism_threads = # <physical cores>
config.inter_op_parallelism_threads = 1
tf.Session(config=config)
```

#### Running inference on the TensorFlow\* deep learning model
Run inference on other machine learning or deep learning models as instructed in [Image Recognition with ResNet50, ResNet101 and InceptionV3](https://github.com/IntelAI/models/blob/master/docs/image_recognition/tensorflow/Tutorial.md). This document describes how to run inference benchmark with ResNet50. For more information, see [ResNet50 (v1.5)](https://github.com/IntelAI/models/blob/master/benchmarks/image_recognition/tensorflow/resnet50v1_5/README.md).

#### Training on the TensorFlow\* deep learning model
This document describes how to run training benchmark with ResNet50. For more information, see [FP32 Training Instructions](https://github.com/IntelAI/models/blob/master/benchmarks/image_recognition/tensorflow/resnet50v1_5/README.md#fp32-training-instructions).

#### TensorFlow performance

The performance data is as shown in [Improving TensorFlow* Inference Performance on Intel® Xeon® Processors](https://www.intel.com/content/www/us/en/artificial-intelligence/posts/improving-tensorflow-inference-performance-on-intel-xeon-processors.html), which may slightly vary according to the models and actual configurations.
 - **Latency performance**:
    We tested models of image classification and object detection at batch size one, and found improved inference performance of Intel Optimization for TensorFlow with AVX-512 instructions against the non-optimized version. For example, the latency performance of optimized ResNet 50 is reduced to 45% of the original version.
 - **Throughput performance**:
    We tested models of image classification and object detection for throughput performance at large batch size, and found significant improvements. The throughput performance of optimized ResNet 50 is increased to 1.98 times of the original version.
:::
::: Sample 2: deploying the learning framework PyTorch*
#### Deployment directions
1. Install Python 3.6 or a later version in the CVM instance. This document uses Python 3.7 as an example.
2. Compile and install PyTorch and Intel<sup>®</sup> Extension for PyTorch (IPEX) as intructed in [Intel<sup>®</sup> Extension for PyTorch](https://github.com/intel/intel-extension-for-pytorch#installation).

#### Setting runtime parameters

PyTorch and IPEX on the 2nd generation Intel <sup>®</sup> Xeon<sup>®</sup> scalable processor Cascade Lake will automatically optimize AVX-512 instructions to maximize the computing performance.

Follow these steps to configure the runtime parameter optimizations. For more information on configurations, see [Maximize Performance of Intel® Software Optimization for PyTorch* on CPU](https://software.intel.com/content/www/us/en/develop/articles/how-to-get-better-performance-on-pytorchcaffe2-with-intel-acceleration.html).
 - **Batch inference**: measures how many input tensors can be processed per second with batches of size greater than one. Typically, for batch inference, optimal performance is achieved by exercising all the physical cores on a CPU socket.
 - **On-line Inference**: (also called real-time inference) is a measurement of the time it takes to process a single input tensor at batch size one, i.e. a batch of size one. In a real-time inference scenario, optimal throughput is achieved by running multiple instances concurrently.

Follow the steps below:

1. Run the following command to obtain the number of physical cores in the system.
```
lscpu | grep "Core(s) per socket" | cut -d':' -f2 | xargs
```
2. Set the optimization parameters using either method:
 - Use GNU OpenMP* Libraries to set the runtime parameters. Add the following configurations in the environment variable file:
``` 
export OMP_NUM_THREADS=physicalcores
export GOMP_CPU_AFFINITY="0-<physicalcores-1>"
export OMP_SCHEDULE=STATIC
export OMP_PROC_BIND=CLOSE
```
 - Use Intel OpenMP* Libraries to set the runtime parameters. Add the following configurations in the environment variable file:
``` 
export OMP_NUM_THREADS=physicalcores
export LD_PRELOAD=<path_to_libiomp5.so>
export KMP_AFFINITY="granularity=fine,verbose,compact,1,0"
export KMP_BLOCKTIME=1
export KMP_SETTINGS=1
```


#### Inference and training optimizations in the PyTorch* deep learning model

- Use Intel<sup>®</sup> Extension for PyTorch to improve performance of the model inference. The sample codes are as follows:
```
import intel_pytorch_extension
...
net = net.to('xpu')       # Move model to IPEX format
data = data.to('xpu')     # Move data  to IPEX format
...
output = net(data)        # Perform inference with IPEX
output = output.to('cpu') # Move output back to ATen format
```
- Both inference and training can use jemalloc to improve performance. jemalloc is a general-purpose `malloc(3)` implementation that emphasizes fragmentation avoidance and scalable concurrency support. It is intended for use as the system-provided memory allocator. jemalloc provides much introspection, memory management, and tuning features beyond the standard allocator functionality. For more information, see [jemalloc](https://github.com/jemalloc/jemalloc/wiki) and [sample codes](https://github.com/mingfeima/op_bench-py/blob/master/run.sh).
- For more information about distributed training for multiple sockets, see [Distributed CPU Training Script for PSSP-Transformer](https://github.com/mingfeima/pssp/blob/master/pssp-transformer/dist_train_cpu.sh).

#### Performance result

Tested on the 2nd generation Intel <sup>®</sup> Xeon<sup>®</sup> scalable processor Cascade Lake with 2*CPU (28 cores per CPU) and 384 GB memory, different models obtain the performance data as shown in [Intel and Facebook* collaborate to boost PyTorch* CPU performance](https://software.intel.com/content/www/us/en/develop/articles/intel-and-facebook-collaborate-to-boost-pytorch-cpu-performance.html). The performance result varies according to model and actual configurations.

:::
::: Sample 3: using Intel<sup>®</sup>AI Low Precision Optimization Tool for acceleration


The Intel<sup>®</sup> Low Precision Optimization Tool (Intel<sup>®</sup> LPOT) is an open-source Python library that delivers an easy-to-use low-precision inference interface across multiple neural network frameworks. It helps user quantify models, improve productivity, and accelerate the inference performance of low precision models on the 3rd generation Intel<sup>®</sup> Xeon<sup>®</sup> DL Boost scalable processor. For more information, see [Intel<sup>®</sup> Low Precision Optimization Tool code repository](https://github.com/Intel/lpot/).

#### Supported neural network frameworks
Intel<sup>®</sup> LPOT supports the following frameworks:
Intel<sup>®</sup> optimized TensorFlow*, including `v1.15.0`, `v1.15.0up1`, `v1.15.0up2`, `v2.0.0`, `v2.1.0`, `v2.2.0`, `v2.3.0` and `v2.4.0`.
Intel<sup>®</sup> optimized PyTorch, including `v1.5.0+cpu` and `v1.6.0+cpu`.
Intel<sup>®</sup> optimized MXNet, including `v1.6.0`, `v1.7.0`; ONNX-Runtime: `v1.6.0`.

#### Implementation frameworks
The following figure shows the Intel<sup>®</sup> LPOT implementation frameworks:
![](https://main.qcloudimg.com/raw/6062f647b40e2900354fbc73d8a4248a.jpg)

#### Workflow
The following figure shows the Intel<sup>®</sup> LPOT workflow:
![](https://main.qcloudimg.com/raw/acbc366d69819b443064ba5df58608fc.png)

#### Performance and accuracy of quantized models

The table below shows the performance and accuracy achieved by Intel® LPOT optimized models on the 2nd Intel<sup>®</sup> Xeon<sup>®</sup> scalable processor Cascade Lake:

<table class="docutils">
<thead>
  <tr>
    <th rowspan="2">Framework</th>
    <th rowspan="2">Version</th>
    <th rowspan="2">Model</th>
    <th colspan="3">Accuracy</th>
    <th>Performance speed up</th>
  </tr>
  <tr>
    <td>INT8 Tuning Accuracy</td>
    <td>FP32 Accuracy Baseline</td>
    <td>Acc Ratio [(INT8-FP32)/FP32]</td>
    <td>Realtime Latency Ratio[FP32/INT8]</td>
  </tr>
</thead>
<tbody>
  <tr>
    <td>tensorflow</td>
    <td>2.4.0</td>
    <td>resnet50v1.5</td>
    <td>76.92%</td>
    <td>76.46%</td>
    <td>0.60%</td>
    <td>3.37x</td>
  </tr>
  <tr>
    <td>tensorflow</td>
    <td>2.4.0</td>
    <td>resnet101</td>
    <td>77.18%</td>
    <td>76.45%</td>
    <td>0.95%</td>
    <td>2.53x</td>
  </tr>
  <tr>
    <td>tensorflow</td>
    <td>2.4.0</td>
    <td>inception_v1</td>
    <td>70.41%</td>
    <td>69.74%</td>
    <td>0.96%</td>
    <td>1.89x</td>
  </tr>
  <tr>
    <td>tensorflow</td>
    <td>2.4.0</td>
    <td>inception_v2</td>
    <td>74.36%</td>
    <td>73.97%</td>
    <td>0.53%</td>
    <td>1.95x</td>
  </tr>
  <tr>
    <td>tensorflow</td>
    <td>2.4.0</td>
    <td>inception_v3</td>
    <td>77.28%</td>
    <td>76.75%</td>
    <td>0.69%</td>
    <td>2.37x</td>
  </tr>
  <tr>
    <td>tensorflow</td>
    <td>2.4.0</td>
    <td>inception_v4</td>
    <td>80.39%</td>
    <td>80.27%</td>
    <td>0.15%</td>
    <td>2.60x</td>
  </tr>
  <tr>
    <td>tensorflow</td>
    <td>2.4.0</td>
    <td>inception_resnet_v2</td>
    <td>80.38%</td>
    <td>80.40%</td>
    <td>-0.02%</td>
    <td>1.98x</td>
  </tr>
  <tr>
    <td>tensorflow</td>
    <td>2.4.0</td>
    <td>mobilenetv1</td>
    <td>73.29%</td>
    <td>70.96%</td>
    <td>3.28%</td>
    <td>2.93x</td>
  </tr>
  <tr>
    <td>tensorflow</td>
    <td>2.4.0</td>
    <td>ssd_resnet50_v1</td>
    <td>37.98%</td>
    <td>38.00%</td>
    <td>-0.05%</td>
    <td>2.99x</td>
  </tr>
  <tr>
    <td>tensorflow</td>
    <td>2.4.0</td>
    <td>mask_rcnn_inception_v2</td>
    <td>28.62%</td>
    <td>28.73%</td>
    <td>-0.38%</td>
    <td>2.96x</td>
  </tr>
  <tr>
    <td>tensorflow</td>
    <td>2.4.0</td>
    <td>vgg16</td>
    <td>72.11%</td>
    <td>70.89%</td>
    <td>1.72%</td>
    <td>3.76x</td>
  </tr>
  <tr>
    <td>tensorflow</td>
    <td>2.4.0</td>
    <td>vgg19</td>
    <td>72.36%</td>
    <td>71.01%</td>
    <td>1.90%</td>
    <td>3.85x</td>
  </tr>
</tbody>
</table>

<table class="docutils">
<thead>
  <tr>
    <th rowspan="2">Framework</th>
    <th rowspan="2">Version</th>
    <th rowspan="2">Model</th>
    <th colspan="3">Accuracy</th>
    <th>Performance speed up</th>
  </tr>
  <tr>
    <td>INT8 Tuning Accuracy</td>
    <td>FP32 Accuracy Baseline</td>
    <td>Acc Ratio [(INT8-FP32)/FP32]</td>
    <td>Realtime Latency Ratio[FP32/INT8]</td>
  </tr>
</thead>
<tbody>
  <tr>
    <td>pytorch</td>
    <td>1.5.0+cpu</td>
    <td>resnet50</td>
    <td>75.96%</td>
    <td>76.13%</td>
    <td>-0.23%</td>
    <td>2.46x</td>
  </tr>
  <tr>
    <td>pytorch</td>
    <td>1.5.0+cpu</td>
    <td>resnext101_32x8d</td>
    <td>79.12%</td>
    <td>79.31%</td>
    <td>-0.24%</td>
    <td>2.63x</td>
  </tr>
  <tr>
    <td>pytorch</td>
    <td>1.6.0a0+24aac32</td>
    <td>bert_base_mrpc</td>
    <td>88.90%</td>
    <td>88.73%</td>
    <td>0.19%</td>
    <td>2.10x</td>
  </tr>
  <tr>
    <td>pytorch</td>
    <td>1.6.0a0+24aac32</td>
    <td>bert_base_cola</td>
    <td>59.06%</td>
    <td>58.84%</td>
    <td>0.37%</td>
    <td>2.23x</td>
  </tr>
  <tr>
    <td>pytorch</td>
    <td>1.6.0a0+24aac32</td>
    <td>bert_base_sts-b</td>
    <td>88.40%</td>
    <td>89.27%</td>
    <td>-0.97%</td>
    <td>2.13x</td>
  </tr>
  <tr>
    <td>pytorch</td>
    <td>1.6.0a0+24aac32</td>
    <td>bert_base_sst-2</td>
    <td>91.51%</td>
    <td>91.86%</td>
    <td>-0.37%</td>
    <td>2.32x</td>
  </tr>
  <tr>
    <td>pytorch</td>
    <td>1.6.0a0+24aac32</td>
    <td>bert_base_rte</td>
    <td>69.31%</td>
    <td>69.68%</td>
    <td>-0.52%</td>
    <td>2.03x</td>
  </tr>
  <tr>
    <td>pytorch</td>
    <td>1.6.0a0+24aac32</td>
    <td>bert_large_mrpc</td>
    <td>87.45%</td>
    <td>88.33%</td>
    <td>-0.99%</td>
    <td>2.65x</td>
  </tr>
  <tr>
    <td>pytorch</td>
    <td>1.6.0a0+24aac32</td>
    <td>bert_large_squad</td>
    <td>92.85</td>
    <td>93.05</td>
    <td>-0.21%</td>
    <td>1.92x</td>
  </tr>
  <tr>
    <td>pytorch</td>
    <td>1.6.0a0+24aac32</td>
    <td>bert_large_qnli</td>
    <td>91.20%</td>
    <td>91.82%</td>
    <td>-0.68%</td>
    <td>2.59x</td>
  </tr>
  <tr>
    <td>pytorch</td>
    <td>1.6.0a0+24aac32</td>
    <td>bert_large_rte</td>
    <td>71.84%</td>
    <td>72.56%</td>
    <td>-0.99%</td>
    <td>1.34x</td>
  </tr>
  <tr>
    <td>pytorch</td>
    <td>1.6.0a0+24aac32</td>
    <td>bert_large_cola</td>
    <td>62.74%</td>
    <td>62.57%</td>
    <td>0.27%</td>
    <td>2.67x</td>
  </tr>
</tbody>
</table>

<dx-alert infotype="explain" title="">
Both PyTorch and Tensorflow shown in the table are Intel-optimized frameworks. A full quantized model list is available in the [Full Validated Models](https://github.com/intel/lpot/blob/master/docs/full_model_list.md).
</dx-alert>



#### Installing and using Intel<sup>®</sup> LPOT 

1. Run the following commands sequentially to create a python3.x virtual environment named `lpot` in anaconda. This document uses python 3.7 as an example.
```plaintext
conda create -n lpot python=3.7
conda activate lpot
```
2. Install LPOT using either method:
    - Run the following command to install from a binary file.
``` plaintext
pip install lpot
```
    - Run the following commands to install from source.
```plaintext
 git clone https://github.com/intel/lpot.git
 cd lpot
 pip install -r requirements.txt
 python setup.py install
```
3. Quantify TensorFlow ResNet50 v1.0, for example.
    1. Prepare datasets.
Run the following commands to download and decompress the mageNet validation datasets.
```plaintext
mkdir -p img_raw/val && cd img_raw
wget http://www.image-net.org/challenges/LSVRC/2012/dd31405981
ef5f776aa17412e1f0c112/ILSVRC2012_img_val.tar
tar -xvf ILSVRC2012_img_val.tar -C val
``` 
Run the following commands to move the image file into a subdirectory classified by label.
```plaintext
cd val
wget -qO -https://raw.githubusercontent.com/soumith/
imagenetloader.torch/master/valprep.sh | bash
``` 
Run the following commands to convert the raw data to the TFrecord format using the [prepare_dataset.sh](https://github.com/intel/lpot/blob/master/examples/tensorflow/image_recognition/prepare_dataset.sh) script.
```plaintext
cd examples/tensorflow/image_recognition
bash prepare_dataset.sh --output_dir=./data --raw_dir=/PATH/TO/img_raw/val/ 
--subset=validation
``` 
For more information about datasets, see [Prepare Dataset](https://github.com/intel/lpot/tree/master/examples/tensorflow/image_recognition#2-prepare-dataset).
    2. Run the following commands to prepare a model.
 ```plaintext
wget https://storage.googleapis.com/intel-optimized-tensorflow/
 models/v1_6/resnet50_fp32_pretrained_model.pb
```
    3. Run the following commands to tune inference.
Modify the `examples/tensorflow/image_recognition/resnet50_v1.yaml` file so that the path of `quantization\calibration`, `evaluation\accuracy` and `evaluation\performance` datasets point to your local actual path, i.e., the location of the TFrecord data generated in the dataset preparations. For more information, see [ResNet50 V1.0](https://github.com/intel/lpot/tree/master/examples/tensorflow/image_recognition#1-resnet50-v10).
```plaintext
cd examples/tensorflow/image_recognition
bash run_tuning.sh --config=resnet50_v1.yaml \
--input_model=/PATH/TO/resnet50_fp32_pretrained_model.pb \
--output_model=./lpot_resnet50_v1.pb
```
    4. Run the following commands to run the benchmark.
```plaintext
bash run_benchmark.sh --input_model=./lpot_resnet50_v1.pb
--config=resnet50_v1.yaml
```
The results are as follows, in which the performance data is only for reference:
```shell
 accuracy mode benchmarkresult:
 Accuracy is 0.739
 Batch size = 32
 Latency: 1.341 ms
 Throughput: 745.631 images/sec
 performance mode benchmark result:
 Accuracy is 0.000
 Batch size = 32
 Latency: 1.300 ms
 Throughput: 769.302 images/sec
```
:::
::: Sample 4: using Intel<sup>®</sup> Distribution of OpenVINO™ Toolkit for inference acceleration
Intel<sup>®</sup> Distribution of OpenVINO™ Toolkit is a comprehensive toolkit for quickly deploying computer vision and other deep learning applications. It supports various Intel accelerator including VPU for CPU, GPU, FPGA and Movidius, and also supports direct heterogeneous hardware execution.

Intel<sup>®</sup> Distribution of OpenVINO™ Toolkit optimizes models trained by TensorFlow\* and PyTorch\*. It includes Model Optimizer, Inference Engine, Open Model Zoo, Post-training Optimization Tool:

- **Model Optimizer**: coverts models that were trained in frameworks such as Caffe\*, TensorFlow\*, PyTorch\* and Mxnet\* to intermediate representations (IRs).
- **Inference Engine**: places the converted IRs on many hardware types including CPU, GPU, FPGA and VPU to enable inference acceleration with an automatic call to the hardware accelerator toolkit.

For more information, see the [Intel<sup>®</sup> Distribution of OpenVINO™ Toolkit website](https://software.intel.com/content/www/us/en/develop/tools/openvino-toolkit.html) or [OpenVINO™ Toolkit Overview](https://docs.openvinotoolkit.org/latest/index.html).

#### Workflow
The following figure shows the workflow of Intel<sup>®</sup> Distribution of OpenVINO™ Toolkit:
![](https://main.qcloudimg.com/raw/98afcac361352773801fbe863d21b912.png)

#### Intel<sup>®</sup> Distribution of OpenVINO™ Toolkit inference performance
The Intel® Distribution of OpenVINO™ provides optimization implementations on multiple Intel processors and accelerator hardware. Based on the Intel <sup>®</sup> Xeon<sup>®</sup> scalable processor, it accelerates the inference network using Intel<sup>®</sup> DL Boost and AVX-512 instructions. 

 #### Using Intel<sup>®</sup> Distribution of OpenVINO™ Toolkit - Deep Learning Development Toolkit (DLDT)
 Refer to the following documents:
- [Introduction to Intel<sup>®</sup> Deep Learning Deployment Toolkit](https://docs.openvinotoolkit.org/downloads/cn/I03030-9-Introduction%20to%20Intel_%20Deep%20Learning%20Deployment%20Toolkit%20-%20OpenVINO_%20Toolkit.pdf)
-  [Image Classification C++ Sample Async](https://docs.openvinotoolkit.org/downloads/cn/I03030-10-Image%20Classification%20Cpp%20Sample%20Async%20-%20OpenVINO_%20Toolkit.pdf)
-  [Object Detection C++ Sample SSD](https://docs.openvinotoolkit.org/downloads/cn/I03030-11-Object%20Detection%20Cpp%20Sample%20SSD%20-%20OpenVINO_%20Toolkit.pdf)
-  [Automatic Speech Recognition C++ Sample](https://docs.openvinotoolkit.org/downloads/cn/I03030-12-Automatic%20Speech%20Recognition%20Cpp%20%20Sample%20-%20OpenVINO_%20Toolkit.pdf)
-  [Action Recognition Python* Demo](https://docs.openvinotoolkit.org/downloads/cn/I03030-13-Action%20Recognition%20Python%20Demo%20-%20OpenVINO_%20Toolkit.pdf)
-  [Crossroad Camera C++ Demo](https://docs.openvinotoolkit.org/downloads/cn/I03030-14-Crossroad%20Camera%20Cpp%20%20Demo%20-%20OpenVINO_%20Toolkit.pdf)
- [Human Pose Estimation C++ Demo](https://docs.openvinotoolkit.org/downloads/cn/I03030-15-Human%20Pose%20Estimation%20Cpp%20Demo%20-%20OpenVINO_%20Toolkit.pdf)

#### Intel<sup>®</sup> Distribution of OpenVINO™ Toolkit benchmark test
For more information, see [Install Intel<sup>®</sup> Distribution of OpenVINO™ toolkit for Linux*](https://docs.openvinotoolkit.org/downloads/cn/I03030-5-Install%20Intel_%20Distribution%20of%20OpenVINO_%20toolkit%20for%20Linux%20-%20OpenVINO_%20Toolkit.pdf).
:::
</dx-accordion>


