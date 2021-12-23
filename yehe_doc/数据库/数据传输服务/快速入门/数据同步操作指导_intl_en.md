## Relevant Information

- [Data Sync Overview](https://intl.cloud.tencent.com/document/product/571/42667).
- [Databases Supported by Data Sync](https://intl.cloud.tencent.com/document/product/571/42579).

## Overall Process

| **Operation Process**              | **Description**                                                     |
| ------------------------- | ------------------------------------------------------------ |
| 1. Prepare               | Before creating a data sync task, you need to [prepare](https://intl.cloud.tencent.com/document/product/571/42652) the source and target databases and a network environment to meet the environment requirements. |
| 2. Create a data sync task       | This section provides only a basic sample sync task. For more scenarios, see [Data Sync](https://intl.cloud.tencent.com/document/product/571/42624). |
| 3. View the sync progress or perform other operations | <li>You can view the overall sync progress and perform operations such as verification and retry as instructed in [Task Management](https://intl.cloud.tencent.com/document/product/571/42620).<li>You can view various data sync metrics as instructed in [Viewing Monitoring Metric](https://intl.cloud.tencent.com/document/product/571/42606).</li> |
| 4. Compare the sync items and stop the task   | After the sync task is done, check whether the source and target database have the same content and manually stop the sync task as instructed in [Stopping Task](https://intl.cloud.tencent.com/document/product/571/42616). |

## Sample Data Sync Task

1. Log in to the [data sync purchase page](https://buy.cloud.tencent.com/dts), select the corresponding configuration items, and click **Buy Now**.
2. After successful purchase, return to the [data sync list](https://console.cloud.tencent.com/dts/replication), and you can see the newly created data sync task. You need to configure it before you can use it.
3. In the data sync list, click **Configure** in the **Operation** column to enter the sync task configuration page.
![](https://qcloudimg.tencent-cloud.cn/raw/afe583b0dd3569cad36da0f3f19acba0.png)
4. On the sync task configuration page, configure the source and target databases and their accounts and passwords, test the connectivity, and click **Next**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/dcad48b082c4bfc8bc25b2aff7a0f579.png"  style="margin:0;">
5. On the **Set sync options and objects** page, set the data initialization, data sync, and sync object options and click **Save and Go Next**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/a8df8150f387ffd56e11f60a6384adba.png"  style="margin:0;">
<strong>Database/Table mapping</strong>: hover over the right side of a selected object, and the **Edit** icon will be displayed. Click it and then enter a mapping name in the pop-up window.
<img src="https://qcloudimg.tencent-cloud.cn/raw/fb3dfa032310e444729a805b503e019b.png"  style="margin:0;">
6. On the task verification page, complete the verification. After all check items are passed, click **Start Task**.
>?If an alarm is displayed in the verification result, it will not affect the task start, but we recommend you click **View Details** to get the suggestions for adjustment.
>
![](https://qcloudimg.tencent-cloud.cn/raw/898e1d8ced68446dfd3e889fb77d7011.png)
7. Return to the data sync task list, and you can see that the task has entered the **Running** status.
>?You can click **More** > **Stop** in the **Operation** column to stop a sync task. You need to ensure that data sync has been completed before stopping the task.
>
![](https://qcloudimg.tencent-cloud.cn/raw/058cf11d354d64ae32e881a421e0d686.png)
