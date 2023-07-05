## Operation Scenario

Currently, the container images of most open-source apps (such as Kubernetes and TensorFlow) are hosted on image hosting platforms outside of the Chinese mainland (such as DockerHub and `quay.io`). As a result, pulling images in the Chinese mainland may be slow or even fail due to network issues. A common solution is to manually pull images to local storage and then push them to a self-built image repository for manual synchronization. This process is very complicated and does not cover all repositories or the latest image versions.
[Tencent Container Registry (TCR)](https://intl.cloud.tencent.com/document/product/1051) Enterprise Edition provides an acceleration service for mainstream image hosting platforms outside of the Chinese mainland to effectively resolve difficulties in image pulling, thereby facilitating the deployment of open-source apps. This document introduces how TKE clusters use the TCR acceleration service to accelerate image pulling outside of the Chinese mainland.



## Limits


- Currently, the acceleration service is available only to TKE and TCR users. If you need this service, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply for it.
- The acceleration service currently can be accessed only from Tencent Cloud [VPCs](https://intl.cloud.tencent.com/document/product/215). Access from the Internet is not yet allowed. The relevant domain name can be accessed but cannot actually provide the acceleration feature.
- If you need to use images on other mainstream image hosting platforms, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to inquire.


## Directions

For TKE clusters, acceleration has been configured for the public images of the DockerHub platform by default. If you need acceleration for image repositories on other platforms, such as `quay.io`, you need to modify the configuration. The configuration method for clusters with a Docker runtime environment is different from that for clusters with a Containerd runtime environment.


### Configuration for Docker clusters
For nodes with a Docker runtime environment, because Docker itself does not support acceleration configuration except for `docker.io`, when you use container images other than `docker.io` from outside the Chinese mainland, you need to run the following command to change the image address domain name from `quay.io` to `quay.tencentcloudcr.com`. See the example below:
```bash
docker pull quay.tencentcloudcr.com/k8scsi/csi-resizer:v0.5.0
```
### Configuration for Containerd clusters
For nodes with a Containerd runtime environment, because Containerd itself supports acceleration address configuration for any image repository, you can modify the Containerd configuration to implement automatic accelerated pulling of images without changing the image address. This is suitable for scenarios where large numbers of images outside the Chinese mainland need to be pulled because it saves you the trouble of modifying large numbers of addresses through a complex procedure.
1. When TKE adds nodes or uses a node pool, you can write the nodes into a custom script and use the script to modify the Containerd configuration of the newly added nodes and add an acceleration address for images outside the Chinese mainland. See the sample script below:
```
sed -i '/\[plugins\.cri\.registry\.mirrors\]/ a\\ \ \ \ \ \ \ \ [plugins.cri.registry.mirrors."quay.io"]\n\ \ \ \ \ \ \ \ \ \ endpoint = ["https://quay.tencentcloudcr.com"]' /etc/containerd/config.toml
```
Alternatively, you can manually modify the Containerd configuration (`/etc/containerd/config.toml`) of existing nodes by adding a configuration similar to the following sample:
```
[plugins.cri.registry]
[plugins.cri.registry.mirrors]
[plugins.cri.registry.mirrors."quay.io"]
endpoint = ["https://quay.tencentcloudcr.com"]
[plugins.cri.registry.mirrors."docker.io"]
endpoint = ["https://mirror.ccs.tencentyun.com"]
```
 >? You can also use Ansible to perform batch modification on the Containerd configurations of existing nodes. For more information, see [Performing batch operations on TKE nodes by using Ansible](https://intl.cloud.tencent.com/document/product/457/38427).
2. Run the following command to restart Containerd. See the sample below:
```
 systemctl restart containerd
```
3. Run the following command to use the original image address to pull images. See the sample below:
```
crictl pull quay.io/k8scsi/csi-resizer:v0.5.0
```
