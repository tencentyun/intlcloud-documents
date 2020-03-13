Log in to [IM Console](https://console.cloud.tencent.com/im), click the target app card, and then click **Callback Configuration** in the left sidebar. On the page that appears, you can configure URLs and enable desired callbacks according to your business needs.

Currently, configuring HTTPS mutual authentication callbacks is not supported. To enable HTTPS mutual authentication, which has the highest security level, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact Tencent Cloud customer service and apply for this feature.

## Configuring the Callback URL

1. On the **Callback Configuration** page, click **Edit** in the callback URL configuration area.
2. In the "Callback URL Configuration" dialog that appears, enter the callback URL.
 >
 >- The callback URL must begin with `http://` or `https://`.
 >- If you have not applied for a domain name, you can directly set an IP address in the domain name, for example, `http://123.123.123.123/imcallback`.
 >
3. Click **OK** to save the setting.

## Configuring Event Callbacks
1. On the **Callback Configuration** page, click **Edit** in the event callback configuration area.
2. In the "Event Callback Configuration" dialog that appears, select desired callbacks.

3. Click **OK** to save the setting.

## Subsequent Operations
After configuring the callback URL and enabling event callbacks, see [Third-Party Callbacks](https://intl.cloud.tencent.com/document/product/1047/34354) to use callback features to track user information and operations in real time.
