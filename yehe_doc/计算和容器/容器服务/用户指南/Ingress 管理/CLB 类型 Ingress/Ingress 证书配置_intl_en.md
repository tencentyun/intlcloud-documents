## Overview
This document describes how to use an Ingress certificate. You can configure an Ingress certificate in the following scenarios:
- If HTTPS is selected as the listener protocol when you create an Ingress, selecting a proper server certificate helps ensure access security.
- If you bind the same certificate for all HTTPS domain names, you can configure a certificate with all HTTPS rules in the Ingress to simplify updates.
- Binding different certificates to different domain names helps improve the SSL/TLS performance of the server and client.

## Notes
- You need to create the certificate to be configured in advance. For more information, see [Creating a server certificate in the console](#create).
- You need to set the Ingress certificate by using a Secret. Tencent Kubernetes Engine (TKE) Ingress creates a Secret with the same name as the certificate by default, which contains the certificate ID.
- If you want to change the certificate, it is recommended that you create a certificate on the certificate platform and update the Secret certificate ID. Because the cluster add-on is synced based on the Secret statement, if you update the certificate on other certificate services or CLB services, the update will be restored by Secret.
- The Secret certificate resource must be in the same namespace as the Ingress resource.
- When you create the Ingress certificate, a Secret certificate resource with the same name will be created automatically by the console. If the Secret resource name already exists, the Ingress certificate cannot be created.
- Generally, when you create an Ingress certificate, the certificate resource associated with a Secret will not be reused. However, you still can create an Ingress certificate that reuses the certificate resource associated with the Secret. When the Secret is updated, all Ingress certificates that are associated with the Secret are also updated.
- Once you add a matching certificate for a domain name, the CLB SNI feature is enabled and cannot be disabled. If the domain name corresponding to the certificate is deleted, the certificate will match the HTTPS domain name corresponding to the Ingress by default.
- Classic CLB does not support domain name- or URL-based forwarding. An Ingress that is created through Classic CLB cannot be configured with multiple certificates.




## Examples
TKE allows you to configure a certificate for a CLB HTTPS listener that is created for an Ingress by using the `spec.tls` field in the Ingress. Where, `secretName` indicates a Kubernetes Secret resource that contains a Tencent Cloud certificate ID, as shown in the following example:
#### Ingress
Creating via YAML:
```yaml
spec:
    tls:
    - hosts:
      - www.abc.com
      secretName: secret-tls-2
```

#### Secret
<dx-tabs>
::: Creating via YAML
```yaml
apiVersion: v1
stringData:
    qcloud_cert_id: Xxxxxxxx ## Set the certificate ID as Xxxxxxxx
kind: Secret
metadata:
    name: tencent-com-cert
    namespace: default
type: Opaque
```
:::
::: Creating via the console
You can create a Secret in the **TKE console**. For more information, see [Secret Management](https://intl.cloud.tencent.com/document/product/457/30676).
The main parameters of a Secret are as follows:
 - **Name**: A custom name. This document uses `cos-secret` as an example.
 - **Secret type**: Select **Opaque**. This type is suitable for saving key certificates and configuration files. The value is Base64-coded.
 - **Validity range**: Select a range as required and ensure that the Secret is in the same namespace as the Ingress.
 - **Content**: Set the variable name to `qcloud_cert_id` and the variable value to the server certificate ID.

:::
</dx-tabs>

>! If you want to configure a mutual authentication certificate, you need to add both the server certificate and the client CA certificate to the Secret. Also, you need to add a key pair to the Secret: The variable name is `qcloud_ca_cert_id`, and the variable value is the  client CA certificate ID.


## Ingress Certificate Configuration
- If only one `spec.secretName` is set and no hosts are configured, the certificate will be configured for all HTTPS forwarding rules, as shown in the following example:
```yaml
spec:
    tls:
    - secretName: secret-tls
```
- You can configure a level-1 domain name with a wildcard, as shown in the following example:
```yaml
spec:
    tls: 
    - hosts:
      - '*.abc.com'
      secretName: secret-tls
```
- If you configure a certificate and a wildcard certificate at the same time, TKE selects a certificate based on priority. As shown in the following example, `www.abc.com` will use the certificate that is described in `secret-tls-2`.
```yaml
spec:
    tls: 
    - hosts:
      - '*.abc.com'
      secretName: secret-tls-1
    - hosts:
      - www.abc.com
      secretName: secret-tls-2
```
- When you update an Ingress that has used multiple certificates, the TKE Ingress controller will perform the following judgments:
   - If no host matches rules.host in HTTPS, the update cannot be submitted.
   - If one TLS host matches rules.host in HTTPS, the update can be submitted and the certificate corresponding to the Secret can be configured for the host.
   - When a SecretName of TLS is changed, only the existence of the SecretName but not the Secret content will be verified. In this case, the update can be submitted as long as the Secret exists.
> ! Ensure that the certificate ID in the Secret meets requirements.





## Directions
### Creating a sever certificate in the console[](id:create)
>? Skip this step if you already have the target certificate.
>
1. Log in to the CLB console and click [Certificate Management](https://console.cloud.tencent.com/clb/cert) in the left sidebar.
2. On the "Certificate management" page, click **Create**.
3. On the "Create a new certificate" page, set the parameters based on the following description:
   - **Certificate name**: Set a custom certificate name.
   - **Certificate type**: Select “Server certificate”, which indicates an SSL certificate. An encrypted HTTP protocol based on the SSL certificate for secure data transmission enables a site to be switched from Hypertext Transfer Protocol (HTTP) to Hyper Text Transfer Protocol over Secure Socket Layer (HTTPS).
   - **Certificate content**: Enter the certificate content based on your actual requirements. For more information on certificate format requirements, see [SSL Certificate Format](https://intl.cloud.tencent.com/document/product/214/6155).
   - **Key content**: It is displayed only when "Certificate type" is "Server certificate". For more information on how to add key content, see [SSL Certificate Format](https://intl.cloud.tencent.com/document/product/214/6155).
4. Click **Submit**.

### Creating an Ingress object that uses the certificate

#### Notes:
- When HTTPS service is enabled for an Ingress object created in the console, a Secret resource with the same name will be created to store the certificate ID. Then, this Secret is used and referenced to in the Ingress.
- The mappings between domain names and certificates that can be configured in TLS are as follows:
 	- A level-1 domain name with the wildcard can be configured.
  - If a domain name matches several certificates, a certificate is randomly selected. We recommend that you not use different certificates for the same domain name.
  - You must configure certificates for all HTTPS domain names. Otherwise, the Ingress object may fail to be created.


#### The steps are as follows:
Create an Ingress object. For more information, see [Ingress Management](https://intl.cloud.tencent.com/document/product/457/30673). During the creation, select **Https:443** as the listening port.



### Modifying certificates

#### Notes:
- To modify a certificate, you need to verify all Ingress objects that use the certificate. If multiple Ingress objects are configured with the same Secret resource, the CLB certificates of these Ingress objects will be modified simultaneously.
- You need to modify a certificate by modifying its Secret because the Secret content includes your Tencent Cloud certificate ID.

#### The steps are as follows:
1. Run the following command to open the Secret to be modified in the default editor. Note that you need to replace `[secret-name]` with the name of the target secret.
```
kubectl edit secrets [secret-name]
```
2. Modify the Secret resource and change the value of `qcloud_cert_id` to the new certificate ID.
Similar to the creation of a Secret, modifying a Secret certificate ID requires Base64 encoding. Select Base64 manual encoding or specify `stringData` to perform Base64 automatic encoding based on your actual needs.

### Updating Ingress objects
<dx-tabs>
::: Updating an Ingress object in the console
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the "Cluster management" page, click the cluster ID whose Ingress object needs to be modified.
3. On the cluster details page, select **Service and route** > **Ingress** in the left sidebar.
![](https://main.qcloudimg.com/raw/86707379f0cd64956ed64a29725787fc.png)
4. Find the target Ingress object, and click **Update forwarding configuration** in the "Operation" column.
5. On the "Update forwarding configuration" page, update the forwarding configuration rules as required.
6. Click **Update forwarding configuration** to complete the update.
:::
::: Updating an Ingress object by using YAML
Run the following command to open the Ingress object to be modified in the default editor. Modify the YAML file and save the modification.
```
kubectl edit ingress <ingressname> -n <namespaces>
```
:::
</dx-tabs>



