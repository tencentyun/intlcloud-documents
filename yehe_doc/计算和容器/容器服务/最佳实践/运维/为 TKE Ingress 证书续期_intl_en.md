## Overview
Ingress certificates created in the Tencent Kubernetes Engine (TKE) console will reference certificates hosted in the [SSL Certificate Service](https://console.cloud.tencent.com/ssl). If an Ingress is used for a long time, the Ingress certificate may expire, which will have a major impact on online businesses. This document describes how to renew an Ingress certificate before it expires.

## Directions
### Querying the certificate expiration time

1. Log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl) and click **Certificate Management** in the left sidebar.
2. In the certificate list, click **Expiration Date** to view certificates that are about to expire.

### Adding a certificate
On the **Certificate Management** page, you can renew an existing certificate to generate a new certificate. You can **Purchase Certificate**, **Apply for Free Certificate**, or **Upload Certificate** to add a certificate.
<span id="ingress"></span>

### Viewing the Ingress that references the old certificate 
1. Log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl) and select **Associate Cloud Resources** next to a certificate to view the load balancer that references this certificate.
2. Click the load balancer ID to redirect to the CLB details page. If the CLB is used for the TKE Ingress, `tke-clusterId` and `tke-lb-ingress-uuid` will appear in the **Tag** section. `tke-clusterId` and `tke-lb-ingress-uuid` indicate the cluster ID and Ingress UID, respectively.
3. On the **Basic Info** page of the CLB, click the editing icon in the tag line to enter the **Edit Tags** page.
4. Use Kubectl to query the Ingress of the cluster based on the cluster ID and filter out the Ingress resource whose UID is `tke-lb-ingress.uuid`. The sample reference code is as follows:
```
$ kubectl get ingress --all-namespaces -o=custom-columns=NAMESPACE:.metadata.namespace,INGRESS:.metadata.name,UID:.metadata.uid | grep 1a******-****-****-a329-eec697a28b35
api-prod    gateway      1a******-****-****-a329-eec697a28b35
```
According to the query result, `api-prod/gateway` in this cluster references the certificate. Therefore, this Ingress needs to be updated.

### Updating an Ingress

1. In the [TKE console](https://console.cloud.tencent.com/tke2), find [the Ingress that reference the old certificate](#ingress) and click **Update Forwarding Configuration**.
2. On the **Update Forwarding Configuration** page, create a secret for the new certificate.
 On the **Create Key** page, select the new certificate and click **Create Secret**.
Return to the **Update Forwarding Configuration** page, modify the TLS configuration of the Ingress, and add the created certificate secret.
Click **Update Forwarding Configuration** to renew the Ingress certificate.
