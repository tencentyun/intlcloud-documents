
 ## 操作场景
 生产环境（base namespace）的服务已经稳定运行，电商网站业务团队希望对网格中的服务做权限控制，限制生产环境（base namespace）下的服务不能被测试环境（test namesapce）下的服务访问。


## 操作步骤
对网格中的服务进行权限控制可通过配置 AuthorizationPolicy 实现，配置以下 AuthorizationPolicy 策略限制 base namespace 下所有服务不能被 test namespace 下的服务访问。
通过控制台配置授权规则，如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/0033bec88e5ba961f11d308f360120be.png)


也可以通过提交 YAML 文件至主集群完成授权配置：

```yaml
apiVersion: security.istio.io/v1beta1
kind: AuthorizationPolicy
metadata:
  name: base-authz
  namespace: base
spec:
  action: DENY
  rules:
    - from:
        - source:
            namespaces:
              - test
```

配置完成后通过 TKE 控制台查看 test namespace 下 client 服务的 pod 日志，发现 client 服务访问 base namespace 的 user 服务失败。授权策略生效。
授权规则限制后，访问失败如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/218a0d4f1d1056953e54398a7de18e10.png)