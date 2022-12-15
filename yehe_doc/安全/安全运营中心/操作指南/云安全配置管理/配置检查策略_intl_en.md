
## First login to the page
1. Log on to the [Security Operation Center Console](https://console.cloud.tencent.com/ssav2/config). In the left navigation pane, click **Cloud Security Configuration Management** -> **Configuration Check Policies** to go to the Configuration Check Policy page.
2. Initially, two cloud security configuration check policies are available:
   - Default security specification check policy on Tencent Cloud: The check policy that is built in the system and enabled by default. In this policy, all assets are checked based on all configuration check items.
   - Configuration check policy for migration for the previous version: The custom configuration check policy that is used for migration by users of the previous version. This policy is enabled by default, while the default security specification check policy on Tencent Cloud is disabled. The policy period is the same as the check time configured for the previous version. All configuration check items are enabled.
    ![](https://qcloudimg.tencent-cloud.cn/raw/0efdbeb9b411e46454409f872f304ba1.png)
	
## Retrieve a policy
In the list of cloud security configuration check policies, you can view the asset check range and the list of configuration check items. You can also retrieve the required policies by searching, filtering, and sorting policies.
- **Search**
In the upper-right corner of the list of cloud security configuration check policies, you can search for a policy by entering the keywords of a policy name.
![](https://qcloudimg.tencent-cloud.cn/raw/9deb3f392dc77bbe7052d80a92b304f0.png)
- **Filter**
In the list of cloud security configuration check policies, click the header "Policy Type" and "Status" to filter policies.
![](https://qcloudimg.tencent-cloud.cn/raw/0f72c1b12f558b5b0cabe116de2e5697.png)
- **Sort**
In the list of cloud security configuration check policies, click the header "Configuration Check Item" and "Last Checked" to sort policies.
![](https://qcloudimg.tencent-cloud.cn/raw/d59d42db1cee4aad19e7606d7d0b4c43.png)

## New configuration check policy
1. At the top of the list of [Configuration Check Policies](https://console.cloud.tencent.com/ssav2/config/strategy), click **New Policy** to go to the New Policy page.
2. On the New Policy page, customize the basic information, asset check range, and configuration check items for the check policy.
 - **Basic Info**
Policy name, policy check period, and policy check time are required fields. Multiple items can be selected for the policy check period.
![](https://qcloudimg.tencent-cloud.cn/raw/3ea2e7133b603e7bf588b31fe0a78eff.png)
 - **Asset check range**
You can filter/search assets by the keyword of asset group, project, asset type, and asset name. All assets should be checked by default. It is also acceptable not to set any assets for this configuration check policy.
![](https://qcloudimg.tencent-cloud.cn/raw/3eba602e4db0ead81b6c26dd6c0b7320.png)
 - **Configuration check items**
    1. You can search check items by the keywords of configuration requirements. At least one configuration check item must be checked. The Configuration Requirement column cannot be left empty.
   ![](https://qcloudimg.tencent-cloud.cn/raw/d68034329e3823c49df3b2cfd52171cf.png)
    2. Below the list of configuration check items, you can enable or disable the "Send a notice after check" option. If you enable the "Send a notice after check" option, you must select the account (primary account and sub-accounts) for receiving the notice.
>?
>- Once the "Send a notice after check" option is enabled, the system will send SMS, email, and inmail to the preset account after the policy is executed. The content of notice includes the check policy name, check completion time, and statistics of check results. You can click the link in the notice to view full check results.
>- Before selecting a sub-account, click the Refresh button ![](https://qcloudimg.tencent-cloud.cn/raw/b02e145719908ef376840df3b5b1abfb.png) to refresh the sub-account drop-down list.

![](https://qcloudimg.tencent-cloud.cn/raw/679d307cf76c7da74cb767b2639d16b8.png)
3. After the above three items are set, click **OK**. The new configuration check policy, which is enabled by default, appears in the list of configuration check policies.

## Manage configuration check policies
>? The enabled configuration check policies cannot be edited and deleted.

- **Edit a policy**
In the list of [Configuration Check Policies](https://console.cloud.tencent.com/ssav2/config/strategy), click **Edit** in the Operation column to re-edit the basic information, asset check range, and configuration check items of this policy. Then click **OK** to save your changes.
![](https://qcloudimg.tencent-cloud.cn/raw/c102baf47c2a95f365db818acf3ed455.png)
- **Delete a policy**
In the list of [Configuration Check Policies](https://console.cloud.tencent.com/ssav2/config/strategy), click **Delete** in the Operation column. The policy is deleted after you confirm them in the confirmation prompt box.
![](https://qcloudimg.tencent-cloud.cn/raw/8850a5cd7a2683d7df6960a33042387f.png)
- **Enable configuration check policy**
In the list of [Configuration Check Policies](https://console.cloud.tencent.com/ssav2/config/strategy), click ![](https://qcloudimg.tencent-cloud.cn/raw/b3c12b2ba7f0234f58427ae12146f25c.png) to enable the policy. Then you can perform configuration check by using the enabled policy on the [Configuration Check Results](https://console.cloud.tencent.com/ssav2/config/result) page.
![](https://qcloudimg.tencent-cloud.cn/raw/4af1487e31b69df241a0b7a7a59ff946.png)
- **Execute a configuration check policy**
 1. In the list of [Configuration Check Policies](https://console.cloud.tencent.com/ssav2/config/strategy), click **Check Now** in the Operation column to perform configuration check as per the preset configuration requirements.
![](https://qcloudimg.tencent-cloud.cn/raw/6aa91d22304c2e0d1520015be8976fd8.png)
 2. During the check, all buttons for the policy are grayed out, and the "Last Checked" column displays "Checking". At the end of the check, a prompt "Operation successful" pops up on this page, and the "Last Checked" column displays the time when the check ended.
 ![](https://qcloudimg.tencent-cloud.cn/raw/070d0d918315dc39561d76d98f507360.png)