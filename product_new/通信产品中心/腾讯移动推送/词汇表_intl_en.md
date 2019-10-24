# Glossary

## Application List
<hr>

- ACCESS ID: This is the unique identifier of an app and cannot be modified. It needs to be configured in client SDK and also provided when a backend API is called.

- ACCESS KEY: This is the client authentication key, which is used together with the Access ID to verify if the call is valid. It needs to be configured in client SDK and cannot be modified.


## Creating a push
<hr>

- Push content: The message command is the code that is received and executed by the app. The specific code format is defined by the app developer. By using the message command, you can remotely control the activities of the app, such as: downloading apps and changing the flickering screen, modifying item prices in mobile games, and silently updating text or images in apps.

- Immediate/scheduled push: Immediate push is suitable for push testing. Scheduled push is often used for official external push.

- Additional parameters: You can also set custom key-value pairs to meet your custom needs.

- Offline push retention: If a user is offline, he can still receive the push notification when getting online next time before the pre-set expiration time. Otherwise, the push notification will expire and the user will no longer receive it. For events that do not have time limit, we strongly recommend that you retain the push for 72 hours.

- Time control: Set the time period during which a user can receive the push notification. This allows you to avoid disturbing the user at night, and indicate a specified time when the user can receive the push.

- Action after the notification click: This is to set the response action after the user clicks on the push notification, which includes directly launching the app, jumping to a specified function page of the app, or opening a URL using the browser.

- Multi-package push: In multi-package push mode, all apps on the device that register for the push service with this access_id will receive the message. This feature is used to differentiate apps from different channels and with different package names.

## Push Records
<hr>

- Message ID: The ID of the push job.

- Push time: The time when the push starts.

- Target devices: This indicates the number of pushes sent within the past 30 days to devices that were connected to the server. If offline retention is configured for the message, the number of effective pushes will increase numerically over time as users go online, which means that users who just get online also receive this push.


## Push Data
<hr>

- Planned push count: This indicates the number of pushes sent within the past 30 days to devices that were connected to the server. If offline retention is configured for the message, the number of effective pushes will increase numerically over time as users go online, which means that users who just get online also receive this push.

- Online device count: The number of devices connected to the server when the push is still valid (messages can be successfully pushed only after the device is connected to the server).

- Device arrival count: The number of users to whom this push is successfully sent. Real-time data has a delay of around 5 minutes.

- Display count: The number of messages that are displayed, checked by calling the system's message display API.

- Click count: The number of clicks on a message that is successfully pushed. The device needs to call a specific function to report the number of clicks.

- Clear count: The number of messages that are cleared, checked by calling the system’s message clearing API.


## My Tags
<hr>

- Tag: This refers to tags set for a certain user or a group of users. Custom tags can be configured through client or server calls and then used at the frontend.

- Advanced data tag: TPNS sets tags for specific users directly by sorting data. Advanced tags are for use only and cannot be edited or deleted.