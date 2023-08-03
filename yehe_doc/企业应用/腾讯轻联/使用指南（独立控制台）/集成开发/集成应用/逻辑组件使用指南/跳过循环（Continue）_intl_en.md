## Overview

Like the Break component, Continue needs to be used together with the For Each or While component. It is used to jump out of the current loop and execute the next loop.

## Operation Configuration

### Connection description

None.

### Parameter configuration

None.

### Data preview

None.

### Output

The `message` output by the component is as detailed below:

| `message` Attribute | Value                                                           |
| ----------- | ------------------------------------------------------------ |
| payload     | <ul><li>In the For Each component, after the Continue component is executed, `payload` will be the data to be traversed next time.</li><li>In the While component, after the Continue component is executed, `payload` will inherit the `payload` output by the component previous to Continue.</li></ul> |
| error       | Null.                                                           |
| attribute   | <ul><li>In the For Each component, after the Continue component is executed, `attribute` will inherit the `attribute` output by the component previous to For Each.</li><li>In the While component, after the Continue component is executed, `attribute` will inherit the `attribute` output by the component previous to While.</li></ul> |
| variable    | <ul><li>In the For Each component, after the Continue component is executed, `variable` will inherit the `variable` output by the component previous to Continue.</li><li>In the While component, after the Continue component is executed, the `variable` will inherit the `variable` output by the component previous to Continue.</li></ul> |

## Example

In the following example, the For Each component is used to calculate the sum of all odd numbers in the list, and the Continue component is used to jump out of the loop for an even number.
1. Add a For Each component and enter the set to be traversed `[1,2,3,4,5]`.
2. Add a Choice component and filter data on the When node.
3. Add a Continue node on the When node.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/fsmI766_1.png)
