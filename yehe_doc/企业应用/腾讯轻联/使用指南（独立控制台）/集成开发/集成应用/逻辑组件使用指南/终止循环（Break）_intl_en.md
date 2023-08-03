## Overview

Break needs to be used together with the For Each or While component to stop a loop. It can stop executing the loop statement even if the sequence is still in recursion or the loop condition is not `false`. When there is a nested loop, Break will jump out of the loop at the current layer and start to execute the next component.

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
| payload     | <ul><li>In the For Each component, after the Break component is executed, `payload` will inherit the `payload` of the component previous to For Each.</li><li>In the While component, after the Break component is executed, `payload` will inherit the `payload` output by the component previous to Break.</li></ul> |
| error       | Null.                                                           |
| attribute   | <ul><li>In the For Each component, after the Break component is executed, `attribute` will inherit the `attribute` output by the component previous to For Each.</li><li>In the While component, after the Break component is executed, `attribute` will inherit the `attribute` output by the component previous to While.</li></ul> |
| variable    | <ul><li>In the For Each component, after the Break component is executed, `variable` will be the `variable` output by the component previous to For Each and the `variable` declared in the For Each subflow.</li><li>In the While component, after the Break component is executed, the `variable` will be the `variable` output by the component previous to While and the `variable` declared in the While subflow.</li></ul> |

## Example

1. Add a For Each component and set the list to be traversed.
2. Use a Choice component and add a condition in **Conditional branch**.
3. On the **Conditional branch** node, add a **Break** component to jump out of the traversal process when `BMW` is traversed.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/ggvL129_1.png)
