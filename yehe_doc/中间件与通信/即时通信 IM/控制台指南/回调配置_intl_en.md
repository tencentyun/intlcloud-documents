Log in to the [IM console](https://console.cloud.tencent.com/im), click the target app card, and select **Callback Configuration** in the left sidebar. You can configure callback URLs and decide which callbacks to enable according to your business needs.

## Configuring Callback URLs

1. On the **Callback Configuration** page, click **Edit** in the callback URL configuration area.
2. In the callback URL configuration dialog box that pops up, enter the callback URL.

>?
>- The callback URL must start with `http://` or `https://`.
>- If you have not yet applied for a domain name, you can directly configure an IP address, for example, `http://123.123.123.123/imcallback`.
>- Only letters (`a–z`, case-insensitive), digits (0–9) and hyphens (-) can be used. Spaces and the following characters are not supported: `!$&?`.
>- The hyphen (-) cannot appear consecutively, be registered independently, or be placed at the beginning or end.  
>- The length of the domain name cannot exceed 63 characters.
>- The callback URL of IM uses ports 80/443 by default. When the callback URL is replaced, port changes are involved. Please avoid the situation where the ports before and after the replacement are mutually prefixed; for example, avoid changing `https://xxx:443` to `https://xxx:4433` or changing `https://xxx` to `https://xxx:4433`.

3. Click **OK** to save the configuration.

## Configuring Event Callbacks
1. On the **Callback Configuration** page, click **Edit** in the third-party callback configuration area.
2. In the third-party callback configuration dialog box that pops up, check the desired callbacks.
![](https://main.qcloudimg.com/raw/67cb8c9fd2365e3e2014e6940c468aaf.png)
3. Click **OK** to save the configuration.

## Downloading an HTTPS Mutual Authentication Certificate
After configuring callback URLs, you can download an HTTPS mutual authentication certificate from the console for future use.
>? You can configure mutual authentication based on your actual needs. For the detailed configuration methods, see [Mutual Authentication Configuration](https://intl.cloud.tencent.com/document/product/1047/34379).

1. Go to the [console](https://console.cloud.tencent.com/im-detail/callback-setting), open the **[Callback Configuration](https://console.cloud.tencent.com/im-detail/callback-setting)** page, and click **Download HTTPS Mutual Authentication Certificate** in the callback URL configuration area in the upper-right corner.
![](https://main.qcloudimg.com/raw/52a1d6fc283f07e29842da512ba303a3.png)
2. In the certificate download dialog box that pops up, click **Download**.
![](https://main.qcloudimg.com/raw/584dcfbed3a36a691971f6edcca19b43.png)
3. Save the certificate file.


## Subsequent Operations
After configuring callback URLs and enabling the corresponding event callbacks, you can refer to [Third-Party Callbacks](https://intl.cloud.tencent.com/document/product/1047/34354) to use the corresponding callback features in order to obtain user and operation information in real time.
