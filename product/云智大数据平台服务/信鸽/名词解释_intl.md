# Metrics Descriptions

## List of Apps
<hr>

- Connected devices yesterday: The number of devices that were successfully connected to the TPNS server yesterday.

- Uninstalled devices yesterday: The number of devices on which the app was uninstalled yesterday. TPNS can count the actions of uninstalling the app and reports every single uninstallation, so the number of devices here is not deduplicated.

- Valid devices: The number of devices currently registered with TPNS.

## App Configuration
<hr>

- App package name: It is the package name of the app used for AndroidManifest.xml configuration, such as com.tencent.news. Push operations can be performed only after the app package name is entered, which cannot be modified once entered for security reasons.

- Admin: All admins have the same permissions. One admin can delete other admins but not themself. If you want to transfer an admin, it is recommended to add a new one and then use the new admin account to delete the old account to complete the transfer.

- Test device: It is used to test push conditions on the specific device to make sure everything works as expected before pushing real messages. The ID of the test device is DeviceToken, which can be obtained through logcat. For details, see the developer manual.

- ACCESS KEY: It is the client authentication key, which verifies together with the Access ID to determine that the call is valid. It needs to be configured into the client SDK and cannot be modified.

- SECRET KEY: It is used to verify together with the APPKEY to determine that the API call is valid. If it is disclosed, you need to replace with a new one and reconfigure the client SDK immediately.

- ACCESS ID: It is the unique identifier of an app, which cannot be modified and needs to be configured into the client SDK. It has to be provided when a backend API is called.

## Creating a Push
<hr>

- Push content: The message command is the code that is run after received by the app. The specific code form is defined by the app developer. Using the message command, you can remotely control various behaviors of the app, such as downloading the app and changing the splash screen, modifying item prices in a mobile game, or silently updating in-app text or image content.

- Immediate/scheduled push: Immediate push is more suitable for test push. Scheduled push is mostly used for formal push.

- Custom parameter: You can also set custom key-value pairs to implement custom requirements based on different key-value pairs.

- Offline retention: If the user is offline, they can receive the push when they go back online. You need to set an offline storage expiration time, and if the user is still offline after the expiration time, they will not receive this push. If it is not for a limited-time offer, it is highly recommended to retain the push for 72 hours!

- Time period control: This is to set the time period during which the user can receive the push, so that you can avoid disturbing the user at night, or allow the user to receive the push only in a specific time period.

- Action for notification tap: This is to set the response action after the user taps the notification, which can be launching the app directly, jumping to a specified function page of the app, or opening a URL using the browser.

- Multi-package name push: In multi-package name prompt mode, all apps on the device that use this access_id to register the push service will receive the message. This feature is used to differentiate apps with different channels and package names.

## Push List
<hr>

- Push list: It displays the data of full/batch push (broadcast), but not the data of peer-to-peer (unicast) push. To view unicast push, go to the "Push data" page.

- Push time: The time to start this push.

- Android effective pushes: It refers to the amount of pushes sent to currently online devices (i.e., the devices connected to the server). If offline retention is set for the message, the amount of effective pushes will increase numerically over time as users go online, indicating that subsequent online users also receive this push.

- iOS effective pushes: It refers to the amount of pushes successfully sent to Apple's server. TPNS is responsible for successfully pushing the message to Apple's server, but due to Apple's server restrictions, the amount of arrivals cannot be counted.

- Arrivals: The number of users to whom this push is successfully sent. Real-time data collection has a delay of around 5 minutes.

- Undo scheduled task: This is to undo the scheduled push that has not yet occurred; after that, the push will not be executed.

- Delete offline message: This is to delete the offline message which is retained in the backend and will be sent. After the offline message is successfully deleted, the message will not be sent. However, messages that have already been successfully sent cannot be deleted.

## Push Data
<hr>

- Android effective pushes: It refers to the amount of pushes sent to currently online devices (i.e., the devices connected to the server). If offline retention is set for the message, the amount of effective pushes will increase numerically over time as users go online, indicating that subsequent online users also receive this push.

- iOS effective pushes: It refers to the amount of pushes successfully sent to Apple's server. TPNS is responsible for successfully pushing the message to Apple's server, but due to Apple's server restrictions, the amount of arrivals cannot be counted.

- Arrivals: The number of users to whom this push is successfully sent. Real-time data collection has a delay of around 5 minutes.

- Arrival rate: Arrivals/pushes × 100%

- Taps: The number of taps on the message after successfully pushed. The device needs to call a specific function to report the taps.

- Tap rate: Taps/arrivals × 100%

## Basic Data
<hr>

- Daily new devices: The number of devices newly registered today. The client SDK V2.3.6 or higher needs to be integrated.

- Daily uninstalled devices: The number of devices on which the app is uninstalled today. The client SDK V2.3.6 or higher needs to be integrated.

- Daily connected devices: The number of devices connected to the TPNS server today.

## My Tags
<hr>

- Tag: It usually refers to labeling a user or a group of users. Custom tags can be set by calling the client or server and then used in the frontend.

- Advanced data tag: It means that TPNS directly labels specific users by sorting data. Advanced tags are for use only and cannot be edited or deleted.
