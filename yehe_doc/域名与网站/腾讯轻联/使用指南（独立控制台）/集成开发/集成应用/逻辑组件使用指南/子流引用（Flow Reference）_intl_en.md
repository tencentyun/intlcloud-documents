## Overview

Flow Reference is used to reference other flows in the current app. Unlike Async, Flow Reference is a sync process. It will continue to execute the next action only after the execution of the referenced flow. After the subflow in Flow Reference is executed, `message` will be passed to the main flow, and the next node will be executed based on the `message` of the subflow.

If the subflow in Flow Reference contains a trigger node, and the subflow execution is triggered by the Flow Reference component, the trigger node of the subflow won't be executed; that is, the subflow will be executed from the second node.

## Operation Configuration

### Parameter configuration

| Parameter | Data Type | Description | Required | Default Value |
|:----|:-------|:-----------------------|:-----|-----|
| Flow | string | Flow name. You can select a flow shared by another app in the same project. | Yes    | None   |

### Configuration page

![img_3.png](https://staticintl.cloudcachetci.com/yehe/backend-news/bsKL204_1.png)

### Data preview
None.

### Output

| `message` Attribute | Value                  |
|-----------|--------------------|
| payload   | The `payload` output by the last node of the subflow. |
| error     | `error` will be empty if the flow is executed successfully.     |
| attribute | The `attribute` output by the subflow.     |
| variable  | All set variables in the subflow.   |

## Examples

### Referencing a flow in the same app

1. Create a flow and name it `Subflow`. Add a **Set Payload** component to the subflow and output `payload`. Add a **Set Variable** component and set variable `a`.
![img_9.png](https://staticintl.cloudcachetci.com/yehe/backend-news/jDAw919_2.png)
2. Add a Flow Reference component and select **Subflow** in the drop-down list.

3. After the unit test is completed, click the Flow Reference component, select the Professional mode to view the output, and you can see that the `payload` and variable `a` configured in the subflow are passed to the current flow.
![img_11.png](https://staticintl.cloudcachetci.com/yehe/backend-news/ykTs871_3.png)


### Referencing a flow from another app in the same project
#### Flow reference methods
Multiple apps in the same project may use the flow of the same general feature, such as user login authentication. Generally, there are three methods for using this flow:

| Method | Pros and Cons |
|---------|---------|
| Edit or copy a **User login authentication** flow in each app | There are a large number of repeated flows, which are difficult to maintain. |
| Call an app in other apps through a public HTTP API | HTTP calls consume traffic, and debugging and maintenance are difficult. |
| Use Flow Reference for cross-app flow reference | Like flow reference within an app, this method can be used when two apps run at the same time. |

#### Using Flow Reference for cross-app flow reference
1. Create an app "Shared app" which provides a general feature flow "Shared flow" and share the flow.
	![img_12.png](https://staticintl.cloudcachetci.com/yehe/backend-news/uRu8156_4.png)
2. In the shared flow, set `payload` and variable `share`.
	![img_13.png](https://staticintl.cloudcachetci.com/yehe/backend-news/RKJJ109_5.png)
3. Publish "Shared app", and "Shared flow" can be selected and used in the Flow Reference list in other apps in the project.
Then, start an app test, so that a test can be performed after "Shared flow" is referenced in other apps.
	![img_15.png](https://staticintl.cloudcachetci.com/yehe/backend-news/TjrQ015_6.png)
4. Edit the flow in another app in the project, add a Flow Reference component, and select "Shared flow" of "Shared app" in the project to reference it.
	![img_16.png](https://staticintl.cloudcachetci.com/yehe/backend-news/Wh2L062_7.png)
5. Perform a unit test and view the output of the Flow Reference ("Shared flow") node. Switch to the Professional mode, and you can see that `payload` and variable `share` configured in the shared flow are passed to the current flow.
	![img_17.png](https://staticintl.cloudcachetci.com/yehe/backend-news/dHWC969_8.png)

   ​    
