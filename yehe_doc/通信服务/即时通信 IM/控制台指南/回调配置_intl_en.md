Log in to the [IM Console](https://console.cloud.tencent.com/im), click the target app card, and select **Callback configuration** in the left sidebar. Here, you can configure callback URLs and decide which callbacks to enable according to your business needs.

## Configuring Callback URLs

1. On the **Callback configuration** page, click **Edit** in the callback URL configuration area.
2. In the **Callback URL Configuration** dialog box that pops up, enter the callback URL.
 >
 >- The callback URL must begin with `http://` or `https://`.
 >- If you have not applied for a domain name, you can directly configure an IP address, for example, `http://123.123.123.123/imcallback`.
 >
3. Click **OK** to save the configuration.

## Configuring Event Callbacks
1. On the **Callback configuration** page, click **Edit** in the event callback configuration area.
2. In the **Event Callback Configuration** dialog box that pops up, check the desired callbacks.
3. Click **OK** to save the configuration.

## Downloading an HTTPS Mutual Authentication Certificate
After configuring callback URLs, you can download an HTTPS mutual authentication certificate from the console for future use.
> You can configure mutual authentication as required. For more information about how to configure, see [Configuring Mutual Authentication with Apache](https://intl.cloud.tencent.com/document/product/1047/34379).

1. On the **Callback configuration** page, click **Download HTTPS Mutual Authentication Certificate** in the callback URL configuration area.
2. In the certificate download dialog box that pops up, click **Download**.
3. Save the certificate file.


## Subsequent Operations
After configuring the callback URL and enabling event callbacks, see [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354) to use callback features to track user information and operations in real time.
