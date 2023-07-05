## Overview
The Tencent Container Registry (TCR) Enterprise supports security scanning of managed container images and can generate scanning reports, expose potential security vulnerabilities in container images, and provide suggestions for fixing them. Container image security is an important part of cloud native application delivery security. Timely security scanning of uploaded container images and blocking application deployment based on the scanning results can effectively reduce the risk of vulnerabilities in the production environment.

The image deployment blocking feature is configured at the namespace level. You can enable it, and configure the blocking policy and the ignorable image vulnerabilities. Then, if a container client is trying to pull images that meet the blocking policy, the pulling will be denied and error reports will be returned.

## Prerequisites

Before using the image deployment blocking feature, you need to perform the following operations:
- [Create a TCR Enterprise Instance](https://intl.cloud.tencent.com/document/product/1051/35486).
- If you are using a sub-account, you must have granted the sub-account operation permissions for the corresponding instance. For more information, see [Example of Authorization Solution of TCR Enterprise](https://intl.cloud.tencent.com/document/product/1051/37248).

## Directions
### Configuring the blocking policy
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **Namespace** in the left sidebar.
2. On the "Namespace" page, click the name of the instance for which you want to configure the blocking policy to go to the namespace details page.
3. On the "Deployment security" page, enable the blocking and configure the vulnerability level to be blocked.

### Configure the allowlist of vulnerabilities
After enabling the blocking, you can configure the allowlist of vulnerabilities. Enter one or more CVE IDs and separate them with commas. Then, if the image ID is contained in the security scanning result, it will be ignored by the blocking policy. That means, if there is a high-risk vulnerability in the image, and the vulnerability is configured in the allowlist, the image can be pulled normally even if it is configured to block the pulling of images with high-risk vulnerabilities.
