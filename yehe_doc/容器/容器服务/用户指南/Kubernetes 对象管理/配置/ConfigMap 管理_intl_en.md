## Introduction

ConfigMap allows you to decouple configuration artifacts from images to ensure that the application is more portable. ConfigMap is a key-value pair. You can log in to the console to create ConfigMap objects or use kubectl. ConfigMap is useful when mounting data volumes, environment variables, or running container commands.

## Using ConfigMap via the Console

### Creating a ConfigMap
1. Log in to the [TKE Console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the ID of the cluster where ConfigMap needs to be created to go to the cluster management page.
4. Select **Configuration Management** > **ConfigMap** to go to the ConfigMap information page, as shown in the following figure:
![ConfigMap](https://main.qcloudimg.com/raw/96edefc7b8ddc416b9148eb914855954.png)
5. Click **Create** to go to the "Create a ConfigMap" page, as shown in the following figure:
![Create ConfigMap](https://main.qcloudimg.com/raw/9e3a84ee38b4d3bff209d139ba47e1c7.png)
6. Set the ConfigMap parameters.
 - Name: name of the ConfigMap.
 - Namespace: select the namespace type and set the variable name and value.
7. Click **Create ConfigMap** to finish the process.

### Using a ConfigMap

#### Using the ConfigMap for a data volume
1. Log in to the [TKE Console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the ID of the cluster where workload needs to be deployed to enter the cluster management page.
4. Under “Workload”, select any workload type to go to the page for the relevant information. For example, select **Workload** > **DaemonSet**, to go to the page for the relevant information.
5. Click **Create** to go to the "Create a workload" page.
6. Set the workload name, namespace and other information as instructed. For **Volume**, click **Add Volume** .
7. Select "Use a ConfigMap", enter the name, and click **Select a ConfigMap**, as shown below:
![](https://main.qcloudimg.com/raw/2549f59b529775a2b7453ebef596fd90.png)
8. In the “Set ConfigMap” window that pops up, configure the mounting point (refer to the following information), and click **Submit**, as shown in the following figure.
 - **Use ConfigMap**: Select a ConfigMap as needed.
 - **Options**: select **All** or **Specific keys**.
 - **Items**: if you select **Specific keys**, you can mount a specific path by adding an item. For example, if the mounting point is `/data/config`, and the path is `dev`, it is saved under `/data/config/dev`.
9. Click **Create a workload**. Now you have successfully created a workload.

#### Using ConfigMap with an environmental variable

1. Log in to the [TKE Console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the ID of the cluster where the workload needs to be deployed to enter the cluster management page.
4. Select a type for the **Workload** to go to the relevant information page. For example, select **Workload** > **DaemonSet** to go to the DaemonSet information page, as shown below:
![](https://main.qcloudimg.com/raw/76a0a6c8e0f8f52a390893946671d066.png)
5. Click **Create** to go to the "Create a workload" page.
6. Set the workload name, namespace and other information as instructed. In **Environment Variable** under **Containers in the pod**, click **Reference ConfigMap/Secret** .
7. Select **ConfigMap** for the environment variable and select the resource.
![](https://main.qcloudimg.com/raw/2549f59b529775a2b7453ebef596fd90.png)
8. Click **Create a workload** to finish the process.

### Updating a ConfigMap

1. Log in to the [TKE Console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the cluster ID for which you want to update the YAML to go to the cluster management page.
4. Select **Configuration Management** > **ConfigMap** to go to the ConfigMap information page.
![ConfigMap](https://main.qcloudimg.com/raw/76a0a6c8e0f8f52a390893946671d066.png)
5. In the row of the ConfigMap to update the YAML, click **Edit YAML** to go to the ConfigMap updating page.
6. On the **Update a ConfigMap** page, edit the YAML and click **Finish** to update the YAML.
 > To modify key-values, edit the parameter values of data in YAML and click **Finish** to complete the update.

## Using ConfigMaps with kubectl

### Sample YAML

```Yaml
apiVersion: v1
data:
  key1: value1
  key2: value2
  key3: value3
kind: ConfigMap
metadata:
  name: test-config
  namespace: default
```
- data: ConfigMap data in the form of key-value pairs.
- kind: ConfigMap resource type.
- metadata: information such as ConfigMap name and Label.
- metadata.annotations: an additional description of the ConfigMap. You can set additional enhancements to TKE through this parameter.

### Creating a ConfigMap

#### Using a YAML file

1. Use the [Sample YAML](#YAMLSample) to prepare the ConfigMap YAML file.
2. Install kubectl and connect to a cluster. For detailed operations, refer to [Connecting to Clusters](https://intl.cloud.tencent.com/document/product/457/30639).
3. Run the following command to create the ConfigMap YAML file.
```shell
kubectl create -f ConfigMap YAML filename
```
For example, to create a ConfigMap YAML file named web.yaml, run the following command:
```shell
kubectl create -f web.yaml
```
4. Run the following command to check if the file was successfully created:
```shell
kubectl get configmap
```
A message similar to the one below indicates that the YAML file has successfully been created.
```
NAME          DATA      AGE
test          2         39d
test-config   3         18d
```

#### Using a command

Run the following command to create a ConfigMap.
```
kubectl create configmap <map-name> <data-source>
```
- &lt;map-name&gt;: name of the ConfigMap.
- &lt;data-source&gt;: the directory, file, or literal value to draw the data from.

For more details about the parameters, refer to [Kubernetes official documentation](https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/#create-a-configmap).

### Using a ConfigMap

#### Using the ConfigMap with a data volume

The following is a sample YAML file:
```Yaml
apiVersion: v1
 kind: Pod
 metadata:
   name: nginx
 spec:
   containers:
     - name: nginx
       image: nginx:latest
       volumeMounts:
        name: config-volume
        mountPath: /etc/config
   volumes:
        name: config-volume
        configMap:
          name: test-config ## ConfigMap data source
          ## items: ## Set the key mounting of the specified ConfigMap
          ## key: key1 ## Select specific keys
          ## path: keys ## Mount to the specified path
   restartPolicy: Never
```

#### Using the ConfigMap with an environment variable

The following is a sample YAML file:
```Yaml
apiVersion: v1
 kind: Pod
 metadata:
   name: nginx
 spec:
   containers:
     - name: nginx
       image: nginx:latest
       env:
         - name: key1
           valueFrom:
             configMapKeyRef:
               name: test-config ## file name of the source ConfigMap
               key: test-config.key1 ## source of value of the environment variable
   restartPolicy: Never
```
