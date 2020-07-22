## Scenario
This document describes how to configure Ingress certificates. You can configure them in the following scenarios:
- When you select the HTTPS listening protocol in creating an Ingress, select an appropriate server certificate to ensure access security.
- Bind the same certificate for all HTTPS domain names to simplify the certificate configuration for all HTTPS rules under the Ingress. This facilitates future certificate updates.
- Bind different certificates for different domain names to improve SSL/TLS performance between the server and clients.

## Notes
- You need to create the certificate to be configured in advance. For more information, see [Creating a server certificate in the console](#create).
- You need to configure the Ingress certificate by using Secret. By default, the TKE Ingress will create a Secret with the same name, which contains the ID of the certificate.
- The Secret certificate resource must reside in the same namespace as the Ingress resource.
- When you create an Ingress, a Secret certificate resource with the same name will be created in the console by default. If the Secret resource name already exists, the Ingress cannot be created.
- In normal cases, the certificate resource associated with a Secret is not reused when an Ingress is created. However, this resource can be reused. When a Secret is updated, the certificates of all Ingresses that reference this Secret are updated synchronously.
- After the matching certificate is added for a domain name, the CLB SNI feature is enabled (and cannot be disabled) at the same time. If the domain name corresponding to a certificate is deleted, the certificate will be matched to the HTTPS domain name corresponding to the Ingress by default.
- Classic CLB instances do not support domain-name-based or URL-based forwarding. Therefore, an Ingress created by a classic CLB instance does not support the configuration of multiple certificates.




## Examples
TKE allows you to configure a certificate for the CLB HTTPS listener created by an Ingress by using the `spec.tls` field of the Ingress. In the following example, `secretName` specifies a Kubernetes Secret resource containing the certificate ID.
- **Ingress**
```yaml
spec:
    tls:
    - hosts:
      - www.abc.com
      secretName: secret-tls-2
```
- **Sercret**
```yaml
apiVersion: v1
stringData:
    qcloud_cert_id: Xxxxxxxx ## Set the certificate ID to Xxxxxxxx
kind: Secret
metadata:
    name: tencent-com-cert
    namespace: default
type: Opaque
```
>? You can also create a Secret in the TKE console. For more information, see [Creating a Secret](https://intl.cloud.tencent.com/document/product/457/30676).


## Ingress Certificate Configuration
- If a `spec.secretName` is configured with no `hosts` specified, the certificate is configured for all HTTPS forwarding rules. The following is an example.
```yaml
spec:
    tls:
    - secretName: secret-tls
```
- Unified configuration of first-level wildcard certificates is supported. The following is an example.
```yaml
spec:
    tls: 
    - hosts:
      - *.abc.com
      secretName: secret-tls
```
- If both the certificate and wildcard certificate are configured, the certificate is preferred. In the following example, `www.abc.com` will use the certificate specified in `secret-tls-2`.
```yaml
spec:
    tls: 
    - hosts:
      - *.abc.com
      secretName: secret-tls-1
    - hosts:
      - www.abc.com
      secretName: secret-tls-2
```
- When updating an Ingress with multiple certificates, the TKE Ingress controller runs the following checks:
   - When rules.host of HTTPS has no matches, the update cannot be submitted.
   - When rules.host of HTTPS matches a single TLS, the update can be submitted, and the corresponding certificate in Secret can be configured for the host.
   - When you modify `SecretName` of TLS, the system verifies only the existence of `SecretName`, but not the content of Secret. The update can be submitted if the Secret exists.
   > ! Ensure that the certificate ID in Secret meets requirements.





## Directions
<span id="create"></span>

### Creating a server certificate in the console
>? Skip this procedure if you already have the certificate to be configured.
>
1. Log in to the CLB console and click **[Certificate Management](https://console.cloud.tencent.com/clb/cert)** in the left sidebar.
2. On the "Certificate Management" page, click **Create**.
3. In the "Create a new certificate" window that appears, set the parameters as follows:
 - **Certificate Name**: define a custom name.
 - **Certificate Type**: select **Server Certificate**.
- **Server Certificate**: a server certificate is an SSL certificate. With an SSL certificate, you can switch the site from HTTP to HTTPS, which is an encrypted HTTP protocol for secure data transmission based on SSL.
   - **Certificate Content**: specify the content of the certificate as appropriate. For more information on the format, see [SSL Certificate Format Requirements and Format Conversion Instructions](https://intl.cloud.tencent.com/document/product/214/5369).
   - **Key Content**: this parameter is displayed only when the certificate type is **Server Certificate**. For more information on how to add the related key content, see [SSL Certificate Format Requirements and Format Conversion Instructions](https://intl.cloud.tencent.com/document/product/214/5369).
4. Click **Submit** to complete the configuration.

### Creating an Ingress object
For more information on how to create an Ingress, see [Creating an Ingress](https://intl.cloud.tencent.com/document/product/457/30673). Set the listening port to **Https:443**.

>!
>
>- When the HTTPS service is enabled for an Ingress created in the console, a Secret resource with the same name will be created to store the certificate ID. Then, this Secret is used and listened to in the Ingress.
- The mapping between domain names and certificates in TLS is as follows:
 - You can use first-level wildcard certificates for unified domain name configuration.
 - If a domain name matches multiple certificates, one of the certificates will be selected at random. However, it is not recommended that you use multiple certificates for one domain name.
 - You need to configure certificates for all HTTPS domain names. Otherwise, the Ingress cannot be created.


### Modifying a certificate
>! 
>- To modify a certificate, confirm all Ingresses that use this certificate. If multiple Ingresses use the same Secret resource, the certificates of the CLB instances corresponding to these Ingresses will be modified synchronously.
>- To modify a certificate, you need to modify the Secret, which contains the ID of the used Tencent Cloud certificate.
>
1. Run the following command to open the Secret to modify by using the default editor. Note that you must replace `[secret-name]` with the name of the Secret to modify.
```
kubectl edit secrets [secret-name]
```
2. Modify the Secret resource. Change the value of `qcloud_cert_id` to the new certificate ID.
Similar to creating a Secret, changing the certificate ID in a Secret requires Base64 encoding. To do this, select manual Base64 encoding or specify `stringData` to enable automatic Base64 encoding as needed.

### Updating an Ingress object

#### Updating an Ingress object in the console
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the **Cluster Management** page, select the cluster ID of the Ingress to update.
3. On the cluster details page, choose **Services and Routes** > **Ingress**, as shown in the following figure.
![](https://main.qcloudimg.com/raw/86707379f0cd64956ed64a29725787fc.png)
4. Locate the target Ingress and click the **Update Forwarding Configuration** button for this Ingress.
5. On the **Update Forwarding Configuration** page, update the forwarding configuration rules as needed.
6. Click **Update Forwarding Configuration** to complete the update.

#### Updating an Ingress object by editing the YAML file
Run the following command to open the Ingress to modify by using the default editor, modify the YAML file, and save the configuration to complete the update.
```
kubectl edit ingress <ingressname> -n <namespaces>
```


