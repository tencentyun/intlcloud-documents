

### Version Strategy

Tencent Cloud Mesh currently provides commercialization of only Istio even-numbered versions. It provides two mainstream Istio minor versions on the console for you to choose, for example, 1.8 and 1.10, and launches a new version within half a year after a latest Istio even-numbered minor version is released. You can upgrade your meshes to the latest version by using the mesh canary upgrade feature of Tencent Cloud Mesh. Based on the current iteration frequency of Istio versions, each even-numbered minor version is expected to provide services online for about 12 months. When a new version is launched, the second latest version originally provided by Tencent Cloud Mesh will enter a 3-month maintenance window period. For example, after version 1.12 is launched, version 1.8 will enter the maintenance window period.

For the same Istio minor version, Tencent Cloud Mesh provides only one patch version by default, for example, 1.10.3. In a case of major updates and bug fixes, Tencent Cloud Mesh will irregularly provide updates and prompt you to perform an upgrade.

### Constraints Upon Exceeded Maintenance Window Period

For a mesh within the maintenance window period, you can use all features normally; however, you need to complete the upgrade as soon as possible. Otherwise, after the maintenance window period is exceeded, the timeliness and effectiveness of services cannot be guaranteed, and the console features will also be restricted, including:

1. Mesh configurations can no longer be modified on the console.
2. The console will no longer provide display of observability-related features such as topology invoking and monitoring metrics.
3. A mesh version cannot be upgraded by using the canary upgrade feature on the console.

