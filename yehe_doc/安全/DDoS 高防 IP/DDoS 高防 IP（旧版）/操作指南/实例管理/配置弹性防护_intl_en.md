After you enable elastic protection on the Anti-DDoS Advanced instance, when the attack traffic bandwidth exceeds the base protection bandwidth, Anti-DDoS Advanced will continue protection based on your elastic protection bandwidth.
If elastic protection is not enabled when you purchase the Anti-DDoS Advanced instance, you can enable it when using the instance. If elastic protection is not triggered on a day, no relevant fees will be incurred. When elastic protection is triggered (i.e., the attack bandwidth exceeds the base protection bandwidth), fees will be charged based on the billing tier corresponding to the actual attack bandwidth peak on the day and a bill will be generated the next day. You can modify the elastic protection bandwidth of the Anti-DDoS Advanced instance as needed with immediate effect.

## Enabling Elastic Protection
>If elastic protection is not enabled when you purchase the Anti-DDoS Advanced instance, you can enable it when using the instance and set the elastic protection bandwidth to higher than the highest historical attack traffic bandwidth. This helps avoid potential IP blockage in case of excessive attacks.

1. Log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/overview), select **Anti-DDoS Advanced** > **Asset List**, and click **Enable Elastic Protection** next to the target instance.
2. In the **Enable Elastic Protection** box, select the needed **Elastic Protection Bandwidth**.
3. Click **OK**.


## Modifying Elastic Protection Bandwidth

1. Log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/overview), select **Anti-DDoS Advanced** > **Asset List**, and click the target instance ID to enter the basic information page of the instance.
2. In the "Elastic Protection" section, click **Modify** on the right of "Elastic Bandwidth".
3. In the **Modify Elastic Protection** box, select an appropriate **Elastic Protection Bandwidth**.
>
>- You can increase or reduce the elastic protection bandwidth. The protection capability varies by region. For more information, please see [Product Overview](https://intl.cloud.tencent.com/document/product/1029/31742).
>- Modification of the elastic protection bandwidth takes effect immediately.

4. Click **OK**.


## Disabling Elastic Protection
>If you disable elastic protection, the maximum protection bandwidth will degrade to the base protection bandwidth. Please ensure that the base protection bandwidth meets your actual needs before disabling elastic protection.

1. Log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/overview), select **Anti-DDoS Advanced** > **Asset List**, and click **Disable Elastic Protection** next to the target instance.
2. In the **Disable Elastic Protection** box, click **OK**.
