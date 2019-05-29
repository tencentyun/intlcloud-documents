## Overview

With a ConfigMap, you can decouple the configuration from the running image to make the application more portable. ConfigMap is a key-value pair. You can create a corresponding ConfigMap object using kubectl in the console, and use a ConfigMap by mounting a volume, through environment variables, or in the container's run command.

## Operation Guide for ConfigMaps in the Console

### Creating a ConfigMap

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the ID of the cluster where ConfigMap needs to be created to enter the cluster management page.
4. Select "Configuration Management" > "ConfigMap" to go to the ConfigMap information page. See the figure below:
![ConfigMap](https://main.qcloudimg.com/raw/598a4226024bb347995ffbef370dc329.png)
5. Click **Create** to go to the "Create a ConfigMap" page. See the figure below:
![Create a ConfigMap](https://main.qcloudimg.com/raw/9a1f6cba071c092ad06464538f7d1f99.png)
6. Set the ConfigMap parameters based on actual needs. Key parameters are as follows:
 - Name: Custom.
 - Namespace: Select the namespace type and set the variable name and value based on actual needs.
7. Click **Create a ConfigMap** to complete the creation.

### Using a ConfigMap

#### Method 1: Using the ConfigMap Type for a Volume

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the ID of the cluster where to deploy the workload to go to the management page of the cluster.
4. Under "Workload", select a workload type to go to the corresponding information page. For example, select "Workload" > "DaemonSet" to go to the DaemonSet information page. See the figure below:
![](https://main.qcloudimg.com/raw/73b214fcb0cf26e569310894dd44c512.png)
5. Click **Create** to go to the "Create a workload" page.
6. Set the workload name, namespace and other information as instructed. In "Volume", click **Add a volume** to add a volume. See the figure below:
![Add a volume](https://main.qcloudimg.com/raw/2e036dc898bd3fecfc59edd8742ff18a.png)
7. Select "Use a ConfigMap", enter the name, and click **Select a ConfigMap**. See the figure below:
![](https://main.qcloudimg.com/raw/2647c950bda4780a0e254acc9fe10f94.png)
8. In the "Set a ConfigMap" window that pops up, configure the mount point and click **OK**.
9. Click **Create a workload** to complete the creation.

#### Method 2: Using the ConfigMap Type for an Environmental Variable

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the ID of the cluster where to deploy the workload to go to the management page of the cluster.
4. Under "Workload", select a workload type to go to the corresponding information page. For example, select "Workload" > "DaemonSet" to go to the DaemonSet information page. See the figure below:
![](https://main.qcloudimg.com/raw/73b214fcb0cf26e569310894dd44c512.png)
5. Click **Create** to go to the "Create a workload" page.
6. Set the workload name, namespace and other information as instructed. In "Environment variables" of "In-Pod containers", click **Reference a ConfigMap/Secret**. See the figure below:
![Reference a ConfigMap/Secret](https://main.qcloudimg.com/raw/379d16ccf3ecc3a8c9ab90664b74168b.png)
7. Select "ConfigMap" for the environment variable and select the resource based on actual needs. See the figure below:
![](https://main.qcloudimg.com/raw/5fb899969c95a4e157c9f2d9bc69a944.png)
9. Click **Create a workload** to complete the creation.

### Updating a ConfigMap

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the ID of the cluster where YAML needs to be updated to enter the cluster management page.
4. Select "Configuration Management" > "ConfigMap" to go to the ConfigMap information page. See the figure below:
![ConfigMap](https://main.qcloudimg.com/raw/598a4226024bb347995ffbef370dc329.png)
5. In the row of the ConfigMap for which to update the YAML, click **Edit YAML** to go to the ConfigMap updating page.
6. On the "Update a ConfigMap" page, edit the YAML and click **Finish** to update the YAML.
 >? To modify key-values, edit the parameter values of data in YAML and click **Finish** to complete the update.

## Using kubectl to Manipulate ConfigMaps

### YAML Sample

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
- data: The data of ConfigMap presented as key-value.
- kind: This identifies the ConfigMap resource type.
- metadata: Basic information such as ConfigMap name and Label.
- metadata.annotations: An additional description of the ConfigMap. You can set additional enhancements to TKE through this parameter.

### Creating a ConfigMap

#### Method 1: Creating Using the YAML Sample File

1. See the [YAML sample](#YAMLSample) to prepare the ConfigMap YAML file.
2. Install kubectl and connect to a cluster. For detailed operations, see [Connecting a Cluster via kubectl](https://cloud.tencent.com/document/product/457/8438).
3. Run the following command to create the ConfigMap YAML file.
```shell
kubectl create -f ConfigMap YAML filename
```
For example, to create a ConfigMap YAML file named web.yaml, run the following command:
```shell
kubectl create -f web.yaml
```
4. Run the following command to verify whether the creation is successful.
```shell
kubectl get configmap
```
If a message similar to the one below is returned, the creation is successful.
```
NAME          DATA      AGE
test          2         39d
test-config   3         18d
```

#### Method 2: Creating by Running a Command

Run the following command to create the ConfigMap in the directory.
```
kubectl create configmap <map-name> <data-source>
```
- &lt;map-name&gt;: Name of the ConfigMap.
- &lt;data-source&gt;: Directory, file, or literal.

For more details about the parameters, see [Kubernetes' official document about ConfigMap](https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/#create-a-configmap).

### Using a ConfigMap

#### Method 1: Using the ConfigMap Type for a Volume

Below is a YAML sample:
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
          name: test-config ## Set the ConfigMap source
          ## items:  ## Set the key mounting of the specified ConfigMap
          ##   key: key1  ## Select the specified key
          ##   path: keys ## Mount to the specified subpath
   restartPolicy: Never
```

#### Method 2: Using the ConfigMap Type for an Environmental Variable

Below is a YAML sample:
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
               name: test-config ## Set the filename of the source ConfigMap
               key: test-config.key1  ## Set the value source of the environment variable
   restartPolicy: Never
```
