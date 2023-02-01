You can disable a trigger to temporarily prevent a function from being triggered by an event occurring at the event source. This document describes how to do so in the console.

## Enabling or Disabling a Trigger in the Console
1. Log in to the SCF console and select **[Functions](https://console.cloud.tencent.com/scf/list)** on the left sidebar.
2. At the top of the **Functions** page, select the region and namespace where the function resides as shown below: 
![](https://staticintl.cloudcachetci.com/yehe/backend-news/wnBG038_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219142236.png)
3. Click the function name to enter the function details page.
4. Select **Trigger management** on the left to enter the trigger browsing and operation page. Click <img src="https://main.qcloudimg.com/raw/707031668bf900e6e1543ff08cecbae7.png" style="margin:-6px 0px"> in the status of the target trigger to enable or disable it as shown below: 
![](https://staticintl.cloudcachetci.com/yehe/backend-news/6U3n680_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219162032.png)

## Setting the Enables/Disabled Status of a Trigger During Creation

When you create a trigger, you can set its enabled/disabled status, and the trigger will be in the set status once created.
For example, when creating a timer trigger, if you want the trigger to take effect later as needed, you can deselect **Enable now** as shown below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/5UyC937_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219162136.png)
After the trigger is created, you can enable it by switching its enabled/disabled status.

## Notes

At present, the enabled/disabled status switch is not supported for certain triggers, and the **Enable** button is not displayed for them in the console. When this is supported for them subsequently, the status and button will be displayed accordingly.
