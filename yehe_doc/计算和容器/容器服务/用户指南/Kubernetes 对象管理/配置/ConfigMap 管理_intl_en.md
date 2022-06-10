## Overview 

ConfigMap allows you to decouple configurations from images to make the application more portable. ConfigMap is a key-value pair. You can create a ConfigMap object by using kubectl in the console, and use a ConfigMap by mounting a volume, through environment variables, or by running commands in the container.


## Operation Guide for ConfigMap in Console

### Creating ConfigMap
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. On the left sidebar, click **Cluster** to enter the cluster list page.
3. Click the ID of the cluster where you want to create a ConfigMap to enter the cluster management page.
4. Select **Configuration Management** > **ConfigMap** to enter the ConfigMap information page.
5. Click **Create** to enter the **Create ConfigMap** page.
6. Set the ConfigMap parameters as needed. Key parameters are as follows:
 - Name: Customize a name.
 - Namespace: Select the namespace type and set the variable name and value as needed.
7. Click **Create ConfigMap**.

### Using ConfigMap

#### Method 1. Use the ConfigMap type for a volume
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. On the left sidebar, click **Cluster** to enter the cluster list page.
3. Click the ID of the cluster where you want to deploy a workload to enter the cluster management page.
4. Select any workload type under **Workload** to enter the information page. For example, select **Workload** > **DaemonSet** to enter the DaemonSet information page as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/c001d6fd4cdefaeed125b341099bd465.png)
5. Click **Create** to enter the **Create Workload** page.
6. Set the workload name, namespace, and other information as instructed. In **Volume**, click **Add Volume** as shown below:
![Add Volume](https://qcloudimg.tencent-cloud.cn/raw/7309f6d8d47fc4a772aa644fb24db713.png)
7. Select **Use ConfigMap**, enter the name, and click **Select ConfigMap** as shown below:
![](https://main.qcloudimg.com/raw/2549f59b529775a2b7453ebef596fd90.png)
8. In the **Set ConfigMap** pop-up window, configure the mount point according to the following information and click **OK** as shown below:
 - **Select ConfigMap**: Select a ConfigMap as needed.
 - **Options**: **All** and **Specific keys** are available.
 - **Items**: If you select **Specific keys**, you can mount to a specific path by adding an item. For example, if the mount point is `/data/config` and the filename is `filename`, the value of the key-value pair will be stored under `/data/config/filename`.
![](https://qcloudimg.tencent-cloud.cn/raw/9cec4dc509b673e988c021a9e968f20d.png)
9. Click **Create Workload**.

#### Method 2. Use the ConfigMap type for an environment variable

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. On the left sidebar, click **Cluster** to enter the cluster list page.
3. Click the ID of the cluster where you want to deploy a workload to enter the cluster management page.
4. Select any workload type under **Workload** to enter the information page. For example, select **Workload** > **DaemonSet** to enter the DaemonSet information page as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/769018132b755cb219a17cccbfabb230.png)
5. Click **Create** to enter the **Create Workload** page.
6. Set the workload name, namespace, and other information as instructed. In **Environment Variable** under **Containers in the Pod**, click **Add Variable** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/a57b0d0f387482ca924f448885ffefb6.png)
7. Select **ConfigMap** for the environment variable and select the resources as needed.
9. Click **Create Workload**.

### Updating ConfigMap

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. On the left sidebar, click **Cluster** to enter the cluster list page.
3. Click the ID of the cluster where you want to update the ConfigMap to enter the cluster management page.
4. Select **Configuration Management** > **ConfigMap** to enter the ConfigMap information page.
5. Click **Update Configuration** on the right of the target ConfigMap to enter the **Update Configuration** page.
![](https://qcloudimg.tencent-cloud.cn/raw/5f98fe781372b6324b302f57fe96f981.png)
7. On the **Update Configuration** page, edit the key-value pair of the key-value type and click **Done**.
![](https://qcloudimg.tencent-cloud.cn/raw/481f4d9b57d33cf40d64faf62786a8d3.png)





## Using kubectl to Manipulate ConfigMap

### YAML sample
<dx-codeblock>
::: Yaml
apiVersion: v1
data:
  key1: value1
  key2: value2
  key3: value3
kind: ConfigMap
metadata:
  name: test-config
  namespace: default
:::
</dx-codeblock>

- **data**: The data of ConfigMap presented as key-value.
- **kind**: This identifies the ConfigMap resource type.
- **metadata**: Basic information such as ConfigMap name and label.
- **metadata.annotations**: An additional description of the ConfigMap. You can set additional enhancements to TKE through this parameter.

### Creating ConfigMap

#### Method 1. Create through the sample YAML file

1. See the [YAML sample](#YAMLSample) to prepare the ConfigMap YAML file.
2. Install kubectl and connect to a cluster. For detailed operations, see [Connecting to a Cluster](https://intl.cloud.tencent.com/document/product/457/30639).
3. Run the following command to create the ConfigMap YAML file.
```shell
kubectl create -f <ConfigMap YAML filename>
```
 For example, to create a ConfigMap YAML file named `web.yaml`, run the following command:
```shell
kubectl create -f web.yaml
```
4. Run the following command to check whether it is successfully created.
```shell
kubectl get configmap
```
 If a message similar to the following is returned, the creation is successful.
```
NAME          DATA      AGE
test          2         39d
test-config   3         18d
```


#### Method 2. Create by running the command

Run the following command to create the ConfigMap in the directory.
```
kubectl create configmap <map-name> <data-source>
```
- &lt;map-name&gt;: Name of the ConfigMap.
- &lt;data-source&gt;: Directory, file, or literal.

For more information about the parameters, see [Kubernetes' official document about ConfigMap](https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/#create-a-configmap).

### Using ConfigMap

#### Method 1. Use the ConfigMap type for a volume

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
          ## items: ## Set the key mounting of the specified ConfigMap
          ##   key: key1  ## Select the specified key
          ##   path: keys ## Mount to the specified subpath
   restartPolicy: Never
```

#### Method 2. Use the ConfigMap type for an environmental variable

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
