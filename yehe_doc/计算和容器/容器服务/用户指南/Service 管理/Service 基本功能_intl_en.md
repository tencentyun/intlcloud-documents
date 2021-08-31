
## Managing Services in the Console

### Creating a service

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. Click the ID of the cluster for which you need to create a service to go to the cluster management page.
3. Choose **Services and Routes** -> **Service** to go to the service management page, as shown below:
![](https://main.qcloudimg.com/raw/ad9db14ae516c9f1652a3ac5f6018120.png)
4. Click **Create** to go to the "Create a Service" page.
   Set the service parameters as needed. The key parameter information is as follows:
   - **Service Name**: customize a service name.
   - **Namespace**: select a namespace based on your requirements.
   - **Access Settings (Service)**: configure account settings based on Overview and your requirements.
   > To use an existing CLB, see "Using Existing CLBs".
   >
6. Click **Create Service** to complete creation.



### Updating a Service
#### Updating the YAML file


1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. Click the ID of the cluster for which you want to update the YAML file to go to the cluster management page.
3. Choose **Services and Routes** -> **Service** to go to the service information page, as shown below:
![](https://main.qcloudimg.com/raw/af2835a138b38f1b5abf8671ac9c846e.png)
4. In the row of the service for which you want to update the YAML file, click **Edit YAML** to go to the service update page.
5. On the "Update a Service" page, edit the YAML file and click **Finish**.

## Managing Services Using kubectl

<span id="YAMLSample"></span>
### YAML sample
```Yaml
kind: Service
apiVersion: v1
metadata:
  ## annotations:
  ## service.kubernetes.io/qcloud-loadbalancer-internal-subnetid: subnet-xxxxxxxx ## If you are creating a service for private network access, you need to specify this annotation.
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

- **kind**: identifies the service resource type.
- **metadata**: basic information such as the service name and label.
- **metadata.annotations**: additional service description. You can use this parameter to set enhanced features for TKE.
- **spec.type**: identifies the service access type.
  - **ClusterIP**: the service is available and accessible in the cluster.
  - **NodePort**: maps the node port to the backend service. The service can be accessed from outside the cluster using `IP:NodePort`.
  - **LoadBalancer**: the service is opened using the CLB provided by TKE. By default, a public CLB is created. You can specify annotations to create a private CLB.
  - **ExternalName**: the service is mapped to the DNS. This only applies to kube-dns v1.7 or later.



### Creating a service

1. Refer to the [YAML sample](#YAMLSample) to prepare the service YAML file.
2. Install kubectl and connect it to a cluster. For more information, see [Connecting to a Cluster](https://intl.cloud.tencent.com/document/product/457/30639).
3. Run the following command to create the service YAML file:
```shell
kubectl create -f Service YAML file name
```
For example, to create a service YAML file named my-service.yaml, run the following command:
```shell
kubectl create -f my-service.yaml
```
4. Run the following command to check whether the service YAML file was successfully created:
```shell
kubectl get services
```
If information similar to the following is returned, the service YAML file was created successfully.
```
NAME         TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   172.16.255.1   <none>        443/TCP   38d
```

### Updating a service

#### Method 1
Run the following command to update a service:
```
kubectl edit service/[name]
```

#### Method 2
1. Manually delete the old service.
2. Run the following command to create a service:
```
kubectl create/apply
```

### Deleting a service
Run the following command to delete a service:
```
kubectl delete service [NAME]
```

<style>
	.params{margin-bottom:0px !important;}
</style>
