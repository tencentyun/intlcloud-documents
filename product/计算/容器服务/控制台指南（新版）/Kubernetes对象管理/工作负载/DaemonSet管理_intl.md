## Overview

A DaemonSet is mainly used to deploy daemons residing in the cluster, such as log collection of the node. It guarantees that the specified Pod is run on all or some nodes. When a new node is added to the cluster, a Pod will be automatically deployed; after the node is removed from the cluster, the Pod will be automatically reclaimed.

## Notes on Scheduling

If the nodeSelector or affinity parameter of the Pod is configured, the Pod managed by the DaemonSet will be scheduled according to the specified scheduling rule. If the nodeSelector or affinity parameter of the Pod is not configured, the Pod will be deployed on all nodes.

## Operation Guide for DaemonSet in the Console

### Creating a DaemonSet

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the ID of the cluster where DaemonSet needs to be created to enter the cluster management page.
4. Select "Workload" > "DaemonSet" to go to the DaemonSet information page. See the figure below:
![DaemonSet](https://main.qcloudimg.com/raw/73b214fcb0cf26e569310894dd44c512.png)
5. Click **Create** to go to the "Create a workload" page. See the figure below:
![Create a DaemonSet](https://main.qcloudimg.com/raw/525bb7049cd0a8435bff6afe7a7f1e93.png)
6. Set the DaemonSet parameters based on actual needs. Key parameters are as follows:
 - Workload name: Custom.
 - Namespace: Select based on actual needs.
 - Type: Select "DaemonSet (run the Pod on each server)".
 - In-Pod containers: Set one or more different containers for a Pod of the DaemonSet based on actual needs.
    - Name: Custom.
    - Image: Select based on actual needs.
    - Image tag: Enter based on actual needs.
    - CPU/memory limits: Set the CPU and memory limit according to [Kubernetes' resource limits](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/) to improve the robustness of the business.
    - Advanced settings: Parameters such as "**working directory**", "**run commands**", "**run parameters**", "**container health check**", and "**privilege level**" can be set.
7. Click **Create a workload** to complete the creation.

### Updating a DaemonSet

#### Updating YAML

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the ID of the cluster where YAML needs to be updated to enter the cluster management page.
4. Select "Workload" > "DaemonSet" to go to the DaemonSet information page. See the figure below:
![DaemonSet](https://main.qcloudimg.com/raw/73b214fcb0cf26e569310894dd44c512.png)
5. In the row of the DaemonSet for which to update the YAML, click **Edit YAML** to go to the DaemonSet updating page.
6. On the "Update a DaemonSet" page, edit the YAML and click **Finish** to update the YAML.

#### Updating an Image
 Rolling update of DaemonSet is only supported in Kubernetes v1.6 or higher.

1. On the cluster management page, click the ID of the cluster for which to update the DaemonSet image to go to the management page of the cluster.
2. In the row of the DaemonSet for which to update the image, click **Update an image**. See the figure below:
![Update a DaemonSet image](https://main.qcloudimg.com/raw/928b50bc33cdb6c64c188c9e7be2099d.png)
3. On the **Roll update an image** page, modify the update method and set the parameters based on actual needs. See the figure below:
![Roll update an image](https://main.qcloudimg.com/raw/c94ee36da1a8c7d0cd25d38607f8c770.png)
4. Click **Finish** to update the image.

## Using kubectl to Manipulate DaemonSet

<span id="YAMLSample"></span>
### YAML Sample
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
>Note: The YAML sample above comes from https://kubernetes.io/docs/concepts/workloads/controllers/daemonset. There may be cases where the container image pulling fails during creation. The sample is only used to describe the composition of DaemonSet.

- kind: This identifies the DaemonSet resource type.
- metadata: Basic information such as DaemonSet name and Label.
- metadata.annotations: An additional description of the DaemonSet. You can set additional enhancements to TKE through this parameter.
- spec.template: Detailed template configuration of the Pod managed by the DaemonSet.

For more information, see [Kubernetes' official document about DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/).

### Using kubectl to Create a DaemonSet

1. See the [YAML sample](#YAMLSample) to prepare the StatefulSet YAML file.
2. Install kubectl and connect to a cluster. For detailed operations, see [Connecting a Cluster via kubectl](https://cloud.tencent.com/document/product/457/8438).
3. Run the following command to create the DaemonSet YAML file.
```shell
kubectl create -f DaemonSet YAML filename
```
For example, to create a StatefulSet YAML file named fluentd-elasticsearch.yaml, run the following command:
```shell
kubectl create -f fluentd-elasticsearch.yaml
```
4. Run the following command to verify whether the creation is successful.
```shell
kubectl get DaemonSet
```
If a message similar to the one below is returned, the creation is successful.
```
NAME       DESIRED   CURRENT   READY     UP-TO-DATE   AVAILABLE   NODE SELECTOR       AGE
frontend   0         0         0         0            0           app=frontend-node   16d
```

### Using kubectl to Update a DaemonSet

Run the following command to view the update policy type of the DaemonSet.
```
kubectl get ds/<daemonset-name> -o go-template='{{.spec.updateStrategy.type}}{{"\n"}}'
```
DaemonSet has the following two update policy types:
- OnDelete: This is the default update policy. With this policy, after the DaemonSet is updated, you have to manually delete the old DaemonSet Pod to create a new one.
- RollingUpdate: This update policy is supported in Kubernetes v1.6 or higher. With this policy, after the DaemonSet template is updated, the old DaemonSet Pod will be terminated, and a new DaemonSet Pod will be created in a rolling update manner.

#### Method 1

Run the following command to update a DaemonSet.
```
kubectl edit DaemonSet/[name]
```
This method is well suited for simple debugging and verification, which is not recommended for direct use in a production environment. You can update any DaemonSet parameters in this way.

#### Method 2

Run the following command to update the image of the specified container.
```
kubectl set image ds/[daemonset-name][container-name]=[container-new-image]
```
It is recommended to keep other DaemonSet parameters unchanged and only update the container image when the business is updated.

### Using kubectl to Roll back a DaemonSet

1. Run the following command to view the update history of the DaemonSet.
```
kubectl rollout history daemonset /[name]
```
2. Run the following command to view the details of the specified version.
```
kubectl rollout history daemonset /[name] --revision=[REVISION]
```
3. Run the following command to roll back to the previous version.
```
kubectl rollout undo daemonset /[name]
```
To specify the version number to roll back, run the following command.
```
kubectl rollout undo daemonset /[name] --to-revision=[REVISION]
```

### Using kubectl to Delete a DaemonSet

1. Run the following command to delete a DaemonSet.
```
kubectl delete  DaemonSet [NAME]
```

