## Overview

As HTTPS becomes increasingly popular, most websites have begun to upgrade from HTTP to HTTPS. To use HTTPS, you need to apply for a certificate from an authority and pay a certain cost. The more certificates you apply for, the higher the cost will be. cert-manager is a powerful certificate management tool for Kubernetes. You can use cert-manager based on the [ACME](https://tools.ietf.org/html/rfc8555) protocol and [Let's Encrypt](https://letsencrypt.org/) to issue free certificates and have certificates automatically renewed. In this way, you can use certificates permanently for free.


## Principles
### How cert-manager works

After being deployed to a Kubernetes cluster, cert-manager queries custom CRD resources that it supports. You can create CRD resources to instruct cert-manager to issue certificates and automatically renew certificates, as shown in the figure below:
![](https://main.qcloudimg.com/raw/f4e57b54c56515446c86ba05e7bc8f6c.svg)
- **Issuer/ClusterIssuer**: indicates the method used by cert-manager to issue certificates. This document mainly describes the ACME method for issuing free certificates.
>? Issuer differs from ClusterIssuer in that Issuer can only be used to issue certificates under your own namespace, whereas ClusterIssuer can be used to issue certificates under any namespace.

- **Certificate**: is used to pass the domain name certificate information, the configuration required for issuing a certificate, and Issuer/ClusterIssuer references to cert-manager.

### Issuing a free certificate

Let’s Encrypt uses the ACME protocol to verify the ownership of a domain name. After successful verification, a free certificate is automatically issued. The free certificate is valid for only 90 days, so verification needs to be performed again to renew the certificate before the certificate expires. cert-manager supports automatic renewal of certificates, which allows you to use certificates permanently for free. You can verify the ownership of a certificate by using two methods: **HTTP-01** and **DNS-01**. For more information on the verification process, see [How It Works](https://letsencrypt.org/how-it-works/).
<dx-tabs>
::: HTTP-01 verification

HTTP-01 verification adds a temporary location for the HTTP service to which a domain name is directed. This method is only applicable to issuing a certificate for services that use open ingress traffic and does not support wildcard certificates.
For example, Let’s Encrypt sends an HTTP request to `http://<YOUR_DOMAIN>/.well-known/acme-challenge/<TOKEN>`. `YOUR_DOMAIN` indicates the domain name to be verified, and `TOKEN` indicates a file placed by the ACME client. In this case, the ACME client is cert-manager. You can modify or create ingress rules to add temporary verification paths and direct them to the service that provides `TOKEN`. Let’s Encrypt will then verify whether `TOKEN` meets the expectation. If the verification succeeds, a certificate is issued.
:::
::: DNS-01 verification

DNS-01 verification uses the API Key provided by DNS providers to obtain users’ DNS control permissions. This method does not require the use of an ingress and supports wildcard certificates.
After Let’s Encrypt provides a token to the ACME client, the ACME client `\(cert-manager\)` will create a TXT record derived from the token and the account key, and then place the record in `_acme-challenge.<YOUR_DOMAIN>`. Let’s Encrypt will then query the record in the DNS system. Once a matching item is found, a certificate is issued.
:::
</dx-tabs>
### Verification method comparison

The HTTP-01 methods features simple configuration and extensive applicability. Different DNS providers can use the same configuration method. The disadvantages of this method are that it relies on ingress resources, is applicable only to services that support open ingress traffic, and does not support wildcard certificates.
The advantages of DNS-01 are that it does not rely on ingress resources and supports wildcard domain names. Its disadvantages are that different DNS providers have different configuration methods, and cert-manager Issuer does not support too many different DNS providers. However, you can deploy the cert-manager-enabled [webhook](https://cert-manager.io/docs/concepts/webhook/) service to extend Issuer in order to support more DNS providers, such as DNSPod and Alibaba DNS. For more information on supported providers, see the [webhook list](https://cert-manager.io/docs/configuration/acme/dns01/#webhook). 
This document uses the recommended `DNS-01` method, which offers comprehensive features with few restrictions.

## Directions

### Installing cert-manager

Usually, you can use YAML to install cert-manager in your cluster with one click. For more information, see this document on the official website: [Installing with regular manifests](https://cert-manager.io/docs/installation/kubernetes/#installing-with-regular-manifests).
The official image used by cert-manager can be pulled from `quay.io`. Alternatively, you can run the following command to use the image synchronized to the mainland China CCR for one-click installation:
>! This method requires that the cluster version is 1.16 or later.
>
```
kubectl apply --validate=false -f https://raw.githubusercontent.com/TencentCloudContainerTeam/manifest/master/cert-manager/cert-manager.yaml
```



### Configuring DNS

Log in to a DNS provider backend system, configure the DNS A record of the domain name, and direct it to the opened IP address of the real server that needs the certificate. To do this, see the figure below, where Cloudflare is used as an example.
<img style="width:80%" src="https://main.qcloudimg.com/raw/c133190ee796d15fb56b54e6b2417dc6.png" data-nonescope="true">

### Issuing a certificate by using the HTTP-01 verification method

HTTP-01 validation can be performed by using Ingress. Cert-manager will automatically modify the Ingress or add an Ingress to expose the temporary HTTP path needed for validation. When HTTP-01 validation is configured for Issuer, if the `name` of an Ingress is specified, the specified Ingress will be modified to expose the HTTP path needed for validation. If `class` is specified, an Ingress will be added automatically. You can refer to the following [Example](#eg1).

Each ingress provided by TKE corresponds to a CLB. If you use an existing ingress provided by TKE to open services while using the HTTP-01 verification method, you can only adopt the automatic ingress modification mode, but not the automatic ingress addition mode. For automatically added ingresses, other CLBs will be automatically created, causing the opened IP address inconsistent with the ingress of the real server. In this case, Let's Encrypt fails to find the temporary path needed for verification in the service ingress, which results in verification failure and the failure to issue a certificate. If you use a user-created ingress, for example, by [deploying Nginx Ingress on TKE](https://intl.cloud.tencent.com/document/product/457/38072), and ingresses in the same ingress class share the same CLB, the automatic ingress addition mode is supported.



#### Example
If you use an ingress provided by TKE to open a service, you cannot use cert-manager to issue and manage free certificates. This is because certificates are referenced in [Certificate Management](https://console.cloud.tencent.com/ssl) and are not managed in Kubernetes.
If you [deploy Nginx Ingress on TKE](https://intl.cloud.tencent.com/document/product/457/38072) and the ingress of the real server is `prod/web`, you can create an Issuer by referring to the following sample code:
``` yaml
apiVersion: cert-manager.io/v1
kind: Issuer
metadata:
  name: letsencrypt-http01
  namespace: prod
spec:
  acme:
    server: https://acme-v02.api.letsencrypt.org/directory
    privateKeySecretRef:
      name: letsencrypt-http01-account-key
    solvers:
    - http01:
       ingress:
         name: web # Specifies the name of the ingress for automatic modification.
```
When you use an Issuer to issue a certificate, cert-manager will automatically create an ingress and automatically modify `prod/web` of the ingress to open the temporary path needed for verification. See the following sample code for automatic ingress addition:
``` yaml
apiVersion: cert-manager.io/v1
kind: Issuer
metadata:
  name: letsencrypt-http01
  namespace: prod
spec:
  acme:
    server: https://acme-v02.api.letsencrypt.org/directory
    privateKeySecretRef:
      name: letsencrypt-http01-account-key
    solvers:
    - http01:
       ingress:
         class: nginx # Specifies the ingress class of the automatically created ingress.
```

After successfully creating an Issuer, refer to the following sample code to create a certificate and reference the Issuer to issue the certificate:
``` yaml
apiVersion: cert-manager.io/v1
kind: Certificate
metadata:
  name: test-mydomain-com
  namespace: prod
spec:
  dnsNames:
  - test.mydomain.com # Indicates the domain name for issuing a certificate.
  issuerRef:
    kind: Issuer
    name: letsencrypt-http01 # References Issuer and indicates the HTTP-01 method is used for verification.
  secretName: test-mydomain-com-tls # The issued certificate will be saved in this Secret.
```

### Issuing a certificate by using the DNS-01 verification method

If you choose to use the DNS-01 verification method, you must select a DNS provider. cert-manager provides built-in support for DNS providers. For the detailed list and usage, see [Supported DNS01 providers](https://cert-manager.io/docs/configuration/acme/dns01/#supported-dns01-providers). If you need to use a DNS provider other than those on the list, refer to the following two schemes:
<dx-tabs>
::: Scheme 1: Configuring a custom nameserver
On the backend system of the DNS provider, configure a custom nameserver and direct it to the address of a nameserver that can manage other DNS providers’ domain names, such as Cloudflare. You can log in to the backend of Cloudflare to view the specific address, as shown in the figure below:
<img style="width:80%" src="https://main.qcloudimg.com/raw/9e07f843cae3ff5123442e7dc5b024d0.png" data-nonescope="true">
You can configure a custom nameserver for namecheap, as shown in the figure below:
<img style="width:80%" src="https://main.qcloudimg.com/raw/1ad9889154d2b4125cef8a41de26d413.png" data-nonescope="true">
Finally, when configuring the Issuer and specifying the DNS-01 verification method, add the Cloudflare information.
:::
::: Scheme 2: Using webhooks
You can use the cert-manager webhook to extend the list of DNS providers supported in cert-manager DNS-01 verification. This scheme has been implemented for many third parties, such as DNSPod and Alibaba DNS, that are widely used in mainland China. For more information on the webhook list and its usage, see [Webhook](https://cert-manager.io/docs/configuration/acme/dns01/#webhook).

#### Example
Complete the following steps to issue a certificate for Cloudflare:
1. Log in to Cloudflare and create a token, as shown in the figure below:
<img style="width:80%" src="https://main.qcloudimg.com/raw/4c18b4884f3ec7c5f57aa53e9fbffe9f.png" data-nonescope="true">
2. Copy the token and save it to the Secret. The sample YAML file is as follows:
>!
>- If you need to create a ClusterIssuer, create the Secret in the namespace to which cert-manager belongs.
>- If you need to create an Issuer, create the Secret in the namespace to which the Issuer belongs.
>
<dx-codeblock>
::: yaml
   apiVersion: v1
   kind: Secret
   metadata:
     name: cloudflare-api-token-secret
     namespace: cert-manager
   type: Opaque
   stringData:
     api-token: <API Token> # Paste the token here without Base64 encryption.
:::
</dx-codeblock>
3.Create a ClusterIssuer. The following shows a sample YAML file:
<dx-codeblock>
::: yaml
   apiVersion: cert-manager.io/v1
   kind: ClusterIssuer
   metadata:
     name: letsencrypt-dns01
   spec:
     acme:
       privateKeySecretRef:
         name: letsencrypt-dns01
       server: https://acme-v02.api.letsencrypt.org/directory
       solvers:
       - dns01:
           cloudflare:
             email: my-cloudflare-acc@example.com # Replace it with your Cloudflare email account. API token authentication is optional, but API key authentication is required.
             apiTokenSecretRef:
               key: api-token
               name: cloudflare-api-token-secret # References the Secret that stores the Cloudflare authentication information.
:::
</dx-codeblock>
4. <span id="Certificate"></span>Create a Certificate. The following shows a sample YAML file:
<dx-codeblock>
::: yaml
   apiVersion: cert-manager.io/v1
   kind: Certificate
   metadata:
     name: test-mydomain-com
     namespace: default
   spec:
     dnsNames:
     - test.mydomain.com # Indicates the domain name for issuing a certificate.
     issuerRef:
       kind: ClusterIssuer
       name: letsencrypt-dns01 # References ClusterIssuer and indicates that the DNS-01 method is used for verification.
     secretName: test-mydomain-com-tls # The issued certificate will be stored in this Secret.
:::
</dx-codeblock>
:::
</dx-tabs>

### Obtaining and using certificates

After [creating a certificate](#Certificate), you can run the kubectl command to check whether the certificate has been issued successfully.
```
$ kubectl get certificate -n prod
NAME                READY   SECRET                  AGE
test-mydomain-com   True    test-mydomain-com-tls   1m
```
- `READY` = `False`: indicates that the certificate failed to be issued. You can run the `describe` command to check the event and analyze the failure cause.
```
$ kubectl describe certificate test-mydomain-com -n prod
```
- `READY` = `True`: indicates that the certificate was issued successfully. In this case, the certificate will be stored in the specified Secret, for example, `default/test-mydomain-com-tls`. You can run kubectl to view the certificate, where `tls.crt` indicates the certificate, and `tls.key` indicates the key.
```
$ kubectl get secret test-mydomain-com-tls -n default
...
data:
  tls.crt: <cert>
  tls.key: <private key>
```

You can mount the certificate to the app that needs it or directly reference the Secret in an ingress that you created. The following shows a sample YAML file:
``` yaml
apiVersion: networking.k8s.io/v1beta1
kind: Ingress
metadata:
  name: test-ingress
  annotations:
    kubernetes.io/Ingress.class: nginx
spec:
  rules:
  - host: test.mydomain.com
    http:
      paths:
      - path: /web
        backend:
          serviceName: web
          servicePort: 80
  tls:
    hosts:
    - test.mydomain.com
    secretName: test-mydomain-com-tls
```

## References

- [cert-manager official website](https://cert-manager.io/)
- [How It Works](https://letsencrypt.org/how-it-works/)
- [API reference docs](https://cert-manager.io/docs/reference/api-docs/#cert-manager.io/v1.Issuer)
- [Certificate](https://cert-manager.io/docs/reference/api-docs/#cert-manager.io/v1.Certificate)
