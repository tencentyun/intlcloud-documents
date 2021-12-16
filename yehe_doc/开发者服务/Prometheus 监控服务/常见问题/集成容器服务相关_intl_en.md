### What should I do if I can't access the TKE cluster over the private network?[](id:question1)

When installing an agent, you need to access TKE over the private network. If **private network access** is not enabled for the corresponding TKE cluster, the installation will fail. You can solve this problem by following the steps below:
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2/cluster?rid=1) and select a container cluster in the corresponding region.
2. Enable **Private Network Access** under **Basic Information** > **Cluster APIServer Information**.

### What should I do if the status of all kube-proxy collection targets is "Down"?[](id:question2)

In TKE, the launch parameter `--metrics-bind-address` is not specified for kube-proxy, and the default listening address of the metrics service is 127.0.0.1; therefore, the agent cannot pull metrics by Pod IP. You can solve this problem by following the steps below:
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2/cluster?rid=1) and select a container cluster in the corresponding region.
2. Go to **Basic Information** > **Cluster APIServer Information** > **Connecting to Kubernetes cluster through Kubectl** to configure Kubectl as instructed.
3. Run `kubectl edit ds kube-proxy -n kube-system` and add the launch parameter `--metrics-bind-address=0.0.0.0` in `spec.template.spec.containers.args`.

### What should I do if the status of all component collection targets on the master node in a dedicated TKE cluster is "Down"?[](id:question3)

The inbound rule of the default security group of the master node in a dedicated TKE cluster does not allow access to the metrics ports of some components. You can solve this problem by following the steps below:
1. Log in to the [Security Group console](https://console.cloud.tencent.com/vpc/securitygroup?rid=1) and select the corresponding region.
2. Enter `tke-master-security-for-<tke cluster id>` in the security group search box. For example, if the cluster ID is `cls-xxx`, then enter `tke-master-security-for-cls-xxx`.
3. Click the returned security group ID to enter the **Edit Inbound Rule** window.
4. The protocol port column of the rule to be edited should include `TCP:60001,60002`. Select the rules one by one and add ports 10249, 10252, 10251, 9100, and 9153 for the following purposes respectively:
  - 10249: kube-proxy metrics port
  - 10252: kube-controller-manager metrics port
  - 10251: kube-scheduler metrics port 
  - 9100: node-exporter metrics port
  - 9153: core-dns metrics port
