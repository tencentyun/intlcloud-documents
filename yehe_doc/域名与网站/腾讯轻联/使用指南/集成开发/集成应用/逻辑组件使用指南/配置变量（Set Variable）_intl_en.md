## Overview

Set Variable is used to declare a variable and save it in `variables` in `message`, so that subsequent nodes can reference it in the form of `msg.vars.get('name')`.



[](id:method1)

## Method 

### Parameter configuration

| Parameter | Data Type | Description | Required | Default Value | Remarks |
| :----- | :------- | :----------- | :------- | ------ |------ |
| Variable name | string   | Variable name.     | Yes       | None     | -     |
| Value | any      | Specific value of the variable. | Yes       | None     | -     |
| Type | string      | Data type of the variable | Yes       | string     | -     |
| Operation | string      | Variable operation | No       | None     | This parameter is available only if a variable of `list` or `dict` type exists.  |

### Configuration page

![image-20210325155553571](https://staticintl.cloudcachetci.com/yehe/backend-news/sTJS778_1.png)

### Output

To reference `variables`, you need to use the `msg.vars.get('company')` expression.

The `message` output by the component is as detailed below:

| `message` Attribute | Value                                                           |
| ----------- | ------------------------------------------------------------ |
| payload     | This attribute inherits the `payload` of the previous component.                                        |
| error       | <ul style="margin:0;"><li>`error` will be empty if the flow is executed successfully.</li><li>`error` will be of `dict` type and contain the `Code` and `Description` fields if the flow fails to be executed. The `Code` field indicates the error type, and the `Description` field indicates the error details.</li></ul> |
| attribute   | This attribute inherits the `attribute` of the previous component.                                  |
| variable    | `variable` of the previous component and the variables added in the current component.                 |

### Data preview
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/g9Dw732_2.png" alt="https://staticintl.cloudcachetci.com/yehe/backend-news/g9Dw732_2.png" style="zoom:50%;" />

