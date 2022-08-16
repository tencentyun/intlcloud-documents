

## Overview
This document describes the feature of deducting the freight with member points designed to win over more members for an ecommerce website. The currently deployed order service provided by Deployment v1 does not support this feature, while the newly developed v2 of the order service does. Ideally, traffic is routed based on the cookies in the header; if a user is a member of the website as indicated in the cookies, traffic will be routed to order v2 (with freight deduction); otherwise, traffic will be routed to order v1 (without freight deduction).
An overview of multi-version service routing is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/32b7be8c38eb80546687b43ea3a1cf23.png)

## Directions
Submit the following YAML file to the primary cluster to deploy order v2 to the cluster.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: order-v2
  namespace: base
  labels:
    app: order
    version: v2
spec:
  replicas: 1
  selector:
    matchLabels:
      app: order
      version: v2
  template:
    metadata:
      labels:
        app: order
        version: v2
    spec:
      containers:
        - name: order
          image: ccr.ccs.tencentyun.com/zhulei/testorder2:v1
          imagePullPolicy: Always
          env:
            - name: POD_NAME
              valueFrom:
                fieldRef:
                  fieldPath: metadata.name
            - name: REGION
              value: "guangzhou-zoneA"
          ports:
            - containerPort: 7000
              protocol: TCP
```

After the deployment, as no routing rule is configured, traffic to the order service will be randomly routed to v1 or v2 as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/5a17c0d1ab6ec49522b314e2198fd828.png) 

To configure a routing rule based on traffic characteristics, define the two versions of the order service through `DestinationRule` as shown below:

Define the versions of the order service as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/d364db7456a8b5a57e37471042ca4762.png)

The versions of the order service are as defined below:
![](https://qcloudimg.tencent-cloud.cn/raw/c3f90333dd5d575779c8dffbad8723c3.png)


Or you can submit the following YAML file to the primary cluster to create a destination rule:

```yaml
apiVersion: networking.istio.io/v1alpha3
kind: DestinationRule
metadata:
  name: order
  namespace: base
spec:
  host: order
  subsets:
    - name: v1
      labels:
        version: v1
    - name: v2
      labels:
        version: v2
  exportTo:
    - '*'
```

After the two versions are defined, routing will be performed based on traffic characteristics through the `VirtualService` definition. If the `header-cookie` of a request contains `vip=false`, traffic will be routed to v1 subset of the order service; otherwise, traffic will be routed to v2 subset. That is, member requests and non-member requests will be routed to order v2 and order v1, respectively. This configuration can be performed by submitting the following YAML file to the primary cluster.



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
    - match:
        - headers:
            cookie:
              exact: vip=true
      route:
        - destination:
            host: order.base.svc.cluster.local
            subset: v2
```

After the configuration, if you log in to a member account (ID: 1–3), add an item to the cart, and make the payment, you will find that the freight is deducted, and the traffic is routed to order v2; if you log in to a non-member account (ID: 4–5), add an item to the cart, and make the payment, you will find that the freight is not deducted, and according to the `VIP` field in the header, the traffic is routed to the originally deployed order v1. Version information can be viewed in the floating window in the bottom-left corner.
The request from a member is routed to v2 as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/3dbecdb8e7c511688e961112ce25c53c.png)

The request from a non-member user is routed to v1 as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/ac7204f19e7708f77d8bdefe7248b4be.png)

Routing based on traffic rules is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/32b7be8c38eb80546687b43ea3a1cf23.png)

