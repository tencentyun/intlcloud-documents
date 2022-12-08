 

## Add-on management description

TKE provides a variety of add-ons and rich cluster features to enhance cluster performance and overall stability. Three types of add-ons are available:

| Add-On Type | Description | Documentation |
|---------|---------|---------|
|System add-on | It is the default and core add-on in a cluster, such as CBS-CSI, IPAMD, monitoring add-on, and log add-on. If it is abnormal, the cluster may fail. |-|
|Enhanced add-on | It is also called the extended add-on, an extended feature package provided by TKE. You can select one as needed. |[Add-on Overview](https://intl.cloud.tencent.com/document/product/457/33988)|
|Application market | It provides [Helm 3.0](https://helm.sh/) features integrated by TKE and supports creating various products and services such as Helm charts, container images, and software services. | [Application Market](https://intl.cloud.tencent.com/document/product/457/37706)|



<dx-alert infotype="notice" title="">
- **Disclaimer**: Tencent Cloud supports your proper installation of applications from the application market for supported cluster types and Kubernetes versions, but is not responsible for other matters such as application issues during running, application exceptions due to custom configuration modification, or lack of support for specified cluster types and Kubernetes versions.
- Tencent Cloud aftersales team provides applications from the application market specifically for experienced system admins or IT personnel. Tencent Cloud doesn't provide debugging or SLAs for such applications. If you encounter any problems when using an application, contact us via the reference link provided in the application details or at the official website of the application.
- For more information on the TKE SLA, see [Service Level Agreement](https://intl.cloud.tencent.com/document/product/457/12356).
</dx-alert>

The three types of add-ons are managed as follows:

| Add-On Type                       | Scope                                                     | Service Level                                                 | Upgrade Method                                                     |
| ------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| System add-on<br>(Default installation that cannot be deleted) | CBS-CSI, IPAMD, monitoring add-on, log add-on, etc.                                 | TKE prioritizes the stability of system add-ons and promptly releases security and compatibility updates and fixes on the backend. | TKE will not update certain versions with special features, which need to be manually updated as needed. For detailed directions, see [Add-On Version Maintenance Description](https://intl.cloud.tencent.com/document/product/457/49395). |
| Enhanced add-on<br>(Custom installation)     | For more information on the list, see [Add-on Overview](https://intl.cloud.tencent.com/document/product/457/33988). | TKE guarantees the stability of enhanced add-ons and promptly releases security and compatibility updates and fixes on the backend. Each enhanced add-on comes with a list of supported versions and may fail if you don't update it promptly. | TKE will not update certain versions with special features, which need to be manually updated as needed. For detailed directions, see [Add-On Version Maintenance Description](https://intl.cloud.tencent.com/document/product/457/49395). |
| Application market<br>(Custom installation)     | For more information on the list, see [here](https://console.cloud.tencent.com/tke2/market). | TKE only supports the installation and deployment of applications for supported cluster types and Kubernetes versions. | TKE provides application update methods and may push new charts from time to time. For detailed directions, see [Use the application](https://intl.cloud.tencent.com/document/product/457/30683). |



## Feature management description

Certain features are identified as "preview" by TKE in the documentation and in the console, indicating that they are try-outs and are not covered by the [Service Level Agreement](https://intl.cloud.tencent.com/document/product/457/12356).
