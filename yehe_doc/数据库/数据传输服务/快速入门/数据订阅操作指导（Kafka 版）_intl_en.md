## Relevant Information

- [Data Subscription Overview](https://intl.cloud.tencent.com/document/product/571/13713).
- [Databases Supported by Data Subscription](https://intl.cloud.tencent.com/document/product/571/42663).

## Overall Process
| **Operation Process**        | **Description**                                                     |
| ------------------- | ------------------------------------------------------------ |
| 1. Prepare         | Before creating a data subscription task, you need to [prepare](https://intl.cloud.tencent.com/document/product/571/42652) a network environment.                       |
| 2. Create a data subscription task | This section provides only a basic sample subscription task. For more scenarios, see [Data Subscription](https://intl.cloud.tencent.com/document/product/571/42664). |
| 3. Manage the subscription task     | For more information on operations such as modifying the subscription object, see [Task Management](https://intl.cloud.tencent.com/document/product/571/42660).                    |
| 4. Consume the subscribed data     | Manage a consumer group and use the Kafka client to subscribe to the data. For more information, see [Consuming Subscribed Data](https://intl.cloud.tencent.com/document/product/571/39538). |
| 5. Stop the task         | After the subscription task is completed, you need to manually stop it.                           |

## Sample Data Subscription Task

1. Log in to the [DTS console](https://console.cloud.tencent.com/dts/dss), select **Data Subscription** on the left sidebar, and click **Create Subscription**.
2. On the **Create Subscription** page, select the corresponding configuration and click **Buy Now**.
3. After successful purchase, return to the data subscription list. You need to click **Configure Subscription** in the **Operation** column to configure the newly purchased subscription before you can use it.
![](https://qcloudimg.tencent-cloud.cn/raw/e3d28df3f5199d18abcb0d789994bb4c.png)
4. On the **Subscription Configuration** page, select the corresponding configuration items and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/8fdd91f5a9071bbcb0e8471738113c07.png)
5. On the **Subscription Type and Object** page, select a subscription type and click **Save**.
>?Subscription objects exclude the system tables and databases named `test`, as DTS does not support subscription to system tables, and `test` databases are recognized as test data by DTS.
>
![](https://qcloudimg.tencent-cloud.cn/raw/e3bd14c693fa91096ef47f254de7200a.png)
6. On the **Pre-verification** page, a pre-verification task will run for 2–3 minutes. After the pre-verification is passed, click **Start** to complete data subscription task configuration.
>?If verification fails, modify the task in the instance to be subscribed to as prompted and initiate the verification again.
>
![](https://qcloudimg.tencent-cloud.cn/raw/458f6897c7b200a59c5c7fa58ecd6f81.png)
7. After you click **Start**, the subscription task will be initialized, which will take 3–4 minutes. After successful initialization, the task will enter the **Running** status.
