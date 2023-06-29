


<blockquote class="d-mod-alarm">
<div class="d-mod-title d-alarm-title">
<i class="d-icon-alarm"></i>Notice:
</div>
<p></p>This feature is in beta testing and will become generally available soon.</p>
</blockquote>


## Feature Description

Tencent Cloud CDN supports version management for a single domain name. You can create one configuration for each domain name version, and deploy it to the production environment and staging environment.

- Production environment: the live environment where acceleration services are put into operation.
- Staging environment: a sandbox for testing domain name configurations only. This environment is built on a small scale and is only expected for domain name configuration tests in the console. It should not be use for actual business running or performance tests.

>!
>1. For domain names without using external certificates and image optimization, version management is supported.
>2. Only one version can be deployed at a time in each environment.
>3. URL refresh is supported in both the production environment and staging environment, while directory refresh and URL prefetch are only allowed in the production environment. For more information, see [Purge and Prefetch](https://intl.cloud.tencent.com/document/product/228/33982).
>4. Data and usage monitoring features, like [usage limit configuration](https://intl.cloud.tencent.com/document/product/228/7541), are only available in the production environment.


## Overview

- Applicable to beta test for domain name configuration



[](id:open)
## Enabling Version Management

Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and select **Domain Management** to view the domain name list. Click the target domain name to enter the configuration page, and check **Enable Version Management** in the top right corner.
![](https://main.qcloudimg.com/raw/52d05f1d49c1143e572d5bd2ff7cb88c.png)

After version management is enabled, Ver.1 will be created with the current domain name configuration and deployed to both the production environment and staging environment.

## Managing Versions

After enabling version management, you can view and manage versions on the **Version Management** page. Each version is identified by a version number Ver.n (n=1,2,3,...).
To access the version management page, you can select **More** > **Version Management** under the operation column in the domain name list. You can also click a domain name to find **Version Management** in its configuration page.
![](https://main.qcloudimg.com/raw/6d74d6b53b75ef97a63926718f50cda4.png)



### Adding versions
Click **Add Version**. A version will be created based on the current configuration of the production environment by default. You can modify the configuration as needed and then create the new version.
![](https://main.qcloudimg.com/raw/7d6277fad76dd1391f9be965c4c99df0.png)

>! If you’re prompted with an error message after submitting the new version, you don’t need to create a new one. Go back to the version management page and modify the version you submitted.

### Editing versions

The latest version is editable before it’s released to the staging environment. You can select **More** > **Edit** under the operation column.
![](https://main.qcloudimg.com/raw/ccd2e75a24c5076c0a624b5cd8cbbecb.png)
Historical versions (all versions before the latest version), no matter whether they have been released to the staging environment, can only be viewed but not edited.

>!Before adding a new version, please make sure all the existing versions are released. Otherwise, the version not released will become a historical version that cannot be edited and released to the staging environment.


### Releasing versions

For domain names with version management enabled, release versions as follows:

1. Locate the version that need to release to the staging environment, select **More** > **Release to the staging environment** under the operation column.
![](https://main.qcloudimg.com/raw/13b8f5a168719c31c2c1b03b532933a9.png)
2. CDN will assign an IPv4 IP to the domain name. To test the version deployed in the staging environment, modify the client HOSTS, and point the domain name to the IP.
3. If you want to adjust the configuration and test again, you need to add and submit a new version, and then repeat step 1 and 2.
4. After testing, click **Sync to Production Env.** next to the version number to sync it to the production environment and deploy the configuration to the live site.
![](https://main.qcloudimg.com/raw/89b2d937dcba03f68c62a2aad60b9f6f.png)
5. If you need to change the version in the production environment, repeat steps 1 through 4.

>!
>- You can only release the latest version (the one with the largest version number) to the staging environment. Historical versions can only be viewed.
>- Special backend configuration or platform updates will be released to the production environment directly.
>- In case of special backend configuration and platform upgrade, conflicts may occur while synchronizing the staging environment to the production environment, and you will receive a error message about “special backend configuration”. In this case, you should create another version to release.
>- The IP of the staging environment is not suppose to be changed frequently. But to ensure accuracy, it is recommended to get a new IP by clicking the refresh button before testing each time.



### Viewing versions

If you want to view configuration details of a version, click **View** under the operation column.


### Enable/Disable versions
Click **Disable** in the production environment section. The version deployed in the production environment and staging environment will be disabled at the same time, indicating the domain name will be deactivated and the acceleration service will be closed.

To enable the version again, click **Enable** in the production environment section and the version will be enabled in both the production and staging environment.

## Disabling Version Management

Once you disable it, the version deployed in the production environment will be introduced as the live configuration. All other existing versions will be discarded and cannot be restored.

You can click **Enable Version Management** to enable it again as needed.


## Notes

For domain names with version management enabled:
- Batch configuring features, like [copying configuration](https://intl.cloud.tencent.com/document/product/228/38936) and [batch changing configuration](https://intl.cloud.tencent.com/document/product/228/39911), are not supported.
- You cannot configure a certificate for a domain name on the certificate management page in the console.
- When you enable or disable acceleration for a domain name, the version deployed in the production environment and staging environment will be enabled or disabled accordingly.
- The tag and project of the domain name are editable.
- To change the acceleration region and service type, you should disable version management first. 
