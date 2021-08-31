## Product Introduction
A secret is a key-value pair that can store sensitive information such as passwords, tokens, and keys to help you lower the risk of information disclosure. You can create a secret object using kubectl in the console, and use a secret by mounting a volume, through environment variables, or in a container's run command.

## Console Directions

### Creating a secret
1. Log in to the TKE console and select **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Select the ID of the cluster where you want to create a secret to enter the cluster management page.
3. Select **Configuration Management** -> **Secret** in the left sidebar to go to the Secret page, as shown below:
![](https://main.qcloudimg.com/raw/e48919ef47fdc60fa4fd39198f66f4fe.png)
4. Click **Create** to go to the **Create Secret** page.
5. On the "Create Secret" page, set the following configurations based on your needs.
![](https://main.qcloudimg.com/raw/9a9babcb79782ad55d8c19d325139b04.png)
 - **Name**: enter a name.
 - **Secret Type**: select **Opaque** or **Dockercfg** based on your needs.
        - **Opaque**: suitable for storing key certificates and configuration files. The value will be base64-encoded.
        - **Dockercfg**: suitable for storing the authentication information of a private Docker Registry.
 - **Effective Scope**: select one from the following two options based on your needs.
        - **All existing namespaces**: exclude kube-system, kube-public, and new namespaces added hereafter.
        - **Specific namespaces**: you can specify one or more available namespaces in the current cluster. 
 - **Content**: make configuration based on your secret type.
    - If the secret type is **Opaque**, set the variable name and value based on your needs.
    - If the secret type is **Dockercfg**:
		 		 - Repository domain name: enter the domain name or IP as applicable.
			 		 - Username: enter the username for the third-party repository based on your needs.
				 		 - Password: enter the login password for the third-party repository based on your needs.
> If this is the first time that you log in to the system, an account will be created and related information will be written to the `~/.dockercrg` file.
6. Click **Create Secret** to complete the creation.

### Using a secret

<span id="Volume"></span>

#### Method 1: using a secret as a volume
1. Log in to the TKE console and select **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Click the ID of the cluster where you want to deploy the workload to enter the cluster management page.
3. Under **Workload**, select a workload type to go to the corresponding information page.
For example, select **Workload** -> **DaemonSet** to go to the DaemonSet page, as shown below:
![](https://main.qcloudimg.com/raw/ec181a50743703e95ddba570f24d6734.png)
4. Click **Create** to go to the **Create Workload** page.
5. Set the workload name, namespace, and other information as instructed. In "Volume", click **Add Volume**, as shown below:
![](https://main.qcloudimg.com/raw/95d912af0af1ffeec2060f45d2108373.png)
6. Select **Use Secret** from the drop-down list, enter a name, and click **Select Secret**, as shown below:
![](https://main.qcloudimg.com/raw/20ac28f182c201dd0df88b492ec6493c.png)
7. In the pop-up **Configure Secret** window, configure the mounting point and click **OK**, as shown below:
![](https://main.qcloudimg.com/raw/760367ca00db0be33fc30d10d406829f.png)
 - **Select a secret**: select a secret based on your needs.
 - **Options**: select **All** or **Specific keys**.
 - **Items**: if you select **Specific keys**, you can mount the secret to a specific path by adding an item. For example, if the mounting point is `/data/config` and the sub-path is `dev`, it will finally be saved under `/data/config/dev`.
8. Click **Create Workload** to complete the creation.

   <span id="Environment"></span>

#### Method 2: using a secret as an environmental variable
1. Log in to the TKE console and select **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.

2. Click the ID of the cluster where you want to deploy a workload to enter the cluster management page.

3. Under **Workload**, select a workload type to go to the corresponding information page.
  For example, select **Workload** -> **DaemonSet** to go to the DaemonSet page, as shown below:
  ![](https://main.qcloudimg.com/raw/d283d7fc289e34ebf8293a95d2c2c8de.png)

4. Click **Create** to go to the **Create Workload** page.

5. Set the workload name, namespace, and other information as instructed. In "Environment Variable" under "Containers in the pod", click **Reference ConfigMap/Secret**, as shown below:
  ![](https://main.qcloudimg.com/raw/1703850463b0bf78406cc421f52a4d4c.png)

6. Select **Secret** for the environment variable and select resources based on your needs, as shown below:
  ![](https://main.qcloudimg.com/raw/5d145c2eb694af38f3e3a6f73d74bc13.png)

7. Click **Create Workload** to complete the creation.

   <span id="ThirdRepository"></span>

#### Method 3: referencing a secret when using third-party image repositories
1. Log in to the TKE console and select **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Click the ID of the cluster where you want to deploy the workload to enter the cluster management page.
3. Under **Workload**, select a workload type to go to the corresponding information page.
For example, select **Workload** -> **DaemonSet** to go to the DaemonSet page, as shown below:
![](https://main.qcloudimg.com/raw/c02d49524d5c797f9cd3dab03ecca1fa.png)
4. Click **Create** to go to the **Create Workload** page.
5. Set the workload name, namespace, and other information as instructed. Click **Advanced Settings** in the lower-left corner of the page.
6. Click **Add** under **imagePullSecrets** and select a dockercfg-type secret based on your needs, as shown below:
![](https://main.qcloudimg.com/raw/2bab4fa82d83dba3c4a4a9651de20f68.png)
7. Click **Create Workload** to complete the creation.

### Updating a secret
1. Log in to the TKE console and select **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Select the ID of the cluster for which you want to update the YAML file to go to the cluster management page.
3. Select **Configuration Management** -> **Secret** to go to the Secret page, as shown below:
![Secret](https://main.qcloudimg.com/raw/8f92bfd6dc32a125409a57f623bd0a2f.png)
4. In the row of the secret for which you want to update the YAML file, click **Edit YAML** to go to the secret updating page.
5. On the "Update Secret" page, edit the YAML file and click **Complete**.
> To modify key-values, edit the parameter values of data in the YAML file and click **Finish** to complete the update.

## kubectl Instructions

### Creating a secret

<span id="SpecifyFile"></span>

#### Method 1: creating a secret with a specified file
1. Run the following commands to obtain the username and password of the pod:
```shell
$ echo -n 'username' > ./username.txt
$ echo -n 'password' > ./password.txt
```
2. Run the following kubectl command to create a secret.
```shell
$ kubectl create secret generic test-secret --from-file=./username.txt --from-file=./password.txt
secret "testSecret" created
```
3. Run the following command to view details about the secret:
```
kubectl describe secrets/ test-secret
```

<span id="YamlManual"></span>

#### Method 2: manually creating a secret with a YAML file

> To manually create a secret using a YAML file, you need to Base64-encode the data of the secret in advance.

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

### Using a secret

<span id="KubectlVolume"></span>

#### Method 1: using a secret as a volume

The following shows a YAML sample.
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

<span id="KubectlEnvironment"></span>

#### Method 2: using a secret as an environmental variable

The following shows a YAML sample.
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

<span id="KubectlThirdRepository"></span>

#### Method 3: referencing a secret when using third-party image repositories

The following shows a YAML sample.
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
   - name: test-secret ## Set the filename of the source secret
   restartPolicy: Never
```
