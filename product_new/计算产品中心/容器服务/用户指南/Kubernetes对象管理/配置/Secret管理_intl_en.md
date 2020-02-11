## Introduction
A secret is a key-value pair that can store sensitive information such as passwords, tokens, and keys to help you lower the risk of information exposure. You can create a secret object using kubectl in the console, and use a secret by mounting a volume, through environment variables, or in the container's run command.

## Console Directions

### Creating a Secret
1. Log in to the TKE console and select **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Select the ID of the cluster where you want to create a secret to enter the cluster management page.
3. Select **Configuration Management** > **Secret** on the left sidebar to go to the Secret page as shown below:
![](https://main.qcloudimg.com/raw/de4fcb50d53db97af9f1d6ede08be1e1.png)
4. Click **Create** to go to the **Create Secret** page.
5. In the “Create Secret” page, make the following configurations according to your needs .
![](https://main.qcloudimg.com/raw/a0c5ec51165aa0cfff4bfbfc303246b7.png)
 - **Name**: enter a name.
 - **Secret Type**: please select one from **Opaque** and **Dockercfg** according to your needs.
        - **Opaque**: suitable for storing key certificates and configuration files. The value will be base64-encoded.
        - **Dockercfg**: suitable for storing the verification information of private Docker Registry.
 - **Effective Scope**: please select one from the following two options based on your needs.
        - **All existing namespaces**: excluding kube-system, kube-public, and new namespaces added hereafter.
        - **Specific namespaces**: you can specify one or more available namespaces in the current cluster. 
 - **Content**: make configuration according to your secret type.
    - If the secret type is **Opaque**: set the variable name and value as needed.
    - If the secret type is **Dockercfg**:
 		 - Repository domain name: enter the domain name or IP as applicable.
 		 - Username: enter the username for the third-party repository according to your needs.
 		 - Password: enter the login password for the third-party repository according to your needs.
> If this is the first time you log in to the system, an account will be created and the related information will be written to the `~/.dockercrg` file.
6. Click **Create Secret** to complete the creation.

### Using a Secret
#### Method 1: Using secret as a volume
1. Log in to the TKE console and select **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Click the ID of the cluster where you want to deploy a workload to enter the cluster management page.
3. Under **Workload**, select a workload type to go to the corresponding information page.
For example, select **Workload** > **DaemonSet** to go to the DaemonSet page as shown below:
![](https://main.qcloudimg.com/raw/743aa4292e75f58e92033ee829d44cbb.png)
4. Click **Create** to go to **Create Workload** page.
5. Set the workload name, namespace and other information as instructed. In **Volume**, click **Add Volume** as shown below: 
![](https://main.qcloudimg.com/raw/15e95703427ae44a8bae6b608ee34101.png)
6. Select **Use Secret** in the drop-down menu, enter a name, and click **Select Secret** as shown below:
![](https://main.qcloudimg.com/raw/9b560e9458c2253ad422a163d59e8532.png)
7. In the **Configure Secret** pop-up window, configure the mounting point and click **OK** as shown below:
![](https://main.qcloudimg.com/raw/ec9c1f5055eb5ed8779777efe4ce6f03.png)
 - **Select a secret**: select a secret as needed.
 - **Options**: you can select from **All** or **Specific keys**.
 - **Items**: if you select the **Specific keys** option, you can mount the secret to a specific path by adding an item. For example, if the mounting point is `/data/config`, the sub-path is `dev`, it will finally be saved under `/data/config/dev`.
8. Click **Create Workload** to complete the creation.

#### Method 2: Using secret as an environmental variable
1. Log in to the TKE console and select **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Click the ID of the cluster where you want to deploy a workload to enter the cluster management page.
3. Under **Workload**, select a workload type to go to the corresponding information page.
For example, select **Workload** > **DaemonSet** to go to the DaemonSet page as shown below:
![](https://main.qcloudimg.com/raw/743aa4292e75f58e92033ee829d44cbb.png)
4. Click **Create** to go to **Create Workload** page.
5. Set the workload name, namespace and other information as instructed. In **Environment Variable** under **Containers in the pod**, click **Reference ConfigMap/Secret** as shown below:
![](https://main.qcloudimg.com/raw/f9ca9039ce314fe65a302963c2ddf254.png)
6. Select **Secret** for the environment variable and select resources based on your needs as shown below:
![](https://main.qcloudimg.com/raw/5ae67cf051ed20a4c1e509c3f7ac6fb9.png)
7. Click **Create Workload** to complete the creation.

#### Method 3: Referencing secret when using third-party image repositories
1. Log in to the TKE console and select **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Click the ID of the cluster where you want to deploy the workload to enter the cluster management page.
3. Under **Workload**, select a workload type to go to the corresponding information page.
For example, select **Workload** > **DaemonSet** to go to the DaemonSet page as shown below:
![](https://main.qcloudimg.com/raw/743aa4292e75f58e92033ee829d44cbb.png)
4. Click **Create** to go to **Create Workload** page.
5. Set the workload name, namespace and other information as instructed. Click **Advanced Settings** in the bottom left corner of the page.
6 Click **Add** under **imagePullSecrets** and select a dockercfg-type secret according to your needs as shown below:
![](https://main.qcloudimg.com/raw/e744a226a75914f8cccaec30da86d213.png)
7. Click **Create Workload** to complete the creation.

### Updating a Secret
1. Log in to the TKE console and select **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Select the ID of the cluster for which you want to update the YAML to go to the cluster management page.
3. Select **Configuration Management** > **Secret** to go to the Secret page as shown below:
![Secret](https://main.qcloudimg.com/raw/de4fcb50d53db97af9f1d6ede08be1e1.png)
4. In the row of the Secret for which you want to update the YAML, click **Edit YAML** to go to the secret updating page.
5. On the Update Secret page, edit the YAML and click **Complete**.
> To modify key-values, edit the parameter values of data in YAML and click **Finish** to complete the update.

## kubectl Instructions

### Creating a Secret

#### Method 1: Creating a secret with a specified file
1. Run the following commands to obtain the username and password of the Pod.
```shell
$ echo -n 'username' > ./username.txt
$ echo -n 'password' > ./password.txt
```
2. Run the following kubectl command to create a secret.
```shell
$ kubectl create secret generic test-secret --from-file=./username.txt --from-file=./password.txt
secret "testSecret" created
```
3. Run the following command to view the details about the secret.
```
kubectl describe secrets/ test-secret
```

#### Method 2: Manually creating a secret with a YAML file

> To manually create a secret using YAML, you need to Base64-encode the data of the secret in advance.

```Yaml
apiVersion: v1
kind: Secret
metadata:
  name: test-secret
type: Opaque
data:
  username: dXNlcm5hbWU=  ## Generated by echo -n 'username' | base64
  password: cGFzc3dvcmQ= ## Generated by echo -n 'password' | base64
```

### Using a Secret

#### Method 1: Using secret as a volume

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
        name: secret-volume
        mountPath: /etc/config
   volumes:
        name: secret-volume
        secret:
          name: test-secret ## Set the secret source
          ## items: ## Set the key mounting of the specified secret
          ##   key: username  ## Select the specified key
          ## path: group/user ## Mount to the specified subpath
          ## mode: 256 ## Set file permission
   restartPolicy: Never
```

#### Method 2: Using secret as an environmental variable

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
         - name: SECRET_USERNAME
           valueFrom:
             secretKeyRef:
               name: test-secret ## Set the filename of the source secret
               key: username ## Set the value source of the environment variable
   restartPolicy: Never
```

#### Method 3: Referencing secret when using third-party image repositories

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
   imagePullSecrets:
   name: test-secret ## Set the filename of the source secret
   restartPolicy: Never
```
