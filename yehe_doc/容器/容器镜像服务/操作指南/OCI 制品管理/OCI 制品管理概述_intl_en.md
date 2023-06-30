## Overview
Tencent Container Registry (TCR) is compatible with OCI standard and supports hosting of multiple cloud-native artifacts including Docker Image, meeting the requirements of advanced users for hosting and distribution of Helm Chart, CNAB and custom OCI artifacts.

Currently, TCR Enterprise and TCR Individual instances support hosting of OCI artifacts. You can push OCI artifacts to image repositories, check the artifact type and pull commands.

For more about OCI artifacts and the usage, please see the official project [opencontainers/artifacts](https://github.com/opencontainers/artifacts) on the GitHub.

## Prerequisites
You must complete the following preparations before you can upload and manage OCI artifacts in the TCR instances.
- [Create a TCR Enterprise instance](https://intl.cloud.tencent.com/document/product/1051/35486) or initialize the TCR Individual.
- If you are using a sub-account, you must have granted the sub-account required permissions for the instance. For more information, see [Example of Authorization Solution of the TCR Enterprise](https://intl.cloud.tencent.com/document/product/1051/37248).

## Directions
### Managing OCI artifacts in the console
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **Image Repository** in the left sidebar.
2. On the page that appears, you can view the list of image repositories in the current instance. It supports hosting of OCI artifacts by default. You can build OCI artifacts using the specific client tools and push the artifacts to the image repository.
3. Click the name of the desired image repository to go to the details page, where you can view the existing artifacts in the image repository.

## References
### Helm Charts Management

If you want to use Helm Charts, you can push them as OCI artifacts to the image repository for unified management. The Helm V3 tools are required if you choose this management method. Also, you can use the Helm Chart hosting feature provided by TCR Enterprise instances based on the Chart Museum open source project. For more information, see [Helm Chart Hosting](https://intl.cloud.tencent.com/document/product/1051/35493).