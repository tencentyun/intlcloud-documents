## Introduction

A Deployment declares the Pod template and the policies for running the Pod. It is used to deploy stateless applications. You can specify the number of replicas, scheduling policy, and update policy for the Pod running in the Deployment as needed.

## Using Deployments via the Console

<span id="creatDeployment"></span>
### Creating a Deployment
1. Log in to the TKE console and select **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Click the ID of the cluster where Deployment needs to be created to enter the cluster management page.
3. Click **Create** to go to the "Create a workload" page.
Set Deployment parameters as needed. Key parameters are as follows:
 - **Workload name**: name of the workload.
 - **Namespace**: select a namespace.
 - **Type**: select **Deployment (deploy Pods in an extensible manner)**.
 - **In-Pod containers**: set one or more containers for a Pod of the Deployment.
    - **Name**: enter a name.
    - **Image**: select an image.
    - **Image tag**: tag of the image.
    - **Image pull policy**: select one of the following.
       If you do not set a image pull policy and **Image tag** is `latest` or left empty, `Always` is used. Otherwise, `IfNotPresent` is used.
         - **Always**: the image is always pulled from a remote location.
         - **IfNotPresent**: use local image by default. If the image is unavailable locally, pull it from a remote location.
         - **Never**: use local image only. If the image is unavailable locally, throw an exception.
    - **CPU/memory limits**: set the CPU and memory limit according to [Kubernetes' resource limits](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/) to improve the robustness of the business.
    - **Advanced settings**: parameters such as **working directory**, **run commands**, **run parameters**, **container health check**, and **privilege level** are found here.
 - **Pod quantity**: select the adjustment method and set the Pod quantity.
4. Click **Create Workload** to complete the creation, as shown in the following figure.
When the running quantity is equal to the expected quantity, all Pods under the Deployment are created.
![](https://main.qcloudimg.com/raw/c458fdbc8d9770d8704327a9dbd16f55.png)

### Updating a Deployment

#### Updating the YAML file
1. Log in to the TKE console and select **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
3. Click the ID of the cluster for which the Deployment should be updated to go to the management page of the cluster, as shown below:
![](https://main.qcloudimg.com/raw/7e7acba7f2d84a9a0626458efb357ff0.png)
3. In the row of the Deployment for which YAML should be updated, click **More** > **Edit YAML** to go to the Deployment updating page.
5. On the "Update Deployment" page, edit the YAML and click **Finish** to update the YAML, as shown below:
![Update YAML](https://main.qcloudimg.com/raw/93c576f09ad8817abb794385f68b38ad.png)

#### Updating Pod configurations

1. On the cluster management page, click the ID of the cluster for which Pod configurations should be updated to go to the management page of the cluster.
2. In the DaemonSet row for which Pod configurations need to be updated, click **Update Pod Configurations**.
3. On the **Update Pod Configurations** page, modify the update method and set parameters as needed.
4. Click **Finish** to update the configurations.

### Rolling back a Deployment
1. Log in to the TKE console and select **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Click the ID of the cluster for which Deployment rollback is needed to go to the management page of the cluster.
4. Click the name of the Deployment to be rolled back to go to the Deployment information page.
5. Select the **Modification History** tab, and click **Rollback** in the row of the version for which rollback is needed.

6. In the "Roll back a resource" page, click **Submit** to complete the rollback.

### Adjusting Pod quantity
1. Log in to the TKE console and select **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Click the ID of the cluster for which Pod quantity should be adjusted to go to the management page of the cluster.
3. In the row of the Deployment for which the Pod quantity should be adjusted, click **Update Pod quantity** to go to the Pod quantity updating page.
5. Adjust the Pod quantity based on actual needs and click **Update Pod quantity** to complete the adjustment.

## Using Deployments via kubectl

### Sample YAML file <span id="YAMLSample"></span>
```Yaml
apiVersion: apps/v1beta2
kind: Deployment
metadata:
  name: nginx-deployment
  namespace: default
  labels:
    app: nginx-deployment
"spec":
  replicas: 3
  selector:
    matchLabels:
      app: nginx-deployment
  Template:
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
- **kind**: Deployment resource type.
- **metadata**: information such as Deployment name, Namespace, and Label.
- **metadata.annotations**: an additional description of the Deployment. You can set additional enhancements to TKE through this parameter.
- **spec.replicas**: the number of Pods managed by the Deployment.
- **spec.selector**: the label of the Pod selected by the selector managed by the Deployment.
- **spec.template**: detailed template configuration of the Pod managed by the Deployment.

For more details about the parameters, refer to [Kubernetes official documentation](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/).

### Using kubectl to create a Deployment

1. See the [sample YAML file](#YAMLSample) to prepare the Deployment YAML file.
2. Install kubectl and connect to a cluster. For details, refer to [Connecting to Clusters](https://intl.cloud.tencent.com/document/product/457/30639).
3. Run the following command to create the Deployment YAML file.
```shell
kubectl create -f Deployment YAML filename
```
For example, to create a Deployment YAML file named nginx.yaml, run the following command:
```shell
kubectl create -f nginx.yaml
```
4. Run the following command to check whether the Service YAML file has successfully been created:
```shell
kubectl get deployments
```
A message similar to the one below indicates that the file has been created successfully.
```
NAME             DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
first-workload   1         1         1            0           6h
ng               1         1         1            1           42m
```

### Using kubectl to update a Deployment

You can use kubectl to update a Deployment in the following ways. The [first](#Method1) and [second](#Method2) method support both **Recreate** and **RollingUpdate** update policies.
- Recreate: all Pods are terminated and recreated using the Deployment.
- RollingUpdate: each Pod is updated one by one. RollingUpdate also supports pausing and update intervals.

<span id="Method1"></span>
#### Method 1

Run the following command to update a Deployment.
```
kubectl edit deployment/[name]
```
Use this for debugging and verification. We do not recommended using it in production environments. You can update any Deployment parameters this way.

<span id="Method2"></span>
#### Method 2

Run the following command to update the image of a specific container.
```
kubectl set image deployment/[name] [containerName]=[image:tag]
```
We recommend that you keep parameters unchanged and update the container image only when updating your service.

<span id="Method3"></span>
#### Method 3

Run the following command to perform a rolling update on the specified resources.
```
kubectl rolling-update [NAME] -f FILE
```
For more information, refer to [Rolling Update](https://kubernetes.io/docs/tasks/run-application/rolling-update-replication-controller/).

### Using kubectl to rollback a Deployment

1. Run the following command to view the update history of the Deployment.
```
kubectl rollout history deployment/[name]
```
2. Run the following command to view the details of a specific version.
```
kubectl rollout history deployment/[name] --revision=[REVISION]
```
3. Run the following command to rollback to the last version.
```
kubectl rollout undo deployment/[name]
```
To specify the version to rollback to, run the following command.
```
kubectl rollout undo deployment/[name] --to-revision=[REVISION]
```

### Using kubectl to update Pod quantity

#### Manually updating the Pod quantity

Run the following command to manually update the Pod quantity.
```
kubectl scale deployment [NAME] --replicas=[NUMBER]
```

#### Automatically updating Pod quantity

**Prerequisites**

HPA is enabled. TKE created clusters have HPA enabled by default.

**Directions**

Run the following command to set automatic scaling for the Deployment.
```
kubectl autoscale deployment [NAME] --min=10 --max=15 --cpu-percent=80
```

### Using kubectl to delete a Deployment

Run the following command to delete a Deployment.
```
kubectl delete deployment [NAME]
```
