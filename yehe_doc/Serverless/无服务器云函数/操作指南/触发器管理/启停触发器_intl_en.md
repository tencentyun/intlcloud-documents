You can disable a trigger to temporarily prevent a function from being triggered by an event occurring at the event source.
This can be done in the console.

## Enabling/Disabling Trigger in Console
1. Log in to the SCF Console and select **[Functions](https://console.cloud.tencent.com/scf/list)** on the left sidebar.
2. At the top of the "Functions" page, select the region and namespace where the function for which to enable/disable a trigger resides.
The function list contains the function name, monitoring information, runtime environment, creation time, and modification time.
3. Click the function name to enter the function details page.
The function details page contains the function configuration, function code, triggers, logs, and monitoring tabs.
4. Select the **Triggers** tab to enter the trigger browsing and operation page.
5. Click <img src="https://main.qcloudimg.com/raw/707031668bf900e6e1543ff08cecbae7.png" style="margin:-3px 0px"> in the top-right corner of the desired trigger to switch the enabled/disabled status of the trigger.


## Setting the Enables/Disabled Status of Trigger During Creation

When you create a trigger, you can set its enabled/disabled status, and the trigger will be in the set status once created.
For example, when creating a timer trigger, if you want the trigger to take effect later as needed, you can deselect "Enable Now". After the trigger is created, you can enable it by switching its enabled/disabled status.

## Notes

At present, the enabled/disabled status switch is not supported for certain triggers, and the "Enable" button is not displayed for them in the console. When this is supported for them subsequently, the status and button will be displayed accordingly.
