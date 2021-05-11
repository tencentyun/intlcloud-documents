## Protocols Supported by Service by Default

 Service is a mechanism and abstraction through which Kubernetes opens apps to traffic outside clusters. You can access apps in a cluster via Service.

By default, Service supports the following protocols:
- In Cluster IP and NodePort modes, the TCP and UDP protocols are supported and can be used together.
- In LoadBalancer mode, the TCP and UDP protocols are supported, but cannot be used together.



## TKE Extension of Service Forwarding Protocols

Based on the rules of the protocols supported by native Service, there are some scenarios where Service must support the mixed use of TCP and UDP as well as TCP SSL, HTTP, and HTTPS protocols. TKE extends support for more protocols in LoadBalancer mode.



### Prerequisite Notes

- Extension protocols are only effective for Service in LoadBalancer mode.
- Extension protocols describe the relationships between protocols and ports through annotations.
- The relationships between protocols and annotations are as follows:
   - When the extension protocol annotation does not cover the port described in Service Spec, Service Spec is configured according to the user description.
   - When the port described in the extension protocol annotation does not exist in Service Spec, the configuration is ignored.
   - When the port described in the extension protocol annotation exists in Service Spec, the protocol configuration that users state in Service Spec will be overwritten.




### Extension protocol usage instructions

```yaml
apiVersion: v1
kind: Service
metadata:
    annotations:  
      service.cloud.tencent.com/specify-protocol: {"80":{"protocol":["TCP_SSL"],"tls":"cert-secret"}}
    name: test
   ....
```

- **Annotation name:**: `service.cloud.tencent.com/specify-protocol`
- Extension protocol annotation samples:
#### TCP SSL sample
```
{"80":{"protocol":["TCP_SSL"],"tls":"cert-secret"}}
```
#### HTTP sample
```
{"80":{"protocol":["HTTP"],"hosts":{"[a.tencent.com](http://a.tencent.com/)":{},"[b.tencent.com](http://b.tencent.com/)":{}}}}
```
#### HTTPS sample
```
 {"80":{"protocol":["HTTPS"],"hosts":{"[a.tencent.com](http://a.tencent.com/)":{"tls":"cert-secret-a"},"[b.tencent.com](http://b.tencent.com/)":{"tls":"cert-secret-b"}}}}
```
#### TCP/UDP mixed-use sample
```
{"80":{"protocol":["TCP","UDP"]}}
```
#### Mixed-use sample
```
 {"80":{"protocol":["TCP_SSL","UDP"],"tls":"cert-secret"}}
```


