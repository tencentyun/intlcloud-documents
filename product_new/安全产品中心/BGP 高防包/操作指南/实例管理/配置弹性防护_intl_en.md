After you enable the elastic protection on the Anti-DDoS Pro instance, when the attack traffic bandwidth exceeds the base protection bandwidth, Anti-DDoS Pro will continue protection according to your elastic protection bandwidth.
If the elastic protection is not enabled when you [purchase the Anti-DDoS Pro instance](https://intl.cloud.tencent.com/document/product/1029/31748), you can enable it during usage. No extra cost will be incurred if the elastic protection is not triggered on the day. If the elastic protection is triggered (when the attack traffic is higher than the base protection bandwidth), the [fee](https://intl.cloud.tencent.com/document/product/1029/31747) is charged based on the highest attack traffic of the day, and the bill is generated the next day. You can adjust the elastic protection bandwidth of the Anti-DDoS Pro instance as required any time.

## Enabling Elastic Protection
>If you do not enable elastic protection when you [purchase an Anti-DDoS Pro instance](https://intl.cloud.tencent.com/document/product/1029/31748), you can enable it during usage. Refer to the highest historical attack traffic and select an elastic protection bandwidth slightly higher than the highest historical bandwidth. This will offer protection against heavy traffic attacks and avoid IP blocking due to exceeding of the protection bandwidth.

1. Log in to [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/overview), select **Anti-DDoS Pro** -> **Resource List**, and click **Enable Elastic Protection** next to the target instance.
2. In the **Enable Elastic Protection** box, select a proper **Elastic Protection Bandwidth**.
![](https://main.qcloudimg.com/raw/41441264d5dbda3e9fc3e97610be7cf5.png)
3. Click **OK**.

## Modifying the Elastic Protection Bandwidth

1. Log in to [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/overview) and choose **Anti-DDoS Pro** -> **Protection Configuration**.
2. Select the target instance from the drop-down menu, find **Protection Bandwidth** under **Elastic Protection** section, and click **Modify**.
![](https://main.qcloudimg.com/raw/823529178a9e54e3108feedfdee3d994.png)
3. In the **Modify Elastic Protection** dialog box, select a proper **Elastic Protection Bandwidth**.
>- You can increase or reduce the elastic protection bandwidth. The protection capability varies from region to region. For more information, please see [Product Overview](https://intl.cloud.tencent.com/document/product/297/16497).
>- Modifying of elastic protection bandwidth takes effect immediately.


 ![](https://main.qcloudimg.com/raw/85fd16e905976bf8bc890d7eb56df2e1.png)
4. Click **OK**.

## Disabling Elastic Protection
>If you disable elastic protection, the max protection bandwidth degrades to the base protection bandwidth. Please ensure that the base protection bandwidth meets the actual requirements before disabling elastic protection.

1. Log in to [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/overview), choose **Anti-DDoS Pro** -> **Resource List**, and click **Disable Elastic Protection** next to the target instance.
2. In the **Disable Elastic Protection** dialog box, click **OK**.
