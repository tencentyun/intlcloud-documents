## Overview

**Choice** is a branch selection statement. Similar to if-else, it is used to execute actions by condition.

Choice contains two types of branches: conditional branch and default branch. In Choice, you can add multiple conditional branch nodes, each of which contains a Boolean expression. Choice will evaluate the conditional branch nodes one by one until the first Boolean expression meets the condition. Then, it will execute the subflow configured on the conditional branch node. If all When conditions cannot be matched, the action of the default branch will be executed.

## Operation Configuration

#### Parameter configuration in expression mode

On the When node, you can configure a conditional statement to control branch selection.

| Parameter | Data Type | Description | Required | Default Value |
|:-----|:-----|:--------------------|:-----|-----|
| Execution condition | bool | Condition. If the condition is met, the corresponding subflow will be executed. | Yes    | None   |





#### Configuration page in expression mode

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/CCYi029_1.png" width="900px"/>


#### Parameter configuration in list mode

When configuring multiple comparison conditions on the GUI, you can use the logical operator `OR` or `AND` to connect them.

| Parameter | Data Type | Description | Required | Default Value |
|:-----|:-----|:--------------------|:-----|-----|
| Value | any | Value. | Yes    | None   |
| Condition | Enumeration | Condition, i.e., comparison operator. | Yes    | None   |

#### Configuration page in list mode

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/95GQ918_2.png" width="500px"/>


#### Data preview
None.

#### `message` input to the subflow
The entire `message` of the main flow is inherited.

#### Output
The entire `message` eventually output by the subflow is output, including the error.

