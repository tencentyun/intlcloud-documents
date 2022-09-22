## [Create CAPTCHA](id:xjyz)
1. Log in to the [Captcha console](https://console.cloud.tencent.com/captcha/graphical) and select **CAPTCHA** -> **Manage CAPTCHA** on the left navigation pane.
2. On the Manage CAPTCHA page, click **Create CAPTCHA**.
>? Up to 50 CAPTCHAs can be created in the Captcha console. You can create multiple CAPTCHAs according to different business requirements and configure different client types and security policies for each CAPTCHA. For Captcha integration process, please see [Quick Start](https://intl.cloud.tencent.com/document/product/1159/49678).

3. In the **Create CAPTCHA** pop-up window, set parameters such as CAPTCHA name according to your business requirements and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/4c04773a196a37f0ab3d755ba64c0dec.png)
4. After the CAPTCHA is created, you can view it on the Manage CAPTCHA page.
![](https://qcloudimg.tencent-cloud.cn/raw/b34c8320ef661440fd8b109f3650c415.png)
Instructions:
 - Click **Basic Configuration** to modify the CAPTCHA name and set the verification scenario, domain name, and others. For more information, please see [Basic Configuration](#jcpz).
 - Click **Appearance Configuration** to configure the CAPTCHA prompt language. For more information, please see [Appearance Configuration](#ygpz).
 - Click **Security Configuration** to update security policies such as the risk control level. For more information, please see [Security Configuration](#aqpz).
 - Click **Statistics Details** to view data such as requests, passed ticket verifications, and failed ticket verifications. For more information, please see [Statistics](#sjtj).

## [Statistics](id:sjtj)
- On the **[CAPTCHA](https://console.cloud.tencent.com/captcha/graphical)** -> **CAPTCHA Statistics** page, you can view the statistics of all CAPTCHAs.
![](https://qcloudimg.tencent-cloud.cn/raw/bc017cc74c15f80454f5315da65135bb.png)
- On the **[CAPTCHA](https://console.cloud.tencent.com/captcha/graphical)** -> **Manage CAPTCHA** page, you can go to the CAPTCHA you want to view and click **Statistics** to go to the **CAPTCHA Details** -> **Statistics** tab to view the statistics of the CAPTCHA.
  ![](https://qcloudimg.tencent-cloud.cn/raw/c898f461b84ee966689158c42cd9fa63.png)

- You can view the following metrics in the Captcha console:
<table class="tg">
<thead>
  <tr>
    <th class="tg-0pky">Metric Name</th>
    <th class="tg-0pky">Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0pky">Load requests
</td>
    <td class="tg-0pky">The number of times the client loads verification.</td>
  </tr>
  <tr>
    <td class="tg-0pky">Verification requests
</td>
    <td class="tg-0pky">The number of verifications initiated after a user responds to the verification question.</td>
  </tr>
  <tr>
    <td class="tg-0pky">Verification requests passed
</td>
    <td class="tg-0pky">The number of passed verifications.</td>
  </tr>
  <tr>
    <td class="tg-0pky">Verification requests blocked</td>
    <td class="tg-0pky">The number of blocked verification requests.</td>
  </tr>
  <tr>
    <td class="tg-0pky">Failed verifications for wrong responses</td>
    <td class="tg-0pky">The number of verifications blocked due to the wrong responses given by the user.</td>
  </tr>
  <tr>
    <td class="tg-0pky">Verifications blocked by security policies</td>
    <td class="tg-0pky">The number of verifications blocked by security policies.</td>
  </tr>
  <tr>
    <td class="tg-0pky">Requests to verify tickets
</td>
    <td class="tg-0pky">The number of ticket verifications initiated by a server.</td>
  </tr>
  <tr>
    <td class="tg-0pky">Ticket verification requests passed
</td>
    <td class="tg-0pky">The number of passed ticket verifications.</td>
  </tr>
  <tr>
    <td class="tg-0pky">Ticket verification requests blocked</td>
    <td class="tg-0pky">The number of blocked ticket verification requests.</td>
  </tr>
</tbody>
</table>

## [Security configuration](id:aqpz)
1. Log in to the [Captcha console](https://console.cloud.tencent.com/captcha/graphical) and select **CAPTCHA** -> **Manage CAPTCHA** on the left navigation pane.
2. On the Manage CAPTCHA page, select the CAPTCHA you want to configure and click **Security Configuration**.
3. On the Security Configuration tab, configure related parameters and click **Save Changes**.
    ![](https://qcloudimg.tencent-cloud.cn/raw/c80269cac802ef1af9c91a210f6330ac.png)

    Parameters:
  - **Verification Method**: Currently, only the sliding puzzle verification method can be selected.
  - **Risk Control Level**: Three risk control levels are available for you to choose from—Experience-Oriented, Balanced, and Security-Focused.
  - **Smart Verification**: You can enable or disable this feature.

## [Appearance configuration](id:ygpz)
1. Log in to the [Captcha console](https://console.cloud.tencent.com/captcha/graphical) and select **CAPTCHA** -> **Manage CAPTCHA** on the left navigation pane.
2. On the Manage CAPTCHA page, select the verification you want to configure and click **Appearance Configuration**.
3. On the Appearance Configuration tab, configure the CAPTCHA prompt language and click **Save Changes**.
    ![](https://qcloudimg.tencent-cloud.cn/raw/ac055652129a1c228fabf8cd6fda592f.png)
4. Captcha also allows you to configure the hidden help button at the time of client code integration. For more information, please see [Web Integration](https://intl.cloud.tencent.com/document/product/1159/49680).

## [Basic configuration](id:jcpz)
1. Log in to the [Captcha console](https://console.cloud.tencent.com/captcha/graphical) and select **CAPTCHA** -> **Manage CAPTCHA** on the left navigation pane.
2. On the Manage CAPTCHA page, select the CAPTCHA you want to configure and click **Basic Configuration**.
3. On the Basic Configuration tab, click **Edit** to modify the CAPTCHA name, set information such as the verification scenario and domain name, and click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/61ba4b683ee944a87ebd290848643b1d.png)

## More information
You can log in to the [Captcha console](https://console.cloud.tencent.com/captcha/graphical), and click **Quick Consulting** in the upper right corner to learn more.
