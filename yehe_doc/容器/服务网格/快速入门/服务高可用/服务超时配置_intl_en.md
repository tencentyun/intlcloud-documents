 ## Overview

The order service has a timeout period of three seconds as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/572ef6bf104b3d9d09abc5e995777663.png)


 After fault injection is configured for the stock service, it is found that user requests to the website will be in the waiting status due to the fault. To optimize the browsing experience, a timeout period needs to be configured.


## Directions
Configure a timeout period of three seconds for the order service by applying the following `VirtualService` and no timeout period for the cart service.

```yaml
apiVersion: networking.istio.io/v1alpha3
kind: VirtualService
metadata:
  name: order-vs
  namespace: base
spec:
  hosts:
    - order.base.svc.cluster.local
  http:
    - match:
        - headers:
            cookie:
              exact: vip=false
      route:
        - destination:
            host: order.base.svc.cluster.local
            subset: v1
      timeout: 3000ms
    - match:
        - headers:
            cookie:
              exact: vip=true
      route:
        - destination:
            host: order.base.svc.cluster.local
            subset: v2
      timeout: 3000ms
```

After the configuration, add an item to the cart, and the cart service will experience an access latency of seven seconds due to the injected fault, without a timeout. Then, click **CHECKOUT** to start the checkout process and call the order service, and, in addition to the access latency of seven seconds, the order service will experience a timeout period of three seconds, which means a timeout will occur if no operation is performed within three seconds after the order service is called.
The timeout occurring when the cart service calls the order service is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/7d255c7b0ad89e371f93c912ba1ac5c5.png)


After completing the timeout configuration and the fault injection test on the service, delete the `VirtualService` resource associated with the stock service to disassociate the configured fault injection policy from the stock service.

Delete the `VirtualService` associated with the stock service as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/c12435ad08d2433ac019f1a10fc2d9c8.png)