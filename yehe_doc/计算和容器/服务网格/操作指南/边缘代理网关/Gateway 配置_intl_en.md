

Ports and monitoring rules of a gateway are configured by using a gateway CRD. The following is a gateway configuration example, with major fields being explained by comments:

```yaml
apiVersion: networking.istio.io/v1alpha3
kind: Gateway
metadata:
  name: gateway-sample
  namespace: default
spec:
  selector: # Match pods delivered by the gateway configurations based on the entered labels.
    istio: ingressgateway
    app: istio-ingressgateway
  servers:
  - port:
      number: 80
      name: http
      protocol: HTTP
    hosts:
    - uk.bookinfo.com
    - eu.bookinfo.com
    tls:
      httpsRedirect: true # Send a 301 https redirect.
  - port:
      number: 443
      name: https-443
      protocol: HTTPS # Enable HTTPS ports.
    hosts:
    - uk.bookinfo.com
    - eu.bookinfo.com
    tls:
      mode: SIMPLE # TLS one-way authentication
      serverCertificate: /etc/certs/servercert.pem # Load the certificate in the file mount manner.
      privateKey: /etc/certs/privatekey.pem
  - port:
      number: 9443
      name: https-9443
      protocol: HTTPS # Enable HTTPS ports.
    hosts:
    - "bookinfo-namespace/*.bookinfo.com"
    tls:
      mode: SIMPLE # TLS one-way authentication
      credentialName: bookinfo-secret # Load the certificate from the Kubernetes secret in the SDS manner.
  - port:
      number: 5443
      name: https-ssl
      protocol: HTTPS # Enable HTTPS ports.
    hosts:
    - "*"
    tls:
      mode: SIMPLE # TLS one-way authentication
      credentialName: qcloud-abcdABCD # Load the certificate with the certificate ID of abcdABCD from the Tencent Cloud SSL Certificate Service console in the SDS manner.
  - port:
      number: 6443
      name: clb-https-6443-ABCDabcd # Have certificate offloading on port 6443 to take place at CLB, where the certificate is the SSL certificate with ID of ABCDabcd.
      protocol: HTTP
    hosts:
    - "tcm.tencent.com"

```

## Gateway Configuration Field Description

Major fields of the gateway CRD are described as follows.

| Name | Type | Description |
| ----- | ---- | ----- |
| `metadata.name` | `string` | Gateway name. | 
| `metadata.namespace` | `string` | Gateway namespace. | 
| `spec.selector` | `map<string, string>` | Label key-value pair used by the gateway to match the gateway instances delivered by the configurations. |
| `spec.servers.port.number` | `uint32` | Port number. |
| `spec.servers.port.protocol` | `string` | Communication protocol. The following protocols are supported: `HTTP, HTTPS, GRPC, HTTP2, MONGO, TCP, TLS`. Note that the protocol configurations of the same port on the same gateway need to be consistent. |
| `spec.servers.port.name` | `string` | Port name. Currently, Tencent Cloud Mesh implements the feature of enabling SSL certificate offloading to take place at CLB based on the port name. If you need to configure this feature, you can set the port name in the format of `clb-https-{port number}-{SSL certificate ID}`. This feature takes effect only when the current port communication protocol is set to **HTTP**. The gateway controller automatically creates a CLB layer-7 listener to implement certificate offloading. After SSL offloading is completed at CLB, the CLB instance and the ingress gateway pod adopt plaintext communication. Note that the certificate offloading configurations of the same port on the same gateway need to be consistent; otherwise, a configuration conflict occurs. |
| `spec.severs.hosts` | `string[]` | Domain name, which supports wildcard `*`. |
| `spec.servers.tls.httpsRedirect` | `bool` | When the value is `true`, the gateway returns a 301 redirect to all HTTP requests, requiring the client to initiate an HTTPS request. |
| `spec.servers.tls.mode` | - | TLS security authentication mode of the current port. Specify this field if you need to enable security authentication of the current port. The following values are supported: `PASSTHROUGH, SIMPLE, MUTUAL, AUTO_PASSTHROUGH, ISTIO_MUTUAL`. |
| `spec.servers.tls.credentialName` | `string` | Name of the secret from which the TLS certificate key is found. Tencent Cloud Mesh supports loading the certificate and key from the Kubernetes secret in the same namespace of the ingress gateway instance. Ensure that the secret you entered contains the appropriate certificate and key. Tencent Cloud Mesh also implements the feature of loading a Tencent Cloud SSL certificate. If you specify this field in the format of `qcloud-{SSL certificate ID}`, the gateway controller of Tencent Cloud Mesh will load the SSL certificate for the gateway. Currently, Tencent Cloud Mesh supports loading only server certificates and private keys in SIMPLE mode (one-way authentication) from the SSL Certificate Service console. |
| `spec.servers.tls.serverCertificate` | `string` | Certificate path that needs to be entered when the TLS certificate key of the port is mounted in the file mount manner (not recommended; it is recommended that you enter the `credentialName` field to load the certificate private key). By default, Istio uses the istio-ingressgateway-certs secret in the namespace where the gateway locates to load the certificate to the path `/etc/istio/ingressgateway-certs`. |
| `spec.servers.tls.privateKey ` | `string` | Private key path that needs to be entered when the TLS certificate key of the port is mounted in the file mount manner (not recommended; it is recommended that you enter the `credentialName` field to load the certificate private key). By default, Istio uses the istio-ingressgateway-certs secret in the namespace where the gateway locates to load the private key to the path `/etc/istio/ingressgateway-certs`. |
| `spec.servers.tls.caCertificates` | `string` | Root certificate path that needs to be entered when the TLS certificate key of the port is mounted in the file mount manner (not recommended; it is recommended that you enter the `credentialName` field to load the certificate private key). By default, Istio uses the istio-ingressgateway-ca-certs secret in the namespace where the gateway locates to load the root certificate to the path `/etc/istio/ingressgateway-ca-certs`. A root certificate needs to be configured in mutual authentication. |


## Examples

#### A configuration example for loading a certificate from a Kubernetes secret to an ingress gateway

<dx-tabs>
::: YAML Configuration Example
```yaml
apiVersion: networking.istio.io/v1alpha3
kind: Gateway
metadata:
  name: sample-gw
  namespace: default
spec:
  servers:
    - port:
        number: 443
        name: HTTPS-443-6cph
        protocol: HTTPS
      hosts:
        - '*'
      tls:
        mode: SIMPLE
        credentialName: {kubernetes secret name}
  selector:
    app: istio-ingressgateway
    istio: ingressgateway
```
:::
::: Console Configuration Example
The process of creating gateway configurations in the console to load an HTTPS-based SSL certificate of an ingress gateway from a Kubernetes secret (one-way authentication) is as follows:

1. Select protocol **HTTPS** and **SIMPLE** for **TLS authentication**.
2. Select **Terminate at ingress gateway** for **Offload mode**.
3. Select **SDS loading** for **Certificate mount mode**.
4. Select **K8S secret** for **Certificate source**.
5. Select **Select existing** for **K8S secret**, and select the secret in the namespace where the selected ingress gateway locates. Ensure that the secret contains the appropriate certificate, private key, and root certificate.
![](https://qcloudimg.tencent-cloud.cn/raw/32cdf66ed5392300880cc8fb9c38876e.png)
6. If the secret does not contain any appropriate certificate, select **Create** for **K8S secret** and copy appropriate certificate, private key, and root certificate content to corresponding input boxes.
![](https://qcloudimg.tencent-cloud.cn/raw/860bcac8f603e5abcc49b4adb8dc7162.png)
:::
</dx-tabs>



#### A configuration example for loading a certificate from the SSL Certificate Service console to an ingress gateway

<dx-tabs>
::: YAML Configuration Example
```yaml
apiVersion: networking.istio.io/v1alpha3
kind: Gateway
metadata:
  name: test-gw
spec:
  servers:
    - port:
        number: 443
        name: HTTPS-443-9ufr
        protocol: HTTPS
      hosts:
        - '*'
      tls:
        mode: SIMPLE
        credentialName: qcloud-{Certificate ID}
  selector:
    app: istio-ingressgateway
    istio: ingressgateway
```
:::
::: Console Configuration Example
In addition to configuring a gateway by using a YAML file, you can also create gateway configurations by using UI in the console. The following is a configuration example for loading a certificate from the SSL Certificate Service console to an ingress gateway. You can select the SSL certificate to be loaded by selecting **SSL certificate** for **Certificate source**.

 ![](https://qcloudimg.tencent-cloud.cn/raw/653233096b0d8da11a96522aa9a8464d.png)

:::
</dx-tabs>





#### A configuration example for SSL certificate offloading to take place at CLB

<dx-tabs>
::: YAML Configuration Example
In the following example, certificate offloading on port 443 is configured to take place at CLB, SNI is enabled for this port, the domain name `sample.hosta.org` uses certificate 1, and the domain name `sample.hostb.org` uses certificate 2.
```yaml
apiVersion: networking.istio.io/v1alpha3
kind: Gateway
metadata:
  name: test-gw
spec:
  servers:
    - port:
        number: 443
        name: clb-https-443-{Certificate ID 1}
        protocol: HTTP
      hosts:
        - sample.hosta.org
    - port:
        number: 443
        name: clb-https-443-{Certificate ID 2} 
        protocol: HTTP
      hosts:
        - sample.hostb.org
  selector:
    app: istio-ingressgateway
    istio: ingressgateway
```
:::
::: Console Configuration Example
The process of creating gateway configurations by using UI in the console to implement the feature of enabling certificate offloading to take place at CLB is as follows:

1. Select protocol **HTTPS**. The **TLS authentication** parameter appears.
2. Select **SIMPLE** for **TLS authentication**.
3. Select **Terminate at CLB** for **Offload mode**. The port protocol is automatically changed to **HTTP** (if certificate offloading takes place at CLB, all traffic will be passed to the gateway in plaintext).
4. Select an appropriate server certificate. 

![](https://qcloudimg.tencent-cloud.cn/raw/46e23c1bd470e98c82e34caf68ee0545.png)

After creation is successful, you are redirected to the details page of the created gateway CRD.

![](https://qcloudimg.tencent-cloud.cn/raw/f1bd9bf2dc9d14337c7dec92e9d3bf75.png)
:::
</dx-tabs>
