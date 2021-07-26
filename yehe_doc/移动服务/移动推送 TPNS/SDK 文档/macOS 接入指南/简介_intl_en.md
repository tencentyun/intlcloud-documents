
Pushing messages to macOS devices involves client app, Apple Push Notification service (APNs), and TPNS sever (TPNS Provider). They need to collaborate throughout the entire process to successfully push messages to the client. An exception from any of them can lead to a failure to push messages.

## File Composition
-  XG_SDK_Cloud_macOS.framework (primary SDK file)
-  XGMTACloud_macOS.framework ("click report" component)

## Update Description
- Supports macOS v10.8 and later.
- For macOS v10.14 and later:
 - You need to introduce `UserNotification.framework`.
 - You are advised to use Xcode v10.0 or later.

## Key Features
TPNS SDK for macOS contains APIs for clients to implement message push. They are mainly used to:
- Get and register device tokens automatically to facilitate integration.
- Bind accounts, tags, and devices, so you can push messages to specific user groups and have more push methods.
- Report the number of clicks, i.e., how many times a message is clicked by users.

### Differences between TPNS SDKs for macOS and iOS

- Feature Differences 
>! TPNS SDK for macOS does not provide the following features because they are not officially supported by Apple.
>
<table>
<thead>
	<tr><th>Feature</th><th>iOS</th><th>macOS</th><th>Description</th></tr>
</thead>
<tbody>
	<tr>
		<td>Notification extension plugin</td><td>✓</td><td>×</td><td>TPNS SDK for macOS does not support the notification extension plugin, rich media notifications, and offline reach statistics.</td>
	</tr>
	<tr><td>Custom notification sounds</td><td>✓</td><td>×</td><td>TPNS SDK for macOS does not support custom notification sounds.</td></tr>
	<tr><td>Silent messages</td><td>✓</td><td>×</td><td>TPNS SDK for macOS does not support silent messages.</td></tr>
	<tr><td>Notification grouping</td><td>✓</td><td>×</td><td>TPNS SDK for macOS does not support notification grouping.</td></tr>
</tbody>
</table>
- TPNS SDK for iOS is recommended for apps built with Mac Catalyst.
- `DeviceToken` cannot be obtained in the Big Sur (v11.3 or earlier) production environment.
This is a bug of Big Sur and has been fixed in v11.4.
