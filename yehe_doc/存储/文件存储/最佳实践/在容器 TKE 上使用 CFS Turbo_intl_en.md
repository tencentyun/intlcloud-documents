## Overview
This document describes how to integrate CFS Turbo with a Tencent Cloud Kubernetes Engine (TKE) cluster.


## Prerequisites

- The operating system of the TKE host node is compatible with the Turbo series.
- You have installed a Turbo-based client on all TKE nodes. You are advised to use pshell to operate in batches.
For the compatible operating systems and how to install the clients, see [Using CFS Turbo on Linux Clients](https://intl.cloud.tencent.com/document/product/582/40298).

## Directions

### Download and configure kubectl

1. Download kubectl by referring to [kubectl Documentation](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/).
2. Log in to the TKE console and select [**Cluster**](https://console.cloud.tencent.com/tke2/cluster) on the left sidebar.
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



### Creating a Pod for mounting Turbo through YAML files

1. See [TKE Turbo Plugin Guide](https://github.com/TencentCloud/kubernetes-csi-tencentcloud/blob/master/docs/README_CFSTURBO.md) and [download the script](https://github.com/TencentCloud/kubernetes-csi-tencentcloud).
2. Go to the `kubernetes-csi-tencentcloud/deploy/cfsturbo/kubernetes/` directory and upload `csi-node-rbac.yaml`, `csi-node.yaml`, and `csidriver-new.yaml` files to the kubectl management node.
3. Go to the `kubernetes-csi-tencentcloud/deploy/cfsturbo/examples/` directory and download the `pv.yaml`, `pvc.yaml`, and `pod.yaml` sample files. 

4. Modify the `pv.yaml`, `pvc.yaml`, and `pod.yaml` files based on the PV, PVC, and Pod attributes, such as name and image address. 

Below are the sample YAML files:
```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: csi-cfsturbo-pv
spec:
  accessModes:
  - ReadWriteMany
  capacity:
    storage: 10Gi
  csi:
    driver: com.tencent.cloud.csi.cfsturbo
    # volumeHandle in PV must be unique, use pv name is better
    volumeHandle: csi-cfsturbo-pv
    volumeAttributes:
      # cfs turbo proto
      proto: lustre
      # cfs turbo rootdir
      rootdir: /cfs
      # cfs turbo fsid (not cfs id)
      fsid: d3dcc487
      # cfs turbo server ip
      host: 10.0.1.16
      # cfs turbo subPath
      path: /
  storageClassName: ""
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: csi-cfsturbo-pvc
spec:
  accessModes:
  - ReadWriteMany
  resources:
    requests:
      storage: 10Gi
  # You can specify the pv name manually or just let kubernetes to bind the pv and pvc.
  volumeName: csi-cfsturbo-pv
  # cfsturbo only supports static provisioning, the StorageClass name should be empty.
  storageClassName: ""
---
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    k8s-app: csi-cfsturbo-pod
  name: csi-cfsturbo-pod
spec:
  replicas: 1
  selector:
    matchLabels:
      k8s-app: csi-cfsturbo-pod
  template:
    metadata:
      labels:
        k8s-app: csi-cfsturbo-pod
    spec:
      containers:
        - image: nginx
          name: csi-cfsturbo-pod
          volumeMounts:
            - mountPath: /csi-cfsturbo
              name: csi-cfsturbo
      volumes:
        - name: csi-cfsturbo
          persistentVolumeClaim:
            # Replaced by your pvc name.
            claimName: csi-cfsturbo-pvc
```
Below is the sample command for mounting:
```
sudo mount.lustre -o sync,user_xattr 10.0.1.16@tcp0:/d3dcc487/cfs /path/to/mount
```
Below are key parameters:
 - proto:lustre: Keep this parameter unchanged.
 - roodir:/cfs: Keep this parameter unchanged.
 - fsid:d3dcc487: Here, `fsid` is not the `CFSID`, and you need to enter the information in the mounting path.
 - host:10.0.1.16: IP of the mount point.
 - path: You can adjust it based on the target subpath. To directly mount the root directory, enter "/".
5. Run the following commands in sequence in the directory where the script is uploaded:
 - Configure RBAC:
```
kubectl apply -f csi-node-rbac.yaml
```
 - Configure the node CSI plugin:
```
kubectl apply -f csidriver-new.yaml
```
```
kubectl apply -f csi-node.yaml
```
 - Create PV, PVC, and pod:
```
kubectl create -f pv.yaml
kubectl create -f pvc.yaml
kubectl create -f pod.yaml
```
6. Run the following command to view the pod status:
```
kubectl get pod -n default -o wide
```
If the message below is displayed, the pod is created successfully:
![](https://main.qcloudimg.com/raw/5e7014090522b1667afcc0b7d351fef9.png)
If the value of `STATUS` is `ContainerCreating`, the creation failed. You can find the events in the TKE console to troubleshoot.
