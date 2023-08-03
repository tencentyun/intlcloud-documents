## Overview

The Try-Catch component consists of an **execution** subflow and one or multiple **error capture** subflows. You can configure it to capture errors thrown when the **execution** subflow runs as well as system errors. It can also be used together with the Raise Error component to capture custom errors. If the **execution** subflow throws an error, the first matched **error capture** subflow will be executed. If no subflows are matched, the error will be thrown to the outer layer.

## Operation Configuration

### Connection description

None.

### Parameter configuration

| Parameter | Data Type | Description | Required | Default Value |
| :------- | :------------------- | :----------------------------------------------------------- | :------- | ------ |
| Transaction     | Enumeration | This parameter is used together with the `Database` component and is used to roll back the database operation when execution fails.             | Yes       | None     |
| Error type | string               | Type of the error thrown during flow execution, which is selected in the drop-down list. You can select one, multiple, or all types. | Yes       | None     |
| Number of retries | int                  | The maximum number of retries of the **execution** subflow when an error of the specified type occurs. Value range: 0–5. The number of retries for each **error capture** subflow is counted separately. | Yes       | No retry |
| Retry interval | int                  | Interval between two retries. Value range: 1–300s.                              | No       | 60     |


The transaction is configured on the **Start Error Capture** node.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/WvTZ077_1.png)

The error type and the maximum number of retries are configured on the **Try-Catch** node.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Vc5k121_2.png)

### Data preview

None.

### `message` input to the subflow

| `message` Attribute | Value                                      |
| ----------- | --------------------------------------- |
| payload     | This attribute inherits the `payload` of the component previous to **Try-Catch**.                                        |
| error       | This attribute inherits the `error` of the component previous to **Try-Catch**.     |
| attribute   | This attribute inherits the `attribute` of the component previous to **Try-Catch**.     |
| variable    | This attribute inherits the `variable` of the component previous to **Try-Catch**.  |

### Output

The `message` output by the component is as detailed below:

| `message` Attribute | Value                                                           |
| ----------- | ------------------------------------------------------------ |
| payload     | <ul><li>If the **execution** subflow runs normally, the value of `payload` will be the `payload` output by the **execution** subflow.</li><li>If an error is thrown and captured, the value of `payload` will be the `payload` output by an **error capture** subflow.</li><li>If a thrown error is not captured, the flow will stop running.</li></ul> |
| error       | <ul><li>If the **execution** subflow throws an error and the error is not captured, or if an **error capture** subflow throws an error, `error` will store the error message of `dict` type and contain the `Code` and `Description` fields. The `Code` field indicates the error type, and the `Description` field indicates the error description.</li><li>Otherwise, `error` will be empty.</li></ul> |
| attribute     | <ul><li>If the **execution** subflow runs normally, the value of `attribute` will be the `attribute` output by the **execution** subflow.</li><li>If an error is thrown and captured, the value of `attribute` will be the `attribute` output by an **error capture** subflow.</li><li>If a thrown error is not captured, the flow will stop running.</li></ul> |
| variable     | <ul><li>If the **execution** subflow runs normally, the value of `variable` will be the `variable` output by the **execution** subflow.</li><li>If an error is thrown and captured, the value of `variable` will be the `variable` output by an **error capture** subflow.</li><li>If a thrown error is not captured, the flow will stop running.</li></ul> |

## Example

1. Add the custom error type **Request failure**.
2. When a request fails, an error of this type will be thrown.
3. Capture the error and execute the retry policy. The HTTP request in the **execution** subflow will be executed again, and the Choice component will be executed. If all retries fail, the error will be logged.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/hm92975_3.png)
