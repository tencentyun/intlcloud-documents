
## Overview

Contrary to the Set Variable component, Remove Variable is used to delete the specified variable in `message`.

## Operation Configuration

### Parameter configuration

| Parameter | Data Type | Description | Required | Default Value |
| :------- | :------- | :--------------- | :------- | ------ |
| Variable name | string   | Name of the variable to be removed. | Yes       | None     |

### Configuration page

![image-20210325145534545](https://staticintl.cloudcachetci.com/yehe/backend-news/hBBi636_1.png)

### Output

The output `message` no longer contains the deleted variable. The `message` output by the component is as detailed below:

| `message` Attribute | Value                                                           |
| ----------- | ------------------------------------------------------------ |
| payload     | This attribute inherits the `payload` of the previous component.                                        |
| error       | `error` will be empty if the flow is executed successfully. `error` will be of `dict` type and contain the `Code` and `Description` fields if the flow fails to be executed. The `Code` field indicates the error type, and the `Description` field indicates the error details. |
| attribute   | This attribute inherits the `attribute` of the previous component.                                  |
| variable    | The variable removed from `variable` in the previous component.                       |

### Data preview

None.

## Example

1. Add a Remove Variable component.
![image-20210330172804271](https://staticintl.cloudcachetci.com/yehe/backend-news/gjhz731_2.png)
2. Enter the name of the variable to be removed.
![image-20210330172924688](https://staticintl.cloudcachetci.com/yehe/backend-news/sz5B685_3.png)

