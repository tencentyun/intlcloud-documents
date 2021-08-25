
## Overview
IoT Hub provides the multi-level device grouping feature to meet your needs for managing devices under different products by group in different business scenarios. You can:
- Add, delete, modify, and query groups.
- Add devices under different products or the same product to a group.
- Add subgroups under a group or subgroup.
- Query the list of devices in a group.

This document describes how to group devices in the console.

## Directions
### Creating group
1. Log in to the [IoT Hub console](https://console.cloud.tencent.com/iotcloud) and click **[Groups](https://console.cloud.tencent.com/iothub/groups)** on the left sidebar.
2. On the group management page, click **Create Group**.
3. In the group adding pop-up window, enter relevant information. When creating a group, you need to select the group to which it belongs. A level-1 group always belongs to the default project, a level-2 group can belong to a level-1 group, a level-3 group can belong to a level-2 group, and so on. You can customize the group name and description.
 - Parent Group: there is no limit on the number of group levels. One group can have up to 100 subgroups. 
 - Group Name: it can contain 4–30 letters, digits, and underscores. 
 - Group Description: it can contain up to 255 characters.
![](https://main.qcloudimg.com/raw/822eff73b1d905374a22d5fc4777f071.png)
4. Click **Confirm**.



### Viewing group
1. Log in to the [IoT Hub console](https://console.cloud.tencent.com/iotcloud).
2. Click **[Groups](https://console.cloud.tencent.com/iothub/groups)** on the left sidebar to view the group list, where you can manage, edit, and delete groups.
3. View the basic information of a group displayed in the console, including:
 - Group Name: it is customizable.
 - Group ID (groupID): it is randomly assigned by the backend and is the unique group identifier.
 - Group Description: it is customizable and describes the group.
 - Devices: it indicates the total number of devices in the group.
 - Included Subgroups: it indicates the total number of subgroups in the group.
 - Creation Time: it indicates the time the group was created in the console or through APIs, accurate to the second.



### Managing group
1. Log in to the [IoT Hub console](https://console.cloud.tencent.com/iotcloud).
2. Click the group name to enter the group management page, where you can manage the device list.
3. To add one or more devices to the group, click **Add Device** under the device list. You can search for devices by product name or device name and select different devices for batch adding.
![](https://main.qcloudimg.com/raw/40dc34c9452ab5565dc83c66a45b7f39.png)
4. The device list displays the information of the devices in the group (e.g., floor1), including device name, status, product, and last connection time and operation.
 - Device Name: `devicename`.
 - Status: online/offline status of the device.
 - Product: name of the product to which the device belongs.
 - Login Time: last connection time of the device, accurate to the second. "-" will be displayed if the device has never been connected.
 - Click **Manage** in the **Operation** column to enter the device details page of the corresponding device.
 - Click **Remove** in the **Operation** column to remove the device from the group. **This operation will not delete the device**.
5. You can add subgroups to or remove subgroups from any group. Click the group name to enter the group management page, where you can manage the subgroup list.
 - Just like under parent groups, you can create subgroups under subgroups and add devices to them.
 - As regards the group level, if the group is a level-1 group, only the name of the level-1 group is displayed; if it is a level-n group, the names of the n levels of groups are displayed, such as `group1` and `group1/group2.../groupn`.
![](https://main.qcloudimg.com/raw/1bea0d0fb73de0ffecc7a5b9bede8471.png)
