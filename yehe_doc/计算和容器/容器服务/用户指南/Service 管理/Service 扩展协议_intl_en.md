## Protocols Supported by Services by Default

 A Service is a mechanism and abstraction through which Kubernetes exposes applications outside the cluster. You can access the applications in a cluster through a Service.


<dx-alert infotype="notice" title="">
- For access in [direct access mode](https://intl.cloud.tencent.com/document/product/457/36837), there are no restrictions on the use of extension protocols, and TCP and UDP protocols can be used together.
- In non-direct access scenarios, `ClusterIP` and `NodePort` modes can be used together. However, the community has restrictions on Services of the `LoadBalance` type, and only protocols of the same type can be used currently.
- When `LoadBalance` is declared as TCP, the port can use the capabilities of extension protocols to change the protocol of CLB to TCP_SSL, HTTP, or HTTPS.
- When `LoadBalance` is declared as UDP, the port can use the capabilities of extension protocols to change the protocol of CLB to UDP.
</dx-alert>



## TKE Extension of Service Forwarding Protocols

In addition to the rules of the protocols supported by a native Service, a Service needs to support the hybrid use of TCP and UDP as well as the TCP SSL, HTTP, and HTTPS protocols in certain scenarios. TKE extends the support for more protocols in `LoadBalancer` mode.



### Prerequisites

- Extension protocols are only effective for Services in `LoadBalancer` mode.
- An extension protocol describes the relationship between the protocol and the port through an annotation.
- The relationship between the extension protocol and the annotation is as follows:
   - When the port described in `Service Spec` is not covered in the annotation of the extension protocol, `Service Spec` will be configured according to your declaration.
   - When the port described in the annotation of the extension protocol does not exist in `Service Spec`, the configuration will be ignored.
   - When the port described in the annotation of the extension protocol exists in `Service Spec`, the protocol configuration declared in `Service Spec` will be overwritten.



### Annotation name
`service.cloud.tencent.com/specify-protocol`

### Sample annotations of extension protocols


<dx-tabs>
::: Sample for TCP_SSL
<dx-codeblock>
::: xml 
{"80":{"protocol":["TCP_SSL"],"tls":"cert-secret"}}
:::
</dx-codeblock>
:::
::: Sample for HTTP
<dx-codeblock>
::: xml 
{"80":{"protocol":["HTTP"],"hosts":{"a.tencent.com":{},"b.tencent.com":{}}}}
:::
</dx-codeblock>
:::
::: Sample for HTTPS
<dx-codeblock>
::: xml 
 {"80":{"protocol":["HTTPS"],"hosts":{"a.tencent.com":{"tls":"cert-secret-a"},"b.tencent.com":{"tls":"cert-secret-b"}}}}
:::
</dx-codeblock>
:::
::: Sample for TCP/UDP
<dx-codeblock>
::: xml 
{"80":{"protocol":["TCP","UDP"]}} # Only supported in [direct access mode](https://intl.cloud.tencent.com/document/product/457/36837)
:::
</dx-codeblock>
:::
::: Sample for hybrid use
<dx-codeblock>
::: xml 
 {"80":{"protocol":["TCP_SSL","UDP"],"tls":"cert-secret"}} # Only supported in [direct access mode](https://intl.cloud.tencent.com/document/product/457/36837)
:::
</dx-codeblock>
:::
</dx-tabs>

>! The field `cert-secret` in TCP_SSL and HTTPS indicates that a certificate must be specified when you use the protocol. The certificate is an Opaque type Secret, the key of Secret is qcloud_cert_id, and the value is the certificate ID. For details, see [Ingress Certificate Configuration](https://intl.cloud.tencent.com/document/product/457/37016).


### Extension protocol use instructions
<dx-tabs>
::: Use instructions of extension protocol `YAML`
```yaml
apiVersion: v1
kind: Service
metadata:
    annotations:  
      service.cloud.tencent.com/specify-protocol: '{"80":{"protocol":["TCP_SSL"],"tls":"cert-secret"}}' # To use other protocols, change the value in the key-value pair to the above content
    name: test
   ....
```
:::
::: Use instructions of extension protocols in the console
- If you expose a Service in the form of "**public network CLB**" or "**private network CLB**" when creating it, in modes other than [direct access mode](https://intl.cloud.tencent.com/document/product/457/36837), only TCP and TCP SSL can be used together in **Port Mapping** as shown below:
![](https://main.qcloudimg.com/raw/1f9ff7c6ebcffd2cfb35404f9d1f728e.png)

- When the Service is in "**ClusterIP**" or "**NodePort**" mode, any protocols can be used together.
- If you are [using services with CLB-to-Pod direct access mode](https://intl.cloud.tencent.com/document/product/457/36837), hybrid use of any protocols is supported.
:::
</dx-tabs>

### Cases
A native Service does not support hybrid use of protocols. Upon some special modifications, TKE supports hybrid use of protocols in [CLB-to-Pod direct access mode](https://intl.cloud.tencent.com/document/product/457/36837).

Please note that the same protocol is used in YAML, but you can specify the protocol type for each port via the annotation. In the sample below, port 80 uses the TCP protocol, and port 8080 uses the UDP protocol.


```
apiVersion: v1
kind: Service
metadata:
  annotations:
      service.cloud.tencent.com/direct-access: "true"  # EKS clusters default to use the CLB-to-Pod direct access mode. For TKE clusters, you must enable the CLB-to-Pod direct access mode with reference to the document.
      service.cloud.tencent.com/specify-protocol: '{"80":{"protocol":["TCP"]},"8080":{"protocol":["UDP"]}}'   # It specifies that port 80 uses the TCP protocol, and port 8080 uses the UDP protocol.
  name: nginx
spec:
  externalTrafficPolicy: Cluster
  ports:
  - name: tcp-80-80
    nodePort: 32150
    port: 80
    protocol: TCP 
    targetPort: 80
  - name: udp-8080-8080
    nodePort: 31082
    port: 8080
    protocol: TCP # Note: Only the same type of protocols can be used because of the limits of Kubernetes Service Controller.
    targetPort: 8080 
  selector:
    k8s-app: nginx
    qcloud-app: nginx
  sessionAffinity: None
  type: LoadBalancer
```

