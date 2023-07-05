In the process of migrating some services to Istio, pods may fail to start and then keep restarting. Through troubleshooting, it is found that other services (for example, pulling configurations from the configuration center) need to be called when such a service starts. In addition, the service will exit upon a call failure because there is no retry logic. The call failure reason is that Envoy is unready (it takes a while for Envoy to pull the configurations from the control plane). As a result, the traffic sent by the service cannot be processed. (For details, see k8s issue [#65502](https://github.com/kubernetes/kubernetes/issues/65502).)

### Best Practices

At present, the best practice for this problem is to make applications more robust. You can add retry logic, so that the applications do not exit immediately after the call fails. Alternatively, you can add the sleep time before the startup command, so that the applications will wait for a few seconds.

If you do not want to modify your applications, refer to the following workaround solution. 

### Workaround Solution

The workaround solution is to adjust the sidecar injection sequence.
In Istio 1.7, this problem is resolved by adding a switch named `HoldApplicationUntilProxyStarts` to the istio-injector injection logic. After the switch is enabled, the proxy will be injected into the first container.

Example:
![img](https://main.qcloudimg.com/raw/2b0b4ab385411f76a1be816c0c292dd9.png)

![img](https://main.qcloudimg.com/raw/6a614019db2e05a4a1e7990afa7db023.png)

View the template used by istio-injector for automatic injection. It is found that if `HoldApplicationUntilProxyStarts` is enabled, a postStart hook is added to the sidecar.

![img](https://main.qcloudimg.com/raw/4a2e01dde93aa13a37be2a5c5254c39b.png)

The hook is used to block the startup of the subsequent service containers, so that the subsequent service containers will start only after the sidecar is fully started.

The switch configuration supports global configuration and local configuration, which can be enabled as follows:

<dx-tabs>
::: Global Configuration
Modify Istio's global ConfigMap configurations.

```bash
kubectl -n istio-system edit cm istio
```

Add `holdApplicationUntilProxyStarts: true` under `defaultConfig`.

```yaml
apiVersion: v1
data:
  mesh: |-
    defaultConfig:
      holdApplicationUntilProxyStarts: true
  meshNetworks: 'networks: {}'
kind: ConfigMap
```

If IstioOperator is used, modify defaultConfig under the CR field `meshConfig`.

```yaml
apiVersion: install.istio.io/v1alpha1
kind: IstioOperator
metadata:
  namespace: istio-system
  name: example-istiocontrolplane
spec:
  meshConfig:
    defaultConfig:
      holdApplicationUntilProxyStarts: true
```
:::
::: Local Configuration
If you are using Istio 1.8 or later, you can add the `proxy.istio.io/config` annotation to the pod for which the switch needs to be enabled and set `holdApplicationUntilProxyStarts` to `true`. For example:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      annotations:
        proxy.istio.io/config: |
          holdApplicationUntilProxyStarts: true
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: "nginx"
```


:::
</dx-tabs>



Note that after the switch is enabled, the service containers need to wait for the sidecar to be completely ready before they can be started. As a result, pods will start at a slower speed, which may be difficult in scenarios where rapid capacity expansion is required to cope with burst traffic. Therefore, it is recommended to evaluate the service scenarios by yourself and use the local configuration method to enable this switch only for the required service.
