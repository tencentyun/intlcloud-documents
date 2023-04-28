>!Note that the DNS address should be changed to the CNAME address provided, which will be updated (Non-BGP resources are not supported).

## Accessing a Rule
1. Log in to the [Anti-DDoS Advanced Console](https://console.cloud.tencent.com/ddos/antiddos-advanced/access/l4), select **Anti-DDoS Advanced (New)** > **Application Accessing** on the left sidebar, and then open the **Access via ports** tab.
2. Click **Start Access**.
![](https://main.qcloudimg.com/raw/fd5e5fff3727183e497db5a0d643a8ce.png)
3. On the **Access via Port** page, select an associated instance ID and click **Next: Set Port Parameter**.
>? You can select multiple instances.

4. Select a forwarding protocol, specify a forwarding port and real server port, and then click **Next: Set Forwarding Method**.
5. Select a forwarding method, specify a "real server IP+port"/real sever domain name, and add an alternate real server and set the weight if you have one. Then click **Next: Modify DNS Resolution**.

>?
>- An alternate real server is used when the real server’s forwarding fails.
>- If the forwarding port you specify in the second step "Set Port Parameter" is occupied, you cannot proceed to the next step.

6. Click **Complete**.

## Querying a Rule
On the [Access via ports](https://console.cloud.tencent.com/ddos/antiddos-advanced/access/l4) page, enter a real server IP/domain name, real server port, forwarding protocol/port or an associated instance ID in the search box.
![](https://qcloudimg.tencent-cloud.cn/raw/a26bee93c987a36989e19f842c850601.png)

## Editing a Rule
1. On the [Access via ports](https://console.cloud.tencent.com/ddos/antiddos-advanced/access/l4) page, select a rule you want to edit and click **Configuration**.
2. On the **Configure Layer-4 Forwarding Rule** page, modify parameters and click **OK** to save changes.

## Deleting Rules
1. On the [Access via ports](https://console.cloud.tencent.com/ddos/antiddos-advanced/access/l4) page, you can delete one or more rules.
   - To delete a rule, select a rule you want to delete. Click **Delete**.
   - To delete multiple rules, select more than one rules you want to delete. Click **Batch Delete**.
2. In the pop-up window, click **Delete**.

## Importing a Rule
1. To import multiple rules, you can click **Batch Import** on the [Access via ports](https://console.cloud.tencent.com/ddos/antiddos-advanced/access/l4) page.
2. In the **Configure Layer-4 Forwarding Rule** window, enter the rules, and click **OK**.

## Exporting a Rule
1. To import multiple rules, you can click **Batch Export** on the [Access via ports](https://console.cloud.tencent.com/ddos/antiddos-advanced/access/l4) page.
2. In the **Batch Export Layer-4 Forwarding Rules** window, select the rules you want to export, and click **Copy**.