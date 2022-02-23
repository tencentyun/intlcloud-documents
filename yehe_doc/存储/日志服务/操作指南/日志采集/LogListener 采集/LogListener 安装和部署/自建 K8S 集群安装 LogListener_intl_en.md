This document describes how to install LogListener on a self-built Kubernetes cluster to collect logs to CLS.
During the installation process, the system automatically performs the following operations:
1. Create a CLS-logconfigs CRD.
2. Deploy cls-provisioner.
3. Install LogListener in DaemonSet mode.


## Directions

1. Log in to the Kubernetes cluster.
2. Run the following commands in sequence to install cls-provisioner Helm.
```
wget https://mirrors.tencent.com/install/cls/k8s/tencentcloud-cls-k8s-install.sh
```
```
chmod 744 tencentcloud-cls-k8s-install.sh
```
```
./tencentcloud-cls-k8s-install.sh --region xxx --secretid xxx --secretkey xxx 
```
When the installation is completed, CLS automatically creates a default machine group named `cls-k8s-Random ID`.
>! Before installing cls-provisioner Helm, check that the Helm CLI is already installed in the Kubernetes cluster. For more information, please see [Installing Helm](https://docs.helm.sh/docs/intro/install/).
>

## Parameters

---secretid: Tencent Cloud account access key ID.
---secretkey: Tencent Cloud account access key.
---region: CLS region.
---docker_root: root directory of the cluster Docker. The default value is `/var/lib/docker`. If the actual directory is different from the default one, specify the actual root directory of Docker.
---cluster_id: cluster ID. If you do not specify a cluster ID, the system will generate a default ID for machine group association during the installation process.
>? 
> - We recommend you use different `cluster_id` values for different clusters.
> - Data of different clusters can be shipped to the same topic.
> - The default ID is in the following format: cls-k8s-Random ID consisting of 8 characters.
>   
---network: network type, private or internet (default).
---api_network: TencentCloud API network type, private or internet (default).
- --api_region: TencentCloud API region. For more information, please see [Available Regions](https://intl.cloud.tencent.com/document/product/614/18940).

#### Sample

Deploying LogListener in the Beijing region
```
./tencentcloud-cls-k8s-install.sh --secretid xxx --secretkey xx --region ap-beijing  --network internet --api_region ap-beijing
```


