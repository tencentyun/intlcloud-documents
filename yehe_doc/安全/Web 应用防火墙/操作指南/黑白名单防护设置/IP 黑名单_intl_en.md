## Adding IPs to Blocklist
#### Adding IPs manually
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-iplist) and select **Configuration Center** > **Blocklist/Allowlist** on the left sidebar.
2. On the blocklist/allowlist page, select a target domain name in the top-left corner and click **IP blocklist**.
3. On the IP blocklist page, click **Add address**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/f50d10ebc99b7edf684efebca33beb03.png" style="zoom:67%;" />
4. On the page that appears, configure relevant parameters and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/eac1efdd96cd0a31445cf2064277eeaa.png)

**Field description:**
 - **IP address:** IP address such as `10.0.0.10` or `FF05::B5`. CIDR blocks are supported, such as `10.0.0.0/16` or `FF05:B5::/60`. You can enter up to 20 items and separate them with line breaks.
>?
>- If you select **All** for the domain name, the added IP address or range will be blocked/allowed globally.
>- The domain name quotas in each edition are as follows: Premium Edition: 1,000 entries/domain name; Enterprise Edition: 5,000 entries/domain name; Ultimate Edition: 20,000 entries/domain. Each IP address or range occupies one entry in the quota.

 - **Expiration time:** **Never expire** or a specified date.
 - **Remarks:** Custom remarks, which can contain up to 50 characters.

#### Importing IPs
1. On the [blocklist/allowlist page](https://console.cloud.tencent.com/guanjia/tea-iplist), select a target domain name in the top-left corner and click **IP blocklist**.
2. On the IP blocklist page, click **Import data** > **Import**. After the data is parsed successfully, click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/b771886aec2788cb271e2113c3707ca5.png)

## Editing IP Blocklist
1. On the [blocklist/allowlist page](https://console.cloud.tencent.com/guanjia/tea-iplist), select a target domain name in the top-left corner and click **IP blocklist**.
2. On the IP blocklist page, select a target IP address, click **Edit** in the **Operation** column, modify the expiration time and remarks, and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/c19dc972b7dc939f39952a7ebf0fcc70.png)

## Deleting IPs from IP Blocklist
1. On the [blocklist/allowlist page](https://console.cloud.tencent.com/guanjia/tea-iplist), select a target domain name in the top-left corner and click **IP blocklist**.
2. You can delete one, multiple, or all IP addresses on the IP blocklist page as follows:
 - One: Select an IP address and click **Delete address** or **Delete** in the **Operation** column. A window will pop up to ask you to confirm the deletion operation.
>? Once deleted, it cannot be restored and can take effect only after being added again.

![](https://qcloudimg.tencent-cloud.cn/raw/cdddda6314ccbaa7963ad01cd1e34705.png)

 - Multiple: Select multiple IP addresses and click **Delete address**. A window will pop up to ask you to confirm the deletion operation.
>? Once deleted, it cannot be restored and can take effect only after being added again.

![](https://qcloudimg.tencent-cloud.cn/raw/36c7b77ff8673d295e2701c22aabdaeb.png)

 - All: Click **Delete all**. A window will pop up to ask you to confirm the deletion operation.
>! This operation will clear all IP blocklist/allowlist information under the current domain name. Therefore, proceed with caution. Once deleted, the addresses cannot be restored and can take effect only after being added again.

3. In the pop-up window, click **OK**.

## Exporting All Filtered Results
1. On the [blocklist/allowlist page](https://console.cloud.tencent.com/guanjia/tea-iplist), select a target domain name in the top-left corner and click **IP blocklist**.
2. On the IP blocklist page, click the search box to filter IPs by **IP address** or click **Source** to filter IPs by source type.
![](https://qcloudimg.tencent-cloud.cn/raw/583edaeb01b1a0b788aa6306574f361c.png)
3. After filtering required IPs, click **Export all**.
![](https://qcloudimg.tencent-cloud.cn/raw/8162577876e0d42c70e9e47890d3f86d.png)