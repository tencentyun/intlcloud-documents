## Introduction
An Ingress is a collection of rules that allow access to services within a cluster. You can configure different forwarding rules to allow different URLs to access different services within the cluster.
For the proper running of Ingress resources, the cluster must run an Ingress controller. TKE enables the CLB-based `l7-lb-controller` by default in the cluster. It supports HTTP, HTTPS, and nginx-ingress types. You can select different Ingress types based on your business needs.
<span id="annotations"></span>   
## Notes
- Do not use the same CLB for TKE and CVM.
- For a CLB managed by TKE, you cannot modify its listeners, forwarding paths, certificates, and backend-bound servers on CLB console. Changes made on the CLB console will be automatically overwritten by TKE.
- When using an existing CLB:
  - You can only use load balancers created through the CLB Console, not balancers automatically created by TKE.
  - Do not use one CLB for multiple Ingresses.
  - Do not use the same CLB for Ingress and Service.
  - When you delete an Ingress, the real server bound to the reused CLB needs to be unbound manually, and `tag tke-clusterId: cls-xxxx` is kept for the CLB. You need to clear it manually.

## Operation Guide for Ingresses in the Console

### Creating an Ingress

1. Log in to the [TKE Console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the cluster ID where the Ingress needs to be created to go to the cluster management page.
4. Select **Service** -> **Ingress** to go to the Ingress information page.
5. Click **Create** to go to the **Create an Ingress** page. See the figure below:
![](https://main.qcloudimg.com/raw/f2fd4c00a82da4e564b964c87b7e7bcb.png)
6. Set the Ingress parameters as needed. Key parameters are as follows:
 - Ingress name: custom.
 - Network type: the default value is "Public network". Select an option as needed.
 - Load balancer: create one automatically or use an existing CLB.
 - Namespace: select an option as needed.
 - Listener port: the default is **Http:80**. Select another port if needed.
 If **Https:443** is selected, a server certificate must be bound to ensure access security. For more information, see [SSL certificate format requirements and format conversion description](https://intl.cloud.tencent.com/document/product/214/5369).
 - Forwarding configuration: set this parameter as needed.
7. Click **Create Ingress** to create an Ingress.

### Updating an Ingress

#### Updating YAML

1. Log in to the [TKE Console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the cluster ID for which you want to update the YAML to go to the cluster management page.
4. Select **Service** -> **Ingress** to go to the Ingress information page. See the figure below:
![](https://main.qcloudimg.com/raw/9d8befd5a41b4c922999f3337a71f2ab.png)
5. In the row of the Ingress for which you want to update YAML, click **Edit YAML** to go to the **Update an Ingress** page.
6. On the **Update an Ingress** page, edit YAML and click **Complete** to update YAML.

#### Updating a forwarding rule

1. On the cluster management page, click the cluster ID for which you want to update the YAML to go to the cluster management page.
2. Select **Service** -> **Ingress** to go to the Ingress information page. See the figure below:
![](https://main.qcloudimg.com/raw/6fdbb1dacd69b382e93204a3ead2cbbb.png)
3. In the row of the Ingress for which you want to update the forwarding rule, click **Update forwarding configuration** to go to the **Update forwarding configuration** page. See the figure below:
![](https://main.qcloudimg.com/raw/ac813654063e6349790d10216d3eab47.png)
4. Modify the forwarding configuration based on actual needs and click **Update forwarding configuration** to complete the update.

## Managing Ingress Using kubectl

<span id="YAMLSample"></span>
### YAML sample
```Yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  annotations:
    kubernetes.io/ingress.class: qcloud ## Options: qcloud (CLB-type Ingress), nginx (nginx-ingress)
	## kubernetes.io/ingress.existLbId: lb-xxxxxxxx  ## Specify an existing load balancer to use to create the Ingress for public/private network access.
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
- spec.rules: the Ingress forwarding rule, which can be configured to implement a simple routing service, domain name-based simple fan-out routing, default domain name for simple routing, and securely configured routing service.

#### annotations: create an Ingress for public/private network access using an existing load balancer

If the existing application CLB is idle and you want to use it for an Ingress created by TKE or you want to use the same CLB within the cluster, you can set it using the following annotations:
>Read the [Notes](#annotations) before using it.
>
```Yaml
metadata:
  annotations:
    kubernetes.io/ingress.existLbId： lb-6swtxxxx
```

#### annotations: create an Ingress of the CLB type

If you need to use a private network CLB, set it with the following annotations:
```Yaml
metadata:
  annotations:
    kubernetes.io/ingress.subnetId: subnet-xxxxxxxx
```

#### Notes
If you are using an account with **IP bandwidth packages**, you need to specify the following two annotations when creating a service accessible to the public network:
- `kubernetes.io/ingress.internetChargeType` identifies the public network bandwidth billing method. Optional values include:
 - TRAFFIC_POSTPAID_BY_HOUR (Bill-by-traffic)
 - BANDWIDTH_POSTPAID_BY_HOUR (Bill-by-bandwidth)
> - `kubernetes.io/ingress.internetMaxBandwidthOut` for bandwidth upper limit (value range: [1,2000] Mbps).
For example:
```Yaml
metadata:
  annotations:
    kubernetes.io/ingress.internetChargeType: TRAFFIC_POSTPAID_BY_HOUR
    kubernetes.io/ingress.internetMaxBandwidthOut: "10"
```
For more information on **IP bandwidth packages**, see the [Bandwidth Package Types](https://intl.cloud.tencent.com/document/product/684/15246) document.

### Creating an Ingress

1. Prepare the Ingress YAML file as instructed by [YAML sample](#YAMLSample).
2. Install kubectl and connect to a cluster. For detailed operations, please see [Connecting to a Cluster](https://intl.cloud.tencent.com/document/product/457/30639).
3. Run the following command to create the Ingress YAML file.
```shell
kubectl create -f Ingress YAML filename
```
For example, to create an Ingress YAML file named my-ingress.yaml, run the following command:
```shell
kubectl create -f my-ingress.yaml
```
4. Run the following command to check whether the Ingress YAML file was successfully created:
```shell
kubectl get ingress
```
A message similar to the one below indicates that the Ingress YAML file is successfully created.
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
