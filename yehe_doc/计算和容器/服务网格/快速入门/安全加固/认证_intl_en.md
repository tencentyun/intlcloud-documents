
 ## Overview
 This document describes how to implement mutual authentication of mTLS for all service accesses in the production environment (base namespace) to prevent man-in-the-middle attacks.



## Directions
The mTLS mode defaults to `PERMISSIVE`, that is, both mTLS encryption and plaintext connection can be used for service communications.

Log in to the `istio-proxy` container in the TKE console and use plaintext connection to send the `curl http://product.base.svc.cluster.local:7000/product` request to the product service in the production environment (base namespace). In this case, the product service can be accessed via plaintext connection, as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/776aceac62e3397d540a99eb35d03263.png)
 The access via plaintext connection is successful as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/ea61666f0d85828fc8c60b951fd4be52.png)


Implement the mTLS mode for service communications in the base namespace by setting the mTLS mode to `STRICT` in the `PeerAuthentication` policy:
![](https://qcloudimg.tencent-cloud.cn/raw/7bd569e3daede39b9c93899e9cbcb877.png)


Or submit the following YAML file to the primary cluster via kubectl:

```yaml
apiVersion: security.istio.io/v1beta1
kind: PeerAuthentication
metadata:
  name: base-strict
  namespace: base
spec:
  mtls:
    mode: STRICT
```

After the configuration, log in to the `istio-proxy` container in the TKE console and use plaintext connection to send the `curl http://product.base.svc.cluster.local:7000/product` request to the product service in the production environment (base namespace). In this case, the product service cannot be accessed via plaintext connection, as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/eb07dba5ba6157783141e09a66e4fc6e.png)