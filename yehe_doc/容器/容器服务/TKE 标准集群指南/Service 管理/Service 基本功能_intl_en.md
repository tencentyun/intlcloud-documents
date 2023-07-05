
## Managing a Service in the Console

### Creating a Service

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. In the **Cluster** page, click the ID of the cluster for which you need to create a Service to go to the cluster management page.
4. Select **Services and Routes** > **Service** to go to the **Service** management page, as shown below:
![](https://main.qcloudimg.com/raw/ad9db14ae516c9f1652a3ac5f6018120.png)
5. Click **Create** to enter the **Create Service** page.
Set the Service parameters as needed. Key parameters are as follows:
   - **Service Name**: Customize a name.
   - **Namespace**: Select a namespace based on your requirements.
   - **Access Settings**: Set it as needed and as instructed in [Overview](https://intl.cloud.tencent.com/document/product/457/36832).
   - **Workload binding**: Reference an existing workload or customize a label. Then, the Service will select workloads with the label.
>?
>- To use an existing CLB instance, see [Using Existing CLBs](https://intl.cloud.tencent.com/document/product/457/36835).
>- As a layer-4 CLB instance has only **the unique quadruple of CLB VIP, listener protocol, backend RS VIP, and backend RS port** and doesn't contain a CLB listener port, scenarios with different CLB listener ports but the same protocol and RS are not supported. In addition, TKE doesn't support opening different ports of the same protocol for the same business.
>
7. Click **Create service**.



### Updating a Service
#### Updating YAML


1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the **Cluster Management** page, select the target cluster ID.
3. Select **Services and Routes** > **Service** to enter the Service information page as shown below:
![](https://main.qcloudimg.com/raw/af2835a138b38f1b5abf8671ac9c846e.png)
5. Click **Edit YAML** on the right of the target Service.
6. On the **Update Service** page, edit the YAML and click **Done**.

## Managing a Service Using kubectl

[](id:YAMLSample)
### YAML sample
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

- **kind**: It identifies the Service resource type.
- **metadata**: Basic information such as Service name and label.
- **metadata.annotations**: An additional description of the Service. You can set additional enhancements to TKE through this parameter.
- **spec.selector**: The Service will select workloads with the label in the label selector.
- **spec.type**: It identifies the mode for accessing the Service.
  - **ClusterIP**: The Service is made public in the cluster for internal access.
  - **NodePort**: The node port mapped to the backend Service. External access to the cluster can be implemented through `IP:NodePort`.
  - **LoadBalancer**: The Service is made public through the Tencent Cloud CLB instance. A public network CLB instance is created by default, and a private network one can be created by specifying annotations.
	- By default, you can create up to 100 public network or private network CLB instances. If you need more, [submit a ticket](https://console.tencentcloud.com/workorder/category) to increase the quota.
	- The management and sync of configurations between Service and CLB instances are based on the resource object of the `LoadBalancerResource` type named the CLB ID. Do not perform any operations on this CRD; otherwise, the Service may fail.
  - **ExternalName**: The Service is mapped to DNS, which applies to only kube-dns 1.7 or later.



### Creating a Service

1. Prepare the Service YAML file as instructed in the [YAML sample](#YAMLSample).
2. Install kubectl and connect to a cluster. For detailed operations, see [Connecting to a Cluster](https://intl.cloud.tencent.com/document/product/457/30639).
3. Run the following command to create the Service YAML file.
```shell
kubectl create -f Service YAML filename
```
For example, to create a Service YAML file named `my-service.yaml`, run the following command:
```shell
kubectl create -f my-service.yaml
```
4. Run the following command to check whether the Job is successfully created.
```shell
kubectl get services
```
If a message similar to the following is returned, the creation is successful.
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
