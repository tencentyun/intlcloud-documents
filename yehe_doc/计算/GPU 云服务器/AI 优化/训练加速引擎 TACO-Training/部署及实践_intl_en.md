This document describes how to deploy and use TACO-Training on GPU instances.

## Notes
- Currently, TACO-Training is supported only by Cloud GPU Service.
- Currently, the three acceleration components of TACO-Training have been integrated into the same Docker image, which can be pulled at the following address:
```plaintext
ccr.ccs.tencentyun.com/qcloud/taco-training:cu112-cudnn81-py3-0.3.2
```



## Directions

### Preparing the instance environment
1. Create at least two instances meeting the following requirements as instructed in Purchasing NVIDIA GPU Instance:
 - **Instance**: We recommend you select the [Computing GT4](https://intl.cloud.tencent.com/document/product/560/19701) GT4.41XLARGE948 8-card model.
 - **Image**: Select CentOS 7.8 or Ubuntu 18.04 or later and select **Automatically install GPU driver on the backend** to use the automatic installation feature to install the GPU driver.
Automatic installation of CUDA and cuDNN is not required for this deployment, and you can choose as needed.
![](https://qcloudimg.tencent-cloud.cn/raw/7fb885a81a2ea530dd323c473bb2d8eb.png)
 - **System disk**: We recommend you configure a system disk of 100 GB or above in size to store the Docker image and intermediate state files generated during training.
2. Install Docker as instructed in the corresponding document based on the operating system type of your instance: 
<table>
<thead>
<tr>
<th>OS</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>CentOS</td>
<td>For detailed directions, see <a href="https://docs.docker.com/engine/install/centos/">Install Docker Engine on CentOS</a>.</td>
</tr>
<tr>
<td>Ubuntu</td>
<td>For detailed directions, see <a href="https://docs.docker.com/engine/install/ubuntu/">Install Docker Engine on Ubuntu</a>.</td>
</tr>
</tbody></table>
3. Install nvidia-docker as instructed in [Docker](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html#docker).


### Using TTF

#### Installation
1. Run the following command as the root user and install TTF through a Docker image:
```plaintext
docker pull ccr.ccs.tencentyun.com/qcloud/taco-training:cu112-cudnn81-py3-0.3.2
```
2. Run the following command to start Docker:
```plaintext
docker run -it --rm --gpus all --shm-size=32g --ulimit memlock=-1 --ulimit stack=67108864 --name ttf1.15-gpu ccr.ccs.tencentyun.com/qcloud/taco-training:cu112-cudnn81-py3-0.3.2
```
3. Run the following command to view the TTF version:
```plaintext
pip show ttensorflow
```

#### Model adaptation

#### Dynamic embedding

Below is the code for the native static embedding of TF and dynamic embedding of TTF:

<dx-tabs>
::: Native static embedding of TF
```python
deep_dynamic_variables = tf.get_variable(
    name="deep_dynamic_embeddings",
    initializer=tf.compat.v1.random_normal_initializer(0, 0.005),
    shape=[100000000, self.embedding_size])
deep_sparse_weights = tf.nn.embedding_lookup(
    params=deep_dynamic_variables,
    ids=ft_sparse_val,
    name="deep_sparse_weights")
deep_embedding = tf.gather(deep_sparse_weights, ft_sparse_idx)
deep_embedding = tf.reshape(
    deep_embedding,
    shape=[self.batch_size, self.feature_num * self.embedding_size])
```
:::
::: Dynamic embedding of TTF
```python
deep_dynamic_variables = tf.dynamic_embedding.get_variable(       
    name="deep_dynamic_embeddings",                               
    initializer=tf.compat.v1.random_normal_initializer(0, 0.005), 
    dim=self.embedding_size,                                      
    devices=["/{}:0".format(FLAGS.device)],                       
    init_size=100000000)                                           
deep_sparse_weights = tf.dynamic_embedding.embedding_lookup(      
    params=deep_dynamic_variables,                                
    ids=ft_sparse_val,                                            
    name="deep_sparse_weights")          
deep_embedding = tf.gather(deep_sparse_weights, ft_sparse_idx)    
deep_embedding = tf.reshape(
    deep_embedding,
    shape=[self.batch_size, self.feature_num * self.embedding_size])
```
:::
</dx-tabs>


By comparing the code, you can see that TTF mainly modifies the following two parts:
- Embedding uses `tf.dynamic_embedding.get_variable`. For more information, see [tfra.dynamic_embedding.get_variable](https://github.com/tensorflow/recommenders-addons/blob/master/docs/api_docs/tfra/dynamic_embedding/get_variable.md).
- Lookup uses `tf.dynamic_embedding.embedding_lookup`. For more information, see [tfra.dynamic_embedding.embedding_lookup](https://github.com/tensorflow/recommenders-addons/blob/master/docs/api_docs/tfra/dynamic_embedding/embedding_lookup.md).
For the detailed API documentation, see [Module: tfra.dynamic_embedding](https://github.com/tensorflow/recommenders-addons/blob/master/docs/api_docs/tfra/dynamic_embedding.md).

#### Mixed precision
Mixed precision can be implemented by rewriting the code of the optimizer or modifying environment variables:
- Through code modification:
```python
opt = tf.train.experimental.enable_mixed_precision_graph_rewrite(opt)
```
- Through environment variable modification:
```python
export TF_ENABLE_AUTO_MIXED_PRECISION=1
```

The loss change curve of resnet50 training with the ImageNet dataset by TTF at mixed precisions is as follows:                 
![](https://staticintl.cloudcachetci.com/yehe/backend-news/SSVd454_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221209113846.png)  

#### XLA

XLA can be configured through the code or environment variables:
- Through code modification:
```python
config = tf.ConfigProto()
config.graph_options.optimizer_options.global_jit_level = tf.OptimizerOptions.ON_1
sess = tf.Session(config=config)
```
- Through environment variable modification:
```python
TF_XLA_FLAGS=--tf_xla_auto_jit=1
```

#### Demo
Before running the demo:
1. Run the following command to enter the `demo` directory:
```plaintext
cd /opt/dynamic-embedding-demo
```
2. Run the following command to download the dataset:
```plaintext
bash download_dataset.sh 
```

You can get started with TTF quick by using the following demo:
<dx-accordion>
::: benchmark
This demo is used to compare and test the performance of the dynamic embedding and the native static embedding:
```plaintext
# Enter the `benchmark` directory
cd benchmark
# Run the demo according to the default configuration
python train.py

# You need to delete the local dataset cache files every time you modify `batch size`.
rm -f .index .data-00000-of-00001
python train.py --batch_size=16384

# Use the static embedding and dynamic embedding to train the DeepFM model respectively
python train.py --batch_size=16384 --is_dynamic=False
python train.py --batch_size=16384 --is_dynamic=True

# Adjust the number of fully connected layers of the deep part
python train.py --batch_size=16384 --dnn_layer_num=12
```
:::
::: ps
This demo shows how to use the dynamic embedding in `ps` mode.
```plaintext
cd ps && bash start.sh
```
:::
::: Estimator
This demo shows how to use the dynamic embedding in estimator mode.
```plaintext
cd estimator && bash start.sh
```
:::
</dx-accordion>


### Using LightCC

#### Installation
1. Run the following command as the root user and install LightCC through a Docker image:
```plaintext
docker pull ccr.ccs.tencentyun.com/qcloud/taco-training:cu112-cudnn81-py3-0.3.2
```
2. Run the following command to start Docker:
```plaintext
docker run --network host -it --rm --gpus all --privileged --shm-size=32g --ulimit memlock=-1 --ulimit stack=67108864 --name lightcc ccr.ccs.tencentyun.com/qcloud/taco-training:cu112-cudnn81-py3-0.3.2
```
3. Run the following command to view the LightCC version:
```plaintext
pip show light-horovod
```
<dx-alert infotype="notice" title="">
When the kernel protocol stack is used for NCCL network communication, or if the runtime environment of the HARP protocol stack is not configured, you need to move the `/usr/lib/x86_64-linux-gnu/libnccl-net.so` file in the image to a path other than the system `lib` directory, such as the `/root` directory, as the system will check whether the HARP configuration file exists in a certain directory in the `lib` directory during `init` and will report an error if the file doesn't exist.
</dx-alert>





#### Environment variable configuration
LightCC environment variables are as detailed below, which can be configured as needed:

| Environment Variable                     | Default Value     | Description                                                         |
| ---------------------------- | ---------- | ------------------------------------------------------------ |
| LIGHT_2D_ALLREDUCE           | 0          | Whether to use the 2D-Allreduce algorithm                                     |
| LIGHT_INTRA_SIZE             | 8          | Number of GPUs in a 2D-Allreduce group                                        |
| LIGHT_HIERARCHICAL_THRESHOLD | 1073741824 | Threshold for 2D-Allreduce in bytes. Only data of a size less than this threshold can use 2D-Allreduce. |
| LIGHT_TOPK_ALLREDUCE         | 0          | Whether to use TOPK to compress the communication data                                         |
| LIGHT_TOPK_RATIO             | 0.01       | Compression ratio of TOPK                                           |
| LIGHT_TOPK_THRESHOLD         | 1048576    | Threshold for TOPK compression in bytes. Only communication data of a size greater than or equal to this threshold can be compressed through TOPK. |
| LIGHT_TOPK_FP16              | 0          | Whether to convert the values of the compressed communication data to FP16                                  |

#### Demo
1. After creating two GPU instances, install LightCC and configure environment variables in the above steps.
2. Run the following commands in the container to configure passwordless SSH login for the instances:
```plaintext
# Allow the root user to use the SSH service and start the service (default port: 22)
sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
service ssh start && netstat -tulpn
```
```plaintext
# Change the default SSH port in the container to 2222 to avoid conflicts with the host
sed -i 's/#Port 22/Port 2222/' /etc/ssh/sshd_config
service ssh restart && netstat -tulpn
```
```plaintext
# Set `root passwd`
passwd root
```
```plaintext
# Generate an SSH key
ssh-keygen
```
```plaintext
# Configure SSH to use port 2222 by default
# Create `~/.ssh/config`, add the following content, and save and exit the file:
# Note: The IP used here is the IP displayed in `ifconfig eth0` of the two instances.
Host gpu1
 hostname 10.0.2.8
 port 2222
Host gpu2
 hostname 10.0.2.9
 port 2222
```
```plaintext
# Configure mutual passwordless login for the instances and local passwordless login for each instance
ssh-copy-id gpu1
ssh-copy-id gpu2
```
```plaintext
# Test whether passwordless login is configured successfully
ssh gpu1 
ssh gpu2
```
3. Run the following command to download the benchmark test script of Horovod:
```plaintext
wget https://raw.githubusercontent.com/horovod/horovod/master/examples/tensorflow/tensorflow_synthetic_benchmark.py
```
4. Run the following command to start multi-server training benchmark based on ResNet-50:
```plaintext
/usr/local/openmpi/bin/mpirun -np 16 -H gpu1:8,gpu2:8 --allow-run-as-root -bind-to none -map-by slot -x NCCL_ALGO=RING -x NCCL_DEBUG=INFO -x HOROVOD_MPI_THREADS_DISABLE=1 -x HOROVOD_FUSION_THRESHOLD=0  -x HOROVOD_CYCLE_TIME=0 -x LIGHT_2D_ALLREDUCE=1 -x LIGHT_TOPK_ALLREDUCE=1 -x LIGHT_TOPK_THRESHOLD=2097152 -x LD_LIBRARY_PATH -x PATH -mca btl_tcp_if_include eth0 python3 tensorflow_synthetic_benchmark.py --model=ResNet50 --batch-size=256
```
Here, the command parameters are used for an 8-card model. To configure another model, modify the `-np` and `-H` parameters. Other parameters are as detailed below:
 - `NCCL_ALGO=RING`: Select the ring algorithm as the communication algorithm in NCCL.
 - `NCCL_DEBUG=INFO`: Enable debugging output in NCCL.
 - `-mca btl_tcp_if_include eth0`: Select the eth0 device as network device for MPI multi-server communication. As some ENIs cannot communicate, you need to specify the ENI if there are multiple ones; otherwise, an error will occur if MPI chooses an ENI that cannot communicate.

The reference throughput rates of LightCC multi-server training benchmark in two GT4.41XLARGE948 instances are as detailed below:

<table>
    <tr>
        <th colspan="3">Model: CVM GT4.41XLARGE948 (A100 * 8 + 50G VPC)<br>
      GPU driver: 460.27.04<br>
      Container: ccr.ccs.tencentyun.com/qcloud/taco-training:cu112-cudnn81-py3-0.3.2</th>
    <tr>
    <tr>
      	<th rowspan="4" align=center>network</th>
        <td colspan="2" align=center>ResNet50 Throughput(images/sec)</td>
    <tr>
    <tr>
        <td align=center>horovod 0.21.3</td>
      	<td align=center>lightcc 3.0.0</td>
    <tr>
    <tr>
      	<th>NCCL + HRAP</th>
        <td align=right>8970.7</td>
      	<td align=right>10229.9</td>
    <tr>
    <tr>
      	<th>NCCL + kernel socket</th>
        <td align=right>5421.9</td>
      	<td align=right>7183.5</td>
    <tr>
</table>

### Using HARP

#### Preparing the instance environment
1. Run the following command as the root user to modify `cmdline` of the kernel and configure a 50 GB huge page memory.
```plaintext
sed -i '/GRUB_CMDLINE_LINUX/ s/"$/ default_hugepagesz=1GB hugepagesz=1GB hugepages=50"/' /etc/default/grub
```
<dx-alert infotype="notice" title="">
You can configure `hugepages=50` for an 8-card instance or `hugepages= (number of GPU cards * 5 + 10)` for other models.
</dx-alert>
2. Run the following command based on your operating system version to make the configuration take effect and restart the instance:
<dx-tabs>
::: Ubuntu
```plaintext
sudo update-grub2 && sudo reboot
```
:::
::: CentOS or TencentOS
```plaintext
sudo grub2-mkconfig -o /boot/grub2/grub.cfg && sudo reboot
```
:::
</dx-tabs>
3. Bind ENIs as follows. The number of ENIs should be the same as the number of GPU cards.
 1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index), select **More** > **IP/ENI** > **Bind ENI** on the right of the target instance.
 2. In the **Bind ENI** pop-up window, select created ENIs or create new ones and bind them as needed.
 3. Click **OK**.
4. Run the following command to initialize the configuration information.
```plaintext
curl -s -L http://mirrors.tencent.com/install/GPU/taco/harp_setup.sh | bash
```
If the input result contains "Set up HARP successfully", and the `ztcp*.conf` configuration file is generated in the `/usr/local/tfabric/tools/config` directory, the configuration has been completed successfully.




#### Installation
1. Run the following command as the root user and install HARP through a Docker image:
```plaintext
docker pull ccr.ccs.tencentyun.com/qcloud/taco-training:cu112-cudnn81-py3-0.3.2
```
2. Run the following command to start Docker:
```plaintext
docker run -it --rm --gpus all --privileged --net=host -v /sys:/sys -v /dev/hugepages:/dev/hugepages -v /usr/local/tfabric/tools:/usr/local/tfabric/tools ccr.ccs.tencentyun.com/qcloud/taco-training:cu112-cudnn81-py3-0.3.2
```

#### Demo
1. After creating two GPU instances, configure the instance environment and install HARP in the above steps.
2. Run the following commands in Docker to configure passwordless SSH login for the instances:
```plaintext
# Allow the root user to use the SSH service and start the service (default port: 22)
sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
service ssh start && netstat -tulpn
```
```plaintext
# Change the default SSH port in the container to 2222 to avoid conflicts with the host
sed -i 's/#Port 22/Port 2222/' /etc/ssh/sshd_config
service ssh restart && netstat -tulpn
```
```plaintext
# Set `root passwd`
passwd root
```
```plaintext
# Generate an SSH key
ssh-keygen
```
```plaintext
# Configure SSH to use port 2222 by default
# Create `~/.ssh/config`, add the following content, and save and exit the file:
# Note: The IP used here is the IP displayed in `ifconfig eth0` of the two instances.
Host gpu1
 hostname 10.0.2.8
 port 2222
Host gpu2
 hostname 10.0.2.9
 port 2222
```
```plaintext
# Configure mutual passwordless login for the instances and local passwordless login for each instance
ssh-copy-id gpu1
ssh-copy-id gpu2
```
```plaintext
# Test whether passwordless login is configured successfully
ssh gpu1 
ssh gpu2
```
2. Run the following command to download the benchmark script of Horovod:
```plaintext
wget https://raw.githubusercontent.com/horovod/horovod/master/examples/tensorflow/tensorflow_synthetic_benchmark.py
```
3. Run the following command to start multi-server training benchmark based on ResNet-50:
```plaintext
/usr/local/openmpi/bin/mpirun -np 16 -H gpu1:8,gpu2:8 --allow-run-as-root -bind-to none -map-by slot -x NCCL_ALGO=RING -x NCCL_DEBUG=INFO -x HOROVOD_MPI_THREADS_DISABLE=1 -x HOROVOD_FUSION_THRESHOLD=0  -x HOROVOD_CYCLE_TIME=0 -x LIGHT_2D_ALLREDUCE=1 -x LIGHT_TOPK_ALLREDUCE=1 -x LIGHT_TOPK_THRESHOLD=2097152 -x LD_LIBRARY_PATH -x PATH -mca btl_tcp_if_include eth0 python3 tensorflow_synthetic_benchmark.py --model=ResNet50 --batch-size=256
```
Here, the command parameters are used for an 8-card model. To configure another model, modify the `-np` and `-H` parameters. Other parameters are as detailed below: 
 - `NCCL_ALGO=RING`: Select the ring algorithm as the communication algorithm in NCCL.
 - `NCCL_DEBUG=INFO`: Enable debugging output in NCCL. After it is enabled, HARP will output the following content:
![](https://main.qcloudimg.com/raw/d8a9b021511fd7cbd5c6dc0699c01d4e.png)
 - `-mca btl_tcp_if_include eth0`: Select the eth0 device as network device for MPI multi-server communication. As some ENIs cannot communicate, you need to specify the ENI if there are multiple ones; otherwise, an error will occur if MPI chooses an ENI that cannot communicate.
After NCCL initialization, you can view the network output:
![](https://main.qcloudimg.com/raw/084d8f0c9ac52a98cbe9e5ccb1626923.png)
4. HARP is integrated to NCCL as a plugin and is enabled automatically without any configuration required. To disable HARP, run the following command in the container:
```plaintext
mv /usr/lib/x86_64-linux-gnu/libnccl-net.so /usr/lib/x86_64-linux-gnu/libnccl-net.so_bak
```
