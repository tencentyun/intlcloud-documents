## Overview
An Ingress is a collection of rules that allow access to services within a cluster. You can configure different forwarding rules to allow different URLs to access different services within the cluster.
In order for the Ingress resources to work properly, the cluster must run an Ingress controller. The TKE service has enabled the `l7-lb-controller` implemented based on CLB by default in the cluster, which supports HTTP, HTTPS, and nginx-ingress types. You can select different Ingress types based on your business needs.

## Operation Guide for Ingresses in the Console

### Creating an Ingress

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the ID of the cluster where Ingress needs to be created to enter the cluster management page.
4. Select "Service" > "Ingress " to go to the Ingress information page. See the figure below:
![Ingress](https://main.qcloudimg.com/raw/72d715c235d98e1a8e38c05ddf105a21.png)
5. Click **Create** to go to the "Create an Ingress" page. See the figure below:
![Create an Ingress](https://main.qcloudimg.com/raw/116d6add93717282a62f1793e2146317.png)
6. Set the Ingress parameters based on actual needs. Key parameters are as follows:
 - Ingress name: Custom.
 - Network type: The default value is "Public network". Please select based on actual needs.
 - Namespace: Select based on actual needs.
 - Listening port: The default value is "Http:80". Please select based on actual needs.
 - Forwarding configuration: Set based on actual needs.
7. Click **Create an Ingress** to complete the creation.

### Updating an Ingress

#### Updating YAML

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the ID of the cluster where YAML needs to be updated to enter the cluster management page.
4. Select "Service" > "Ingress " to go to the Ingress information page. See the figure below:
![Ingress](https://main.qcloudimg.com/raw/72d715c235d98e1a8e38c05ddf105a21.png)
5. In the row of the Ingress for which to update the YAML, click **Edit YAML** to go to the Ingress updating page.
6. On the "Update an Ingress" page, edit the YAML and click **Finish** to update the YAML.

#### Updating a Forwarding Rule

1. On the cluster management page, click the ID of the cluster for which to update the YAML to go to the management page of the cluster.
2. Select "Service" > "Ingress" to go to the Ingress information page. See the figure below:
![Ingress](https://main.qcloudimg.com/raw/72d715c235d98e1a8e38c05ddf105a21.png)
3. In the row of the Ingress for which to update the forwarding rule, click **Update forwarding configuration** to go to the forwarding configuration updating page. See the figure below:
![Update forwarding configuration](https://main.qcloudimg.com/raw/4246dede3aaa2e21bdb691dd6ccf1a48.png)
3. Modify the forwarding configuration based on actual needs and click **Update forwarding configuration** to complete the update.

## Using kubectl to Manipulate Ingresses

<span id="YAMLSample"></span>
### YAML Sample
```Yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  annotations:
    kubernetes.io/ingress.class: qcloud ## Options: qcloud (CLB-type Ingress), nginx (nginx-ingress)
    ## kubernetes.io/ingress.subnetId: subnet-xxxxxxxx  ## If you are creating a CLB-type Ingress for a private network, you need to specify this annotation
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
- kind: This identifies the Ingress resource type.
- metadata: Basic information such as Ingress name and Label.
- metadata.annotations: An additional description of the Ingress. You can set additional enhancements to TKE through this parameter.
- spec.rules: The forwarding rule of the Ingress, which can be configured to implement simple routing service, domain name-based simple fan-out routing, default domain name for simple routing, and securely configured routing service.

>? If you are using a bill-by-IP account, you need to specify the following two annotations when creating a service accessible to the public network:
> - `kubernetes.io/ingress.internetChargeType` for public network bandwidth billing method: TRAFFIC_POSTPAID_BY_HOUR (bill-by-traffic) or BANDWIDTH_POSTPAID_BY_HOUR (bill-by-bandwidth).
> - `kubernetes.io/ingress.internetMaxBandwidthOut` for bandwidth upper limit (value range: [1,2000] Mbps).
For example:
```Yaml
metadata:
  annotations:
    kubernetes.io/ingress.internetChargeType: TRAFFIC_POSTPAID_BY_HOUR
    kubernetes.io/ingress.internetMaxBandwidthOut: "10"
```

### Creating an Ingress

1. See the [YAML sample](#YAMLSample) to prepare the Ingress YAML file.
2. Install kubectl and connect to a cluster. For detailed operations, see [Connecting a Cluster via kubectl](https://cloud.tencent.com/document/product/457/8438).
3. Run the following command to create the Ingress YAML file.
```shell
kubectl create -f Ingress YAML filename
```
For example, to create an Ingress YAML file named my-ingress.yaml, run the following command:
```shell
kubectl create -f my-ingress.yaml
```
4. Run the following command to verify whether the creation is successful.
```shell
kubectl get ingress
```
If a message similar to the one below is returned, the creation is successful.
```
NAME          HOSTS       ADDRESS   PORTS     AGE
clb-ingress   localhost             80        21s
```

### Updating an Ingress

#### Method 1

Run the following command to update an Ingress.
```
kubectl edit  ingress/[name]
```

#### Method 2

1. Manually delete the old Ingress.
2. Run the following command to recreate an Ingress.
```
kubectl create/apply
```
