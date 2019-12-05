## Introduction
An Ingress is a collection of rules that allow access to services within a cluster. You can configure different forwarding rules to allow different URLs to access different services within the cluster.
For the proper running of Ingress resources, the cluster must run an Ingress controller. TKE enables the CLB-based `l7-lb-controller` by default in the cluster. It supports HTTP, HTTPS, and nginx-ingress types. You can select different Ingress types based on your business needs.

## Managing Ingress in Console

### Notes
- Make sure your container and CVM instance do not share a CLB.
- For a CLB managed by TKE, you cannot modify its listeners, forwarding paths, certificates, and backend-bound servers on CLB console. Changes made on CLB console will be automatically overwritten by TKE.

### Creating an Ingress

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the cluster ID where the Ingress needs to be created to go to the cluster management page.
4. Select **Services** -> **Ingress** to go to the Ingress information page. See the figure below:
![Ingress](https://main.qcloudimg.com/raw/72d715c235d98e1a8e38c05ddf105a21.png)
5. Click **Create** to go to the **Create an Ingress** page. See the figure below:
![Create an Ingress](https://main.qcloudimg.com/raw/116d6add93717282a62f1793e2146317.png)
6. Set the Ingress parameters as needed. Key parameters are as follows:
 - Ingress name: custom.
 - Network type: the default value is `Public network`. Select an option as needed.
 - Namespace: select an option as needed. 
 - Listening port: the default value is **Http:80**. Select an option as needed.
 - Forwarding configuration: set this parameter as needed.
7. Click **Create Ingress** to create an Ingress.

### Updating an Ingress

#### Updating YAML

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the cluster ID for which you want to update the YAML to go to the cluster management page.
4. Select **Services** -> **Ingress** to go to the Ingress information page. See the figure below:
![Ingress](https://main.qcloudimg.com/raw/72d715c235d98e1a8e38c05ddf105a21.png)
5. In the row of the Ingress for which you want to update YAML, click **Edit YAML** to go to the **Update an Ingress** page.
6. On the **Update an Ingress** page, edit YAML and click **Complete** to update YAML.

#### Updating a forwarding rule

1. On the cluster management page, click the cluster ID for which you want to update the YAML to go to the cluster management page.
2. Select **Services** -> **Ingress** to go to the Ingress information page. See the figure below:
![Ingress](https://main.qcloudimg.com/raw/72d715c235d98e1a8e38c05ddf105a21.png)
3. In the row of the Ingress for which you want to update the forwarding rule, click **Update forwarding configuration** to go to the forwarding configuration updating page. See the figure below:
![Update forwarding configuration](https://main.qcloudimg.com/raw/4246dede3aaa2e21bdb691dd6ccf1a48.png)
3. Modify the forwarding configuration based on actual needs and click **Update forwarding configuration** to complete the update.

## Managing Ingress Using kubectl

<span id="YAMLSample"></span>
### YAML Sample
```Yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  annotations:
    kubernetes.io/ingress.class: qcloud ## Options: qcloud (CLB-type Ingress), nginx (nginx-ingress)
    ## kubernetes.io/ingress.subnetId: subnet-xxxxxxxx  ##If you are creating a CLB-type private network Ingress, you need to specify this annotation.
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

### Descriptions
If you are using an account with **IP bandwidth packages**, you need to specify the following two annotations when creating a service accessible to the public network:
- `kubernetes.io/ingress.internetChargeType` identifies the public network bandwidth billing method. Optional values include:
 - TRAFFIC_POSTPAID_BY_HOUR (Bill-by-traffic)
 - BANDWIDTH_POSTPAID_BY_HOUR (Bill-by-bandwidth)
- `kubernetes.io/ingress.internetMaxBandwidthOut` identifies the bandwidth cap, value range: [1, 2000] Mbps.
For example:
```Yaml
metadata:
  annotations:
    kubernetes.io/ingress.internetChargeType: TRAFFIC_POSTPAID_BY_HOUR
    kubernetes.io/ingress.internetMaxBandwidthOut: "10"
```
For more information on **IP bandwidth packages**, please see [Bandwidth Package Types](https://cloud.tencent.com/document/product/684/15246).

### Creating an Ingress

1. Prepare the Ingress YAML file as instructed by [YAML sample](#YAMLSample).
2. Install kubectl and connect to a cluster. For detailed operations, please see [Connecting to Clusters](https://intl.cloud.tencent.com/document/product/457/31086).
3. Run the following command to create the Ingress YAML file.
```shell
kubectl create -f Ingress YAML filename
```
For example, to create an Ingress YAML file named “my-ingress.yaml”, run the following command:
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
