## Overview

DaemonSet is used to deploy resident background programs in the cluster. For example, it can collect logs for a node. DaemonSet ensures that specified Pods are running on all or certain nodes. When you add new nodes to a cluster, Pods are deployed automatically. When nodes are removed from the cluster, Pods are recovered automatically.

## Notes on Scheduling

If nodeSelector or affinity parameters are configured on the Pod, the Pod managed by DaemonSet is scheduled based on the specified rules. If the nodeSelector or affinity parameters are not configured on the Pod, the Pod will be deployed on all nodes.

## Operation Guide for DaemonSet in the Console

### Creating a DaemonSet
1. Log in to the TKE console and select **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Click the ID of the cluster where DaemonSet needs to be created to enter the cluster management page.
3. Select **Workload** > **DaemonSet** to go to the DaemonSet information page. See the figure below:
![](https://main.qcloudimg.com/raw/ec694431e23d70a8f327fb7ef497480b.png)
4. Click **Create** to open the **Create Workload** page.
Set DaemonSet parameters as needed. The key parameters are as follows:
 - **Workload**: enter the customized name.
 - **Label**: a key-value pair, which is used for classified management of resources.
 - **Namespace**: select a namespace based on your requirements.
 - **Type**: select **DaemonSet (run the Pod on each server)**.
 - **Volume (optional)**: provides storage for the container. It can be a temp path, CVM path, CBS volume, file storage NFS, configuration file and PVC, and it must be mounted to the specified path of the container.
 - **Containers in the Pod**: set one or more different containers for a Pod of the DaemonSet based on actual needs.
    - **Name**: custom.
    - **Image**: select as needed.
    - **Image Tag**: fill as needed.
    - **Image Pull Policy**: the following three policies are available. Select as needed.
      If you do not set any image pull policy and **Image Tag** is left empty or `latest`, the `Always` policy is used. Otherwise, the `IfNotPresent` policy is used.
       - **Always**: always pull the image from the remote end.
       - **IfNotPresent**: a local image is used by default. If no local image is available, the image is pulled remotely.
       - **Never**: only use a local image. If no local image is available, an exception occurs.
    - **CPU/Memory Limit**: set the CPU and memory limit according to [Kubernetes' resource limits](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/) to improve the robustness of the business.
    - **GPU Resource**: you can configure the least GPU resource used by the workload.
    - Advanced Settings: you can set the parameters such as **Working Directory**, **Running Command**, **Running Parameter**, **Container Health Check**, and **Privileged Container**.
 - **Image Access Credential**: a container image is private by default. You need to select the image access credential for the TCR instance when creating a workload.
 - **Node Scheduling Policy**: the Pod can be scheduled to the node of the Label that meets the expectation according to the scheduling rules.
5. Click **Create Workload** to complete the process.

### Updating a DaemonSet

#### Updating YAML
1. Log in to the TKE console and select **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Click the ID of the cluster for which to update the YAML to go to the management page of the cluster.
4. Select **Workload** > **DaemonSet** to go to the DaemonSet information page. See the figure below:
![](https://qcloudimg.tencent-cloud.cn/raw/c001d6fd4cdefaeed125b341099bd465.png)
5. In the row of DaemonSet for which YAML is to be updated, click **More** > **Edit YAML** to go to the DaemonSet updating page.
6. On this page, edit the YAML and click **Done** to update the YAML.

#### Updating Pod configuration
>? Rolling update of DaemonSet is only supported in Kubernetes v1.6 or higher.
>
1. On the cluster management page, click the ID of the cluster for which Pod configuration should be updated, and go to the management page of the cluster.
2. In the DaemonSet row for which Pod configuration needs to be updated, click **Update Pod Configuration**, as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/833a33caefa780ec962b12a1ccc825ee.png)
3. On the **Update Pod Configuration** page, modify the updating method and set parameters as needed, as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/51e24a5ddbc44f4e342ee9e4d0d39d67.png)
4. Click **Done** to update the Pod configuration.

## Using kubectl to Manipulate DaemonSet


### YAML sample[](id:YAMLSample)
```Yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: fluentd-elasticsearch
  namespace: kube-system
  labels:
    k8s-app: fluentd-logging
spec:
  selector:
    matchLabels:
      name: fluentd-elasticsearch
  template:
    metadata:
      labels:
        name: fluentd-elasticsearch
    spec:
      tolerations:
      - key: node-role.kubernetes.io/master
        effect: NoSchedule
      containers:
      - name: fluentd-elasticsearch
        image: k8s.gcr.io/fluentd-elasticsearch:1.20
        resources:
          limits:
            memory: 200Mi
          requests:
            cpu: 100m
            memory: 200Mi
        volumeMounts:
        - name: varlog
          mountPath: /var/log
        - name: varlibdockercontainers
          mountPath: /var/lib/docker/containers
          readOnly: true
      terminationGracePeriodSeconds: 30
      volumes:
      - name: varlog
        hostPath:
          path: /var/log
      - name: varlibdockercontainers
        hostPath:
          path: /var/lib/docker/containers
```
>!Note: The YAML sample described above comes from `https://kubernetes.io/docs/concepts/workloads/controllers/daemonset`. The container image may not be got during creation. The sample is only used to describe the composition of DaemonSet.

- **kind**: this identifies the DaemonSet resource type.
- **metadata**: basic information such as the DaemonSet name and label.
- **metadata.annotations**: an additional description of the DaemonSet. You can set additional enhancements to TKE through this parameter.
- **spec.template**: detailed template configuration of the Pod managed by the DaemonSet.

For more information, see [Kubernetes' official document about DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/).

### Using kubectl to create a DaemonSet

1. Prepare the StatefulSet YAML file as instructed by [YAML sample](#YAMLSample).
2. Install kubectl and connect to a cluster. For detailed operations, see [Connecting to a Cluster](https://intl.cloud.tencent.com/document/product/457/30639).
3. Run the following command to create the DaemonSet YAML file.
```shell
kubectl create -f <DaemonSet YAML filename>
```
For example, to create a StatefulSet YAML file named fluentd-elasticsearch.yaml, run the following command:
```shell
kubectl create -f fluentd-elasticsearch.yaml
```
4. Run the following command to check whether the Job is successfully created.
```shell
kubectl get DaemonSet
```
If a message similar to the following is returned, the creation is successful.
```
NAME       DESIRED   CURRENT   READY     UP-TO-DATE   AVAILABLE   NODE SELECTOR       AGE
frontend   0         0         0         0            0           app=frontend-node   16d
```

### Using kubectl to update a DaemonSet

Run the following command to view the update policy type of the DaemonSet.
```
kubectl get ds/<daemonset-name> -o go-template='{{.spec.updateStrategy.type}}{{"\n"}}'
```
DaemonSet has the following two update policy types:
-OnDelete: default update policy. With this policy, after the DaemonSet is updated, you have to manually delete the old DaemonSet Pod to create a new one.
-RollingUpdate: Kubernetes 1.6 or later is supported. With this policy, after the DaemonSet template is updated, the old DaemonSet Pod will be killed, and a new one will be created in a rolling update manner.

#### Method 1

Run the following command to update a DaemonSet.
```
kubectl edit DaemonSet/[name]
```
This method applies to simple debugg verification. It is not recommended to use it in production environments. You can update any DaemonSet parameters in this way.

#### Method 2

Run the following command to update the image of the specified container.
```
kubectl set image ds/[daemonset-name][container-name]=[container-new-image]
```
It is recommended to keep other DaemonSet parameters unchanged and only update the container image when the business is updated.

### Using kubectl to rollback a DaemonSet

1. Run the following command to view the update history of the DaemonSet.
```
kubectl rollout history daemonset /[name]
```
2. Run the following command to view the details of the specified version.
```
kubectl rollout history daemonset /[name] --revision=[REVISION]
```
3. Run the following command to roll back to the earlier version.
```
kubectl rollout undo daemonset /[name]
```
To specify the rollback version, run the following command.
```
kubectl rollout undo daemonset /[name] --to-revision=[REVISION]
```

### Using kubectl to delete a DaemonSet
Run the following command to delete a DaemonSet.
```
kubectl delete  DaemonSet [NAME]
```

