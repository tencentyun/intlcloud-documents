
## Overview

For Each is a loop control component, which is similar to for/foreach in several programming languages. In For Each, you can configure a subflow to execute the subflow logic for each element in the specified data set.

## Operation Configuration

### Parameter configuration

| Parameter | Data Type | Description | Required | Default Value |
|:----|:---------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-----|-------------|
| Data set | string, list, dict, and int | The data set to be traversed. <ul><li>If the data type is `string`, all characters in the string will be traversed.</li><li>If the data type is `list`, all elements in the list will be traversed.</li><li>If the data type is `dict`, all values in the dictionary will be traversed.</li><li>If the data type is `int`, for example, if the data set is `3`, the data set `[0,1,2]` will be traversed.</li> </ul>                                              | Yes    | None           |
| Counter | string               | The counter is a variable, which stores the current number of iterations and starts from `0`.<br/>You need to enter a variable name such as `msg.vars.get('#counter variable#')` to use the counter.<br/>For example, if the counter variable is set to the default value `counter`:<br/> In the first loop, `msg.vars.get('counter')` will be `0`.<br/>In the second loop, `msg.vars.get('counter')` will be `1`.        | Yes    | counter     |
| Root message | string               | The root message is also a variable, which stores the message of the main flow. You need to enter a variable name.<br/>You can enter `msg.vars.get('#root message name#').payload` to access the payload data of the main flow.<br/>If the default value `rootMessage` is used, you can use `msg.vars.get('rootMessage').payload` to access the payload data of the main flow in the For Each subflow. | Yes    | rootMessage |

>?Generally, you only need to configure the data set.

### Configuration page

![img.png](https://staticintl.cloudcachetci.com/yehe/backend-news/gR3z240_1.png)

### Data preview

| Preview Field    | Data Type | Description                               |
|:--------|:-----|:---------------------------------|
| payload | any  | Input value in each traversal, which is also an element in the data set.            |
| index   | int  | Position in each traversal. This field represents the subscript position of the current input value in the data set, which starts from `0`. |

![img_1.png](https://staticintl.cloudcachetci.com/yehe/backend-news/MfwM000_2.png)

The data preview content is visible only in the subflow. Components in the subflow can directly use `payload` and `index` in the For Each component.
![img_2.png](https://staticintl.cloudcachetci.com/yehe/backend-news/2hXp351_3.png)

### `message` input to the subflow

| `message` Attribute | Value                                                                                                                                                                         |
|-----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| payload   | An element in the data set. For example, if the data set to be iterated is `[1,2,3]`:<br/>In the first loop, `payload` in the subflow will be `1`.<br/>In the second loop, `payload` will be `2`.<br/>If the data set to be iterated is `{"key":"key1", "value":"value1"}` of `dict` type:<br/>In the first loop, `payload` in the subflow will be `value1`.<br/>In the second loop, `payload` will be `value2`.            |
| error     | Null.                                                                                                                                                                         |
| attribute | Null.                                                                                                                                                                         |
| variable  | This attribute inherits the `variable` of the main flow and has two new variables: counter and root message. If you use the default values of the two new variables, you can use expressions `msg.vars.get('counter')` and `msg.vars.get('rootMessage')` to access them.<br/>If Set Variable is used in For Each, the new variables will be added to `variable` during subflow execution. |

### Output

The For Each component doesn't change the content of `message`, and subsequent nodes only notice the changes in variables.

## Example

The following describes how to use the For Each component to traverse the list and add numbers and prefixes to elements in the list.

1. Initialize the variable `listResult`.
![img_4.png](https://staticintl.cloudcachetci.com/yehe/backend-news/Z5pR117_4.png)
2. Add a For Each component and configure it.
![img_5.png](https://staticintl.cloudcachetci.com/yehe/backend-news/k4Pn178_5.png)
3. Set the variable in the For Each subflow. Specifically, add a prefix to each element (the subscript position of the element) and add it to the `listResult` variable.
![img_6.png](https://staticintl.cloudcachetci.com/yehe/backend-news/ZKZt298_6.png)
4. Perform a unit test to check the output effect.
![img_7.png](https://staticintl.cloudcachetci.com/yehe/backend-news/yMBx053_7.png)
