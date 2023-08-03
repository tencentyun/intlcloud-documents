## Overview

Raise Error is used to throw exceptions and stop flow execution. This component can be used alone or together with the Try-Catch component. When it is used alone and is hit, the flow will stop execution and return an error message. When it is used together with Try-Catch, Try-Catch can capture the exception defined in it and execute the subflow configured in Try-Catch.

## Operation Configuration

### Connection description

None.

### Parameter configuration

| Parameter | Data Type | Description | Required | Default Value |
| :------- | :------- | :----------------- | :------- | -------- |
| Error type | string   | Custom error type. | Yes       | General error |
| Error description | string   | Error description.     | Yes       | None       |

![](https://staticintl.cloudcachetci.com/yehe/backend-news/IdFC224_1.png)

You can select an error type in the drop-down list and click **Add** to add a new error type. Error types are visible in all apps in the project.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/3V2A270_2.png)

### Data preview

None.

### Output

The `message` output by the component is as detailed below:

| `message` Attribute | Value                                                           |
| ----------- | ------------------------------------------------------------ |
| payload     | This attribute inherits the `payload` of the previous component.                                        |
| error       | `error` is of `dict` type and contains the `Code` and `Description` fields.<br>The `Code` field indicates the error type and is represented by an internal code, and the `Description` field indicates the error description. |
| attribute   | This attribute inherits the `attribute` of the previous component.                                  |
| variable    | This attribute inherits the `variable` of the previous component.                                   |

## Example

1. Add a Raise Error component.
2. Add the error type **Request failure**.
   ![](https://staticintl.cloudcachetci.com/yehe/backend-news/d7ww138_3.png)
3. Select the error type and configure the error description.
   ![](https://staticintl.cloudcachetci.com/yehe/backend-news/aD4X179_4.png)
4. Output the message.
   ![](https://staticintl.cloudcachetci.com/yehe/backend-news/CNcz095_5.png)
