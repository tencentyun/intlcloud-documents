Sidecar auto-injection is enabled for a namespace through `kubectl label namespace xxx istio-injection=enabled`, but it does not take effect.

## Labels in Tencent Cloud Mesh for Automatic Injection

In Tencent Cloud Mesh 1.6 or later, automatic injection for a namespace is enabled by using a label similar to `istio.io/rev=1-8-1`, but not the label `istio-inejction=enabled`. The specific label used to enable automatic injection varies depending on versions.

- In v1.6, the label `istio.io/rev=1-6-9` is used.
- In v1.8, the label `istio.io/rev=1-8-1` is used.

Therefore, the common label `istio-injection=enabled` in the community will not take effect on Tencent Cloud Mesh. The following describes why the common label in the community is not used.

## Different Labels Are Required During Mesh Canary Upgrade

To support the canary upgrade of a service mesh, the old and new control planes need to coexist for a period of time, so that the old data plane can be gradually updated and upgraded and then connected to the new control plane. If both control planes use a same label to identify whether automatic injection is required, both control planes will inject sidecars in the rolling update process, which will cause a conflict. To avoid the conflict, Istio officially provides the [canary upgrade scheme](https://istio.io/latest/docs/setup/upgrade/canary/#data-plane). This scheme is based on the method of using different labels for different control planes to achieve coexistence of multiple control planes. It is also the scheme adopted by Tencent Cloud Mesh.

## How to Enable Automatic Injection on Tencent Cloud Mesh

On the Tencent Cloud Mesh console, choose **Service** > **Sidecar auto-injection**.

![](https://qcloudimg.tencent-cloud.cn/raw/a14a84e23be6e5b209315700ce2146ef.png)

Then, select the namespace for which automatic injection is to be enabled.

You can also use kubectl to label the namespace to enable automatic injection.

```bash
kubectl label namespace xxx istio.io/rev=1-8-1
```

-16>! Note that the namespace name must be set based on actual conditions and the label must be modified based on actual Istio version.
