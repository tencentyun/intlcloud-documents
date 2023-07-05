
<dx-alert infotype="explain" title="">
This document is written by a Cloud GPU Service user and is for study and reference only.
</dx-alert>

## Overview
You can use Docker to run TensorFlow in a GPU instance quickly. In this way, you only need to install the NVIDIA® driver program in the instance and don't need to install NVIDIA® CUDA® Toolkit.

This document describes how to use Docker to install TensorFlow and configure GPU/CPU support in a GPU instance.


## Notes
- This document uses a GPU instance on Ubuntu 20.04 as an example.
- The GPU driver has been installed in your GPU instance.
<dx-alert infotype="explain" title="">
We recommend you use a public image to create a GPU instance. If you select a public image, then select **Automatically install GPU driver on the backend** to preinstall the driver on the corresponding version. This method only supports certain Linux public images.
</dx-alert>



## Directions

### Installing Docker
1. Log in to the instance and run the following commands to install the required system tools:
```shellsession
sudo apt-get update
```
```shellsession
 sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```
2. Run the following command to install the GPG certificate to write the software source information:
```shellsession
sudo mkdir -p /etc/apt/keyrings
 curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
 echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
3. Run the following commands to update and install Docker-CE:
```shellsession
sudo apt-get update
```
```shellsession
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```



### Installing TensorFlow

#### Setting the NVIDIA container toolkit
1. Run the following command to set the package repository and GPG key as instructed in [Setting up NVIDIA Container Toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html#setting-up-nvidia-container-toolkit):
```shellsession
distribution=$(. /etc/os-release;echo $ID$VERSION_ID) \
      && curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg \
      && curl -s -L https://nvidia.github.io/libnvidia-container/$distribution/libnvidia-container.list | \
            sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
            sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list
```
2. Run the following command to install the nvidia-docker2 package and its dependencies:
```shellsession
sudo apt-get update
```
```shellsession
sudo apt-get install -y nvidia-docker2
```
3. Run the following command to set the default runtime and restart the Docker daemon to complete installation:
```shellsession
sudo systemctl restart docker
```
4. Then, you can run the following command to run the base CUDA container to test the job settings:
```shellsession
sudo docker run --rm --gpus all nvidia/cuda:11.0.3-base-ubuntu20.04 nvidia-smi
```
The following information will appear:
```shellsession
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 450.51.06    Driver Version: 450.51.06    CUDA Version: 11.0     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  Tesla T4            On   | 00000000:00:1E.0 Off |                    0 |
| N/A   34C    P8     9W /  70W |      0MiB / 15109MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|  No running processes found                                                 |
+-----------------------------------------------------------------------------+
```

#### Downloading a TensorFlow Docker image

The official TensorFlow Docker images are in the [tensorflow/tensorflow](https://hub.docker.com/r/tensorflow/tensorflow/) code repository in Docker Hub. Image tags are defined in the following format as listed in [Tags](https://hub.docker.com/r/tensorflow/tensorflow/tags/):

<table>
<thead>
<tr>
<th align="left">Tag</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left"><code>latest</code></td>
<td align="left">Latest (default) tag of the binary TensorFlow CPU image.</td>
</tr>
<tr>
<td align="left"><code>nightly</code></td>
<td align="left">Nightly tag of the TensorFlow image, which is unstable.</td>
</tr>
<tr>
<td align="left"><code>version</code></td>
<td align="left">Tag of the TensorFlow binary image, such as `2.1.0`.</td>
</tr>
<tr>
<td align="left"><code>devel</code></td>
<td align="left">TensorFlow <code>master</code>Nightly tag of the development environment, which contains the TensorFlow source code.</td>
</tr>
<tr>
<td align="left"><code>custom-op</code></td>
<td align="left">Special experimental image for custom TensorFlow operation development. For more information, see <a href="https://github.com/tensorflow/custom-op">tensorflow/custom-op</a>.</td>
</tr>
</tbody></table>
Each basic tag has variants with new or modified features:
<table>
<thead>
<tr>
<th align="left">Tag Variant</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left"><code>tag</code> <code>-gpu</code></td>
<td align="left">Specified tag supporting GPU.</td>
</tr>
<tr>
<td align="left"><code>tag</code> <code>-jupyter</code></td>
<td align="left">Specified tag for Jupyter, which contains the TensorFlow tutorial laptop.</td>
</tr>
</tbody></table>

You can use multiple variants at a time. For example, the following command will download the TensorFlow image tags to your computer:
```shellsession
docker pull tensorflow/tensorflow                     # latest stable release
docker pull tensorflow/tensorflow:devel-gpu           # nightly dev release w/ GPU support
docker pull tensorflow/tensorflow:latest-gpu-jupyter  # latest release w/ GPU support and Jupyter
```


#### Starting the TensorFlow Docker container
Run the following command to start and configure the TensorFlow container. For more information, see [Docker run reference](https://docs.docker.com/engine/reference/run/).
```shellsession
docker run [-it] [--rm] [-p hostPort:containerPort] tensorflow/tensorflow[:tag] [command]
```


## Examples
### Using an image supporting only CPU
Use an image with the `latest` tag to verify the TensorFlow installation result. Docker will download the latest TensorFlow image when it runs for the first time.
```shellsession
docker run -it --rm tensorflow/tensorflow \
   python -c "import tensorflow as tf; print(tf.reduce_sum(tf.random.normal([1000, 1000])))"
```
Below are the samples of other TensorFlow Docker solutions:

- Start the `bash` shell session in the container where TensorFlow is configured:
```shellsession
docker run -it tensorflow/tensorflow bash
```
- To run the TensorFlow program developed on the host in the container, use the `-v hostDir:containerDir -w workDir` parameter to load the server directory and change the container working directory as follows:
```shellsession
docker run -it --rm -v $PWD:/tmp -w /tmp tensorflow/tensorflow python ./script.py
```
<dx-alert infotype="explain" title="">
When you allow the host to access the files created in the container, permission problems may occur. Generally, we recommend you modify files on the host system.
</dx-alert>
- Use TensorFlow with the `nightly` tag to start Jupyter laptop server:
```shellsession
docker run -it -p 8888:8888 tensorflow/tensorflow:nightly-jupyter
```
Use a browser to visit `http://127.0.0.1:8888/?token=...` as instructed at the [Jupyter website](https://jupyter.org/).


### Using an image supporting GPU
Run the following command to download and run the TensorFlow image supporting GPU:
```shellsession
docker run --gpus all -it --rm tensorflow/tensorflow:latest-gpu \
   python -c "import tensorflow as tf; print(tf.reduce_sum(tf.random.normal([1000, 1000])))"
```
It may take a while to set the image supporting GPU. To run the GPU-based script repeatedly, you can use `docker exec` to use the container repeatedly.
Run the following command to use the latest TensorFlow GPU image to start the `bash` shell session in the container:
```shellsession
docker run --gpus all -it tensorflow/tensorflow:latest-gpu bash
```
