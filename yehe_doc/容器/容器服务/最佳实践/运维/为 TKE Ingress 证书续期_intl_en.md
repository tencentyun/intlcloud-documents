## Overview
Ingress certificates created in the Tencent Kubernetes Engine (TKE) console will reference certificates hosted in the [SSL Certificate Service](https://console.cloud.tencent.com/ssl). If an Ingress is used for a long time, the Ingress certificate may expire, which will have a major impact on online businesses. This document describes how to renew an Ingress certificate before it expires. 

## Directions
### Querying the certificate expiration time

1. Log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl) and click **Certificate Management** in the left sidebar. 
2. In the certificate list, click **Expiry date** to view certificates that are about to expire. 

### Adding a certificate
On the **Certificate management** page, you can renew an existing certificate to generate a new certificate. You can **Purchase certificate**, **Apply for free certificate**, or **Upload certificate** to add a certificate. 

### Viewing Ingresses referencing old certificate[](id:ingress)
1. Log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl) and select **Associate cloud resources** next to a certificate to view the load balancer that references this certificate.
2. Click the load balancer ID to redirect to the CLB details page. If the CLB is used for the TKE Ingress, `tke-clusterId` and `tke-lb-ingress-uuid` will appear in the **Tag** section. `tke-clusterId` and `tke-lb-ingress-uuid` indicate the cluster ID and Ingress UID, respectively.
3. On the **Basic info** page of the CLB, click the editing icon in the tag line to enter the **Edit tags** page.
4. Use Kubectl to query the Ingress of the cluster based on the cluster ID and filter out the Ingress resource whose UID is `tke-lb-ingress.uuid`. The sample reference code is as follows:
```
$ kubectl get ingress --all-namespaces -o=custom-columns=NAMESPACE:.metadata.namespace,INGRESS:.metadata.name,UID:.metadata.uid | grep 1a******-****-****-a329-eec697a28b35
api-prod    gateway      1a******-****-****-a329-eec697a28b35
```
According to the query result, `api-prod/gateway` in this cluster references the certificate. Therefore, this Ingress needs to be updated. 

### Updating an Ingress

1. In the [TKE console](https://console.cloud.tencent.com/tke2), find [the Ingress that references the old certificate](#ingress) and click **Update forwarding configuration**.
![](https://qcloudimg.tencent-cloud.cn/raw/44ba860bacb644d1c1f3a3e15f7568d9.png)
2. On the **Update forwarding configuration** page, create a secret for the new certificate.
![](https://qcloudimg.tencent-cloud.cn/raw/931646bb90883beb0ff28ed141ce1b8f.png)
 On the **Create key** page, select the new certificate and click **Create secret**.
![](https://qcloudimg.tencent-cloud.cn/raw/3b40a3fed01728f31c3abb829d210737.png)
Return to the **Update forwarding configuration** page, modify the TLS configuration of the Ingress, and add the created certificate secret.
![](https://qcloudimg.tencent-cloud.cn/raw/78c26a7a003152874d237fcb2f7d516f.png)
Click **Update forwarding configuration** to renew the Ingress certificate. 
