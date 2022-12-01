Log in to the [IM console](https://console.cloud.tencent.com/im), click the target app, and select **Webhook Configuration** in the left sidebar. You can configure webhook URLs and decide which webhooks to enable according to your business needs.

## Configuring Webhook URLs

1. On the **Webhook Configuration** page, click **Edit** in the webhook URL configuration area.
2. In the webhook URL configuration dialog box that pops up, enter the webhook URL.

>?
>- The webhook URL must start with `http://` or `https://`.
>- If you have not yet applied for a domain name, you can directly configure an IP address, for example, `http://123.123.123.123/imcallback`.
>- Only letters (`a–z`, case-insensitive), numbers (0–9) and hyphens (-) can be used. Spaces and the following characters are not supported: `!$&?`.
>- The hyphen (-) cannot appear consecutively, be registered independently, or be placed at the beginning or end.  
>- The length of the domain name cannot exceed 63 characters.
>- The webhook URL of IM uses ports 80/443 by default. When the webhook URL is replaced, port changes are involved. Please avoid the situation where the ports before and after the replacement are mutually prefixed; for example, avoid changing `https://xxx:443` to `https://xxx:4433` or changing `https://xxx` to `https://xxx:4433`.

3. Click **OK** to save the configuration.

## Configuring Event Webhooks
1. On the **Webhook Configuration** page, click **Edit** in the webhook configuration area.
2. In the webhook configuration dialog box that pops up, check the desired webhooks.
![](https://main.qcloudimg.com/raw/67cb8c9fd2365e3e2014e6940c468aaf.png)
3. Click **Confirm** to save the configuration.

## Downloading an HTTPS Mutual Authentication Certificate
After configuring webhook URLs, you can download an HTTPS mutual authentication certificate from the console for future use.
>? You can configure mutual authentication based on your actual needs. For the detailed configuration methods, see [Mutual Authentication Configuration](https://intl.cloud.tencent.com/document/product/1047/34379).

1. Go to the [console](https://console.cloud.tencent.com/im/callback-setting), open the **[Webhook Configuration](https://console.cloud.tencent.com/im/callback-setting)** page, and click **HTTPS Mutual Authentication Certificate Download** in the webhook URL configuration area in the upper-right corner.
![](https://main.qcloudimg.com/raw/52a1d6fc283f07e29842da512ba303a3.png)
2. In the certificate download dialog box that pops up, click **Download**.
![](https://main.qcloudimg.com/raw/584dcfbed3a36a691971f6edcca19b43.png)
3. Save the certificate file.


## Subsequent Operations
After configuring webhook URLs and enabling the corresponding event webhooks, you can refer to [Webhooks](https://intl.cloud.tencent.com/document/product/1047/34354) to use the corresponding webhooks in order to obtain user and operation information in real time.
