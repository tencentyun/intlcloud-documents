## Overview
The leak protection feature replaces the sensitive information returned in your web pages, such as mobile numbers and ID numbers.

## Configuration samples
1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia), and click **Web Application Firewall** > **Defense settings** in the left sidebar. In the domain name list, select the domain name of the site you want to protect. In the **Operation** column on the right, click **Defense configuration** to enter the details page, and select **Leak Resistance**>**Add a Rule**.
 ![](https://main.qcloudimg.com/raw/81b323e8ea975d00ea28b01af8942c01.png)
2. In the “Add leak resistance rule” page, enter the rule name, add a condition by selecting “Sensitive info” for **Field**, “includes” for **Condition**, and “ID card” or “Mobile” for **Content**, select an action, “Replace” or “Observe”, and then click **Confirm**.
![](https://main.qcloudimg.com/raw/8bfe246a997d4a4941e4fab0e9f651a6.png)
3. Once the rule takes effect, it will begin protecting the sensitive information returned in your web pages as shown in the example below (demo content):
 - **Before protection:**
![Before protection](https://mc.qcloudimg.com/static/img/a1f9740fafcf3f8913cc5d5c3370e7f7/image.png)
 - **After protection:**
![After protection](https://mc.qcloudimg.com/static/img/6a738492711125c684fa0f132ba74250/image.png)

[Previous: Custom Rules](https://intl.cloud.tencent.com/document/product/627/11711)
[Next: Region Blocking](https://intl.cloud.tencent.com/document/product/627/14704)

