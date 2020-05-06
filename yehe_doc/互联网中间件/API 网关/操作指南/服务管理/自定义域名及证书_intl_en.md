## Operation Scenarios
The domain name binding feature allows you to bind your own domain name to a service, so that the service can be accessed at it.

## Prerequisites
- Please ensure that the domain name to be bound has been configured for resolution.
- Please ensure that an [ICP filing](https://intl.cloud.tencent.com/document/product/1022/34607) has been obtained for your domain name as required.

## Directions

### Associating custom domain name
1. On the **[Service](https://console.cloud.tencent.com/apigateway/service)** page in the API Gateway Console, click a service ID to enter the service details page.
2. On the service details page, select **Custom domain**, click **Create** in the top-left corner, enter the configuration information, and click **Submit**.
> 
> - If you need the HTTPS protocol that supports independent domain names, you should submit the SSL certificate for your domain name by uploading it or by entering the certificate name, content, and private key.
> - A modified CNAME record will take effect after a period of time. Be sure to proceed with the configuration after it takes effect; otherwise, the configuration will fail.
3. After configuring CNAME resolution, configure the domain name in the service (be sure to configure CNAME resolution first).
4. To unbind a domain name, delete it from the service and then delete its CNAME record.

### Configuring the path mapping of domain name
When configuring a custom domain name, you can use the default path mapping, where the URL of the path is `custom domain name/environment name`. For example, `www.yingxiong.com/release` points to the release environment in the service, `www.yingxiong.com/prepub` points to the pre-release environment in the service, and `www.yingxiong.com/test` points to the test environment in the service.
![](https://main.qcloudimg.com/raw/64fa76c99d4ab806372d7209af9b5880.png)

You can also configure a custom path, where the URL is `custom domain name/custom path`. This URL points to the environment that you map. For example, if the configured path is `/mypath` and the environment is the release environment, the URL of the release environment will be `www.yingxiong.com/mypath`. If you want to use the root path, directly configure the path as `/`.
![](https://main.qcloudimg.com/raw/c810f2addfdd43db5c4a3bdcd626c7f8.png)
When a custom path mapping is used, the default path mapping (i.e., `custom domain name/environment name`) will not take effect.
Both the custom path mapping and default path mapping can be modified after configuration.
![](https://main.qcloudimg.com/raw/e79682d040790884cfb1b6d00ab1c178.png)


