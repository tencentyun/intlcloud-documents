## Overview 

A Deployment declares the Pod template and Pod running policies. It is used to deploy stateless applications. You can specify the number of replicas, scheduling policy, and update policy for Pods running in the Deployment as needed.

## Operation Guide for Deployments in the Console

[](id:creatDeployment)
### Creating a Deployment
1. Log in to the TKE console and select **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Click the ID of the cluster where Deployment needs to be created to enter the cluster management page. See the figure below:
![](https://qcloudimg.tencent-cloud.cn/raw/5b7eef76397c9cf22aa4c317404d2903.png)
3. Click **Create** to go to the **Create Deployment** page and set deployment parameters as needed. Key parameters are described as follows:
 - **Workload**: enter the customized name.
 - **Label**: a key-value pair, which is used for classified management of resources. For more information, see [Querying Resources by Tag](https://intl.cloud.tencent.com/document/product/651/32582).  
 - **Namespace**: select a namespace based on your requirements.
 - **Volume (optional)**: provides storage for the container. It can be a temp path, CVM path, CBS volume, file storage NFS, configuration file and PVC, and it must be mounted to the specified path of the container.
 - **Containers in the Pod**: set one or more different containers for a Pod of the Deployment based on actual needs.
    - **Name**: custom.
    - **Image**: select as needed.
    - **Image Tag**: fill as needed.
    - **Image Pull Policy**: the following three policies are available. Select as needed.
       If you do not set any image pull policy and **Image Tag** is left empty or set to `latest`, the `Always` policy is used. Otherwise, the `IfNotPresent` policy is used.
         - **Always**: always pull the image from the remote end.
         - **IfNotPresent**: a local image is used by default. If no local image is available, the image is pulled remotely.
         - **Never**: only use a local image. If no local image is available, an exception occurs.
    - **Environment Variable**: set the container variables.
    - **CPU/Memory Limit**: set the CPU and memory limit according to [Kubernetes' resource limits](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/) to improve the robustness of the business.
    - **GPU Resource**: you can configure the least GPU resource used by the workload.
    - **Advanced Settings**: parameters such as "**working directory**", "**run commands**", "**run parameters**", "**container health check**", and "**privilege level**" can be set.
 - **Image Access Credential**: a container image is private by default. You need to select the image access credential for the TCR instance when creating a workload.
 - **Number of Pods**: select the adjustment method and set the number of Pods based on actual needs.
     - **Manual Adjustment**: set the number of Pods. You can adjust it by clicking **+** or **-**.
     - **Auto Adjustment**: automatically adjust the number of Pods if any of the set conditions are met. For details, see [Automatic Scaling Basic Operations](https://intl.cloud.tencent.com/document/product/457/32424).   
4. Click **Create Workload** to complete the creation. See the figure below:
When the running quantity is equal to the expected quantity, all Pods under the Deployment have been created.
![](https://main.qcloudimg.com/raw/c458fdbc8d9770d8704327a9dbd16f55.png)

### Updating a Deployment

#### Updating YAML
1. Log in to the TKE console and select **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Click the ID of the cluster for which to update the Deployment to go to the management page of the cluster.
3. In the row of the Deployment for which YAML should be updated, click **More** > **Edit YAML** to go to the Deployment updating page.
5. On the **Update a Deployment** page, edit the YAML and click **Done** to update the YAML.

#### Updating Pod configuration

1. On the cluster management page, click the ID of the cluster for which Pod configuration should be updated to go to the management page of the cluster.
2. In the Deployment row for which Pod configuration needs to be updated, click **Update Pod Configuration**, as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/3877a5185fbcdd0819513f1240384246.png)
3. On the **Update Pod Configuration** page, modify the updating method and set parameters as needed.
4. Click **Update Pod Configuration**.

### Rolling back a Deployment
1. Log in to the TKE console and select **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Click the ID of the cluster for which to roll back the Deployment to go to the management page of the cluster.
3. Click the name of the Deployment to be rolled back to go to the Deployment information page.
5. Select the **Modification History** tab, and click **Rollback** in the row of the version for which rollback is needed, as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/938edee9f304dce3faf51ed0ec09eb46.png)
6. Click **OK** in the **Rollback Resources** prompt box to complete the process.

### Adjusting Pod quantity
1. Log in to the TKE console and select **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Click the ID of the cluster for which to adjust the Pod quantity to go to the management page of the cluster.
3. In the row of the Deployment for which the Pod quantity should be adjusted, click **Update Pod Quantity** to go to the Pod quantity updating page, as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/11a020fc84d6f07346f7e81c43ef9a9f.png)
5. Adjust the Pod quantity based on actual needs and click **Update Number of Instance** to complete the adjustment.

## Using kubectl to Manipulate Deployments

### YAML sample[](id:YAMLSample)
```Yaml
apiVersion: apps/v1beta2
kind: Deployment
metadata:
  name: nginx-deployment
  namespace: default
  labels:
    app: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx-deployment
  template:
    metadata:
      labels:
        app: nginx-deployment
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80
```
- **kind**: this identifies the Deployment resource type.
- **metadata**: basic information such as Deployment name, Namespace, and Label.
- **metadata.annotations**: an additional description of the Deployment. You can set additional enhancements to TKE through this parameter.
- **spec.replicas**: the number of Pods managed by the Deployment.
- **spec.selector**: the label of the Pod selected by the selector managed by the Deployment.
- **spec.template**: detailed template configuration of the Pod managed by the Deployment.

For more details about the parameters, see [Kubernetes' official document about Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/).

### Using kubectl to create a Deployment

1. See the [YAML sample](#YAMLSample) to prepare the Deployment YAML file.
2. Install kubectl and connect to a cluster. For detailed operations, see [Connecting to a Cluster](https://intl.cloud.tencent.com/document/product/457/30639).
3. Run the following command to create the Deployment YAML file.
```shell
kubectl create -f Deployment YAML filename
```
For example, to create a Deployment YAML file named nginx.yaml, run the following command:
```shell
kubectl create -f nginx.yaml
```
4. Run the following command to check whether the Job is successfully created.
```shell
kubectl get deployments
```
If a message similar to the following is returned, the creation is successful.
```
NAME             DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
first-workload   1         1         1            0           6h
ng               1         1         1            1           42m
```

### Using kubectl to update a Deployment

You can update the Deployment through Kubectl in three ways. The [method 1](#Method1) and [method 2](#Method2) support both **Recreate** and **RollingUpdate** update policies.
- The Recreate update policy is to first terminate all Pods and then recreate the Deployment.
- The RollingUpdate is the rolling update policy, which is used to update the Pods of the Deployment one by one on a rolling basis.

<dx-tabs>
::: Method 1[](id:Method1)
Run the following command to update a Deployment.
```
kubectl edit deployment/[name]
```
This method applies to simple debugging verification. It is not recommended to use it in production environments. You can update any Deployment parameters in this way.

:::
::: Method 2[](id:Method2)
Run the following command to update the image of the specified container.
```
kubectl set image deployment/[name] [containerName]=[image:tag]
```
For updates, we recommend that you change none of the Deployment parameters but the one for container's image.
:::
::: Method 3[](id:Method3)
Run the following command to roll update the specified resource.
```
kubectl rolling-update [NAME] -f FILE
```
:::
</dx-tabs>



### Using kubectl to rollback a Deployment

1. Run the following command to view the update history of the Deployment.
```
kubectl rollout history deployment/[name]
```
2. Run the following command to view the details of the specified version.
```
kubectl rollout history deployment/[name] --revision=[REVISION]
```
3. Run the following command to roll back to the earlier version.
```
kubectl rollout undo deployment/[name]
```
To specify the rollback version, run the following command.
```
kubectl rollout undo deployment/[name] --to-revision=[REVISION]
```

### Using kubectl to adjust Pod quantity
<dx-tabs>
::: Manually updating the Pod quantity
Run the following command to manually update the Pod quantity.
```
kubectl scale deployment [NAME] --replicas=[NUMBER]
```
:::
::: Automatically updating the Pod quantity
**Prerequisites**

The HPA features of the cluster is enabled. By default, these features have been enabled for clusters created by TKE.

**Directions**

Run the following command to set automatic scaling for the Deployment.
```
kubectl autoscale deployment [NAME] --min=10 --max=15 --cpu-percent=80
```
:::
</dx-tabs>



### Using kubectl to delete a Deployment

Run the following command to delete a Deployment.
```
kubectl delete deployment [NAME]
```

