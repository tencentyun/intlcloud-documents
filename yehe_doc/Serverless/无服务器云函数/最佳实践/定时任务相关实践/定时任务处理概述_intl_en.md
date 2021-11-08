

With SCF scheduled triggers, you can quickly create and complete scheduled tasks without having to purchase computing resources in advance. Such triggers leverage Serverless' powerful elastic scalability to provide stable and fast capabilities of scheduled task processing.

Unlike other event triggers, [scheduled triggers](https://intl.cloud.tencent.com/document/product/583/9708) can execute tasks by using scheduled time-driven functions. Specifically, you can configure Cron expressions to quickly use such triggers without relying on external invocations. They have natural advantages in typical scheduled task scenarios such as automated monitoring, testing, and alarming, automated task execution, and data archiving, cleansing, and backup. The relevant workflow is as shown below:
![](https://main.qcloudimg.com/raw/7566ea4badbd8480065aeba59036936e.png)

## Advantages of Function Processing

- The full lifecycle of scheduled tasks can be managed to help you quickly build scheduled triggers.
- Tasks are fully managed and can be triggered regularly and retried automatically by standard Cron expressions.
- More and more built-in function templates are added to reduce the development costs for scheduled tasks in popular use cases.
- Computing power is provided based on SCF, with features such as auto scaling, OPS-free usage, and pay-as-you-go billing.

## Multi-scenario Function Processing Practices

The following table lists existing templates for typical use cases and their specific descriptions:


| Function Processing Scenario | Description |
| ------------------------------------------------------------ | --------------------------------------- |
| High-Availability scheduled testing | Use SCF to implement high-availability scheduled testing. |
| [Scheduled task execution](https://intl.cloud.tencent.com/zh/document/product/583/39015) | Use SCF and Puppeteer to perform scheduled tasks on webpage content such as data collection and storage. |
| Scheduled data archiving and backup | Use SCF to regularly back up databases to COS. |


>! SCF offers a free tier for scheduled tasks, and excessive usage will incur corresponding computation fees. For billing details, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/583/17299).
