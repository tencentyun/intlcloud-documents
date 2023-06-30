## Overview 
The HCCPNV4h instance is equipped with A100 GPUs and supports **NVLink and NVSwitch**. You need to install the `nvidia-fabricmanager` service corresponding to the driver version to interconnect GPUs; otherwise, GPU instances cannot be used properly. This document describes how to install the `nvidia-fabricmanager` service.


## Directions
The following takes the driver **470.103.01** as an example, which can be replaced as needed.
 
### Installing the nvidia-fabricmanager service
1. Log in to the instance as instructed in [Logging In To Linux Instance (Web Shell)](https://intl.cloud.tencent.com/document/product/213/5436).
2. The installation directions vary by operating system. Run the corresponding command for installation.
<dx-tabs>
::: CentOS 7.x image
```ruby
version=470.103.01
yum -y install yum-utils
yum-config-manager --add-repo https://developer.download.nvidia.com/compute/cuda/repos/rhel7/x86_64/cuda-rhel7.repo
yum install -y nvidia-fabric-manager-${version}-1
```
:::
::: Ubuntu 18.04 image
```ruby
version=470.103.01
main_version=$(echo $version | awk -F '.' '{print $1}')
apt-get update
apt-get -y install nvidia-fabricmanager-${main_version}=${version}-*
```
:::
</dx-tabs>


### Starting the nvidia-fabricmanager service
Run the following commands to start the service.
```ruby
systemctl enable nvidia-fabricmanager
```
```ruby
systemctl start nvidia-fabricmanager
```

### Viewing the status of the nvidia-fabricmanager service
Run the following command to view the service status.
```ruby
systemctl status nvidia-fabricmanager
```
If the following information appears, the service is installed successfully.
![](https://qcloudimg.tencent-cloud.cn/raw/3575a97948b57964dff2b922d15756a8.png)
