TPNS is a professional mobile app push platform that can deliver tens of billions of notifications/message in a matter of seconds. It now fully supports both Android and iOS systems. It can be used easily through the embedded SDK, API calls, and web-based visual console to push to specific users, greatly improving user activity and effectively waking up inactive users. In addition, it features display of real-time push effect data.

## How TPNS Works

![](https://main.qcloudimg.com/raw/ab62c06066342300aaac01b3f281bf72.png)

**Below are the steps for the Android client to implement the push process (with no vendor-specific channels):**


- When the client app starts, it will start a TPNS master service, which is globally unique and shared on one device.

- The TPNS master service randomly starts a slave service in the app accessing TPNS, both of which keep each other alive and work as the backup of each other.

- The TPNS master service establishes a socket-based persistent connection with the TPNS server and maintains the connection through heartbeat and other mechanisms.

- The master service on the client requests a token from the TPNS server via the socket-based persistent connection.

- The TPNS server pushes the message to the master service on the client via the socket-based persistent connection.

- The master service forwards the push message to the corresponding client app.


**Below are the steps for the Android client to implement the push process (with vendor-specific channels):**


- Send the registration request to the third-party vendor service to request the token.

- Save the third-party token and sync it to the TPNS server.

- Map the third-party token to the TPNS token and save the mapping.

- The TPNS server calls the third-party push API to push the message to the third-party server based on the token mapping.

- The third-party server pushes the message to the client app.

## Overview of Main Features

The Android SDK contains the APIs provided by TPNS for message push implementation.  
It is mainly responsible for:

* Providing two types of push (notification and message) for easy use;
* The binding of account, tag, and device, so that you can implement message pushes to specific user groups for diversified push methods;
* Reporting taps, i.e., the number of times the messages are tapped by users.
* Providing two types of push (notification and message) for easy use;
* Providing multi-vendor channel integration for easy integration with multi-vendor push services.



