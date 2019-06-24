## Overview

A StorageClass describes the type of storage. A cluster admin can define various storage types for the cluster. In Tencent Cloud TKE, the default StorageClass is block storage. Configuring both StorageClass and PersistentVolumeClaim allows you to create your desired storage type and capacity dynamically.

## Operation Guide for StorageClasses in the Console

### Creating a StorageClass

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the ID of the cluster where StorageClass needs to be created to enter the cluster management page.
4. Select "Storage" > "StorageClass" to go to the StorageClass information page. See the figure below:
![StorageClass](https://main.qcloudimg.com/raw/f9490f2903cf3d18e4896a048fed8963.png)
5. Click **Create** to go to the "Create a StorageClass" page. See the figure below:
![Create a StorageClass](https://main.qcloudimg.com/raw/ca37abe20b64e6ae235c0494ba8fcb36.png)
6. Set the StorageClass parameters based on actual needs. Key parameters are as follows:
 - Name: Custom.
 - Billing method: Select based on actual needs.
 - Availability zone: Select based on actual needs. The default value is "Random availability zone".
 - Cloud disk type: Select based on actual needs.
 - Reclaiming policy: Select based on actual needs.
7. Click **Create a StorageClass** to complete the creation.

### Specifying a StorageClass When Creating a PVC

Create a PVC as instructed in the "[Creating a PVC](https://intl.cloud.tencent.com/document/product/457/30679#Creating a PVC)" section in [PV and PVC Management](https://intl.cloud.tencent.com/document/product/457/30679). Select StorageClass when setting the PVC parameters.

### Creating a StatefulSet Mount to Automatically Create a PersistentVolumeClaim

Create a StatefulSet as instructed in the "[Creating a StatefulSet](#createStatefulSet)" section in [StatefulSet Management](https://intl.cloud.tencent.com/document/product/457/30663). When setting the StatefulSet parameters, click **Add a volume** and select "Use a new PVC" to set the PVC. See the figure below:
![](https://main.qcloudimg.com/raw/d0e2ca3c5db78c13fa3b1e70497c5513.png)

## Using kubectl to Manipulate StorageClasses

The following is a sample where which you can perform creation directly using kubectl.

### Creating a StorageClass

If you haven't created any StorageClass, a StorageClass named CBS will exist in the cluster by default.
```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  # annotations:
  #   storageclass.beta.kubernetes.io/is-default-class: "true"
  # If this line is present, it will become the default-class, and if you do not specify a type when creating a PVC, this type will be used automatically
  name: cloud-premium
provisioner: cloud.tencent.com/qcloud-cbs ## The provisioner coming with the TKE cluster
parameters:
  type: CLOUD_PREMIUM
  # This supports CLOUD_BASIC, CLOUD_PREMIUM, and CLOUD_SSD; if not recognized, it will default to CLOUD_BASIC
  # paymode: PREPAID
  # paymode is the billing method of the cloud disk, which can be PREPAID (prepaid method, which only supports the "Retain" reclaiming policy) or POSTPAID (postpaid method, which supports "Retain" or "Delete" reclaiming policy. This is the default value. Retain is only available in cluster version 1.8 or higher)
  # aspid:asp-123
  # You can specify a snapshot policy. After the cloud disk is created, it will be automatically bound to this policy. Binding failure does not affect the creation
```
Supported parameters included:
- type: The type of StorageClass, including CLOUD_BASIC, CLOUD_PREMIUM, and CLOUD_SSD (all in UPPERCASE).
- zone: This specifies the zone. If a zone is specified, the cloud disk will be created in the zone; if no zone is specified, the system will pull the zone information of all nodes and select a random zone. For the identifiers of Tencent Cloud regions and availability zones, see [Regions and Availability Zones](https://intl.cloud.tencent.com/document/product/213/6091).
- paymode: The billing method of the cloud disk. The default value is POSTPAID (postpaid method, which supports "Retain" or "Delete" reclaiming policy. Retain is only available in cluster version 1.8 or higher). It can also be set to PREPAID (prepaid method, which only supports the "Retain" reclaiming policy)
- aspid: It specifies a snapshot ID. After the cloud disk is created, it will be automatically bound to this policy. Binding failure does not affect the creation

### Creating a Multi-Pod StatefulSet

You can create a multi-Pod StatefulSet using CBS as follows:
``` yaml
apiVersion: apps/v1beta1
kind: StatefulSet
metadata:
  name: web
spec:
  serviceName: "nginx"
  replicas: 3
  template:
    metadata:
      labels:
        app: nginx
    spec:
      terminationGracePeriodSeconds: 10
      containers:
      - name: nginx
        image: nginx
        ports:
        - containerPort: 80
          name: web
        volumeMounts:
        - name: www
          mountPath: /usr/share/nginx/html
  volumeClaimTemplates:  # Automatically create a PVC to automatically create a PV
  - metadata:
      name: www
    spec:
      accessModes: [ "ReadWriteOnce" ]
      storageClassName: cloud-premium
      resources:
        requests:
          storage: 10Gi
```
