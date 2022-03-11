## Overview

After creating a product, you can configure the topics that its devices can publish or subscribe to. The device topic list is inherited from the product topic list. You can add, delete, or modify the topic list only at the product level.

## Directions

### Adding a custom topic

1. Log in to the [IoT Hub console](https://console.cloud.tencent.com/iotcloud) and click **Products** on the left sidebar.
2. Click a product name, and select **Topics**.
3. Click **Add Custom Topic** and set the operation name and permission.
	- Operation Name: the name can contain 1–255 letters, digits, and underscores, where different levels are separated by `/`, and `+` indicates a level. The name should be in the format of `/+/name` rather than `/+aaa/`.
	- Permission: you can select **Subscribe**, **Publish**, or **Subscribe and publish**, and the selected permission can be changed subsequently.

![]()

### Editing a custom topic

Click **Edit** in the topic permission list to modify the name of the corresponding topic permission and the permission itself.
![]()

### Deleting a topic permission

Click **Delete** in the topic permission list to delete the corresponding topic permission.



