>? We plan to carry out an operation from 23:00 September 21，2020 (Monday) to 06:00 September 22,2020 (Tuesday) UTC+8 to stop delivering the Kubeconfig file.

## Background
Currently, TKE stores the Kubeconfig file with the admin token in nodes by default. By using this Kubeconfig file, users can easily operate on Kubernetes clusters. However, if users fail to conduct node login permission management carefully, clusters may face security risks. Therefore, we decided to stop delivering the Kubeconfig file.

Existing clusters may use the Kubeconfig file to perform cluster initialization operations in user-defined scripts. To solve this issue, we will provide a client certificate for node initialization with the same permissions as the Kueconfig file, but with a validity period of only 12 hours. After the certificate expires, the Kubeconfig file will be invalidated. If you still need the file after the expiration, refer to [Issues and Solutions](#QA).

>! If you still require default long-term admin permissions instead of a Kubeconfig file whose validity period is only 12 hours for some special scenarios, or if you encounter any other issues, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact us.



[](id:QA)


## Issues and Solutions

#### Issues
If you prefer to use the following command to log in to a TKE cluster node for kubectl operations, you will be prompted with the following error message:
```bash
$ kubectl get node
The connection to the server localhost:8080 was refused - did you specify the right host or port?
```

```bash
$ kubectl get node
error: You must be logged in to the server (Unauthorized)
```

#### Solutions
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. Obtain the credential Kubeconfig file of the current account. For more information, see [Obtaining credentials](https://intl.cloud.tencent.com/document/product/457/37368).
3. After obtaining the Kubeconfig file, you can enable private network access or directly use the service IP address of Kubernetes.
 - Enabling private network access: on the cluster details page, choose **Basic Information** in the left sidebar, enable **Private Network Access** in the **Cluster API Server information** section, and operate according to the prompt.
 - Using the service IP address of Kubernetes: on the cluster details page, choose **Services and Routes** > **Service** in the left sidebar to obtain the service IP address of Kubernetes in the default namespace. Replace the clusters.cluster.server field in the Kubeconfig file with https://\<`IP`\>:443.
4. Copy the content of the Kubeconfig file to `$HOME/.kube/config` on the new node.
5. Access a Kubeconfig cluster and use `kubectl get nodes` to test connectivity.

## Handling Special Scenarios
#### Special scenarios
A workload has mounted the `/root/.kube/config` or `/home/ubuntu/.kube/config` file of the host for use.
#### Solutions
Use Kubernetes serviceaccount correctly to access clusters in incluster mode. For more information, see [Configure Service Accounts for Pods](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/).
