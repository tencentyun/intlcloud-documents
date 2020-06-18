## Introduction

DaemonSet is used to deploy resident background programs in the cluster, such as the log daemon. DaemonSet ensures that specified Pods are running on all or certain nodes. When you add new nodes to a cluster, Pods are deployed automatically. When nodes are removed from the cluster, Pods are repossessed automatically.

## Scheduling

If a Pod has nodeSelector or affinity configured, the Pods managed by DaemonSet are scheduled according to existing policies. If not, the Pods are deployed on all nodes.

## Using DaemonSet via the Console

### Creating a DaemonSet
1. Log in to the TKE console and select **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Click the ID of the cluster where DaemonSet needs to be created to enter the cluster management page.
3. Select **Workload** > **DaemonSet** to go to the DaemonSet page as shown below:
![](https://main.qcloudimg.com/raw/ec694431e23d70a8f327fb7ef497480b.png)
4. Click **Create** to go to **Create Workload** page.
Set DaemonSet parameters as needed. The key parameters are as follows:
 - **Workload name**: name of the workload.
 - **Namespace**: select as needed.
 - **Type**: select **DaemonSet (run the Pod on each server)**.
 - **In-Pod containers**: set containers for the DaemonSet Pod.
    - **Name**: enter a name.
    -** Image**: select a desired image.
    - **Image tag**: enter a tag for the image.
    - **Image pull policy**: the following three policies are available. Select as needed.
      If you do not set an image pull policy and **Image Tag** is `latest` or left empty, use `Always`. Otherwise, use `IfNotPresent`.
       - **Always**: the image is always pulled from a remote location.
       - **IfNotPresent**: use the local image by default. If the image is unavailable, pull it from a remote location..
       - **Never**: use local image only. If the image is unavailable, throw an exception.
    - **CPU/memory limits**: set CPU and memory limit according to [Kubernetes resource limits](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/) to improve service robustness.
    - Advanced settings: parameters such as **working directory**, **run commands**, **run parameters**, **container health check**, and "**privilege level**" are found here.
5. Click **Create a workload** to complete the creation.

### Updating a DaemonSet

#### Updating the YAML file
1. Log in to the TKE console and select **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Click the cluster ID for which you want to update the YAML to go to the cluster management page.
3. Select **Workload** > **DaemonSet** to go to the DaemonSet page.
5. In the row of DaemonSet for which YAML is to be updated, click **More** > **Edit YAML**, to go to the “Update a DaemonSet” page.
6. On the "Update a DaemonSet" page, edit the YAML and click **Finish** to update the YAML.

#### Updating Pod Configruations
> Rolling updates of DaemonSet are only supported in Kubernetes v1.6 or later.
>
1. On the cluster management page, click the ID of the cluster for which Pod configurations are to be updated, and go to the management page of the cluster.
2. Click **Update Pod Configurations** that corresponds to the desired DaemonSet.
3. On the “Updating Pod Configurations” page, modify the update method as needed, and set parameters.
4. Click **Finish** to update the Pod configurations.

## Using DaemonSet via kubectl

<span id="YAMLSample"></span>

### Sample YAML file

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
  Template:
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
> The above sample YAML file comes from `https://kubernetes.io/docs/concepts/workloads/controllers/daemonset`. The container image may not be available during creation. The sample is only used to illustrate DaemonSet creation.

- **kind**: DaemonSet resource type.
- **metadata**: information such as the DaemonSet name and label.
- **metadata.annotations**: an additional description of the DaemonSet. You can set additional enhancements to TKE through this parameter.
- **spec.template**: detailed template configuration of the Pod managed by the DaemonSet.

For more information, refer to [Kubernetes official documentation](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/).

### Using kubectl to create a DaemonSet

1. See the [sample YAML file](#YAMLSample) to prepare a StatefulSet YAML file.
2. Install kubectl and connect to a cluster. For details, refer to [Connecting to Clusters](https://intl.cloud.tencent.com/document/product/457/30639).
3. Run the following command to create the DaemonSet YAML file.
```shell
kubectl create -f DaemonSet YAML filename
```
For example, to create a StatefulSet YAML file named fluentd-elasticsearch.yaml, run the following command:
```shell
kubectl create -f fluentd-elasticsearch.yaml
```
4. Run the following command to check whether the file has successfully been created:
```shell
kubectl get DaemonSet
```
A message similar to the one below indicates that the YAML file has successfully been created.
```
NAME       DESIRED   CURRENT   READY     UP-TO-DATE   AVAILABLE   NODE SELECTOR       AGE
frontend   0         0         0         0            0           app=frontend-node   16d
```

### Using kubectl to update a DaemonSet

Run the following command to view the update policy type of the DaemonSet.
```
kubectl get ds/<daemonset-name> -o go-template='{{.spec.updateStrategy.type}}{{"\n"}}'
```
DaemonSet has the following update policy types:
- OnDelete: the default update policy. After the DaemonSet is updated, you have to manually delete the old DaemonSet Pod to create a new one.
- RollingUpdate: Kubernetes 1.6 or later only. After the DaemonSet is updated, the old DaemonSet Pod will be killed, and a new one is created through a rolling update.

#### Method 1

Run the following command to update a DaemonSet.
```
kubectl edit DaemonSet/[name]
```
Use this for debugging or verification. We do not recommended using it in production environments. You can update any DaemonSet parameter this way.

#### Method 2

Run the following command to update the image of a specific container.
```
kubectl set image ds/[daemonset-name][container-name]=[container-new-image]
```
We recommend that you keep other DaemonSet parameters unchanged and only update the container image when updating your service.

### Using kubectl to rollback a DaemonSet

1. Run the following command to view the update history of the DaemonSet.
```
kubectl rollout history daemonset /[name]
```
2. Run the following command to view the details of a specific version.
```
kubectl rollout history daemonset /[name] --revision=[REVISION]
```
3. Run the following command to roll back to the last version.
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
kubectl delete DaemonSet [NAME]
```
