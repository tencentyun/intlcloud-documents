## Overview

A StatefulSet is primarily used to manage stateful applications, and a created Pod has a persistent identifier for creation according to the specification. The identifier will remain after the Pod is migrated, terminated, or restarted. When you need persistent storage, you can match the storage volumes one to one based on the identifier. If your application does not require a persistent identifier, you are recommended to use a Deployment to deploy the application.

## Operation Guide for StatefulSets in the Console

<span id="createStatefulSet"></span>
### Creating a StatefulSet

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left navigation pane, click **Clusters** to go to the cluster management page.
3. Click the ID of the cluster where to create the StatefulSet to go to the management page of the cluster.
4. Select "Workload" > "StatefulSet" to go to the StatefulSet information page. See the figure below:
![StatefulSet](https://main.qcloudimg.com/raw/7d6d1ddb1b1580f34519dc62d6bab3d8.png)
5. Click **Create** to go to the "Create a workload" page. See the figure below:
![Create a workload](https://main.qcloudimg.com/raw/9c53cf0e24719da48ce4905603c4e4d3.png)
6. Set the StatefulSet parameters based on actual needs. Key parameters are as follows:
 - Workload name: Custom.
 - Namespace: Select based on actual needs.
 - Type: Select "StatefulSet (run the Pod in a stateful manner)".
 - In-Pod containers: Set one or more different containers for a Pod of the StatefulSet based on actual needs.
    - Name: Custom.
    - Image: Select based on actual needs.
    - Image tag: Enter based on actual needs.
    - CPU/memory limits: Set the CPU and memory limit according to [Kubernetes' resource limits](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/) to improve the robustness of the business.
    - Advanced settings: Parameters such as "**working directory**", "**run commands**", "**run parameters**", "**container health check**", and "**privilege level**" can be set.
 - Pod quantity: Select the adjustment method and set the Pod quantity based on actual needs.
7. Click **Create a workload** to complete the creation.

### Updating a StatefulSet

#### Updating YAML

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left navigation pane, click **Clusters** to go to the cluster management page.
3. Click the ID of the cluster for which to update the YAML to go to the management page of the cluster.
4. Select "Workload" > "StatefulSet" to go to the StatefulSet information page. See the figure below:
![StatefulSet](https://main.qcloudimg.com/raw/7d6d1ddb1b1580f34519dc62d6bab3d8.png)
5. In the row of the StatefulSet for which to update the YAML, click **Edit YAML** to go to the StatefulSet updating page.
6. On the "Update a StatefulSet" page, edit the YAML and click **Finish** to update the YAML.

#### Updating an Image

1. On the cluster management page, click the ID of the cluster for which to update the StatefulSet image to go to the management page of the cluster.
2. In the row of the StatefulSet for which to update the image, click **Update an image**. See the figure below:
![Update a StatefulSet image](https://main.qcloudimg.com/raw/208eae0b4970c0f800e16722263d6a00.png)
3. On the **Roll update an image** page, modify the update method and set the parameters based on actual needs. See the figure below:
![Roll update an image](https://main.qcloudimg.com/raw/2d67ba80dcfe3fff0e572b69aea59068.png)
4. Click **Finish** to update the image.

## Using kubectl to Manipulate StatefulSets

<span id="YAMLSample"></span>
### YAML Sample

```Yaml
apiVersion: v1
kind: Service  ## Create a Headless Service to control the network domain
metadata:
  name: nginx
  namespace: default
  labels:
    app: nginx
spec:
  ports:
  - port: 80
    name: web
  clusterIP: None
  selector:
    app: nginx
---
apiVersion: apps/v1
kind: StatefulSet ### Create a Nginx StatefulSet
metadata:
  name: web
  namespace: default
spec:
  selector:
    matchLabels:
      app: nginx
  serviceName: "nginx"
  replicas: 3 # by default is 1
  template:
    metadata:
      labels:
        app: nginx
    spec:
      terminationGracePeriodSeconds: 10
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80
          name: web
        volumeMounts:
        - name: www
          mountPath: /usr/share/nginx/html
  volumeClaimTemplates:
  - metadata:
      name: www
    spec:
      accessModes: [ "ReadWriteOnce" ]
      storageClassName: "cbs"
      resources:
        requests:
          storage: 10Gi
```
- kind: This identifies the StatefulSet resource type.
- metadata: Basic information such as StatefulSet name and Label.
- metadata.annotations: An additional description of the StatefulSet. You can set additional enhancements to TKE through this parameter.
- spec.template: Detailed template configuration of the Pod managed by the StatefulSet.
- spec.volumeClaimTemplates: Provide a templates for creating PVCs and PVs.

For more details about the parameters, see [Kubernetes' official document about StatefulSet](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/).

### Creating a StatefulSet

1. See the [YAML sample](#YAMLSample) to prepare the StatefulSet YAML file.
2. Install kubectl and connect to a cluster. For detailed operations, see [Connecting a Cluster via kubectl](https://cloud.tencent.com/document/product/457/8438).
3. Run the following command to create the StatefulSet YAML file.
```shell
kubectl create -f StatefulSet YAML filename
```
For example, to create a StatefulSet YAML file named web.yaml, run the following command:
```shell
kubectl create -f web.yaml
```
4. Run the following command to verify whether the creation is successful.
```shell
kubectl get StatefulSet
```
If a message similar to the one below is returned, the creation is successful.
```
NAME      DESIRED   CURRENT   AGE
test      1         1         10s
```

### Updating a StatefulSet

Run the following command to view the update policy type of the StatefulSet.
```
kubectl get ds/<daemonset-name> -o go-template='{{.spec.updateStrategy.type}}{{"\n"}}'
```
StatefulSet has the following two update policy types:
- OnDelete: This is the default update policy. With this policy, after the StatefulSet is updated, you have to manually delete the old StatefulSet Pod to create a new one.
- RollingUpdate: This update policy is supported in Kubernetes v1.7 or higher. With this policy, after the StatefulSet template is updated, the old StatefulSet Pod will be terminated, and a new StatefulSet Pod will be created in a rolling update manner (only for Kubernetes v1.7 or higher).

#### Method 1

Run the following command to update a StatefulSet.
```
kubectl edit StatefulSet/[name]
```
This method is suitable for simple debugging and verification, which is not recommended for direct use in a production environment. You can update any StatefulSet parameters in this way.

#### Method 2

Run the following command to update the image of the specified container.
```
kubectl patch statefulset <NAME> --type='json' -p='[{"op": "replace", "path": "/spec/template/spec/containers/0/image", "value":"<newImage>"}]'
```
It is recommended to keep other StatefulSet parameters unchanged and only update the container image when the business is updated.

If the StatefulSet is roll updated, you can view the update status by running the following command:
```
kubectl rollout status sts/<StatefulSet-name>
```

### Deleting a StatefulSet

Run the following command to delete a StatefulSet.
```
kubectl delete  StatefulSet [NAME] --cascade=false
```
The --cascade=false parameter indicates that Kubernetes only deletes the StatefulSet but not the Pods. To delete a Pod, run the following command:
```
kubectl delete  StatefulSet [NAME]
```
For more information about StatefulSet operations, see [Kubernetes' official guide](https://kubernetes.io/docs/tutorials/stateful-application/basic-stateful-set/#scaling-a-statefulset).

