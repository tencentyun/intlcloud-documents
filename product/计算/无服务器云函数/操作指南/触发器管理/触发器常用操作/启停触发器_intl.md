You can disable a trigger to temporarily prevent a function from being triggered by an event occurring at the event source.
This can be done in the console.

## Enabling or Disabling a Trigger in the Console

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf) and select **Functions** on the left.
2. In the "Service" column at the top, select a region to view all the functions in it.
4. The list page includes the function name, monitoring information, function runtime environment, creation time, and modification time.
5. Click the function to enter the details page. It includes the following tabs.
6. Select the "Triggers" tab to enter the trigger browsing and operation interface, and enable or disable a trigger by clicking the "Enable" button for it.

## Setting the Enables/Disabled Status of a Trigger During Creation

When you create a trigger, you can set the enabled/disabled status of the trigger, and the trigger will be in the set status after created.
For example, when creating a timer trigger, if you want the trigger to take effect later as needed, you can deselect "Enable now". After the trigger is created, you can enable it by switching its enabled/disabled status.

## Precautions

At present, the enabled/disabled status switch is not supported for certain triggers, and the Enable button is not displayed for them in the console. When this is supported for them, the status and button will be displayed accordingly.
