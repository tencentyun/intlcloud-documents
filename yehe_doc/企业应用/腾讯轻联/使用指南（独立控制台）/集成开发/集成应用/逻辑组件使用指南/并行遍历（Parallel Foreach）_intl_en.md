## Overview

Parallel Foreach is used to execute tasks in parallel. It executes the same processing logic on all elements in a data set in parallel. The actual parallelism is the lesser value between the number of remaining elements and the configured maximum parallelism.

A Parallel Foreach subflow has read-only access to the variables in the main flow and the output of other components, and modifications performed by the subflow will not affect the main flow.

After processing, the result of each element will be output to `payload` in `message` in the original sequence. Parallel Foreach is generally used in batch data processing scenarios, such as batch query and batch data import.

## Operation Configuration

### Parameter configuration

| Parameter | Data Type | Description | Required | Default Value |
|:------|:---------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-----|-------------|
| Data set | string, list, dict, and int | The data set to be traversed. <ul><li>If the data type is `string`, all characters in the string will be traversed.</li><li>If the data type is `list`, all elements in the list will be traversed.</li><li>If the data type is `dict`, all values in the dictionary will be traversed.</li><li>If the data type is `int`, for example, if the data set is `3`, the data set `[0,1,2]` will be traversed.</li>    </ul>                                              | Yes    | None           |
| Maximum parallelism | int                  | The maximum number of tasks executed in parallel. Value range: 2–8.                                                                                                                                                                      | Yes    | 4           |
| Counter | string               | The counter is a variable, which stores the current number of iterations and starts from `0`. You need to enter a variable name such as `msg.vars.get('#counter variable#')` to use the counter.<br>For example, if the counter variable is set to the default value `counter`, in the first loop, `msg.vars.get('counter')` will be `0`, and in the second loop, it will be `1`.        | No    | counter     |
| Root message | string               | The root message is also a variable, which stores the `message` of the main flow. You need to enter a variable name. You can enter `msg.vars.get('#root message name#').payload` to access the `payload` data of the main flow. If the default value `rootMessage` is used, you can use `msg.vars.get('rootMessage').payload` to access the `payload` data of the main flow in the Parallel Foreach subflow. | No    | rootMessage |
| Stop while error occurred | bool                 | If a subtask throws an error, traversal will stop after the execution of the initiated subtask is completed.                                                                                                                                                           | No    | False       |

### Configuration page
![img_19.png](https://staticintl.cloudcachetci.com/yehe/backend-news/xS64664_1.png)

### Data preview

| Preview Field    | Data Type | Description                               |
|:--------|:-----|:---------------------------------|
| payload | any  | Input value in each traversal, which is also an element in the data set.            |
| index   | int  | Position in each traversal. This field represents the subscript position of the current input value in the data set, which starts from `0`. |

![img_20.png](https://staticintl.cloudcachetci.com/yehe/backend-news/ngPc702_2.png)

The data preview content is visible only in the subflow. Components in the subflow can directly use `payload` and `index` in the Parallel Foreach component as shown below:

![img_21.png](https://staticintl.cloudcachetci.com/yehe/backend-news/HJ4c735_3.png)

### `message` input to the subflow

| `message` Attribute | Value                                                                                                                                                                         |
|-----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| payload   | An element in the data set. For example, if the data set to be iterated is `[1,2,3]`, in the first loop, `payload` in the subflow will be `1`, and in the second loop, it will be `2`.<br/>If the data set to be iterated is `{"key":"key1", "value":"value1"}` of `dict` type, in the first loop, `payload` in the subflow will be `value1`, and in the second loop, it will be `value2`.            |
| error     | Null.                                                                                                                                                                         |
| attribute | Null.                                                                                                                                                                         |
| variable  | This attribute inherits the `variable` of the main flow and has two new variables: counter and root message. If you use the default values of the two new variables, you can use expressions `msg.vars.get('counter')` and `msg.vars.get('rootMessage')` to access them.<br/>If Set Variable is used in For Each, the new variables will be added to `variable` during subflow execution. |

### Output

The output result of Parallel Foreach doesn't contain the `variable` variable used in the processing logic but only the data in `payload`. The output `payload` is a variable of `list` type, which contains the iteration result of each element in the raw data set in the original sequence. `attribute` inherits the value of the previous component.

The `message` output by the component is as detailed below:

| `message` Attribute | Value                                                                                                                                                                         |
|-----------|--------------------------------------------------------------------------------------------------|
| payload   | This attribute is of `list` type and contains the processing result of each element in the input sequence in the raw data set.                                                               |
| error       | <ul><li>`error` will be empty if the flow is executed successfully.</li><li>`error` will be of `dict` type and contain the `Code` and `Description` fields if the flow fails to be executed. The `Code` field indicates the error type, and the `Description` field indicates the error details.</li></ul> |
| attribute   | This attribute inherits the `attribute` of the component previous to Parallel Foreach.                                  |
| variable    | This attribute inherits the `variable` of the component previous to Parallel Foreach.                                   |



## Example

The following describes how to use the Parallel Foreach component to multiply all elements in the list by 2. The raw data set is `[1,2,3,4]`.

1. Add a Parallel Foreach component, configure the data set `[1,2,3,4]`, and set the maximum parallelism to `3`.

2. Add a Set Payload component to Parallel Foreach to multiply the elements in `payload` in the subflow by 2.

3. Output the result.

