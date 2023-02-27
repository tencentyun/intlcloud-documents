## Use Cases 

The non-static IP address mode is suitable for the scenarios where the service does not rely on static IPs of the container. For example, stateless services and stateless offline applications that can deploy multiple copies.

## Features and Limitations

- The node can maintain available ENI/IP pool, so that the Pod can be rebuilt quickly in a massive way.
- It supports the pre-binding policy, so that the Pod can be scaled out quickly.
- It supports auto scaling of ENIs/IPs to avoid waste of IPs and improve their utilization rate.
- `0` cannot be set for the pre-binding. That means fully on-demand allocation is not supported for now, and waste of IPs may occur if there are too many nodes.




## IP Address Management Principle
TKE maintains an auto-scaling exclusive ENI/IP pool on each node. The number of bound exclusive ENIs/IPs ranges from **the number of Pods + the minimum number of pre-bound ENIs/IPs** to **the number of Pods + the maximum number of pre-bound ENIs/IPs**.
- When **the number of bound ENIs/IPs is less than the number of Pods + the minimum number of pre-bound ENIs/IPs**, new exclusive ENIs/IPs will be bound to make **the number of bound ENIs/IPs = the number of Pods + the minimum number of pre-bound ENIs/IPs**.
- When **the number of bound ENIs/IPs is larger than the number of Pods + the maximum number of pre-bound ENIs/IPs**, an ENI/IP will be released about every 2 minutes until **the number of bound ENIs/IPs = the number of Pods + the maximum number of pre-bound ENIs/IPs**.
- When **the maximum number of bindable ENIs/IPs is less than the number of bound ENIs/IPs, the unnecessary idle exclusive ENIs/IPs will be released directly to make **the number of bound ENIs/IPs equal to the maximum number of bindable ENIs/IPs**.

## How to Use


#### Enabling non-static IP address
Select non-static IP address of VPC-CNI mode when creating a cluster. That means you should not check **Enable Support** for **Static Pod IP**.
![](https://qcloudimg.tencent-cloud.cn/raw/f8bfc9f1ebfcca8253d3296537e163d0.png)


### Supporting quick release

The ENI/IP pool managed in non-static IP address mode applies the policy of slow release by default. Only one unnecessary idle ENI/IP is released every two minutes. If you want to utilize IPs more efficiently, you need to enable "quick release". In this mode, the ENI/IP pool is checked every two minutes to release unnecessary idle ENIs/IPs until the number of idle ENIs/IPs is equal to the maximum number of pre-bound ENIs/IPs. The methods for enabling quick release are as follows:

#### tke-eni-ipamd v3.5.0 or later

1. Log in to the [TKE console](https://console.qcloud.com/tke2) and click **Cluster** in the left sidebar.
2. On the **Cluster Management** page, click the ID of the target cluster to go to the cluster details page.
3. On the cluster details page, select **Add-On Management** in the left sidebar.
4. On the **Add-On Management** page, click **Update configuration** in the **Operation** column of the **eniipamd** add-on.
5. On the **Update configuration** page, select **Quick release**, and click **Done**.

#### tke-eni-ipamd earlier than v3.5.0 or no eniipamd to manage

- Run the command `kubectl edit ds tke-eni-agent -n kube-system` to modify the existing tke-eni-agent daemonset.
- Add the following launch parameter to `spec.template.spec.containers[0].args` to enable "quick release". The tke-eni-agent will update and make the feature take effect on a rolling basis after the modification.
```
- --enable-quick-release
```

### Specifying the number of pre-bound ENIs/IPs on a node
You can specify the number of pre-bound ENIs/IPs by modifying the annotation of CRD `NEC` corresponding to the node.
```
# Specifying the minimum number of pre-bound ENIs/IPs in shared ENI mode
"tke.cloud.tencent.com/route-eni-ip-min-warm-target"
# Specifying the maximum number of pre-bound ENIs/IPs in shared ENI mode
"tke.cloud.tencent.com/route-eni-ip-max-warm-target"
# Specifying the minimum number of pre-bound ENIs/IPs in exclusive ENI mode
"tke.cloud.tencent.com/direct-eni-min-warm-target"
# Specifying the maximum number of pre-bound ENIs/IPs in exclusive ENI mode
"tke.cloud.tencent.com/direct-eni-max-warm-target"
```
How to modify:
```
# Sample: modify the minimum number of pre-bound IPs on <nodeName> to 1
kubectl annotate nec <nodeName> "tke.cloud.tencent.com/route-eni-ip-min-warm-target"="1" --overwrite
# Sample: modify the maximum number of pre-bound IPs on <nodeName> to 3
kubectl annotate nec <nodeName> "tke.cloud.tencent.com/route-eni-ip-max-warm-target"="3" --overwrite
```
- Dynamic check for pre-binding is triggered immediately after the modification. If the number of pre-bound ENIs/IPs is insufficient, ENIs/IPs will be bound until the number meets your requirement. Otherwise, the ENIs/IPs will be unbound.
- The two annotations must exist at the same time when you perform the modification, and the condition of `0 <= the minimum number of pre-bound ENIs/IPs <= the maximum number of pre-bound ENIs/IPs` must be met. Otherwise, the modification will be failed.

### Specifying the maximum number of bindable ENIs/IPs on a node
You can specify the maximum number of bindable ENIs/IPs on a node by modifying the annotation of CRD `nec` corresponding to the node. You can use the following annotations to specify the maximum number of bindable ENIs and the maximum number of bindable IPs on a single ENI.
```
# Specifying the maximum number of bindable ENIs in shared ENI mode
kubectl annotate nec <nodeName> "tke.cloud.tencent.com/route-eni-max-attach"="1" --overwrite
# Specifying the number of bindable IPs on a single ENI in shared ENI mode
kubectl annotate nec <nodeName> "tke.cloud.tencent.com/max-ip-per-route-eni"="9" --overwrite
# Specifying the maximum number of bindable exclusive ENIs in exclusive ENI mode
kubectl annotate nec <nodeName> "tke.cloud.tencent.com/direct-eni-max-attach"="5" --overwrite
```
You must ensure that the value you entered for modification is not less than the number of ENIs/IPs currently in use on the node. Otherwise, the modification will be failed.
Dynamic check for pre-binding is triggered immediately after the modification. If `the number of bound ENIs/IPs > the maximum number of bindable ENIs/IPs`, the ENIs/IPs will be unbound until `the number of bound ENIs/IPs = the maximum number of bindable ENIs/IPs`.

### Specifying the default number of pre-bound ENIs/IPs

#### tke-eni-ipamd v3.5.0 or later

1. Log in to the [TKE console](https://console.qcloud.com/tke2) and click **Cluster** in the left sidebar.
2. On the **Cluster Management** page, click the ID of the target cluster to go to the cluster details page.
3. On the cluster details page, select **Add-On Management** in the left sidebar.
4. On the **Add-On Management** page, click **Update configuration** in the **Operation** column of the **eniipamd** add-on.
5. On the **Update configuration** page, enter the pre-bound default values for the shared and exclusive ENI modes, and click **Done**.

#### tke-eni-ipamd earlier than v3.5.0 or no eniipamd to manage

- Run the command `kubectl edit deploy tke-eni-ipamd -n kube-system` to modify the existing tke-eni-ipamd deployment.
- Add the following launch parameter to `spec.template.spec.containers[0].args` to modify the default number of pre-bound ENIs/IPs. The ipamd will restart and take effect automatically after the modification. The default number only affects the added nodes.
```
# The default number of minimum pre-bound ENIs/IPs in shared ENI mode. Default value: 5
  - --ip-min-warm-target=3
# The default number of maximum pre-bound ENIs/IPs in shared ENI mode. Default value: 5
  - --ip-max-warm-target=3
# The default number of minimum pre-bound ENIs/IPs in exclusive ENI mode. Default value: 1
  - --eni-min-warm-target=3
# The default number of maximum pre-bound ENIs/IPs in exclusive ENI mode. Default value: 1
  - --eni-max-warm-target=3
```
