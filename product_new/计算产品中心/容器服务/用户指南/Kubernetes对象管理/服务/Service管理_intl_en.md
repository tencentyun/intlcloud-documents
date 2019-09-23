## Overview

A Service defines a policy for accessing backend Pods and provides a fixed virtual access IP. With a Service, you can access backend Pods in a load balancing manner.
A Service supports the following:

- Public network access: use the Loadbalance mode of the Service to automatically create a public network CLB. Public IP addresses can directly access backend Pods.
- VPC private network access: use the Loadbalance mode of the Service to automatically create a private network CLB. If `annotations:service.kubernetes.io/qcloud-loadbalancer-internal-subnetid: subnet-xxxxxxxx` is specified, the VPC private network can directly access backend Pods through private IP addresses.
- Intra-cluster access: use the ClusterIP mode of the Service which automatically assigns an IP address in the IP range of the Service for intra-cluster access.

## Console Operation Guide for Services

### Notes

- Do not use the same CLB for TKE and CVM.
- Do not directly operate the CLB that is automatically managed by TKE in the CLB console.
- When using an existing CLB:
  - You can only use load balancers created through CLB console but not balancers automatically created by TKE.
  - Ports of Services sharing the same existing CLB cannot be the same.
  - Services in different clusters cannot share the same CLB.
  - Services sharing the same CLB do not support local access.
  - When you delete a Service using an existing CLB, the backend CVM bound with the balancer will not be unbound automatically. You need to unbind it manually. The tag (tke-clusterId: cls-xxxx) will be kept for the CLB. You will need to clear it manually.
- TKE will automatically overwrite and update the listener named TKE_Dedicated_Listener but not other listeners.

### Creating a Service

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the ID of the cluster for which you need to create a Service to enter the cluster management page.
4. Select **Service** > **Service** to go to the Service information page as shown below:
   
   ![Service](https://main.qcloudimg.com/raw/d42865b5fc802688b365cb2c8409e811.png)
5. Click **Create** to go to the "Create a Service" page as shown below:
   
   ![Create a Service](https://main.qcloudimg.com/raw/beb261a208c44327e4d5381f29ac0724.png)
6. Set the Service parameters based on your needs. The key parameter information is as follows:
   - Service name: a user-defined name.
   - Namespace: select based on your needs.
   - Service access method: select an access method based on your needs.
   - Port mapping: configure based on your needs.
7. Click **Create a Service** to complete the creation.

### Updating a Service

#### Updating YAML

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the ID of the cluster for which you want to update YAML to enter the cluster management page.
4. Select **Service** > **Service** to go to the Service information page as shown below:
   
   ![Service](https://main.qcloudimg.com/raw/d42865b5fc802688b365cb2c8409e811.png)
5. In the row of the Service for which you want to update YAML, click **Edit YAML** to go to the Service update page.
6. On the **Update a Service** page, edit the YAML and click **Finish**.

## Using kubectl to Operate Services

<span id="YAMLSample"></span>

### YAML Sample

```Yaml
kind: Service
apiVersion: v1
metadata:
  ## Annotations:
  ## service.kubernetes.io/qcloud-loadbalancer-internal-subnetid: subnet-xxxxxxxx ## If you are creating a Service for private network access, you need to specify this annotation
  name: my-service
spec:
  selector:
    app: MyApp
  ports:
  - protocol: TCP
    port: 80
    targetPort: 9376
  type: LoadBalancer
```

- kind: Service resource type.
- metadata: basic information such as Service name and label.
- metadata.annotations: an additional description of a Service. You can set additional enhancements for TKE through this parameter.
- spec.type: the access policy defined by a Service.
  - ClusterIP: the service is public inside the cluster to enable intra-cluster access.
  - NodePort: the node port is mapped to the backend Service, and the service can be accessed outside the cluster through node IP:NodePort.
  - LoadBalancer: a CLB provided by Tencent Cloud is used to make the service public. A public network CLB is created by default. A private network CLB can be created by specifying the annotations.
  - ExternalName: the service is mapped to DNS. This is applicable to kube-dns v1.7 or higher.

#### annotations: create a Service for public/private network access with an existing load balancer

If the existing CLB is idle and you want to use it for a Service created by TKE, or you expect to use the same CLB within the cluster, you can do so with the following annotations:

> Note:
> 
> - You can only use load balancers created through CLB console but not balancers automatically created by TKE.
> 
> - Ports of Services sharing the same existing CLB cannot be the same.
> 
> - Services in different clusters cannot share the same CLB.
> 
> - Services sharing the same CLB do not support local access.
> 
> - When you delete a service using an existing CLB, the backend CVM bound with the balancer will not be unbound automatically. You need to unbind it manually. The tag (tke-clusterId: cls-xxxx) will be kept for the CLB. You will need to clear it manually.

```Yaml
metadata:
  annotations:
    service.kubernetes.io/tke-existed-lbid: lb-6swtxxxx
```

#### annotations: bind Loadbalancers with speicfied nodes

If your cluster is large, you will need to set affinity scheduling for entry-type applications to schedule them to certain nodes . You can configure the Loadbalancer of the Service to bind the Loadbalancer only with specified nodes. The annotations are as follows:

```yaml
metadata:
  annotations:
    service.kubernetes.io/qcloud-loadbalancer-backends-label: `key in (value1, value2) ` ## LabelSelector format
```

- It is recommended to use this together with the affinity scheduling of the workload.
- The prerequisite is that a label has been set for the nodes based on your needs.
- Use native LabelSelector formats such as:
  - service.kubernetes.io/qcloud-loadbalancer-backends-label: key1=values1, key2=values2
  - service.kubernetes.io/qcloud-loadbalancer-backends-label: key1 in (value1),key2 in (value2)
  - service.kubernetes.io/qcloud-loadbalancer-backends-label: key in (value1, value2)
  - service.kubernetes.io/qcloud-loadbalancer-backends-label: key1, key2 notin (value2)
- If a new node is matched, it will be automatically bound to the Loadbalancer.
- If you modify the label of an existing node, the node will be dynamically bound with or unbound from the Loadbalancer in accordance with the matching rule.

> ? If you are using a account with IP bandwidth packages, you need to specify the following two annotations when creating a service accessible to the public network:
> 
> - `service.kubernetes.io/qcloud-loadbalancer-internet-charge-type` for public network bandwidth billing method; valid values: TRAFFIC_POSTPAID_BY_HOUR (bill-by-traffic) and BANDWIDTH_POSTPAID_BY_HOUR (bill-by-bandwidth).
> - `service.kubernetes.io/qcloud-loadbalancer-internet-max-bandwidth-out` for bandwidth cap (value range: [1,2000] Mbps).
>   
> For example:
>   
> ```Yaml
> metadata:
> annotations:
> service.kubernetes.io/qcloud-loadbalancer-internet-charge-type: TRAFFIC_POSTPAID_BY_HOUR
> service.kubernetes.io/qcloud-loadbalancer-internet-max-bandwidth-out: "10"
>   ```
> For more information on IP bandwidth packages, see [here](https://console.cloud.tencent.com/tke2).

### Creating a Service

1. Prepare the StatefulSet YAML file as instructed by [YAML sample](#YAMLSample).
2. Install Kubectl and connect to a cluster. For detailed operations, see [Connecting to a Cluster via kubectl](https://cloud.tencent.com/document/product/457/8438).
3. Run the following command to create the Service YAML file.
   
   ```shell
   kubectl create -f Service YAML filename
   ```
   
   For example, to create a Service YAML file named my-service.yaml, run the following command:
   
   ```shell
   kubectl create -f my-service.yaml
   ```
4. Run the following command to see if the Service is successfully created.
   
   ```shell
   kubectl get services
   ```
   
   A message similar to the one below indicates that you have successfully created the Service.
   
   ```
   NAME         TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)   AGE
   kubernetes ClusterIP 172.16.255.1 <none> 443/TCP 38d
   ```

### Updating a Service

#### Method 1

Run the following command to update a Service.

```
kubectl edit service/[name]
```

#### Method 2

1. Manually delete the old Service.
2. Run the following command to create a new Service.
   
   ```
   kubectl create/apply
   ```

### Deleting a Service

Run the following command to delete a Service.

```
kubectl delete service [NAME]
```
