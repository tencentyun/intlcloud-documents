 
 ## Overview
 The cart service has multiple running Pods, requiring the session persistence feature to ensure that requests from the same user are routed to the same Pod and the user's cart information will not be lost.
Session persistence is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/4379400bd7fa29e6e1e66f5eebf4bb3e.svg)
 

 ## Directions
Implement the session persistence feature by setting the `DestinationRule` loading balancing policy of the cart service, with `UserID` in the request header for consistent hashing.

```yaml
apiVersion: networking.istio.io/v1alpha3
kind: DestinationRule
metadata:
  name: cart
  namespace: base
spec:
  host: cart
  trafficPolicy:
    loadBalancer:
      consistentHash:
        httpHeaderName: UserID
  exportTo:
    - '*'
```

After the configuration, click **YOUR CART** multiple times or **ADD TO CART** after login to call the cart service to verify whether requests from the same user are routed to the same Pod. The name of the Pod providing the cart service can be viewed in the bottom-left floating window, which is the same for requests from the same user. Requests from the same user are load balanced to the same Pod as shown below:

![](https://qcloudimg.tencent-cloud.cn/raw/28235220c55b260dc436c143ef9a3f97.png)
 
