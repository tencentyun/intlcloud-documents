## Introduction<span id="Introduction"></span>
A Service defines the method for accessing a backend Pod and provides a fixed virtual access IP address. You can access the backend Pod through settings in the Service. Services with different access methods can provide different network capabilities.
TKE provides the following 4 access methods:

<table>
<tr>
<th width="15%">Access methods</th>
<th>Description</th>
</tr>
<tr>
<td>Via Internet</td>
<td>
<ul class="params">
<li>In Loadbalance mode of the Service, a public IP address allows direct access to the backend Pod. This is suitable for Web frontend services.</li>
<li>The created service can be accessed outside the cluster by using the <b>CLB domain name or IP address and the Service port</b>; and inside the cluster by using the <b>Service name and Service port</b>.</li>
</ul>
</td>
</tr>
<tr>
<td>Intra-cluster</td>
<td>
<ul class="params">
<li>Uses the ClusterIP mode of the Service, in which an IP address in the IP address range of the Service is automatically assigned for intra-cluster access. This method is applicable to MySQL and other database services to ensure isolation among service networks.</li>
<li>The created service can be accessed using the <b>Service name and Service port</b>.</li>
</ul>
</td>
</tr>
<tr>
<td>Via VPC</td>
<td>
<ul class="params">
<li>Uses the Loadbalance mode of the Service. If <code>annotations:service.kubernetes.io/qcloud-loadbalancer-internal-subnetid: subnet-xxxxxxxx</code> is specified, the backend Pod can be accessed using a private IP address.</li>
<li>The created service can be accessed outside the cluster by using the <b>CLB domain name or IP address and the Service port</b>; and inside the cluster by using the <b>Service name and Service port</b>.</li>
</ul>
</td>
</tr>
<tr>
<td>Node Port Access</td>
<td>
<ul class="params">
<li>An access method that maps a node port to the container, with support for TCP, UDP, and Ingress. It can be used for forwarding from upper-layer custom LB to Node.</li>
<li>The created service can be accessed using <b>CVM IP and Node port</b> or <b>Service name and Service port</b>.</li>
</ul>
</td>
</tr>
</table>


## Notes<span id="annotations"></span>
- Make sure your container and CVM instance do not share a CLB.
- For a CLB managed by TKE, you cannot modify its listeners and backend-bound servers on CLB console. Changes made on CLB console will be automatically overwritten by TKE.
- When using an existing CLB:
  - You can only use load balancers created through the CLB console, not balancers automatically created by TKE.
  - Ports of Services sharing the same existing CLB cannot be the same.
  - Services in different clusters cannot share the same CLB.
  - Services sharing the same CLB do not support local access.
  - When you delete a Service using an existing CLB, the real server bound to the balancer needs to be unbound manually. The tag (tke-clusterId: cls-xxxx) is kept for the CLB. You need to clear it manually.


## Managing Service in Console



### Creating a Service

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the ID of the cluster for which you need to create a Service to go to the cluster management page.
4. Select **Service** -> **Service** to go to the Service information page. See the figure below:
![](https://main.qcloudimg.com/raw/3628305bd167fca1f3e2eaa2a4e1d615.png)
5. Click **Create** to go to the **Create a Service** page. See the figure below:
![](https://main.qcloudimg.com/raw/be05e7133d8c205a42dbb03a1b1de3a5.png)
6. Set the Service parameters as needed. The key parameter information is as follows:
   - Service name: custom.
   - Namespace: select an option as needed. 
   - Access settings: please see [Introduction](#Introduction) and set this parameter as needed.
7. Click **Create Service** to complete creation.

### Updating a Service

#### Updating YAML

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the cluster ID for which you want to update the YAML to go to the cluster management page.
4. Select **Service** -> **Service** to go to the Service information page. See the figure below:
![](https://main.qcloudimg.com/raw/77224c6dc76ded174f4188c6e184cc90.png)
5. In the row of the Service for which you want to update the YAML, click **Edit YAML** to go to the Service update page.
6. On the **Update a Service** page, edit YAML and click **Finish**.

## Managing Services Using kubectl

<span id="YAMLSample"></span>
### YAML Sample
```Yaml
kind: Service
apiVersion: v1
metadata:
  ## annotations:
  ## service.kubernetes.io/qcloud-loadbalancer-internal-subnetid: subnet-xxxxxxxx ## If you are creating a Service for private network access, you need to specify this annotation.
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

- kind: identifies the Service resource type.
- metadata: basic information such as Service name and Label.
- metadata.annotations: an additional description of a Service. You can set additional enhancements for TKE through this parameter.
- spec.type: identifies the access type of the Service.
  - ClusterIP: the service is open in the cluster and can be accessed inside the cluster. 
   NodePort: Maps the the node port to the backend Service, and the service can be accessed outside the cluster through “[node IP]:[NodePort]”.
  - LoadBalancer: the service is made open to the public through a CLB. A public network CLB is created by default if you choose this type. You can also create a private network CLB by specifying the annotations.
  - ExternalName: the Service is mapped to DNS. This is only applicable to kube-dns v1.7 or higher.

#### annotations: create a Service for public/private network access with an existing load balancer

If the existing CLB is idle and you want to use it for a Service created by TKE, or you expect to use the same CLB within the cluster, you can set it using the following annotations:
>Please read the [Notes](#annotations) before using.
>
```Yaml
metadata:
  annotations:
    service.kubernetes.io/tke-existed-lbid: lb-6swtxxxx
```

#### annotations: specifies the Loadbalancer bound to the node

If your cluster is large, you need to set affinity scheduling for entry-type applications to schedule them to certain nodes. You can configure the Loadbalancer of the Service to bind the Loadbalancer only to specified nodes. The annotations are as follows:

```yaml
metadata:
  annotations:
    service.kubernetes.io/qcloud-loadbalancer-backends-label: `key in (value1, value2) ` ## LabelSelector format
```

- It is recommended to use this together with workload affinity scheduling.
- The prerequisite is that a Label has been set for the nodes according to your business needs.
- Use native LabelSelector formats such as:
  - service.kubernetes.io/qcloud-loadbalancer-backends-label: key1=values1, key2=values2
  - service.kubernetes.io/qcloud-loadbalancer-backends-label: key1 in (value1),key2 in (value2)
  - service.kubernetes.io/qcloud-loadbalancer-backends-label: key in (value1, value2)
  - service.kubernetes.io/qcloud-loadbalancer-backends-label: key1, key2 notin (value2)
- If a new node is matched, it will be automatically bound to the Loadbalancer.
- If you modify the label of an existing node, the node will be dynamically bound with or unbound from the Loadbalancer in accordance with the matching rule.

#### Descriptions
If you are using an account with **IP bandwidth packages**, you need to specify the following two annotations when creating a service accessible to the public network:
- `service.kubernetes.io/qcloud-loadbalancer-internet-charge-type` identifies the public network bandwidth billing method. Optional values include:   
 -  TRAFFIC_POSTPAID_BY_HOUR (Bill-by-traffic)
 -  BANDWIDTH_POSTPAID_BY_HOUR (Bill-by-bandwidth)
- `service.kubernetes.io/qcloud-loadbalancer-internet-max-bandwidth-out` identifies the  bandwidth cap (value range: [1,2000] Mbps).
   For example:
```Yaml
  metadata:
  annotations:
  service.kubernetes.io/qcloud-loadbalancer-internet-charge-type: TRAFFIC_POSTPAID_BY_HOUR
  service.kubernetes.io/qcloud-loadbalancer-internet-max-bandwidth-out: "10"
```
For more information on **IP bandwidth packages**, please see the document [Bandwidth Package Types](https://cloud.tencent.com/document/product/684/15246).

### Creating a Service

1. Prepare the StatefulSet YAML file as instructed by [YAML sample](#YAMLSample).
2. Install kubectl and connect to a cluster. For detailed operations, please see [Connecting to Clusters](https://intl.cloud.tencent.com/document/product/457/31086).
3. Run the following command to create the Service YAML file.
```shell
kubectl create -f Service YAML filename
```
For example, if you want to create a Service YAML file named “my-service.yaml”, run the following command:
 ```shell
kubectl create -f my-service.yaml
 ```
4. Run the following command to check whether the Service YAML file was successfully created:
```shell
kubectl get services
```
A message similar to the one below indicates that the Ingress YAML file is successfully created. 
```
NAME         TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)   AGE
kubernetes ClusterIP 172.16.255.1 <none> 443/TCP 38d
```

### Updating a Service

#### Method 1
Run the following command to update a Service:
```
kubectl edit service/[name]
```

#### Method 2
1. Manually delete the old Service.
2. Run the following command to create a new Service:
```
kubectl create/apply
```

### Deleting a Service
Run the following command to delete a Service:
```
kubectl delete service [NAME]
```

<style>
	.params{margin-bottom:0px !important;}
</style>
