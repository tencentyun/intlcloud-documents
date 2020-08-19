CLB WAF can be bound to a CLB listener by adding a domain name to check and block HTTP or HTTPS traffic passing through the listener. Before connecting to CLB WAF, please make sure that your website business has been deployed in Tencent Cloud and public network CLB (formerly Application LB) is used for it.
>If your website business is not deployed in Tencent Cloud, you are recommended to use SaaS WAF for protection.

In order for CLB WAF to recognize the domain name to be protected, you need to configure CLB and the corresponding domain name on the listener to properly forward business requests. For more information, please see [Configuring HTTP Listeners](https://intl.cloud.tencent.com/document/product/214/32515) and [Configuring HTTPS Listeners](https://intl.cloud.tencent.com/document/product/214/32516).
This document uses protection of `wow.qcloudwaf.com` as an example to describe how to view the configuration information of a configured CLB listener.

1. Log in to the [CLB Console](https://console.cloud.tencent.com/clb) and click **Instance Management** on the left sidebar to enter the instance management page.
2. Select **Region** > **CLB Instance** to view the created CLB instance and click **Configure Listener** in the "Operation" column on its right to view the configuration.
3. On the listener configuration page, click **Listener Management** to view the domain name configuration information of the listener. In this example, the listener name is `waftest`, the listened domain name in the listener's forwarding rule is `wow.qcloudwaf.com`, and domain name protection is disabled.
