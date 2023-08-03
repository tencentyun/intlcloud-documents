## Overview
Scatter Gather can execute multiple tasks in parallel. In this component, you can add multiple branches and configure a subflow in each branch to execute a task independently.

## Operation Configuration

### Parameter configuration

| Parameter | Data Type | Description | Required | Default Value |
|:------|:-------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-----|-------------|
| Maximum parallelism | int                  | Maximum number of tasks executed in parallel. Value range: 2–8. The actual parallelism is the lesser value between the number of branches and the maximum parallelism.                                                                                                                                                                      | Yes    | 4           |
| Root message | string               | The root message is a variable, which stores the `message` of the main flow. You need to enter a variable name. You can enter `msg.vars.get('#root message name#').payload` to access the `payload` data of the main flow. If the default value `rootMessage` is used, you can use `msg.vars.get('rootMessage').payload` to access the `payload` data of the main flow in the subflow. | Yes    | rootMessage |

### Configuration page

![img_26.png](https://staticintl.cloudcachetci.com/yehe/backend-news/x7LA189_1.png)

### Data preview
None.

### `message` input to the subflow

| `message` Attribute | Value                        |
|-----------|--------------------------|
| payload   | This attribute inherits the `payload` in `message` of the main flow.   |
| error     | Null.                        |
| attribute | This attribute inherits the `attribute` in `message` of the main flow. |
| variable  | This attribute inherits the variable of the main flow.                  |

### Output

The output result of Scatter Gather doesn't contain the `variable` variable used in the processing logic but only the data in `payload`.
The output `payload` is of `dict` type and aggregates the processing result of each branch.

The `message` output by the component is as detailed below:

| `message` Attribute | Value                        |
|-----------|--------------------------------------------------------------------------------------------------|
| payload   | This attribute is of `dict` type. `key` is the branch number, which starts from `1`. `value` is the branch execution result (the `payload` output by the last component).                                       |
| error       | <ul><li>`error` will be empty if the flow is executed successfully.</li><li>`error` will be of `dict` type and contain the `Code` and `Description` fields if the flow fails to be executed. The `Code` field indicates the error type, and the `Description` field indicates the error details.</li></ul> |
| attribute | The value is the same as that of the input `attribute`.                                                                                   |
| variable  | The value is the same as that of the input variable.                                                                                         |

## Example

We recommend you use Scatter Gather to execute different tasks in parallel. For example, if you need to query the customer and product information based on the user order data, you can configure two branches to query the two types of information respectively.

1. Add a Scatter Gather component and two branches and use the default configuration.
   ![img_27.png](https://staticintl.cloudcachetci.com/yehe/backend-news/sp4z141_2.png)
2. Configure customer information query in the first branch and product information query in the second branch. Here, two simple HTTP requests are used for simulation.
   ![img_28.png](https://staticintl.cloudcachetci.com/yehe/backend-news/gnTD229_3.png)
3. After execution, view the output of Scatter Gather. Switch to the Professional mode, and you can see that `payload` is a dictionary containing two keys.
Key `1` represents the result of the first branch, i.e., the queried customer information, and key `2` represents the result of the second branch, i.e., the queried product information.
   ![img_29.png](https://staticintl.cloudcachetci.com/yehe/backend-news/3TPw406_4.png)
