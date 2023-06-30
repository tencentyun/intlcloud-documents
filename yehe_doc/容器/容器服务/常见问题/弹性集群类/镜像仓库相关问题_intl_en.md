### How do I use the Tencent Container Registry (TCR) service in an serverless cluster?


If you want to use the TCR service in an serverless cluster, ensure that [you have selected the corresponding image access credential](#ensure1) and [ensure the network connectivity between the serverless cluster and TCR](#ensure2).

[](id:ensure1)
#### Ensuring that you have selected the corresponding image access credential

A container image is private by default. Therefore, you need to select the image access credential for the TCR instance when creating a workload.
![](https://qcloudimg.tencent-cloud.cn/raw/1f2a68b4fce1be7f2ebc13864ea6faab.png)
You can follow the steps below to create the image access credential:
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2/ecluster?rid=1) and go to the “Serverless Cluster” page.
2. Click the name of the serverless cluster you need to create the access credential for to go to the serverless cluster details page.
3. Click “Namespace” on the left and click **Create**.
4. On the “Create Namespace” page, select **Auto release TCR enterprise access credential**
5. Click **Create Namespace** to create a namespace, and then you can select the image access credential at the newly created namespace.

[](id:ensure2)
#### Ensuring the network connectivity between the serverless cluster and TCR

The network between the serverless cluster and TCR is not connected by default, so an error indicating network disconnectivity will be reported when you pull the image:
```
dial tcp x.x.x.x:443: i/o timeout
```


#### Solutions

There are 2 solutions:


| Solution | Note |
| ------------------- | ------------------------------------------------------------ |
| Solution 1: private network access (recommended) | Create a private network access linkage on the TCR console and configure private-network domain name resolution. In this way, the serverless cluster can access TCR via the newly created private network access linkage. |
| Solution 2: public network access | Enable public network access for the serverless cluster so that it can access TCR via the public network. You also need to make TCR accessible via the public network. |


#### Solution 1: private network access (recommended)

1. Create a private network access linkage
   1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr/instance?rid=1) and select **Network ACL** > **Private network** on the left sidebar.
   2. Select the region and instance on the “Private network” page and click **Create**.
   3. In the "Create a private network access linkage" window that appears, configure the VPC and subnet information.
2. Click **OK** to start creating the private network access linkage.
3. Enable domain name private network resolution.
   The domain name of TCR is “&lt;tcr-name>.tencentcloudcr.com”, the resolution of which in the VPC needs to be enabled additionally. If the resolution is not enabled, the aforementioned domain name will be resolved into a public IP rather than a private IP, leading to a private network access failure.

>!After creating an access linkage, please wait until the backend generates a private IP. After that, the following button can be enabled.


#### Solution 2: public network access

1. Ensure that TCR has enabled public network access[](id:step2-1)
    1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr/instance?rid=1) and select **Network ACL** > **Public network** on the left sidebar.
    2. Select the region and instance on the “Public network” page.
    3. Enable public network access for the corresponding TCR instance.
      In the trial stage, you can set the public IP range as 0.0.0.0/0. In the running stage, you can add the elastic IPs of the NAT gateway egress involved in the following step 2 to the public network allowlist.
2. Enable public network access for the serverless cluster.
   Public network access for the serverless cluster is disabled by default, and the serverless cluster needs to access the public network through an NAT gateway. For more information, see [Accessing Internet through NAT Gateway](https://intl.cloud.tencent.com/document/product/457/38369).
   After configuring the NAT gateway, associate the subnet of the serverless cluster with the route table of the NAT gateway, and make sure the elastic IPs of the NAT gateway egress are added to the TCR access allowlist (**for more information, see [step 1](#step2-1)**). In this way, the serverless cluster can normally access TCR and pull the image from the public network.





#### Errors and troubleshooting methods

#### Error:failed to do request:Head "xxxx/manifests/late-st": dial tcp xxx:443: i/o timeout
An error containing “**443: i/o timeout**” is usually caused by the network disconnectivity between EKS and TCR.
Please select an access method mentioned in **[Ensuring the network connectivity between the serverless cluster and TCR]** to realize the network connectivity between EKS and TCR.
<dx-alert infotype="notice" title="">
The domain name “&lt;tcr-name>.tencentcloudcr.com” is resolved into a public IP by default. Please figure out the IP address in “dial tcp xxx” indicates a public or private network when the error is reported and solve the problem according to the actual situation.
</dx-alert>

#### Error:code= Unknown, pull access denied, repository does not exist or may require authorization: server message: insufficient_scope: authorization failed
An error containing **insufficient_scope: authorization failed**” indicates that the network between EKS and TCR is interconnected yet you do not have certain permissions. The cause may be that the namespace does not exist, the key is incorrect, or the key is not suitable for the image being pulled, etc.

#### Error: code = NotFound, failed to resolve reference "xxx:xxx": not found
An error containing “**not found**” indicates that the image does not exist.



For more information on other common errors, see TCR-related [FAQs](https://intl.cloud.tencent.com/document/product/1051/37243).



### How do I use the external image repository that is created based on the self-signed certificate or HTTP?

#### Problem description

When you use the image of an external image repository to create a workload in the serverless cluster, you may encounter the error “**ErrImagePull**” and fail to pull the image, as shown in the figure below:
![](https://qcloudimg.tencent-cloud.cn/raw/0d5bf4a45ce5ef4d4f74be2642583b36.png)

#### Cause

Generally speaking, if network connectivity is ensured, the problem may result from the following two causes:

- The external image repository adopts the HTTPS protocol, but the HTTPS protocol certificate is a self-signed certificate.
- The external image repository adopts the HTTPS protocol.

You can solve the aforementioned 2 problems by adding annotations to the PodTemplate in workload Yaml configurations.

#### Solutions

#### HTTPS-based self-signed image repository
If the external image repository is an HTTPS-based self-signed image repository, you need to add the following annotation to PodTemplate to make it skip certificate verification.
**eks.tke.cloud.tencent.com/registry-insecure-skip-verify: image repository address (for multiple addresses, separate them with “,”, or enter “all”)**

Refer to the figure below:
![](https://main.qcloudimg.com/raw/7291dff6d8be0271c133530b4be49eb2.png)

>?If the images of multiple containers in a Pod are pulled from different repositories, you can enter multiple image repository addresses and separate them with “,”. You can also enter “all”, indicating that all the container image repositories skip certificate verification.

#### HTTP-based image repository
>?By default, an serverless cluster uses the HTTPS protocol to pull images when running, which means if the image repository supports HTTP, it also needs annotations.

With the command `$kubectl describe pod $podname`, if “**http: server gave HTTP response to HTTPS client**” is exported to report an error, it means the image repository that is accessed uses HTTP, as shown in the figure below:
![](https://main.qcloudimg.com/raw/903d96070e1db400a382342940faa227.png)

To solve this problem, you need to add the following annotation to PodTemplate to make it access the image repository through HTTP.
**eks.tke.cloud.tencent.com/registry-http-endpoint: image repository address (for multiple addresses, separate them with “,”, or enter “all”)**

Refer to the figure below:
![](https://main.qcloudimg.com/raw/25b198f03ae26ad1ac8d3be86361655c.png)

>?If the images of multiple containers in a Pod are pulled from different repositories, you can enter multiple image repository addresses and separate them with “,”. You can also enter “all”, indicating that all the container images are pulled through HTTP.




#### Notes

Both annotations above involve the entering of image repository addresses, and you can separate multiple repository addresses with “,”.

>!If the image repository has a port number, include the port number in the image repository address.

For example, if the image address is `10.16.100.174:5000/busybox:latest`, specify the value of the annotation as `10.16.100.174:5000`, which means the image repository address will be `eks.tke.cloud.tencent.com/registry-insecure-skip-verify: 10.16.100.174:5000`.
