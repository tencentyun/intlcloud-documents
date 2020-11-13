## Introduction

The [TKE-KMS plugin](https://github.com/Tencent/tke-kms-plugin) integrates a wide range of key management features of the Key Management Service (KMS) to provide strong secret encryption or decryption for a Kubernetes cluster. This document describes how to use KMS to encrypt Kubernetes cluster data.

## Basic Concepts

#### KMS
[Tencent Cloud KMS](https://intl.cloud.tencent.com/document/product/1030/31961) is a security management solution that leverages a third-party certified hardware security module (HSM) to generate and protect keys so that you can easily create and manage keys to meet your key management and compliance needs in multi-application and multi-business scenarios.

## Prerequisites
You have created **independently deployed clusters** in TKE that meet the following conditions:
- The Kubernetes version is 1.10.0 or later.
- The Etcd version is 3.0 or later.
> To check the version, go to the "[Cluster Management](https://console.cloud.tencent.com/tke2/cluster)" page and select a cluster ID to go to the cluster’s basic information page.


## Directions
<span id="createKMS"></span>
### Creating a KMS key and obtaining the ID

1. Log in to the [KMS console](https://console.cloud.tencent.com/kms2) and go to the "Customer Managed CMK" page.
2. At the top of the page, select a region in which to create a key and click **Create**.
3. In the pop-up "Create Key" window, configure parameters, as shown below:
![](https://main.qcloudimg.com/raw/2f0db7dfc9ca005e5ed8fb16aea5ad29.png)
The following describes the main parameters. Retain the default settings for other parameters.
 - **Key Name**: this field is required and uniquely identifies a key in a region. A key name can only contain letters, digits, underscores (`_`), and hyphens (`-`) and cannot start with `KMS-`. `tke-kms` is used as an example in this document.
 - **Description**: this field is optional and used to specify the type of data to be protected, or the application to be used in conjunction with the CMK.
 - **Key Usage**: select "Symmetric Encryption/Decryption".
 - **Key Material Source**: you can select "KMS" or "External" based on actual requirements. In this document, "KMS" is used as an example.
4. Click **OK** to return to the "Customer Managed CMK" page. The created key will appear.
5. Click the key ID to enter the key information page and record the complete key ID, as shown below:
![](https://main.qcloudimg.com/raw/c4f38249ed9a9d61a083acf176dc8798.png)
<span id="CreateCVM"></span>
### Creating and obtaining the access key
> If an access key has been created, skip this step.

1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam/overview). Click **Access Key** and
then click **API Keys** on the left sidebar to go to the **Manage API Key** page.
2. On the "API Key Management" page, click **Create Key** and wait until the key is created.
3. Then, you can view the key information, including `SecretId` and `SecretKey`, as shown below:
![](https://main.qcloudimg.com/raw/9f705b5a3f7bdc5907ac86573b4c4d04.png)

### Creating a DaemonSet workload and deploying the TKE-KMS plugin

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Clusters** in the left sidebar.
2. On the "Cluster Management" page, click the ID of a cluster that meets the requirements to go to the cluster details page.
3. Click **Create using YAML** in the upper right corner to go to the "Create using YAML" page. Enter `tke-kms-plugin.yaml`, as shown below:
> Modify the following parameters based on actual requirements:
> - `{{REGION}}`: the region where the KMS key resides. Values include `ap-beijing`, `ap-guangzhou`, and `ap-shanghai`.
> - `{{KEY_ID}}`: enter the KMS key ID obtained in [Creating a KMS key and obtaining the key ID](#createKMS).
> - `{{SECRET_ID}}` and `{{SECRET_KEY}}`: enter the SecretID and SecretKey created in [Creating and obtaining the access key](#createCAM).
> - `images: ccr.ccs.tencentyun.com/tke-plugin/tke-kms-plugin:1.0.0`: the tke-kms-plugin image address. If you want to use your own tke-kms-plugin image, change the image address to that of your own image.
> 
```
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: tke-kms-plugin
  namespace: kube-system
spec:
  selector:
    matchLabels:
      name: tke-kms-plugin
  template:
    metadata:
      labels:
        name: tke-kms-plugin
    spec:
      nodeSelector:
        node-role.kubernetes.io/master: "true"
      hostNetwork: true
      restartPolicy: Always
      volumes:
        - name: tke-kms-plugin-dir
          hostPath:
            path: /var/run/tke-kms-plugin
            type: DirectoryOrCreate
      tolerations:
        - key: node-role.kubernetes.io/master
          effect: NoSchedule
      containers:
        - name: tke-kms-plugin
          image: ccr.ccs.tencentyun.com/tke-plugin/tke-kms-plugin:1.0.0
          command:
            - /tke-kms-plugin
            - --region={{REGION}}
            - --key-id={{KEY_ID}}
            - --unix-socket=/var/run/tke-kms-plugin/server.sock
            - --v=2
          livenessProbe:
            exec:
              command:
                - /tke-kms-plugin
                - health-check
                - --unix-socket=/var/run/tke-kms-plugin/server.sock
            initialDelaySeconds: 5
            failureThreshold: 3
            timeoutSeconds: 5
            periodSeconds: 30
          env:
            - name: SECRET_ID
              value: {{SECRET_ID}}
            - name: SECRET_KEY
              value: {{SECRET_KEY}}
          volumeMounts:
            - name: tke-kms-plugin-dir
              mountPath: /var/run/tke-kms-plugin
              readOnly: false
```
4. Click **Complete** and wait until the DaemonSet workload is successfully created.

### Configuring kube-apiserver
1. Log in to each Master node of the cluster by referring to [Log into Linux Instance Using Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436).
> The security group of the Master node disables port 22 by default. Before logging in to the node, go to the security group page and enable port 22. For more information, see [Adding Security Group Rules](https://intl.cloud.tencent.com/document/product/213/34272).
>
2. Run the following command to create and open a YAML file:
```
vim /etc/kubernetes/encryption-provider-config.yaml
```
3. Press **i** to switch to the editing mode and edit the preceding YAML file. Based on the Kubernetes version used, enter the following content:
 -  K8s v1.13+:
```
   apiVersion: apiserver.config.k8s.io/v1
   kind: EncryptionConfiguration
   resources:
     - resources:
         - secrets
       providers:
         - kms:
             name: tke-kms-plugin
             timeout: 3s
             cachesize: 1000
             endpoint: unix:///var/run/tke-kms-plugin/server.sock
         - identity: {}
```
 - K8s v1.10 - v1.12:
```
   apiVersion: v1
   kind: EncryptionConfig
   resources:
     - resources:
         - secrets
       providers:
         - kms:
             name: tke-kms-plugin
             timeout: 3s
             cachesize: 1000
             endpoint: unix:///var/run/tke-kms-plugin/server.sock
         - identity: {}
```
4. After editing, press **Esc** and enter **:wq** to save the file and go back.
5. Run the following command to edit the YAML file:
```
vi /etc/kubernetes/manifests/kube-apiserver.yaml
```
6. Press **i** to switch to the editing mode. Based on the Kubernetes version used, add the following content to `args`:
> For independently deployed clusters of Kubernetes v1.10.5, you need to first remove `kube-apiserver.yaml` from the `/etc/kubernetes/manifests` directory and add it after editing is complete.
>
 - K8s v1.13+:
```
 --encryption-provider-config=/etc/kubernetes/encryption-provider-config.yaml
```
 - K8s v1.10 - v1.12:
```
--experimental-encryption-provider-config=/etc/kubernetes/encryption-provider-config.yaml
```
7. Add the Volume command for `/var/run/tke-kms-plugin/server.sock`. The position and content of the added command are as follows:
> `/var/run/tke-kms-plugin/server.sock` is a Unix socket monitored when the TKE KMS server is started. kube apiserver will access the TKE KMS server through the socket.
> 
 Add the following content for `volumeMounts:`:
```
   - mountPath: /var/run/tke-kms-plugin
     name: tke-kms-plugin-dir
```
 Add the following content for `volume:`:
```
   - hostPath:
       path: /var/run/tke-kms-plugin
     name: tke-kms-plugin-dir
```
8. After you finish editing, press **Esc**, enter **:wq**, save the `/etc/kubernetes/manifests/kube-apiserver.yaml` file, and wait for kube-apiserver to restart.

### Verification

1. Log in to a cluster node and run the following command to create a secret:
```
kubectl create secret generic kms-secret -n default --from-literal=mykey=mydata
```
2. Run the following command to check whether the secret was correctly decrypted:
```
kubectl get secret kms-secret -o=jsonpath='{.data.mykey}' | base64 -d
```
3. If `mydata` appears, the secret was correctly decrypted, as shown below:
![](https://main.qcloudimg.com/raw/7d8980d32ee2b48cc30948152246fc29.png)

## Reference

For more information about Kubernetes KMS, see [Using a KMS provider for data encryption](https://kubernetes.io/docs/tasks/administer-cluster/kms-provider/).
