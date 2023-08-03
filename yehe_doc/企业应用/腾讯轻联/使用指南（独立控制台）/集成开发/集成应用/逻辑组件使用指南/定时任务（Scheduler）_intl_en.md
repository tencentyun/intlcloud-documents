## Overview
As a trigger, Scheduler is used to trigger a flow according to the configured rule at the scheduled time. The graphical Scheduler component supports three trigger modes:
- One-time trigger: The flow can be triggered at multiple specified time points.
- Regular trigger: The flow can be triggered regularly.
- Cron expression: The configuration includes one or more cron rules. When any cron rule matches the current time, the flow where the Scheduler component resides will be triggered.

## Operation Configuration
### Parameter configuration

| Parameter | Data Type | Description | Required | Default Value |
| --------- | ------- | ----------------------------------------------- | ------- | ------------------- |
| Trigger mode   | Int      | You can select **One-time trigger**, **Regular trigger**, or **Cron expression**.     | Yes       | 0 (Cron expression mode). |
| Cron expression | string   | Trigger rule such as once every minute.                | Yes       | None                  |
| Time zone       | string   | Specified time zone.                                         | Yes       | Asia/Beijing UTC+08:00           |
| Triggered only after the previous task is executed   | bool     | If this option is selected, the flow will be triggered only after the previous task is executed. | No       | false               |

Scheduler contains one or multiple cron rules. To add multiple rules, separate them by `\r`. A cron expression is configured as follows:

| Parameter     | Description                       | Value Range    |
| -------- | -------------------------- | ----------- |
| seconds  | Second                         | 0–59      |
| minutes  | Minute                       | 0–59      |
| hours    | Hour                       | 0–23      |
| days     | Date. This parameter is optional and is set to every day by default.     | 1–31      |
| months   | Month. This parameter is optional and is set to every month by default.       | 1–12      |
| weekdays | Day of the week. This parameter is optional and is not specified by default. | 1–7       |
| years    | Year. This parameter is optional and is set to every year by default.     | 1970–2099 |

You can use the following operators when configuring a cron expression:

- `*` indicates all valid values. For example, `hours="*"` indicates every hour.
- `-` indicates a range. For example, `weekdays="1-5"` indicates Monday to Friday.
- `,` indicates enumeration. For example, `months="1,3,5,7,8,10,12"` indicates all months with 31 days.
- `/` indicates increment. For example, `hours="8/2"` indicates every two hours from 08:00.
- `L` indicates the last period. For example, `weekdays="6L"` indicates the last Saturday of the current month.
- `?` indicates an unspecified value. There is a restraint that at least one of the parameters year, month, date, and day of the week must be left unspecified to avoid a conflict; for example, both February 20, 2020 (which should be Thursday) and Wednesday are specified. The day of the week is unspecified by default.

### Configuration page

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/Ju7Q977_1.png" alt="https://staticintl.cloudcachetci.com/yehe/backend-news/Ju7Q977_1.png" style="zoom:50%;" />

### Output

As a trigger component, Scheduler is the first component in a flow. It will generate an empty `message` to trigger the flow execution.

The `message` output by the component is as detailed below:

| `message` Attribute | Value                                                           |
| ----------- | ------------------------------------------------------------ |
| payload     | Null.                                               |
| error       | <ul><li>`error` will be empty if the flow is executed successfully.</li><li>`error` will be of `dict` type and contain the `Code` and `Description` fields if the flow fails to be executed. The `Code` field indicates the error type, and the `Description` field indicates the error details.</li></ul> |
| attribute   | Null.                                               |
| variable    | Null.                                                 |

### Data preview
![](https://staticintl.cloudcachetci.com/yehe/backend-news/ZNtn888_2.png)

## Examples
### Regular trigger mode
Trigger the flow once every 30 seconds:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/C9xY846_3.png)

### One-time trigger mode
Trigger the flow once at 00:00:00 on January 1, 2023:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Z6tG028_4.png)


### Cron expression mode
Trigger the flow once every five minutes:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/itFP938_5.png)

