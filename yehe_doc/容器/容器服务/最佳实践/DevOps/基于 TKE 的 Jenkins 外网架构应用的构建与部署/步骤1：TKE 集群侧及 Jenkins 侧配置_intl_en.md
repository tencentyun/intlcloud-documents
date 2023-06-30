## TKE Cluster Configuration

This document describes how to [customize RBAC authorization ServiceAccount in TKE](https://intl.cloud.tencent.com/document/product/457/39539) and get the cluster access address, token, and cluster CA certificate information required during Jenkins configuration.

### Getting cluster credential[](id:proof)
>? You need to enable private network access in the current cluster. For more information, see [Basic Features](https://intl.cloud.tencent.com/document/product/457/36833).
>
1. Use the following Shell script to create a test namespace `ci` and a test user `jenkins` of ServiceAccount type and get the cluster access credential (token) as shown below:
```
# Create the test namespace `ci`
kubectl create namespace ci
# Create the test ServiceAccount account
kubectl create sa jenkins -n ci
# Get the secret token automatically created by the ServiceAccount account
kubectl get secret $(kubectl get sa jenkins -n ci -o jsonpath={.secrets[0].name}) -n ci -o jsonpath={.data.token} | base64 --decode
```

2. Create a Role permission object resource file `jenkins-role.yaml` in the `ci` test namespace as follows:
```
kind: Role
apiVersion: rbac.authorization.k8s.io/v1beta1
metadata:
  name: jenkins
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["create","delete","get","list","patch","update","watch"]
- apiGroups: [""]
  resources: ["pods/exec"]
  verbs: ["create","delete","get","list","patch","update","watch"]
- apiGroups: [""]
  resources: ["pods/log"]
  verbs: ["get","list","watch"]
- apiGroups: [""]
  resources: ["secrets"]
  verbs: ["get"]
```

3. Create a RoleBinding object resource file `jenkins-rolebinding.yaml`. The following permission binding indicates that the `jenkins` user of ServiceAccount type has `jenkins` (Role type) permissions in the `ci` namespace, as shown below:
```
apiVersion: rbac.authorization.k8s.io/v1beta1
kind: RoleBinding
metadata:
  name: jenkins
  namespace: ci
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: Role
  name: jenkins
subjects:
- kind: ServiceAccount
  name: jenkins
```



### Getting cluster CA certificate[](id:getCA)
1. Log in to the node of the cluster as instructed in [Logging In to Linux Instance Using Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436).
2. Run the following command to view the cluster CA certificate.
```
cat /etc/kubernetes/cluster-ca.crt
```
3. Record and save the returned certificate information, as shown in the following figure:
![](https://main.qcloudimg.com/raw/9431bdeb070e4e2e382bf6ea628b1842.png)

### Authorizing docker.sock 

Each node of the TKE cluster has a `docker.sock` file. The slave pod connects to this file when running `docker build`. Before that, you need to log in to each node and run the following commands to authorize `docker build`:
```
chmod 666 /var/run/docker.sock
```
```
ls -l /var/run/docker.sock
```


## Configuring Jenkins

### Adding a TKE private network access address

1. Log in to the Jenkins Master node as instructed in [Logging in to Linux Instance Using Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436).
2. Run the following command to configure the access domain name.
```
sudo sed -i '$a 10.x.x.x cls-ixxxelli.ccs.tencent-cloud.com' /etc/hosts
```
> ? This command can be obtained from **Cluster APIServer** on the basic information page of the cluster after private network access is enabled in the cluster. For more information, see [Getting cluster credential](#proof). 
> 
3. Run the following command to query whether the configuration is successful.
```
cat /etc/hosts
```
If the result shown in the following figure appears, the configuration was successful.
![](https://main.qcloudimg.com/raw/2e1bd6f1df51f150e9064d68f01e1754.png)
               
### Required plug-ins for Jenkins installation
1. Log in to the Jenkins backend and click **Manage Jenkins** on the left sidebar.
2. On the **Manage Jenkins** panel, click **Manage Plugins**.
3. On the **Available** tab, select **Kubernetes**, **Git Parameter**, and **Extended Choice Parameter**.
 - **Locale**：Chinese language plug-in. Installing this plug-in can make the Jenkins interface default to the Chinese version.
 - **Kubernetes**: indicates the Kubernetes plug-in.
 - **Git Parameter** and **Extended Choice Parameter**: are used to pass parameters during package building.
   Take the Kubernetes plug-in as an example, as shown in the following figure:
   ![](https://qcloudimg.tencent-cloud.cn/raw/1562c0ec0feb000751cf8762c49f9c1e.png)
4. After selecting the above plugins, click **Install without restart** and restart Jenkins.

### Enabling the jnlp port
1. Log in to the Jenkins backend and click **Manage Jenkins** on the left sidebar.
2. On the **Manage Jenkins** panel, click **Configure Global Security**.
3. In **TCP port for inbound agents**, select **Fixed** and enter **50000**.
4. Keep other configuration items as their defaults and click **Save** at the bottom of the page.

### Adding TKE cluster token[](id:addToken)
1. Log in to the Jenkins backend and click **Credentials** > **System** on the left sidebar.
2. On the **System** panel, select **Global credentials (unrestricted)**.
3. On the **Global credentials (unrestricted)** page, click **Add Credentials** on the left sidebar, and configure the basic credential information as follows:
  - **Kind**: select **Secret text**.
  - **Scope**: use the default option **Global (Jenkins, nodes, items, all child items, etc)**.
  - **Secret**: enter the **token** of ServiceAccount `jenkins` obtained in [Getting cluster credential](#proof).
  - **ID**: leave it blank as default.
  - **Description**: complete the information about the credential, which is displayed as the credential name and descriptive information. This document uses `tke-token` as an example.
3. Click **OK** to add the credential, which is displayed in the credential list after being successfully added as shown below:
!![](https://qcloudimg.tencent-cloud.cn/raw/8e6219f412471fe973e6bbd869e98fca.png)

### Adding GitLab authentication[](id:addGitlab)
1. On the **Global credentials (unrestricted)** page, click **Add Credentials** on the left sidebar, and configure the basic credential information as follows:
 - **Kind**: select **Username with password**.
 - **Scope**: use the default option **Global (Jenkins, nodes, items, all child items, etc)**.
 - **Username**: indicates the GitLab username.
 - **Password**: indicates the GitLab login password.
 - **ID**: leave it blank as default.
 - **Description**: complete the information about the credential, which is displayed as the credential name and descriptive information. This document uses `gitlab-password` as an example.
2. Click **OK**.

### Configuring slave Pod template[](id:PodTemplates)
1. Log in to the Jenkins backend and click **Manage Jenkins** on the left sidebar.
2. On the **Manage Jenkins** panel, click **Configure System**.
3. At the bottom of the **Configure System** panel, select **Add a new cloud** > **Kubernetes** in the **Cloud** section as shown below:
4. Click **Kubernetes Cloud details...** to configure the following basic information for Kubernetes:
   The following describes the main parameters. For other parameters, simply keep them as their defaults:
    - **Name**: a custom name. This document uses `kubernetes` as an example.
    - **Kubernetes URL**: the TKE cluster access address, see [Obtaining the cluster credential](#proof).
    - **Kubernetes server certificate key**: to obtain the cluster CA certificate, see [Obtaining the cluster CA certificate](#getCA).
    - **Credentials**: select the `tke-token` credential created in the [Adding TKE cluster token](#addToken) step and then click **Test Connection**. If the connection succeeds, the "Connection successful" prompt will be displayed.
    - **Jenkins URL**: enter a Jenkins private network address, such as `http://10.x.x.x:8080`.
5. Select **Pod Templates** > **Add Pod Template** > **Pod Template details...** and configure the basic information of the pod template.
The following describes the main parameters. For other parameters, simply keep them as their defaults:
 - **Name**: enter a custom name. This document uses `jnlp-agent` as an example.
 - **Labels**: define the tag name. You can select a pod for building based on the tag. This document uses `jnlp-agent` as an example.
  - **Usage**: select **Use this node as much as possible**.
6. [](id:ContainerTemplate)In the **Containers** drop-down list, select **Add Container** > **Container Template** and configure the following container information:
    - **Name**: enter a custom container name. This document uses `jnlp-agent` as an example.
    - **Docker image**: enter the image address `jenkins/jnlp-slave:alpine`.
    - **Working directory*: keep it as its default. Record the working directory, which will be used for building and packaging shell scripts.
    - Leave other options as their defaults.
7. In **Volumes**, complete the following steps to add a volume and configure the docker command for the slave Pod:
  1. Select **Add Volume** > **Host Path Volume**. Enter `/usr/bin/docker` for both the host and mounting paths.
   2. Select **Add Volume** > **Host Path Volume**. Enter `/var/run/docker.sock` for both the host and mounting paths.
8. Click **Save** at the bottom of the page to complete configuring the slave Pod template.

## Subsequent Operations
Go to [Step 2: Slave pod building configuration](https://intl.cloud.tencent.com/document/product/457/34868) to create a task and configure task parameters.
