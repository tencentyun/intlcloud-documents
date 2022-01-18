## Overview
This document describes how to integrate CFS Turbo with a Tencent Cloud Kubernetes Engine (TKE) cluster.


## Prerequisites

- The operating system of the TKE host node is compatible with the Turbo series.
- You have installed a Turbo-based client on all TKE nodes. You are advised to use pshell to operate in batches.
For the compatible operating systems and how to install the clients, please see [Using CFS Turbo on Linux Clients](https://intl.cloud.tencent.com/document/product/582/40298).

## Directions

### Download and configure kubectl

1. Download kubectl by referring to [kubectl Documentation](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/).
2. Log in to the TKE console and click [Cluster](https://console.cloud.tencent.com/tke2/cluster) in the left sidebar.
3. On the **Cluster Management** page, click the ID of the target cluster to go to the cluster details page.
4. On the cluster details page, click **Basic Information**.
5. In **Cluster APIServer Information**, click **Download** to download the `kubeconfig` file to the default environment variable address and name it `config`, that is, `/usr/local/bin/config`.

6. <span id="step6"></span>In **Cluster APIServer Information**, set **Private Network Access** to ![](https://main.qcloudimg.com/raw/557ab76a34a9a1af96a81237e12882c3.png) and click ![](https://main.qcloudimg.com/raw/6603ab4f907562addb1c01596c6296cd.png) to copy the command for host configuration.
7. Switch to the access machine to run the command copied from [Step 6](#step6).
8. Run the following commands to configure the environment variable:
```
vi /etc/profile
KUBECONFIG=/usr/local/bin/config
PATH=$PATH
export KUBECONFIG
export PATH
```
7. Run the following command to verify whether kubectl has been installed successfully:
```
kubectl get node
```
If the following message is displayed, the installation is completed:
![](https://main.qcloudimg.com/raw/8bc11f2f8951c7e6037763dbe1bf190c.png)



### Mounting the Turbo pod with a script

1. See [TKE Turbo Plugin Guide](https://github.com/TencentCloud/kubernetes-csi-tencentcloud/blob/master/docs/README_CFSTURBO.md) and [download](https://github.com/TencentCloud/kubernetes-csi-tencentcloud)  the script.
2. Go to the `kubernetes-csi-tencentcloud/deploy/cfsturbo/kubernetes/` directory and upload `csi-node-rbac.yaml`, `csi-node.yaml`, and `csidriver.yaml` to the CVM management node that can access the TKE cluster.
3. Go to the `kubernetes-csi-tencentcloud/deploy/cfsturbo/examples/` directory to download the `static-allinone.yaml` sample file.
4. Modify the `static-allinone.yaml` file according to the actual PV, PVC, and pod attributes (e.g., name, image address). NGINX is used as an example here.
```
sudo mount.lustre -o sync,user_xattr 10.0.1.16@tcp0:/d3dcc487/cfs /path/to/mount
```
Where, the host is `10.0.1.16` and the fsid is `d3dcc487`.
The modified script sample is as follows:
```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-cfsturbo
spec:
  accessModes:
  - ReadWriteMany
  capacity:
    storage: 10Gi
  csi:
    driver: com.tencent.cloud.csi.cfsturbo
    volumeHandle: pv-cfsturbo
    volumeAttributes: 
      # cfs turbo server ip
      host: 10.0.0.116
      # cfs turbo fsid(not cfs id)
      fsid: xxxxxxxx
      proto: lustre
  storageClassName: ""
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-cfsturbo
spec:
  storageClassName: ""
  volumeName: pv-cfsturbo
  accessModes:
  - ReadWriteMany
  resources:
    requests:
      storage: 10Gi
---
apiVersion: v1
kind: Pod
metadata:
  name: nginx 
spec:
  containers:
  - image: ccr.ccs.tencentyun.com/qcloud/nginx:1.9
    imagePullPolicy: Always
    name: nginx
    ports:
    - containerPort: 80
      protocol: TCP
    volumeMounts:
      - mountPath: /var/www
        name: data
  volumes:
  - name: data
    persistentVolumeClaim:
      claimName: pvc-cfsturbo
```
5. Run the following commands in sequence in the directory where the script is uploaded:
 - Configure RBAC:
```
kubectl apply -f csi-node-rbac.yaml
```
 - Configure the node CSI plugin:
```
kubectl apply -f csidriver.yaml
```
```
kubectl apply -f csi-node.yaml
```
 - Create PV, PVC, and pod:
```
kubectl create -f static-allinone.yaml
```
6. Run the following command to view the pod status:
```
kubectl get pod -n default -o wide
```
If the message below is displayed, the pod is created successfully:
![](https://main.qcloudimg.com/raw/5e7014090522b1667afcc0b7d351fef9.png)
If the value of `STATUS` is `ContainerCreating`, the creation failed. You can find the events in the TKE console to troubleshoot.
