

## 操作场景
网站计划推出会员积分抵扣运费的活动以发展会员。电商网站策划了会员积分抵扣订单金额的新功能，当前部署的 order 服务由 v1 deployment 提供，没有运费抵扣的功能；网站新开发了 order 服务的 v2 版本，有积分抵扣运费的功能。网站希望可以于请求的 header 中是否会员的 cookie 信息进行路由，会员路由至 order v2（有运费抵扣功能），非会员路由至 order v1（无运费抵扣功能）。
服务多版本路由概览图如下所示：
![](https://qcloudimg.tencent-cloud.cn/raw/32b7be8c38eb80546687b43ea3a1cf23.png)

## 操作步骤
提交以下 yaml 文件至主集群，部署 order v2 至集群。

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

部署完成后，由于还未配置路由规则，此时访问 order 服务的流量会被随机路由至 v1 版本或 v2 版本。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/5a17c0d1ab6ec49522b314e2198fd828.png) 

配置基于流量特征内容的路由规则前先需要通过 DestinationRule 定义 order 服务的两个版本。如下图所示：

定义 order 服务的版本如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/d364db7456a8b5a57e37471042ca4762.png)

order 服务版本定义完成如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/c3f90333dd5d575779c8dffbad8723c3.png)


或可通过提交 YAML 文件至主集群完成 Destination Rule 的创建：

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

两个版本定义完成后，通过 VirtualService 定义按流量特征进行路由，请求的 header-cookie 中 vip=false 时路由至 order 服务的 v1 subset，vip=true 时路由至 order 服务的 v2 subset。即会员的请求路由至 order v2，非会员的请求路由至 order v1。提交以下 yaml 资源至主集群，即可完成上述配置。



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

配置完成后，可登录会员帐号（ID：1-3）加购和买单，发现有运费抵扣功能，流量被路由到了 order v2 版本；登录非会员账号（ID：4-5）加购和买单，发现无运费抵扣功能，根据 header 中的 VIP 字段信息，请求被路由到了最初部署的 order v1 版本。版本信息也可通过左下角悬浮窗中的信息观察。
会员用户请求被路由到 v2 版本如下图所示：
![会员用户请求被路由到 v2 版本](https://qcloudimg.tencent-cloud.cn/raw/3dbecdb8e7c511688e961112ce25c53c.png)

非会员用户请求被路由到 v1 版本如下图所示：
![非会员用户请求被路由到 v1 版本](https://qcloudimg.tencent-cloud.cn/raw/ac7204f19e7708f77d8bdefe7248b4be.png)

基于流量规则的路由如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/32b7be8c38eb80546687b43ea3a1cf23.png)

