## Overview

Transform is used to orchestrate and convert the format of the data in `message`. It can modify `payload`, `attribute`, and `variable`.

## Operation Configuration

### Parameter configuration
| Parameter | Data Type | Description | Required | Default Value |
| :----- | :------- | :----------- | :------- | ------ |
| payload | any   | The configured payload.     | No       | None     |
| attribute | dict      | The configured attribute. | No       | None     |
| variable | dict      | The configured variable. | Yes       | None     |

### Configuration page
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/g4Yg270_1.png" alt="https://staticintl.cloudcachetci.com/yehe/backend-news/g4Yg270_1.png" style="zoom:50%;" />

### Output

The `message` output by the component is as detailed below:

| `message` Attribute | Value                                                           |
| ----------- | ------------------------------------------------------------ |
| payload     | If `payload` is added to **Output**, the execution result in `payload` will be output; otherwise, the `payload` of the previous component will be inherited. |
| error       | <ul><li>`error` will be empty if the flow is executed successfully.</li><li>`error` will be of `dict` type and contain the `Code` and `Description` fields if the flow fails to be executed. The `Code` field indicates the error type, and the `Description` field indicates the error details.</li></ul> |
| attribute   | This attribute is of `dict` type. If `attributes` is added to **Output**, the execution result in `attributes` will be output; otherwise, the `attribute` of the previous component will be inherited. |
| variable   | If `variables` is added to **Output**, the `variable` of the previous component and the new `variable` added in the Transform component will be output together; otherwise, the `variable` of the previous component will be inherited. |

## Examples

### Setting `payload`
Add `payload`.
![image-20210426173059453](https://staticintl.cloudcachetci.com/yehe/backend-news/jeS9376_2.png)


### Setting `attribute`
Add and edit `attributes`. As `attributes` is of `dict` type, the expression output also must be of `dict` type.
![image-20210426174817312](https://staticintl.cloudcachetci.com/yehe/backend-news/3tpt438_3.png)

### Setting `variable`
1. Add `variables`. Enter the name of the variable to be declared for **Variable name**.
   ![image-20210426174902089](https://staticintl.cloudcachetci.com/yehe/backend-news/ZBLS223_4.png)
2. Add an expression and edit the variables.
   ![image-20210426175013126](https://staticintl.cloudcachetci.com/yehe/backend-news/SH9Q324_5.png)
