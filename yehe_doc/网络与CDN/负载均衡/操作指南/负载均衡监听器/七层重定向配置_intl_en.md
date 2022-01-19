CLB supports layer-7 redirection, so that you can configure redirection on layer-7 HTTP/HTTPS listeners.
>?
>- Session persistence: if the client accesses `example.com/bbs/test/123.html` and session persistence has been enabled on the backend CVM, after redirection is enabled to forward traffic to `example.com/bbs/test/456.html`, the original session persistence mechanism will not take effect.
>- TCP/UDP redirection: redirection at IP + port level is not supported currently but will be available in subsequent versions.
## Redirection Overview
- Automatic redirection
  - Overview
  For an existing `HTTPS:443` listener, an HTTP listener (port 80) will be created automatically by the system for forwarding. Requests sent to `HTTP:80` will be automatically redirected to `HTTPS:443`.
  - Use case
 Forced HTTPS redirection, i.e., redirecting HTTP requests to HTTPS. When a user accesses a web service in a PC or mobile browser over HTTP, CLB will redirect all requests sent to `HTTP:80` to `HTTPS:443` for forwarding.
  - Strengths
	 - Set-and-Forget configuration: forced HTTPS redirection can be implemented for a domain name with only one configuration operation needed.
	 - Convenient update: if the number of URLs of the HTTPS service changes, you only need to use this feature again in the console for refreshing.
- Manual redirection
 - Overview
You can configure 1-to-1 redirection. For example, in a CLB instance, you can configure redirection of `listener 1 / domain name 1 / URL 1` to `listener 2 / domain name 2 / URL 2`.
>?If the domain name has been configured with automatic redirection, you cannot configure manual redirection for it.
>
 - Use case
Single-path redirection. For example, if you want to temporarily deactivate your web business in cases such as product sellout, page maintenance, or update and upgrade, the original page needs to be redirected to a new page. If no redirection is performed, the old address in a visitor's favorites and search engine database will return a `404/503` error message page, degrading the user experience and resulting in traffic waste.

## Automatic Redirection
CLB supports one-click forced redirection from HTTP to HTTPS.
Assume that you need to configure the website `https://www.example.com`, so that end users can visit it securely over HTTPS no matter whether they send HTTP requests (`http://www.example.com`) or HTTPS requests (`https://www.example.com`) in the browser.

### Prerequisites
The `HTTPS:443` listener has been configured.

### Directions
1. Configure the CLB HTTPS listener in the [CLB console](https://console.cloud.tencent.com/clb) and set up the web environment of `https://example.com`. For more information, see [Configuring an HTTPS Listener](https://intl.cloud.tencent.com/document/product/214/32516).
2. The result of the HTTPS listener configuration is as shown below:
![](https://main.qcloudimg.com/raw/6eaf2d1220d140bc37537f3388d78509.png)
3. On the **Redirection Configuration** tab in CLB instance details, click **Create Redirection Configuration**.
![](https://main.qcloudimg.com/raw/47fa6c0bd8b6f060332333b2685f8efe.png)
4. Select **Automatic Redirection Configuration**, select the configured HTTPS listener and domain name, and click **Next: Configure Path**.
![](https://main.qcloudimg.com/raw/4481d9beac8fa51ee7f6c252c3714a41.png)
5. Click **Submit**.
![](https://main.qcloudimg.com/raw/435e1389eadacc7bc90966480a29a131.png)
6. The result after the redirection is configured is as shown below. As you can see, the `HTTP:80` listener has been automatically configured for the `HTTPS:443` listener, and all HTTP traffic will be automatically redirected to HTTPS.
![](https://main.qcloudimg.com/raw/c3249968deb68888fb591e59289194d9.png)

## Manual Redirection
CLB supports configuring 1-to-1 redirection.
For example, your business uses a `forsale` page for a promotional campaign and needs to redirect the campaign page `https://www.example.com/forsale` to the new homepage `https://www.new.com/index` after the campaign ends.

### Prerequisites
- An HTTPS listener has been configured.
- The forwarding domain name `https://www.example.com/forsale` has been configured.
- The forwarding domain name and path `https://www.new.com/index` has been configured.


### Directions
1. Configure the CLB HTTPS listener in the [CLB console](https://console.cloud.tencent.com/clb) and set up the web environment of `https://example.com`. For more information, see [Configuring an HTTPS Listener](https://intl.cloud.tencent.com/document/product/214/32516).
2. The result of the HTTPS configuration is as shown below:
![](https://main.qcloudimg.com/raw/5c1fc217e1795a2f6a7b31c2a7ba3bfc.png)
3. On the **Redirection Configuration** tab in CLB instance details, click **Create Redirection Configuration**.
![](https://main.qcloudimg.com/raw/47fa6c0bd8b6f060332333b2685f8efe.png)
4. Select **Manual Redirection Configuration**, select the originally accessed frontend protocol port `HTTPS:443` and domain name `https://www.example.com/forsale`, select the frontend protocol port `HTTPS:443` and domain name `https://www.new.com/index` after redirection, and click **Next: Configure Path**.
![](https://main.qcloudimg.com/raw/51106736b5ee61d6e87767652185d57a.png)
5. Select `/forsale` for the original access path and `/index` for the access path after redirection, and click **Submit** to complete the configuration.
![](https://main.qcloudimg.com/raw/5f59b88ecc291d912b7faf2cf1d3770e.png)
6. The result of the redirection configuration is as shown below. As you can see, in the `HTTPS:443` listener, `https://www.example.com/forsale` has been redirected to `https://www.new.com/index`.
![](https://main.qcloudimg.com/raw/34364863bd44202df54e89ec3cb923f9.png)


