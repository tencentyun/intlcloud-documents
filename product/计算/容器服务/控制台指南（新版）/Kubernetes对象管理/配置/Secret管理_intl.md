## Overview
A Secret can be used to store sensitive information such as passwords, tokens, and keys to reduce the risk of direct exposure. Secret is a key-value pair. You can create a corresponding Secret object using kubectl in the console, and use a Secret by mounting a volume, through environment variables, or in the container's run command.

## Operation Guide for Secrets in the Console

### Creating a Secret

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the ID of the cluster where Secret needs to be created to enter the cluster management page.
4. Select "Configuration Management" > "Secret" to go to the Secret information page. See the figure below:
![Secret](https://main.qcloudimg.com/raw/d532285897995fb337682512b875ffb9.png)
5. Click **Create** to go to the "Create a Secret" page. See the figure below:
![Create a Secret](https://main.qcloudimg.com/raw/6c416a0e29de03e7a2057eafda2ca282.png)
6. Set the Secret parameters based on actual needs. Key parameters are as follows:
 - Name: Custom.
 - Namespace: Select the namespace type based on actual needs.
 - Content: Set the variable name and variable value based on actual needs.
7. Click **Create a Secret** to complete the creation.

### Using a Secret

#### Method 1: Using the Secret Type for a Volume

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the ID of the cluster where workload needs to be deployed to enter the cluster management page.
4. Under "Workload", select a workload type to go to the corresponding information page. For example, select "Workload" > "DaemonSet" to go to the DaemonSet information page. See the figure below:
![](https://main.qcloudimg.com/raw/73b214fcb0cf26e569310894dd44c512.png)
5. Click **Create** to go to the "Create a workload" page.
6. Set the workload name, namespace and other information as instructed. In "Volume", click **Add a volume** to add a volume. See the figure below:
![Add a volume](https://main.qcloudimg.com/raw/2e036dc898bd3fecfc59edd8742ff18a.png)
7. Select "Use a Secret", enter the name, and click **Select a Secret**. See the figure below:
![Use a Secret](https://main.qcloudimg.com/raw/f4274791b9d489b1543935ef7cc01985.png)
8. In the "Set a Secret" window that pops up, configure the mount point and click **OK**.
9. Click **Create a workload** to complete the creation.

#### Method 2: Using the Secret Type for an Environmental Variable

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the ID of the cluster where workload needs to be deployed to enter the cluster management page.
4. Under "Workload", select a workload type to go to the corresponding information page. For example, select "Workload" > "DaemonSet" to go to the DaemonSet information page. See the figure below:
![](https://main.qcloudimg.com/raw/73b214fcb0cf26e569310894dd44c512.png)
5. Click **Create** to go to the "Create a workload" page.
6. Set the workload name, namespace and other information as instructed. In "Environment variables" of "In-Pod containers", click **Reference a ConfigMap/Secret**. See the figure below:
![Reference a ConfigMap/Secret](https://main.qcloudimg.com/raw/0422b13b4b4d547799d643a34f466340.png)
7. Select "Secret" for the environment variable and select the resource based on actual needs. See the figure below:
![](https://main.qcloudimg.com/raw/e9df219376365ad32a78bff58b82cf8f.png)
9. Click **Create a workload** to complete the creation.

### Updating a Secret

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the ID of the cluster where YAML needs to be updated to enter the cluster management page.
4. Select "Configuration Management" > "Secret" to go to the Secret information page. See the figure below:
![Secret](https://main.qcloudimg.com/raw/d532285897995fb337682512b875ffb9.png)
5. In the row of the Secret for which to update the YAML, click **Edit YAML** to go to the Secret updating page.
6. On the "Update a Secret" page, edit the YAML and click **Finish** to update the YAML.
 >? To modify key-values, edit the parameter values of data in YAML and click **Finish** to complete the update.

## Using kubectl to Manipulate Secrets

### Creating a Secret

#### Method 1: Creating a Secret Using the Specified File

1. Run the following command to obtain the username and password of the Pod.
```shell
$ echo -n 'username' > ./username.txt
$ echo -n 'password' > ./password.txt
```
2. Run the following kubectl command to create a Secret.
```shell
$ kubectl create secret generic test-secret --from-file=./username.txt --from-file=./password.txt
secret "testSecret" created
```
3. Run the following command to view the details of the Secret.
```
kubectl describe secrets/ test-secret
```

#### Method 2: Manually Creating Using a YAML File

>? To manually create a Secret using YAML, you need to Base64-encode the data of the Secret in advance.

```Yaml
apiVersion: v1
kind: Secret
metadata:
  name: test-secret
type: Opaque
data:
  username: dXNlcm5hbWU=  ## Generated by echo -n 'username' | base64
  password: cGFzc3dvcmQ=  ## Generated by echo -n 'password' | base64
```

### Using a Secret

#### Method 1: Using the Secret Type for a Volume

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
          name:  test-secret ## Set the Secret source
          ## items:  ## Set the key mounting of the specified Secret
          Select the specified key
          ##   path: group/user ## Mount to the specified subpath
          ##   mode: 256  ## Set file permission
   restartPolicy: Never
```

#### Method 2: Using the Secret Type for an Environmental Variable

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
               name: test-secret ## Set the filename of the source Secret
               key: username  ## Set the value source of the environment variable
   restartPolicy: Never
```
