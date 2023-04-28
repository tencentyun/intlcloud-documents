>!Note that the DNS address should be changed to the CNAME address provided, which will be updated (Non-BGP resources are not supported).

## Accessing a Rule
1. Log in to the [Anti-DDoS Advanced Console](https://console.cloud.tencent.com/ddos/antiddos-advanced/access/l4), select **Anti-DDoS Advanced (New)** > **Application Accessing** on the left sidebar, and then open the **Access via domain names** tab.
2. Click **Start Access**.
![](https://qcloudimg.tencent-cloud.cn/raw/c566b02296505e1ae286529ccf81988c.png)
3. On the **Access via Domain Name** page, select an associated instance ID and click **Next: Set Port Parameter**.
>? You can select multiple instances.

![](https://qcloudimg.tencent-cloud.cn/raw/9a7e5418069c1ae134490457e8832ad1.png)
3. Select a forwarding protocol, specify a domain name, and then click **Next: Set Forwarding Method**.
![](https://qcloudimg.tencent-cloud.cn/raw/3a3fd3db21e47b9b149a478879de9ada.png)
4. Select a forwarding method, specify a "real server IP+port"/real sever domain name, and add an alternate real server and set the weight if you have one. Then click **Next: Modify DNS Resolution**.
![](https://qcloudimg.tencent-cloud.cn/raw/e8c3114f7fbecb574180da803551f1be.png)
>? An alternate real server is used when the real server’s forwarding fails.

5. Click **Complete**. Rules that are added will display in the domain name list. You can check whether they access via the domain names successfully.
>?
>- When the access fails due to certification configuration errors, you will get a prompt "Failed to obtain the certificate. Please go to [SSL Certificate Management](https://console.cloud.tencent.com/ssl) to view details".
>- To avoid seconds of interruptions, update the certificate for connected domain names during off-peak periods.

![](https://qcloudimg.tencent-cloud.cn/raw/21a3776933d55e8f70cab930046edacf.png)

## Editing a Rule
1. On the [Access via domain names](https://console.cloud.tencent.com/ddos/antiddos-advanced/access/l4) page, select a rule you want to edit and click **Configuration**.
![](https://qcloudimg.tencent-cloud.cn/raw/95377ab8f1e82d357ed33f551644d1cf.png)
2. On the **Configure Layer-7 Forwarding Rule** page, modify parameters and click **OK** to save changes.
![](https://qcloudimg.tencent-cloud.cn/raw/81b03bf961f2e764dac0c16dafbf38bc.png)

## Deleting Rules
1. On the **Access via domain names**, you can delete one or more rules.
 - To delete a rule, select a rule you want to delete. Click **Delete**.
![](https://qcloudimg.tencent-cloud.cn/raw/195062b3cdaf25e6fe773c9c4e4d11cf.png)
 - To delete multiple rules, select more than one rules you want to delete. Click **Batch Delete**.
![](https://qcloudimg.tencent-cloud.cn/raw/39df53e034fc0105b4585fddbc1015f8.png)
2. In the pop-up window, click **Delete**.

## Importing a Rule
1. To import multiple rules, you can click **Batch Import**.
2. In the **Configure Layer-7 Forwarding Rule** window, enter the rules, and click ***OK*.
![](https://qcloudimg.tencent-cloud.cn/raw/d14e1161d9c788182ce88e78e2042932.png)

## Exporting a Rule
1. To import multiple rules, you can click **Batch Export**.
2. In the **Batch Export Layer-7 Forwarding Rules** window, select the rules you want to export, and click **Copy**.
![](https://qcloudimg.tencent-cloud.cn/raw/550d61d8cd074d4634c314947d962b79.png)