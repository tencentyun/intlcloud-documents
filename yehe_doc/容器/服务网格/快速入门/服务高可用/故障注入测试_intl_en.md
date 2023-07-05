
 ## Overview
 This document simulates website system behaviors upon latency faults when the stock service is accessed, aiming to test the service elasticity and optimize the access experience of website users.
The stock service has a fixed latency of seven seconds as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/6283511dd5b2b814053793048f4dd770.png)

## Directions

Configure the `VirtualService` bound to the stock service and set the fault injection policy for accessing the stock service: 100% of the requests will have a fixed latency of seven seconds.

```yaml
apiVersion: networking.istio.io/v1alpha3
kind: VirtualService
metadata:
  name: stock-vs
  namespace: base
spec:
  hosts:
    - stock.base.svc.cluster.local
  http:
    - route:
        - destination:
            host: stock.base.svc.cluster.local
      fault:
        delay:
          fixedDelay: 7000ms
          percentage:
            value: 100
```

After the configuration, click **ADD TO CART** on the demo website page to add an item to the cart or click **YOUR CART** to call the cart service. The cart service will then call the stock service to query the stock, and the stock service will experience a fixed latency of seven seconds. Click **CHECKOUT** on the cart page to start the checkout process to call the order service. The order service will then call the stock service to query the stock, and the stock service will experience a fixed latency of seven seconds. The latency means that the page will be in the loading status for seven seconds until the fault disappears, which adversely affects users' browsing experience.
The waiting status after the cart service calls the stock service is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/47f29ac5c16d0fa3fc3cc5334d8f04c6.png)

A timeout period can be configured to optimize the browsing experience of website users.