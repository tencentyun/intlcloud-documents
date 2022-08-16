## Overview
You can update configurations of a running service mesh. This section describes how to update the egress traffic mode and configure sidecar auto-injection.

## Directions

### Modifying the Egress Traffic Mode

The egress traffic mode defines a policy for the external access to services in the mesh. Two options are available: **Registry Only** (access to only services automatically discovered by the mesh and manually registered services is allowed) and **Allow Any** (access to any address is allowed).

Steps for configuring the egress traffic mode for the mesh are as follows:

1. Log in to the [Tencent Cloud Mesh console](https://console.cloud.tencent.com/tke2/mesh), and click the mesh ID of the mesh whose configurations are to be updated, to enter the mesh management page.
![](https://qcloudimg.tencent-cloud.cn/raw/bd10b1c574235a8ac2226222b812ee9f.png)
2. On the mesh basic information page, click the **Edit** button of the **Egress traffic mode** field to pop up the **Modify egress traffic mode** window.
![](https://qcloudimg.tencent-cloud.cn/raw/7c97e45ea182ae955c2e10b5871590f2.png)
3. Select **Allow Any** or **Registry Only** as required, and click **Save** to complete the update of the egress traffic mode.
![](https://qcloudimg.tencent-cloud.cn/raw/efc5846fe97bc698b75945a9a778c870.png)

### Configuring Sidecar Auto-injection

Tencent Cloud Mesh currently supports enabling sidecar auto-injection for a specified namespace on the console. After sidecar auto-injection is enabled, mesh sidecars will be automatically installed on newly created workloads under the namespace. Because injection is completed during the workload creation process, sidecars cannot be automatically installed on existing workloads even if sidecar auto-injection is enabled. You can complete sidecar auto-injection by rebuilding workloads.

Steps for configuring namespace-level sidecar auto-injection are as follows:

1. Log in to the [Tencent Cloud Mesh console](https://console.cloud.tencent.com/tke2/mesh), and click the mesh ID of the mesh whose configurations are to be updated, to enter the mesh management page.
![](https://qcloudimg.tencent-cloud.cn/raw/5bfd233ffe3448492283e1dce1f73bc8.png)
2. On the service list page, click **Sidecar auto-injection** to pop up the **Sidecar auto-injection configuration** window.
![](https://qcloudimg.tencent-cloud.cn/raw/aae8187f5a5e5d6170c4d427adb8dac1.png)
3. Select one or more namespaces for which sidecar auto-injection needs to be enabled, and click **OK** to complete sidecar auto-injection configuration.
![](https://qcloudimg.tencent-cloud.cn/raw/dcdd2807357aa5190e716d70cd12ee61.png)

### Customizing Sidecar Injection
Tencent Cloud Mesh also allows you to enable sidecar auto-injection for a specific workload by editing a yaml file. If necessary, you can add a label `istio.io/rev: {Istio version number}` to a pod. (Note that label settings related to sidecar injection in Tencent Cloud Mesh are slightly different from Istio's default syntax.) An example is as follows:
![img](https://qcloudimg.tencent-cloud.cn/raw/e82a35473c7029445160eaed75e96834.png)

If you need to add a special case for a specific pod under a namespace that has auto-injection enabled to disable sidecar auto-injection, you can add a label `sidecar.istio.io/inject="false"` for the pod. Pod-level injection has a higher priority than namespace-level injection. For more details on sidecar auto-injection, see the Istio documentation [Installing the Sidecar](https://istio.io/latest/zh/docs/setup/additional-setup/sidecar-injection/).
