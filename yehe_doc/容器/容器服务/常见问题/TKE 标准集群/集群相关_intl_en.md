## Cluster Creation

### Can I choose not to set a public IP address for the CVM when creating a cluster?

Yes. A CVM instance without a public IP address can only pull images from "My Images" in Image Repository, but cannot pull images from Docker Hub or third-party platforms.
A CVM without a public IP address but with Internet bandwidth can access the Internet by binding an EIP.

### Why do I need to choose a network when creating a cluster?

The selected network and subnet are where the CVM resides. You can add different CVMs to subnets in different AZs for cross-AZ disaster recovery.

### What CVM models are supported when creating a cluster?

We offer Standard, Computing, High-IO, GPU, and BM CVM instances, as displayed in the TKE console.

### What operating systems are supported for TKE hosts?
For more information on the currently operating systems supported by TKE, see [Public Image List](https://intl.cloud.tencent.com/document/product/457/46750)  


### How do I customize Kubelet parameters for a TKE node?
- This feature is made available through an allowlist. To use it, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for application.
- Customize kubelet parameters of a node on the [**Add Node**](https://intl.cloud.tencent.com/document/product/457/30652) page, **Add Exiting Node** page, or **[Create Node Pool](https://intl.cloud.tencent.com/document/product/457/35901)** page.
![](https://qcloudimg.tencent-cloud.cn/raw/d676341888ade202530b6df9e6d1deaa.png)


### How do I customize Kubernetes component parameters when creating a TKE cluster?
For detailed directions, see [Custom Kubernetes Component Launch Parameters](https://intl.cloud.tencent.com/document/product/457/38139).


### Does TKE support self-deployed clusters?

TKE provides an independent Master deployment mode in which you have full control over your cluster. In this mode, the Master and Etcd of the Kubernetes cluster are deployed on the CVM instances you purchased, and you have all the management and operation permissions for the Kubernetes cluster. For more information, see [Independent Master Deployment Mode](https://intl.cloud.tencent.com/document/product/457/31417).

 


### Can I modify the AZ after a TKE serverless cluster is created?	
After a TKE serverless cluster is created successfully, you cannot change or add AZs.


### Can I get IPv6 addresses of TKE clusters on the client?
No.


### Can I export the TKE cluster configuration?

No.

### When a TKE cluster is created, the system prompts me to complete node exception detection plus parameter settings. What should I do?

If you are prompted to complete node exception detection plus parameter settings when creating a cluster, you need to check whether the `NodeProblemDetectorPlus` add-on is selected and configure the parameters if so. For more information, see [NodeProblemDetectorPlus Add-on](https://intl.cloud.tencent.com/document/product/457/38784).
>? If you are unable to evaluate whether you need this add-on, we recommend you create the cluster directly without selecting it. If you need to use it later, simply install it in add-on management.

 

### How do I enable IPVS for TKE clusters?
For detailed directions, see [Enabling IPVS for a Cluster](https://intl.cloud.tencent.com/document/product/457/30641).

 

### How do I view TKE cluster access credentials?

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2/cluster?rid=4) and click **Cluster** in the left sidebar to enter the cluster management page.
2. Click the ID or name of the target cluster to enter the cluster details page.
3. Click **Basic information** in the left sidebar. You can view information such as the access address, public network/private network access status, and kubeconfig access credential of the cluster in the **Cluster APIServer information** section of the **Basic information** page.



### How do I add CVM instances under other accounts to a TKE cluster?	
Currently, you cannot add CVM instances under other accounts to a cluster. You can only add CVM instances in the same VPC.


### What should I do if "certificate verify failed: self signed certificate" is reported when I use the Kubernetes SDK to connect the API server of the cluster?

As the API server in a Kubernetes cluster usually uses a self-signed TLS certificate, which is not trusted by the request library on an earlier Python version or the default settings of Node.js, an error will be reported. This error can be fixed in the following steps:
1. Add the configuration to skip server authentication.
If you use the Node.js SDK, you need to set the environment variable:
```
export NODE_TLS_REJECT_UNAUTHORIZED="0";
```
If you use the Python SDK, you need to set it in `kubeconfig`. 
```
clusters:
- cluster:
    insecure-skip-tls-verify: true
```
2. Put the public key of the root certificate of the self-signed certificate issuing authority in the list of trusted root certificates of the system.

## Cluster Network


### What should I do for the cluster network when I develop a custom webhook?
When you develop a custom webhook, do not block Pods under `kube-system namespace`; otherwise, you cannot use the cluster network normally.

## Adding CVM Instances

### What are the limitations on adding CVMs to a cluster?

You can only choose the CVMs in the same region as the cluster. But you may choose a different AZ to implement cross-AZ deployment of the cluster.

### Is there a limit on the number of CVMs?

Yes. The number of pay-as-you-go CVMs cannot exceed the usage quota of the current account. For details, see [CVM Overview](https://console.cloud.tencent.com/cvm/overview).

## CVM Termination

### After a CVM instance is terminated, what will happen to the containers deployed on it?

When a CVM instance is terminated, the resources it contains, such as containers, will also be terminated. If the number of containers for a service drops below the expected number of running containers, the cluster will launch more containers in other CVM instances until the desired number is reached.
