
The billing mode of TDSQL-C can be changed from pay-as-you-go to serverless. TDSQL-C implements this change by converting the cluster type on the backend. After this change, the [bills and details](https://console.cloud.tencent.com/expense/bill/summary) will also change, while the payment mode will remain as pay-as-you-go.

>!
>- During the change from pay-as-you-go billing to serverless billing, the database can be accessed normally but will experience a momentary interruption when the billing mode is changed. Therefore, we recommend you configure an automatic reconnection feature for your application.
>- The change from pay-as-you-go billing to serverless billing is irreversible.

## Directions
1. Log in to the [TDSQL-C console](https://console.cloud.tencent.com/cynosdb), select the target instance in the instance list, and click **More** > **Pay-as-You-Go to Serverless** in the **Operation** column.
![](https://main.qcloudimg.com/raw/328ba1383f238d0256fc87b9f80c3a13.png)
2. In the pop-up window, set the minimum CCU, the maximum CCU, and the auto-pause time for the target [serverless](https://intl.cloud.tencent.com/document/product/1098/40618) database, check the box to agree to the rules of the pay-as-you-go to serverless billing mode change, and click **OK**.
![](https://main.qcloudimg.com/raw/b6c11314bbe95117aa6ee79f01707069.png)
