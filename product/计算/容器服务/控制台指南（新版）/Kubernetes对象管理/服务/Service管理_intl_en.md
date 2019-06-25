## Overview

A Service defines the access policy for accessing a backend Pod and provides a fixed virtual access IP. You can access the backend Pod through the Service in a load balancing manner.
Services support the following types:

- Public network access: This automatically creates a public CLB using the Service's Loadbalance mode. A public IP can directly access the backend Pod.
- VPC private network access: This automatically creates a private CLB using the Service's Loadbalance mode. If `annotations:service.kubernetes.io/qcloud-loadbalancer-internal-subnetid: subnet-xxxxxxxx` is specified, the VPC private network can directly access the Pod in the backend through the private IP.
- Intra-cluster access: Use the ClusterIP mode of the Service which automatically assigns an IP in the IP address range of the Service for intra-cluster access.

## Operation Guide for Services in the Console

### Considerations

- It is recommended that your container business not share a CLB load balancer with the CVM business.
- It is recommended not to manipulate the CLB load balancers automatically managed by TKE directly in the CLB console.
- If you want to use an existing CLB load balancer, please note that: 
  - You can only use load balancers created through CLB console but not existing balancers automatically created by TKE.
  - Ports of services sharing the same existing CLB load balancer cannot duplicate.
  - Services in different clusters cannot share the same CLB load balancer.
  - Services using sharing CLB load balancers do not support local access. 
  - When you delete a service using an existing CLB load balancer, the balancer will not be deleted, and the bound backend CVM will not be unbound. You need to unbind it manually. The tag (tke-clusterId: cls-xxxx) will be kept for the CLB. You can clear it manually.
- TKE will automatically overwrite and update the listener named TKE_Dedicated_Listener but not other listeners.

### Creating a Service

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the ID of the cluster where Service needs to be created to enter the cluster management page.
4. Select "Service" > "Service" to go to the Service information page. See the figure below:
   
   ![Service](https://main.qcloudimg.com/raw/d42865b5fc802688b365cb2c8409e811.png)
5. Click **Create** to go to the "Create a Service" page. See the figure below:
   
   ![Create a Service](https://main.qcloudimg.com/raw/beb261a208c44327e4d5381f29ac0724.png)
6. Set the Service parameters based on actual needs. Key parameters are as follows:
   - Service name: Custom.
   - Namespace: Select based on actual needs.
   - Service access method: Select the corresponding access method based on actual needs.
   - Port mapping: Set based on actual needs.
7. Click **Create a Service** to complete the creation.

### Updating a Service

#### Updating YAML

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the ID of the cluster where YAML needs to be updated to enter the cluster management page.
4. Select "Service" > "Service" to go to the Service information page. See the figure below:
   
   ![Service](https://main.qcloudimg.com/raw/d42865b5fc802688b365cb2c8409e811.png)
5. In the row of the Service for which to update the YAML, click **Edit YAML** to go to the Service updating page.
6. On the "Update a Service" page, edit the YAML and click **Finish** to update the YAML.

## Using kubectl to Manipulate Services

<span id="YAMLSample"></span>

### YAML Sample

```Yaml
kind: Service
apiVersion: v1
metadata:
  ## annotations:
  ##   service.kubernetes.io/qcloud-loadbalancer-internal-subnetid: subnet-xxxxxxxx ## If you are creating a Service for private network access, you need to specify this annotation
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

- kind: This identifies the Service resource type.
- metadata: Basic information such as Service name and Label.
- metadata.annotations: An additional description of the Service. You can set additional enhancements to TKE through this parameter.
- spec.type: This identifies the access type of the Service.
  - ClusterIP: The Service is made public inside the cluster to enable intra-cluster access.
  - NodePort: The port of the node is mapped to the backend Service, and the cluster can be accessed from outside through node IP:NodePort.
  - LoadBalancer: A CLB load balancer provided by Tencent Cloud is used to make the Service public. A public network load balancer is created by default. A private network load balancer can be created by specifying the annotations.
  - ExternalName: The Service is mapped to DNS. This is only for kube-dns v1.7 or higher.

#### annotations: Create a public/private access Service using an existing load balancer

If your existing classic CLB load balancer is idle and you want to use it for the Service created by TKE, you can set it using the following annotations:

> Note:
> 
> - You can only use load balancers created through CLB console but not balancers automatically created by TKE.
> 
> - Ports of services sharing the same existing CLB load balancer cannot duplicate.
> 
> - Services in different clusters cannot share the same CLB load balancer.
> 
> - Services using sharing CLB load balancers do not support local access. 
> 
> - When you delete a service using an existing CLB load balancer, the balancer will not be deleted, and the bound backend CVM will not be unbound. You need to unbind it manually. The tag (tke-clusterId: cls-xxxx) will be kept for the CLB. You can clear it manually.

```Yaml
metadata:
  annotations:
    service.kubernetes.io/tke-existed-lbid: lb-6swtxxxx
```

#### annotations: Specify the Loadbalances bound to the node

If your cluster is large, you should set affinity scheduling to some nodes for an entry-type application. You can configure the Loadbalance of the Service to bind only the specified nodes. The annotations are as follows:

```yaml
metadata:
  annotations:
    service.kubernetes.io/qcloud-loadbalancer-backends-label: `key in (value1, value2) ` ## LabelSelector format
```

- It is recommended to use this together with the affinity scheduling of the workload.
- The prerequisite is that a Label has been set for the Node based on the business needs.
- Use the native LabelSelector format, such as:
  - service.kubernetes.io/qcloud-loadbalancer-backends-label: key1=values1, key2=values2
  - service.kubernetes.io/qcloud-loadbalancer-backends-label: key1 in (value1),key2 in (value2)
  - service.kubernetes.io/qcloud-loadbalancer-backends-label: key in (value1, value2)
  - service.kubernetes.io/qcloud-loadbalancer-backends-label: key1, key2 notin (value2)
- If a new node is matched, it will be automatically bound to the Loadbalance.
- Modify the Label of an existing node and dynamically bind/unbind the Loadbalance according to the matching rule.

If you are using a bill-by-IP account, you need to specify the following two annotations when creating a service accessible to the public network:
> 
> - `service.kubernetes.io/qcloud-loadbalancer-internet-charge-type` for public network bandwidth billing method; options include: TRAFFIC_POSTPAID_BY_HOUR (bill-by-traffic) and BANDWIDTH_POSTPAID_BY_HOUR (bill-by-bandwidth).
> - `service.kubernetes.io/qcloud-loadbalancer-internet-max-bandwidth-out` for bandwidth upper limit (value range: [1,2000] Mbps).
>   
> For example:
>   
>   ```Yaml
>   metadata:
>   annotations:
>     service.kubernetes.io/qcloud-loadbalancer-internet-charge-type: TRAFFIC_POSTPAID_BY_HOUR
>     service.kubernetes.io/qcloud-loadbalancer-internet-max-bandwidth-out: "10"
>   ```

### Creating a Service

1. See the [YAML sample](#YAMLSample) to prepare the StatefulSet YAML file.
2. Install kubectl and connect to a cluster. For detailed operations, see [Connecting a Cluster via kubectl](https://cloud.tencent.com/document/product/457/8438).
3. Run the following command to create the Service YAML file.
   
   ```shell
   kubectl create -f Service YAML filename
   ```
   
   For example, to create a Service YAML file named my-service.yaml, run the following command:
   
   ```shell
   kubectl create -f my-service.yaml
   ```
4. Run the following command to verify whether the creation is successful.
   
   ```shell
   kubectl get services
   ```
   
   If a message similar to the one below is returned, the creation is successful.
   
   ```
   NAME         TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)   AGE
   kubernetes   ClusterIP   172.16.255.1   <none>        443/TCP   38d
   ```

### Updating a Service

#### Method 1

Run the following command to update a Service.

```
kubectl edit service/[name]
```

#### Method 2

1. Manually delete the old Service.
2. Run the following command to recreate a Service.
   
   ```
   kubectl create/apply
   ```

### Deleting a Service

Run the following command to delete a Service.

```
kubectl delete service [NAME]
```
