
## Overview
 This document describes how to limit the maximum number of concurrent access requests to an ecommerce website to ensure robust service running.

## Directions
To simulate a high number of concurrent requests to the user service, submit the following YAML file to deploy the client service (with ten Pods).

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: test
  labels:
    istio-injection: enabled
spec:
  finalizers:
    - kubernetes
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: client
  namespace: test
  labels:
    app: client
spec:
  replicas: 10
  selector:
    matchLabels:
      app: client
  template:
    metadata:
      labels:
        app: client
    spec:
      containers:
        - name: client
          image: ccr.ccs.tencentyun.com/zhulei/testclient:v1
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
---

apiVersion: v1
kind: Service
metadata:
  name: client
  namespace: test
  labels:
    app: client
spec:
  ports:
    - name: http
      port: 7000
      protocol: TCP
  selector:
    app: client
  type: ClusterIP
```

At this point, all the requests to the user service can pass, as there is no limit on the maximum concurrency. View the client Pod log through the client Deployment in the TKE console, which shows that all the requests returned the username `Kevin`, indicating that requests succeeded.
A high number of concurrent requests is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/4fc17d6c0c8db8507e08b37f6d8d5f7a.svg)

All the requests succeeded as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/ad38ecf719a315b031c359a8c568b05c.png)


Configure the `Destination Rule` of the user service to limit the maximum concurrency to `1`:

```yaml
apiVersion: networking.istio.io/v1alpha3
kind: DestinationRule
metadata:
  name: user
  namespace: base
spec:
  host: user
  trafficPolicy:
    connectionPool:
      http:
        http1MaxPendingRequests: 1
        http2MaxRequests: 1
        maxRequestsPerConnection: 1
  exportTo:
    - '*'
```

View the client Pod log, which shows that some requests are abnormal and failed, with no username returned. In this case, the connection pool succeeded in limiting the maximum number of concurrent requests to the service.
Some access requests failed as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/ab3bbfbebdfec1e3c211a5fbdfd7918b.png)
After the connection pool testing, delete the traffic policy configuration of the connection pool on the details page of the user service.
