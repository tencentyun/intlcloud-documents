## Overview 
Ingress is a collection of rules that allow access to Services of a cluster. You can configure different forwarding rules to allow different URLs to access different Services.
To properly run Ingress resources, the cluster must run an Ingress controller. TKE enables the CLB-based `l7-lb-controller` by default in the cluster. It supports HTTP and HTTPS as well as other self-built Ingress controllers in the cluster. You can select different Ingress types based on your business needs.

## Notes[](id:annotations)   
- Do not use the same CLB for TKE and CVM.
- For a CLB managed by TKE, you cannot modify its listeners, forward paths, certificates, and backend-bound servers on the CLB console. Changes made on the CLB console will be automatically overwritten by TKE.
- When using an existing CLB:
  - You can only use load balancers created through the CLB console, not balancers automatically created by TKE.
  - Do not use one CLB for multiple Ingresses.
  - Do not use the same CLB for Ingress and Service.
  - After you delete an Ingress, the real server bound to the reused CLB will need to be unbound manually. `tag tke-clusterId: cls-xxxx` will be kept for the CLB and will need to be cleared manually.
  - By default, you can create up to 50 forwarding rules under a single CLB instance. If you need more, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) to increase the quota.
  - The management and sync of configurations between Ingress and CLB instances are based on the resource object of the `LoadBalancerResource` type named the CLB ID. Do not perform any operations on this CRD; otherwise, the Ingress may fail.


## Managing Ingress in Console

### Creating an Ingress

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Cluster** to go to the cluster management page.
3. Click the cluster ID where the Ingress needs to be created to go to the cluster management page.
4. Select **Service** > **Ingress** to go to the Ingress information page.
5. Click **Create** to go to the **Create an Ingress** page.
![](https://main.qcloudimg.com/raw/f2fd4c00a82da4e564b964c87b7e7bcb.png)
6. Set the Ingress parameters based on your actual needs. The key parameters are as follows:
 - Ingress name: custom.
 - Network type: the default value is `Public network`. Select another network if needed.
 - IP Version: You can select IPv4 or IPv6 NAT64 as needed.
 - Load balancer: create one automatically or use an existing CLB.
 - Namespace: select the namespace based on your actual needs.
 - Forwarding Configuration: the default value of **Protocol** is **Http**. You can select a protocol as needed.
   If you select **Https**, you need to bind the server certificate to ensure access security.
   ![](https://staticintl.cloudcachetci.com/yehe/backend-news/aGbv982_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221223175112.png)
   For more information, see [Certificate Requirements and Certificate Format Conversion](https://intl.cloud.tencent.com/document/product/214/6155).
 - Forwarding configuration: set this parameter based on your actual needs.
7. Click **Create Ingress** to create an Ingress.

### Updating an Ingress

#### Updating YAML

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Cluster** to go to the cluster management page.
3. Click the cluster ID for which you want to update the YAML to go to the cluster management page.
4. Select **Service** > **Ingress** to go to the Ingress information page.
![](https://main.qcloudimg.com/raw/9d8befd5a41b4c922999f3337a71f2ab.png)
5. In the row of the Ingress for which you want to update YAML, click **Edit YAML** to go to the **Update an Ingress** page.
6. On the **Update an Ingress** page, edit YAML and click **Complete** to update YAML.

#### Updating a forwarding rule

1. On the cluster management page, click the cluster ID for which you want to update the YAML to go to the cluster management page.
2. Select **Service** > **Ingress** to go to the Ingress information page.
![](https://main.qcloudimg.com/raw/6fdbb1dacd69b382e93204a3ead2cbbb.png)
3. In the row of the Ingress for which you want to update the forwarding rule, click **Update the forwarding configuration** to go to the **Update forwarding configuration** page as shown in the figure below:
![](https://main.qcloudimg.com/raw/ac813654063e6349790d10216d3eab47.png)
4. Modify the forwarding configuration based on your actual needs and click **Update forwarding configuration** to complete the update.

## Managing Ingresses Using Kubectl


### YAML sample[](id:YAMLSample)
```Yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  annotations:
    kubernetes.io/ingress.class: qcloud ## Options: qcloud (CLB-type Ingress), nginx (nginx-ingress), traefik 
	## kubernetes.io/ingress.existLbId: lb-xxxxxxxx  ## Specify an existing load balancer to be used to create the Ingress for public/private network access.
    ## kubernetes.io/ingress.subnetId: subnet-xxxxxxxx  ## If you are creating a CLB-type private network Ingress, you need to specify this annotation.
  name: my-ingress
  namespace: default
spec:
  rules:
  - host: localhost
    http:
      paths:
      - backend:
          serviceName: non-service
          servicePort: 65535
        path: /
```
- kind: identifies the Ingress resource type.
- metadata: basic information such as Ingress name and Label.
- metadata.annotations: an additional description of the Ingress. You can set additional enhancements for TKE through this parameter.
- spec.rules: the Ingress forwarding rule, which can be configured to implement a simple routing service, domain name-based simple fan-out routing, default domain name for simple routing, and a securely configured routing service.

#### annotations: create an Ingress for public/private network access using an existing load balancer

If the existing application CLB is idle and you want to use it for an Ingress created by TKE or you want to use the same CLB within the cluster, you can set it using the following annotations:
>? Please read the [Notes](#annotations) before using it.
>
```Yaml
metadata:
  annotations:
    kubernetes.io/ingress.existLbId: lb-6swtxxxx
```

#### annotations: create a private network Ingress of the CLB type

If you need to use a private network CLB, set it with the following annotations:
```Yaml
metadata:
  annotations:
    kubernetes.io/ingress.subnetId: subnet-xxxxxxxx
```

#### Notes
If you are using an account with **IP bandwidth packages**, you need to specify the following two annotations when creating a service accessible to the public network:
- `kubernetes.io/ingress.internetChargeType` identifies the public network bandwidth billing method. Options include:
 - TRAFFIC_POSTPAID_BY_HOUR (bill-by-traffic)
 - BANDWIDTH_POSTPAID_BY_HOUR (bill-by-bandwidth)
- `kubernetes.io/ingress.internetMaxBandwidthOut` identifies the bandwidth cap (value range: [1, 2000] Mbps).
For example:
```Yaml
metadata:
  annotations:
    kubernetes.io/ingress.internetChargeType: TRAFFIC_POSTPAID_BY_HOUR
    kubernetes.io/ingress.internetMaxBandwidthOut: "10"
```

### Creating an Ingress

1. Prepare the Ingress YAML file as instructed by the [YAML sample](#YAMLSample).
2. Install kubectl and connect to a cluster. For detailed operations, see [Connecting to a Cluster](https://intl.cloud.tencent.com/document/product/457/30639).
3. Run the following command to create the Ingress YAML file.
```shell
kubectl create -f Ingress YAML filename
```
For example, to create an Ingress YAML file named “my-ingress.yaml”, run the following command:
```shell
kubectl create -f my-ingress.yaml
```
4. Run the following command to check whether the Job is successfully created.
```shell
kubectl get ingress
```
If a message similar to the following is returned, the creation is successful.
```
NAME          HOSTS       ADDRESS   PORTS     AGE
clb-ingress   localhost             80        21s
```

### Updating an Ingress

#### Method 1

Run the following command to update an Ingress:
```
kubectl edit  ingress/[name]
```

#### Method 2

1. Manually delete the old Ingress.
2. Run the following command to recreate an Ingress:
```
kubectl create/apply
```
