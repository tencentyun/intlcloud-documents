## Overview
Website traffic increase brings along the need to place ads on the product page. Therefore, website developers developed the product v2 as a Deployment and wish to perform a canary release.
An overview of the canary release is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/976ac6f314e83fb8c553dee2ea2e7f57.png)

 ## Directions


Deploy the product v2 Deployment to the primary cluster first:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: product-v2
  namespace: base
  labels:
    app: product
    version: v2
spec:
  replicas: 1
  selector:
    matchLabels:
      app: product
      version: v2
  template:
    metadata:
      labels:
        app: product
        version: v2
    spec:
      containers:
        - name: product
          image: ccr.ccs.tencentyun.com/zhulei/testproduct2:v1
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
```

In the first step, define the service version through disaster recovery and the weighted routing through `VirtualService`. Route 50% of the traffic to the product v2 subset for verification and the other 50% to product v1. This can be configured by submitting the following YAML file to the primary cluster.

```yaml
apiVersion: networking.istio.io/v1alpha3
kind: VirtualService
metadata:
  name: product-vs
  namespace: base
spec:
  hosts:
    - "product.base.svc.cluster.local"
  http:
    - match:
        - uri:
            exact: /product
      route:
        - destination:
            host: product.base.svc.cluster.local
            subset: v1
            port:
              number: 7000
          weight: 50
        - destination:
            host: product.base.svc.cluster.local
            subset: v2
            port:
              number: 7000
          weight: 50
---

apiVersion: networking.istio.io/v1alpha3
kind: DestinationRule
metadata:
  name: product
  namespace: base
spec:
  host: product
  subsets:
    - name: v1
      labels:
        version: v1
    - name: v2
      labels:
        version: v2
```

After the configuration, 50% of the traffic to the product service will be routed to product v1 and the other 50% to product v2. Refresh the product page for verification.

The weighted routing is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/976ac6f314e83fb8c553dee2ea2e7f57.png)

50% of the request traffic is routed to product v2 as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/9e4f33e1d8b6c7759283cc2c13898754.png)


After product v2 passes the verification, modify the destination weight of the routing rule of the associated `VirtualService`. Set to route all the traffic (100%) to the product service to product v2 and refresh the product list page for verification. The weight is adjusted based on `VirtualService` as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/502b2957e998766352a0c449afef2459.png)

Canary release is completed as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/58f9704c1167b46b18344103a1798510.png)