## Overview
The Sleep component is used to execute a flow after the specified period of time.

## Operation Configuration
### Parameter configuration

| Parameter | Data Type | Description | Required | Default Value |
| --- | ------- | -------------------- | ------- | ------ |
| Delay   | int      | The specified delay in milliseconds. |  Yes       | 1000     |

### Output
The `message` output by the component is as detailed below:

| `message` Attribute | Value                                                           |
| ----------- | ------------------------------------------------------------ |
| payload     | This attribute inherits the `attribute` of the previous component.                                  |                                               |
| error       | <ul><li>`error` will be empty if the flow is executed successfully.</li><li>`error` will be of `dict` type and contain the `Code` and `Description` fields if the flow fails to be executed. The `Code` field indicates the error type, and the `Description` field indicates the error details.</li></ul> |
| attribute   | This attribute inherits the `attribute` of the previous component.                                  |
| variable    | This attribute inherits the `variable` of the previous component.                                   |

### Data preview
None.

## Example

1. Add a Sleep component.
![image-20210330173121330](https://staticintl.cloudcachetci.com/yehe/backend-news/rb43174_1.png)
2. Enter the delay.
![image-20210330173057043](https://staticintl.cloudcachetci.com/yehe/backend-news/NWcs218_2.png)

