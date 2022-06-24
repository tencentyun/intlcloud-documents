This document describes the tamper protection feature of WAF. It is used to protect core static webpages. By caching pages and locking access requests, it protects your website from being affected by malicious tampering with your real server pages. In addition, you can also configure tamper protection rules as needed.
## Overview
With the tamper protection feature, you can add protection rules to protect core webpages from being tampered with as needed. You can refresh the protected pages, during which WAF will update them to ensure that they are the same as those on the real server. Moreover, you can also choose whether to retain rule hit logs to analyze hit conditions.
>?CLB WAF doesn't support the tamper protection feature. For more information on detailed specifications, see [Billing Overview](https://intl.cloud.tencent.com/document/product/627/47799).

## Prerequisites
You have [added a protected domain name](https://intl.cloud.tencent.com/document/product/627/35651) to SaaS WAF, and ensured the domain name is in normal protection.

## Adding Rules
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-overview) and select **Configuration Center** > **Basic Security** on the left sidebar.
2. On the basic security page, select the target domain name in the top-left corner and click **Web tamper protection**.
3. On the tamper protection page, click **Add rule**, and the rule adding window will pop up.
![](https://qcloudimg.tencent-cloud.cn/raw/2abfe833bf51f45eb083c23c503cb7cf.png)
4. In the pop-up window, configure relevant fields and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/92666566e9d7b266590491e947d29d2a.png)

**Field description:**
 - Rule name: Tamper protection rule name of up to 50 characters. You can search for rules by name in attack logs.
 - Page path: Path of the page to be protected from tampering. You need to enter a specific URL rather than a path.

>?
>- The specified page is limited to static resources such as .html, .shtml, .txt, .js, .css, .jpg, and .png.
>- After the rule is added, when a user accesses this page for the first time, WAF will cache the page, and subsequent access requests will be directed to the WAF-cached page.

5. After the tamper protection rule is added, it will be enabled by default.

## Searching Rules
1. On the [basic security page](https://console.cloud.tencent.com/guanjia/tea-baseconfig), select the target domain name in the top-left corner and click **Tamper Protection**.
2. On the tamper protection page, click the search box to filter rules by keywords such as rule ID, rule name, and protection path.
![](https://qcloudimg.tencent-cloud.cn/raw/3dc6c0507d5823abaed843dd77ea351d.png)

## Editing Rules
1. On the [basic security page](https://console.cloud.tencent.com/guanjia/tea-baseconfig), select the target domain name in the top-left corner and click **Web tamper protection**.
2. On the tamper protection page, select the target rule, click **Edit** in the **Operation** column, and the rule editing window will pop up.
![](https://qcloudimg.tencent-cloud.cn/raw/bb99a6ad165d82ba8e156a03133f3659.png)
3. In the pop-up window, modify relevant parameters and click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/6667cfc616e84f37be27b9c10f2dbee7.png)
4. After the protected page is updated, click **Refresh** to cache the updated page to WAF.

## Deleting Rules
1. On the [basic security page](https://console.cloud.tencent.com/guanjia/tea-baseconfig), select the target domain name in the top-left corner and click **Web tamper protection**.
2. On the tamper protection page, select the target rule, click **Delete** in the **Operation** column, and the deletion confirmation window will pop up.
![](https://qcloudimg.tencent-cloud.cn/raw/7a7621b720526166210dfdf3d2ee06f9.png)
3. In the pop-up window, click **Delete**.
>?Once deleted, it cannot be restored and takes effect only after being added again.
