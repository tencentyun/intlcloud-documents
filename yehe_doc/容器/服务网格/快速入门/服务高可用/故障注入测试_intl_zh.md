
 ## 操作场景
 电商网站业务团队需要模拟访问库存服务存在延迟故障时网站系统的行为，以测试服务弹性，网站用户的优化访问体验。
stock 服务 fixed delay 7s 如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/6283511dd5b2b814053793048f4dd770.png)

## 操作步骤

通过配置绑定 stock 服务的 VritualService，设置访问 stock 服务的故障注入策略：100%的请求会有 7 秒的固定延迟。

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

配置完成后，在 Demo 网站页面单击 “ADD TO CART” 加入购物车或者单击 “YOUR CART” 调用购物车服务，购物车服务会调用 stock 服务查询库存，访问 stock 服务有 7 秒的固定延迟故障注入策略，以及在购物车页面单击“CHECKOUT”发起结算会调用 order 服务，order 服务会调用 stock 服务查询库存，访问 stock 服务有 7 秒的固定延迟故障注入策略。此时页面处于加载中的状态会持续 7 秒一直等待故障结束，造成网站用户的不流畅浏览体验。
cart 服务调用 stock 服务的等待状态如下图所示：
![cart 服务调用 stock 服务的等待状态](https://qcloudimg.tencent-cloud.cn/raw/47f29ac5c16d0fa3fc3cc5334d8f04c6.png)

网站用户的浏览体验优化可以通过配置超时 timeout 实现。