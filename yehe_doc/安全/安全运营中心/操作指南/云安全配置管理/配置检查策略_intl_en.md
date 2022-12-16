## First login to the page

1. Log on to the [Security Operation Center Console](https://console.cloud.tencent.com/ssav2/config). In the left navigation pane, click **Cloud Security Configuration Management** -> **Configuration Check Policies** to go to the Configuration Check Policy page.
2. Initially, two cloud security configuration check policies are available:
   - Default security specification check policy on Tencent Cloud: The check policy that is built in the system and enabled by default. In this policy, all assets are checked based on all configuration check items.
   - Configuration check policy for migration for the previous version: The custom configuration check policy that is used for migration by users of the previous version. This policy is enabled by default, while the default security specification check policy on Tencent Cloud is disabled. The policy period is the same as the check time configured for the previous version. All configuration check items are enabled.

## Retrieve a policy

In the list of cloud security configuration check policies, you can view the asset check range and the list of configuration check items. You can also retrieve the required policies by searching, filtering, and sorting policies.

- **Search**
  In the upper-right corner of the list of cloud security configuration check policies, you can search for a policy by entering the keywords of a policy name.

- **Filter**
  In the list of cloud security configuration check policies, click the header "Policy Type" and "Status" to filter policies.

- **Sort**
  In the list of cloud security configuration check policies, click the header "Configuration Check Item" and "Last Checked" to sort policies.

## New configuration check policy

1. At the top of the list of [Configuration Check Policies](https://console.cloud.tencent.com/ssav2/config/strategy), click **New Policy** to go to the New Policy page.
2. On the New Policy page, customize the basic information, asset check range, and configuration check items for the check policy.

- **Basic Info**
  Policy name, policy check period, and policy check time are required fields. Multiple items can be selected for the policy check period.

- **Asset check range**
  You can filter/search assets by the keyword of asset group, project, asset type, and asset name. All assets should be checked by default. It is also acceptable not to set any assets for this configuration check policy.

- **Configuration check items** 
    - You can search check items by the keywords of configuration requirements. At least one configuration check item must be checked. The Configuration Requirement column cannot be left empty.
    - Below the list of configuration check items, you can enable or disable the "Send a notice after check" option. If you enable the "Send a notice after check" option, you must select the account (primary account and sub-accounts) for receiving the notice.

  > ?
  > - Once the "Send a notice after check" option is enabled, the system will send SMS, email, and inmail to the preset account after the policy is executed. The content of notice includes the check policy name, check completion time, and statistics of check results. You can click the link in the notice to view full check results.
  > - Before selecting a sub-account, click the Refresh button ![](https://qcloudimg.tencent-cloud.cn/raw/b02e145719908ef376840df3b5b1abfb.png) to refresh the sub-account drop-down list.

3. After the above three items are set, click **OK**. The new configuration check policy, which is enabled by default, appears in the list of configuration check policies.

## Manage configuration check policies

> ? The enabled configuration check policies cannot be edited and deleted.

- **Edit a policy**
  In the list of [Configuration Check Policies](https://console.cloud.tencent.com/ssav2/config/strategy), click **Edit** in the Operation column to re-edit the basic information, asset check range, and configuration check items of this policy. Then click **OK** to save your changes.

- **Delete a policy**
  In the list of [Configuration Check Policies](https://console.cloud.tencent.com/ssav2/config/strategy), click **Delete** in the Operation column. The policy is deleted after you confirm them in the confirmation prompt box.

- **Enable configuration check policy**
  In the list of [Configuration Check Policies](https://console.cloud.tencent.com/ssav2/config/strategy), click ![](https://qcloudimg.tencent-cloud.cn/raw/b3c12b2ba7f0234f58427ae12146f25c.png) to enable the policy. Then you can perform configuration check by using the enabled policy on the [Configuration Check Results](https://console.cloud.tencent.com/ssav2/config/result) page.

- **Execute a configuration check policy**

1.  In the list of [Configuration Check Policies](https://console.cloud.tencent.com/ssav2/config/strategy), click **Check Now** in the Operation column to perform configuration check as per the preset configuration requirements.

2.  During the check, all buttons for the policy are grayed out, and the "Last Checked" column displays "Checking". At the end of the check, a prompt "Operation successful" pops up on this page, and the "Last Checked" column displays the time when the check ended.
