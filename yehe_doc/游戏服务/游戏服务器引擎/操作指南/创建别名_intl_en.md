## Overview

This document describes how to create an alias to abstract the name of a fleet. By using an alias instead of a specific fleet ID, you can change the server fleet associated with the alias to switch player traffic from one fleet to another fleet more easily and seamlessly for zero downtime updates.


## Prerequisites

You have completed the [GSE Application Form](https://intl.cloud.tencent.com/apply/p/k0b6pvbhs6) and your application has been approved.

## Directions

1. Log in to the [GSE Console](https://console.cloud.tencent.com/gse/asset) and click **Alias** on the left sidebar.
2. Click **Create** in the top-left corner.
3. In the alias creation page, enter information such as the name, type, and description, and click **OK**.
   - **Name**: enter the alias name for easy identification in the directory.
   - **Type**: select the alias type in the drop-down list. The types include common alias and terminal alias.
     - Common alias: it points to a fleet, under which the system automatically finds servers and assigns them to clients. If you select common alias, you need to associate an available server fleet.
     ![](https://main.qcloudimg.com/raw/ac9effb90c3a4e1fba7ae6ba1ea3639e.png)
     - Terminal alias: it doesn't point to a fleet. You can describe the reason why the alias cannot be used in **Termination Info**, which will be sent to clients.
     ![](https://main.qcloudimg.com/raw/5a2cb7b406586b193bf3bf3f914edb24.png)
   - **Associate Server Fleet**: select the server fleet to be associated with if "Type" is "Common alias".
   - **Termination Info**: enter the information to be displayed to players if "Type" is "Terminal alias".
   - **Description**: enter a short description of the alias for easy identification.
4. After the alias is successfully created, you can modify or delete it or perform other operations on it on the alias page.

