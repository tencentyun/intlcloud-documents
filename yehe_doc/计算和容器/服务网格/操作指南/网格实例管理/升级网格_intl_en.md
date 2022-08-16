## Overview
Tencent Cloud Mesh provides the mesh upgrade service, which allows you to upgrade a mesh from an earlier version to a later version. The upgrade process follows canary upgrade principles and is divided into the following steps:

<dx-steps>
- Deploy the control plane of a new version to upgrade the control plane of Tencent Cloud Mesh.
- Conduct a canary upgrade of the data plane, and restart services to update sidecars of existing service pods.
- Verify the upgrade to check that the services are normal.
- Take the control plane of the old version offline.
</dx-steps>

Before the control plane of the old version goes offline, you can roll back the mesh to the state before the upgrade. The upgrade process is shown as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/cc08d5a86ead7effe267e57de73ef03f.png)


## Directions
1. Log in to the [Tencent Cloud Mesh console](https://console.cloud.tencent.com/tke2/mesh).
2. When the mesh version can be upgraded, there is a prompt indicating that a new version is available.
![](https://qcloudimg.tencent-cloud.cn/raw/0cb5a5ef56615634eb42adbec8edb8dd.png)
3. Choose **More** > **Upgrade**, and perform the upgrade as prompted.
   The upgrade will be performed in three stages: **Control plane upgrade** > **Data plane upgrade** > **Old control plane offline**. Before the control plane of the old version goes offline, you can roll back the mesh to the state before the upgrade.
   <dx-tabs>
   ::: Control Plane Upgrade
   During the **Control plane upgrade** stage, Tencent Cloud Mesh deploys control plane components of the new version.
   ![](https://qcloudimg.tencent-cloud.cn/raw/cc2119c2bfbf1e2e30059968d736ef38.png)
   ![](https://qcloudimg.tencent-cloud.cn/raw/fb84819ee1a9657f8d25f7629e72049b.png)
   :::
   ::: Data Plane Upgrade
   During the **Data plane upgrade** stage, you need to specify the new version to take effect to sidecar auto-injection of the specified namespace. After this stage starts, sidecars of the new version will be injected into **newly created** service pods under the namespace. **Sidecars in the existing service pods will be updated to the new version only after these pods are rebuilt.** Restart may affect service availability. Therefore, Tencent Cloud Mesh does not automatically rebuild service pods. **Instead, you need to manually rebuild service pods.**
>?
>- You can republish a service through a pipeline or manually rebuild a workload by directly using command lines such as kubectl patch and kubectl rollout restart.
>- In some scenarios, sidecars will be uninstalled instead of being upgraded. For example, assume that a namespace has enabled sidecar injection, sidecars have been successfully injected into some service pods, and then namepsace-level sidecar injection is disabled. After a service pod is restarted, its sidecars will be uninstalled unless a sidecar injection label has been independently set for the pod.
>
![](https://qcloudimg.tencent-cloud.cn/raw/2b7a5e903bd836702f03702ca78b7703.png)
:::
::: Upgrade Verification
Because the version upgrade involves feature changes, there may be compatibility issues. After the service pods are rebuilt, you need to check whether the service is normal. If you find that the upgrade causes service exceptions, you can click **Rollback** on the upgrade page to roll back the data plane sidecars to the source version.
:::
</dx-tabs>
4. Click **Done** or **Cancel upgrade**. During the **Data plane upgrade** stage, you can click **Upgrade** or **Rollback** to check whether the existing pods meet the conditions for entering the next step. When all namespaces are switched to the control plane of the new version, and the sidecars in all the existing service pods have been updated to the new version, you can click **Upgrade** to go to the next step **Old control plane offline** and complete the upgrade. Alternatively, when all namespaces are switched back to the control plane of the old version, and the sidecars in all the existing service pods use the control plane of the old version, you can click **Rollback** to go to the next step to take the control plane of the new version offline and cancel the upgrade. 
![](https://qcloudimg.tencent-cloud.cn/raw/77047f18f8d37a68359511b188f34bdd.png)
