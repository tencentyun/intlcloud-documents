After creating a traffic mirror, you can enable, disable, modify, or delete it or add tags in the console.

## Enabling and Disabling Traffic Mirror[](id:open)
A new traffic mirror task is enabled by default. To disable it and then enable it again, follow the steps below.
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **Diagnostic Tools** > **Traffic Mirror** on the left sidebar and select the target region.
3. Locate the traffic mirror you want to manage, disable or enable it under the **Collect traffic** column.
![](https://qcloudimg.tencent-cloud.cn/raw/258bae0acd52b53654be2b64c0d542e2.png)

## Modifying Traffic Mirror[](id:modify)
To modify an existing traffic mirror, follow the steps below:
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **Diagnostic Tools** > **Traffic Mirror** on the left sidebar and select the target region.
3. Click the target ID from the traffic mirror list.
4. Modify the desired items.
   + Edit traffic collection configurations
    1. Click **Edit** in the top-right corner of the **Traffic Collection** module.
    2. In the pop-up window, modify **Collection ENI**, **Collection type**, **Traffic filtering**, and other configurations as needed, and then click **OK**.
   + Edit traffic receiving configurations
    1. Click **Edit** in the top-right corner of the **Traffic Receiving** module.
    2. In the pop-up window, modify **Target ENI** and **Balance mode**, and then click **OK**.
 ![](https://qcloudimg.tencent-cloud.cn/raw/79c190994a2c908b85abb41de125259d.png)   

## Adding Tags[](id:add)
Tags are used to identify and organize Tencent Cloud resources. Each tag contains a tag key and a tag value. Adding a tag to the traffic mirror makes it easy to filter and manage traffic mirror resources.
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **Diagnostic Tools** > **Traffic Mirror** on the left sidebar and select the target region.
3. Locate the target traffic mirror and click **Edit tags** in the **Operation** column.
4. In the pop-up window, configure the information as follows:
   1. For **Tag key**, enter the key name or select one from the drop-down list.
   2. For **Tag value**, enter the key value.
>?A tag key may be null or contains multiple values.
>
   3. (Optional) Click **Add** and configure **Tag key** and **Tag value** to add a tag.
   4. After completing the configuration, click **OK**.

## Locating Traffic Mirror
1. Click <img src="https://main.qcloudimg.com/raw/6ca6880fc850d1ec41695ec7c1714df7.png" style="width:18px;margin:-4px 0 ;"/> in the top-right corner on the **Traffic Mirror** page and select a filter. Three filters are supported as shown below.
![](https://qcloudimg.tencent-cloud.cn/raw/5aba3c1deffa016559c1f07e57f27ecd.png)
2. Enter a keyword in the edit box and click <img src="https://main.qcloudimg.com/raw/6ca6880fc850d1ec41695ec7c1714df7.png" style="width:18px;margin:-4px 0 ;"/>.
>? Separate keywords with vertical bars (|).
>

## Deleting Traffic Mirror[](id:del)
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **Diagnostic Tools** > **Traffic Mirror** on the left sidebar and select the target region.
2. Locate the target traffic mirror, click **Delete** in the **Operation** column, and confirm the deletion.
