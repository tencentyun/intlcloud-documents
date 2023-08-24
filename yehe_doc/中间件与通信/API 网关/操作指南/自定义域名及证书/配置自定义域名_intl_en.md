## Scenarios
The domain name binding feature allows you to bind your own domain name to a service, so that the service can be accessed at it.

## Prerequisite
- Complete resolution of the domain name to be bound.

## Directions

### Associating a custom domain name
1. Log in to the ‍[PI Gateway console](https://console.cloud.tencent.com/apigateway/index?rid=1) and click **Service** on the left sidebar.
2. In the service list, click a service ID to enter the service details page.
3. On the service details page, select **Custom domain**, click **Create** in the top-left corner, enter the configuration information, and click **Submit**.
>?
>- If you need the HTTPS protocol that supports independent domain names, submit the SSL certificate for your domain name. You can upload the certificate or enter the certificate name, content, and private key.
>- After a CNAME record is modified, it takes a while for it to take effect. CBe sure to proceed with the configuration after it takes effect; otherwise, the configuration will fail.
>- If you select HTTPS for a independent domain, WSS is also supported by default.
4. After configuring CNAME resolution, configure the domain name in the service (be sure to configure CNAME resolution first).
5. To unbind a domain name, delete it from the service and then delete its CNAME record.

### Configuring forced HTTPS
On the custom domain name configuration page, if the protocol is HTTPS&HTTPS or HTTPS, the forced HTTPS feature can be enabled. After it is enabled, API Gateway will redirect requests using the custom domain name over the HTTP protocol to the HTTPS protocol.
![](https://main.qcloudimg.com/raw/afa6246bc12dcc9fd81487f84429a299.png)

### Configuring domain name path mapping
1. On the custom domain name list page, click **Edit Path Mapping** in the **Operation** column.
![](https://main.qcloudimg.com/raw/3a32b52150e2c281baf921543c1f9eed.png)
2. Select the path mapping type:
 - **Default path mapping**: the URL of the path is `custom domain name/environment name`. For example, `www.XXXXX.com/release` points to the release environment in the service, `www.XXXXX.com/prepub` points to the pre-release environment in the service, and `www.XXXXX.com/test` points to the test environment in the service.
![](https://main.qcloudimg.com/raw/72d65ac0190da0757d05837e4223f515.png)
 - **Custom path mapping**: the URL is `custom domain name/custom path`. This URL points to the environment that you map. For example, if the configured path is `/mypath` and the environment is the release environment, the URL of the release environment will be `www.XXXXX.com/mypath`. If you want to use the root path, directly configure the path as `/`.                              ![](https://main.qcloudimg.com/raw/72d65ac0190da0757d05837e4223f515.png)
 >!When a custom path mapping is used, the default path mapping (`custom domain name/environment name`) will not take effect.
Both the custom path mapping and default path mapping can be modified after configuration.
3. Click **Submit** to complete the configuration.
