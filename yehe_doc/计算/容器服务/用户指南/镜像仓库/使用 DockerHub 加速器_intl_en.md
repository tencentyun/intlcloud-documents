Tencent Cloud offers the following DockerHub accelerator to enable quick pulling of container images on the DockerHub platform.
You need to configure the accelerator URL in the CVM to apply the configuration. Do not access the accelerator directly in a browser. Instead, complete the following steps to configure the accelerator.
```
https://mirror.ccs.tencentyun.com
```


## Configuring a CVM Instance in a TKE Cluster
You do not need to manually configure CVM instances in the TKE cluster. The cluster installs the Docker service automatically when creating the node, and configures the Mirror images. The default configuration is as follows:
```shell
[root@VM_1_2_centos ~]# cat /etc/docker/dockerd 
IPTABLES="--iptables=false"
STORAGE_DRIVER="--storage-driver=overlay2"
IP_MASQ="--ip-masq=false"
LOG_LEVEL="--log-level=warn"
REGISTRY_MIRROR="--registry-mirror=https://mirror.ccs.tencentyun.com"
```
## Configurations Common to All CVM Instances
### Linux 
>Configurations for Ubuntu 16.04+, Debian 8+ and CentOS 7 are used as an example. For other versions, configure as needed.
>
1. Create or modify the `/etc/docker/daemon.json` file and add the following content:
```shell
{
  	"registry-mirrors": [
	  	"https://mirror.ccs.tencentyun.com"
	 ]
}
```
2. Run the following commands and restart the Docker service.
```shell
$ sudo systemctl daemon-reload
```
```
$ sudo systemctl restart docker
# For Ubuntu16.04, run the "sudo systemctl restart dockerd" command.
```

### Windows 10
1. Go to “Settings” of the Docker client.
2. After opening the configuration window, select Docker Engine, and enter the following content.
```shell
{
	 "registry-mirrors": [
	  	"https://mirror.ccs.tencentyun.com"
	 ]
}
```
2. Click **Apply & Restart**, and the Docker service will save the configurations and restart.

## Checking Whether the Accelerator Works
Run the `docker info` command. If the returned result contains the following content, the configuration is successful.
```shell
Registry Mirrors:
 https://mirror.ccs.tencentyun.com
```
