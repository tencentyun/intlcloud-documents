## Overview

A Deployment declares the template of a Pod and the run policy controlling the Pod, which is well suited for deploying stateless applications. You can declare the number of Pod copies running in the Deployment, scheduling policy, and update policy based on your business needs.

## Operation Guide for Deployments in the Console
<span id="creatDeployment"></span>
### Creating a Deployment

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the ID of the cluster where Deployment needs to be created to enter the cluster management page. See the figure below:
![Management page of the cluster where to create a Deployment](https://main.qcloudimg.com/raw/b3fe1321d78bf23c519be9418db5fa15.png)
4. Click **Create** to go to the "Create a workload" page. See the figure below:
![Create a workload](https://main.qcloudimg.com/raw/ba140ea4e1916c988d06654bd2fbbf10.png)
5. Set the Deployment parameters based on actual needs. Key parameters are as follows:
 - Workload name: Custom.
 - Namespace: Select based on actual needs.
 - Type: Select "Deployment (deploy Pods in an extensible manner)".
 - In-Pod containers: Set one or more different containers for a Pod of the Deployment based on actual needs.
    - Name: Custom.
    - Image: Select based on actual needs.
    - Image tag: Enter based on actual needs.
    - CPU/memory limits: Set the CPU and memory limit according to [Kubernetes' resource limits](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/) to improve the robustness of the business.
    - Advanced settings: Parameters such as "**working directory**", "**run commands**", "**run parameters**", "**container health check**", and "**privilege level**" can be set.
 - Pod quantity: Select the adjustment method and set the Pod quantity based on actual needs.
6. Click **Create a workload** to complete the creation. See the figure below:
When the running quantity is equal to the expected quantity, all the Pods under the Deployment have been created.
![Create a workload](https://main.qcloudimg.com/raw/4ac45ef3fbee1a679d12fd4682bd8a1a.png)

### Updating a Deployment

#### Updating YAML

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the ID of the cluster where Deployment needs to be updated to enter the cluster management page. See the figure below:
![Deployment management](https://main.qcloudimg.com/raw/a8a99bc14cf09b4c086bc5d4f4ed3fb1.png)
4. In the row of the Deployment for which to update the YAML, click **More** > **Edit YAML** to go to the Deployment updating page.
5. On the "Update a Deployment" page, edit the YAML and click **Finish** to update the YAML. See the figure below:
![Update YAML](https://main.qcloudimg.com/raw/ddc23ea3fc49bdb05e35c59b67a577ac.png)

#### Updating an Image

1. On the cluster management page, click the ID of the cluster for which to update the Deployment image to go to the management page of the cluster.
2. In the row of the Deployment for which to update the image, click **Update an image**. See the figure below:
![Update an image](https://main.qcloudimg.com/raw/c69b2ce36a946791fde874f938957091.png)
3. On the **Roll update an image** page, modify the update method and set the parameters based on actual needs. See the figure below:
![Roll update an image](https://main.qcloudimg.com/raw/ff07e5dd606f329d7ea8077434f5ce74.png)
4. Click **Finish** to update the image.

### Rolling back a Deployment

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the ID of the cluster where Deployment needs to be rolled back to enter the cluster management page. See the figure below:
![Deployment management](https://main.qcloudimg.com/raw/a8a99bc14cf09b4c086bc5d4f4ed3fb1.png)
4. Click the name of the Deployment to be rolled back to go to the Deployment information page.
5. Select the "Revision log" tab and click **Roll back** in the row of the version to roll back to. See the figure below:
![Rollback](https://main.qcloudimg.com/raw/b49741ebe125822ed1017dea3a9e9813.png)
6. In the "Roll back a resource" prompt box that pops up, click **Submit** to complete the rollback.

### Adjusting Pod Quantity

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the ID of the cluster where Pod quantity needs to be adjusted to enter the cluster management page. See the figure below:
![Deployment management](https://main.qcloudimg.com/raw/a8a99bc14cf09b4c086bc5d4f4ed3fb1.png)
4. In the row of the Deployment for which to adjust the Pod quantity, click **Update Pod quantity** to go to the Pod quantity updating page. See the figure below:
![Update Pod quantity](https://main.qcloudimg.com/raw/7547c1eea420bdc8fa6ed2573fecd2a0.png)
5. Adjust the Pod quantity based on actual needs and click **Update Pod quantity** to complete the adjustment.

## Using kubectl to Manipulate Deployments
<span id="YAMLSample"></span>
### YAML Sample

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

- kind: This identifies the Deployment resource type.
- metadata: Basic information such as Deployment name, Namespace, and Label.
- metadata.annotations: An additional description of the Deployment. You can set additional enhancements to TKE through this parameter.
- spec.replicas: The number of Pods managed by the Deployment.
- spec.selector: Label of the Pod selected by the selector managed by the Deployment.
- spec.template: Detailed template configuration of the Pod managed by the Deployment.

For more details about the parameters, see [Kubernetes' official document about Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/).

### Using kubectl to Create a Deployment

1. See the [YAML sample](#YAMLSample) to prepare the Deployment YAML file.
2. Install kubectl and connect to a cluster. For detailed operations, see [Connecting a Cluster via kubectl](https://cloud.tencent.com/document/product/457/8438).
3. Run the following command to create the Deployment YAML file.
```shell
kubectl create -f Deployment YAML filename
```
For example, to create a Deployment YAML file named nginx.yaml, run the following command:
```shell
kubectl create -f nginx.yaml
```
4. Run the following command to verify whether the creation is successful.
```shell
kubectl get deployments
```
If a message similar to the one below is returned, the creation is successful.
```
NAME             DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
first-workload   1         1         1            0           6h
ng               1         1         1            1           42m
```

### Using kubectl to Update a Deployment

There are three methods to update a Deployment using kubectl. Among them, [method 1](#Method1) and [method 2](#Method2) support both **Recreate** and **RollingUpdate** update policies.
- The Recreate update policy is to first terminate all Pods and then recreate the Deployment.
- The RollingUpdate update policy is to update the Pods of the Deployment one by one in a rolling basis. RollingUpdate also supports pausing update and setting update interval.

<span id="Method1"></span>
#### Method 1

Run the following command to update a Deployment.
```
kubectl edit  deployment/[name]
```
This method is well suited for simple debugging and verification, which is not recommended for direct use in a production environment. You can update any Deployment parameters in this way.

<span id="Method2"></span>
#### Method 2

Run the following command to update the image of the specified container.
```
kubectl set image deployment/[name] [containerName]=[image:tag]
```
It is recommended to keep other Deployment parameters unchanged and only update the container image when the business is updated.

<span id="Method3"></span>
#### Method 3

Run the following command to roll update the specified resource.
```
kubectl rolling-update [NAME] -f FILE
```
For more information about rolling update, see [Notes on Rolling Update](https://kubernetes.io/docs/tasks/run-application/rolling-update-replication-controller/).

### Using kubectl to Roll back a Deployment

1. Run the following command to view the update history of the Deployment.
```
kubectl rollout history deployment/[name]
```
2. Run the following command to view the details of the specified version.
```
kubectl rollout history deployment/[name] --revision=[REVISION]
```
3. Run the following command to roll back to the previous version.
```
kubectl rollout undo deployment/[name]
```
To specify the version number to roll back, run the following command.
```
kubectl rollout undo deployment/[name] --to-revision=[REVISION]
```

### Using kubectl to Adjust Pod Quantity

#### Manually Updating the Pod Quantity

Run the following command to manually update the Pod quantity.
```
kubectl scale deployment [NAME] --replicas=[NUMBER]
```
	 
#### Automatically Updating the Pod Quantity

**Prerequisites**

Turn on the HPA feature of the cluster. HPA is turned on by default for clusters created by TKE.

**Directions**

Run the following command to set automatic scaling for the Deployment.
```
kubectl autoscale deployment [NAME] --min=10 --max=15 --cpu-percent=80
```

### Using kubectl to Delete a Deployment

Run the following command to delete a Deployment.
```
kubectl delete deployment [NAME]
```
