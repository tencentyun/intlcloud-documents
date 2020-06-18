## Introduction

StatefulSets are used to manage stateful applications. It creates a standard persistent identifier for each Pod. The identifier is retained after the Pod is migrated, terminated, or restarted. When using persistent storage, you can map storage volumes to identifiers. If your application does not require any persistent identifier, we recommend that you use a Deployment to deploy the application.

## Using StatefulSets via the Console

<span id="createStatefulSet"></span>

### Creating a StatefulSet 

1. Log in to the TKE console and select **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Click the ID of the cluster where StatefulSet needs to be created to enter the cluster management page.
3. Choose **Workload** > **StatefulSet** to go to the management page of **StatefulSet**, as shown below:
![](https://main.qcloudimg.com/raw/88ece12d8464711824eadfb35db0c050.png)
4. Click **Create** to go to **Create Workload** page.
Set the StatefulSet parameters as needed. Key parameters are as follows:
 - **Workload**: name of the workload.
 - **Namespace**: select a namespace.
 - **Type**: select **StatefulSet (run the Pod in a stateful manner)**.
 - **In-Pod containers**: set one or more containers for a Pod of the StatefulSet as needed.
    - **Name**: enter a name.
    - **Image**: select an image.
    - **Image tag**: enter image tags.
    - **Image pull policy**: select one of the following:
       If you do not set any image pull policy and **Image tag** is `latest` or empty, `Always` is used. Otherwise, `IfNotPresent` is used.
        - **Always**: the image is always pulled from a remote location.
        - **IfNotPresent**: use local image by default. If the image is unavailable, the image is pulled from a remote location.
        - **Never**: use local image only. If the image is unavailable, throw an exception.
    - **CPU/memory limits**: set CPU and memory limit according to [Kubernetes resource limits](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/) to improve service robustness.
    - **Advanced settings**: parameters such as "**working directory**", "**run commands**", "**run parameters**", "**container health check**", and "**privilege level**" are found here.
 - Pod quantity: select the adjustment method and set the Pod quantity.
5. Click **Create a workload** to finish creation.

### Updating a StatefulSet

#### Updating YAML
1. Log in to the TKE console and select **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Click the cluster ID for which you want to update the YAML to go to the cluster management page.
3. Choose **Workload** > **StatefulSet** to go to the management page of **StatefulSet**.
4. In the row of the StatefulSet for which YAML should be updated, click **More** > **Edit YAML** to go to the StatefulSet updating page.
5. On the "Update StatefulSet" page, edit the YAML and click **Finish** to update the YAML.

#### Updating Pod configurations
1. On the cluster management page, click the ID of the StatefulSet cluster for which the Pod configurations need to be updated to enter the StatefulSet cluster management page.
2. In the StatefulSet row for which Pod configurations need to be updated, click **Update Pod Configurations**.
3. On the “Updating Pod Configurations” page, modify the update method and set parameters as needed.

4. Click **Finish** to update the Pod configurations.

## Using StatefulSets via kubectl

<span id="YAMLSample"></span>

### Sample YAML file 

```Yaml
apiVersion: v1
kind: Service ## Create a Headless Service to control the network domain
metadata:
  name: nginx
  namespace: default
  labels:
    app: nginx
"spec":
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
  replicas: 3 # The default is 1.
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
- **kind**: StatefulSet resource type.
- **metadata**: information such as StatefulSet name and Label.
- **metadata.annotations**: an additional description of the StatefulSet. You can set additional enhancements to TKE through this parameter.
- **spec.template**: detailed template configuration of the Pod managed by the StatefulSet.
- **spec.volumeClaimTemplates**: templates for creating PVCs and PVs.

For more details, refer to [Kubernetes official documentation](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/).

### Creating a StatefulSet

1. Use the [sample YAML file](#YAMLSample) to prepare the StatefulSet YAML file.
2. Install kubectl and connect to a cluster. For detailed operations, please see [Connecting to Clusters](https://intl.cloud.tencent.com/document/product/457/30639).
3. Run the following command to create the StatefulSet YAML file.
```shell
kubectl create -f StatefulSet YAML filename
```
For example, to create a StatefulSet YAML file named web.yaml, run the following command:
```shell
kubectl create -f web.yaml
```
4. Run the following command to check whether the file has successfully been created:
```shell
kubectl get StatefulSet
```
A message similar to the one below indicates that the file has been created:
```
NAME      DESIRED   CURRENT   AGE
test      1         1         10s
```

### Updating a StatefulSet

Run the following command to view the update policy type of the StatefulSet.
```
kubectl get ds/<daemonset-name> -o go-template='{{.spec.updateStrategy.type}}{{"\n"}}'
```
StatefulSet has the following update policy types:
– OnDelete: the default upgrade policy. You have to manually delete the old StatefulSet Pod to create a new one after the StatefulSet is updated.
- RollingUpdate: Kubernetes 1.7 or later. The old StatefulSet Pod is terminated, and a new StatefulSet Pod is created through a rolling update after the StatefulSet is updated.

#### Method 1

Run the following command to update a StatefulSet.
```
kubectl edit StatefulSet/[name]
```
Use for debugging and verification. We do not recommend using this in production environments. You can update any StatefulSet parameters this way.

#### Method 2

Run the following command to update the image of a specific container.
```
kubectl patch statefulset <NAME> --type='json' -p='[{"op": "replace", "path": "/spec/template/spec/containers/0/image", "value":"<newImage>"}]'
```
We recommend that you only update the container image and keep other parameters unchanged when the service is updated.

If the StatefulSet is updated using a rolling update, you can check the update status by running the following command:
```
kubectl rollout status sts/<StatefulSet-name>
```

### Deleting a StatefulSet

Run the following command to delete a StatefulSet.
```
kubectl delete  StatefulSet [NAME] --cascade=false
```
--cascade=false indicates that only the StatefulSet is deleted, not the Pods. Run the following command if you need to delete the Pods as well.
```
kubectl delete StatefulSet [NAME]
```
For more information about StatefulSet, refer to [Kubernetes official documentation](https://kubernetes.io/docs/tutorials/stateful-application/basic-stateful-set/#scaling-a-statefulset).

