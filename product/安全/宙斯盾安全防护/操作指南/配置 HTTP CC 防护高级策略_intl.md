
Aegis Anti-DDoS provides advanced protection policies against HTTP CC attacks. The anti-CC defense policy triggers CC protection when the number of HTTP requests exceeds the set QPS value. For more information on the configuration, see [**Custom Advanced Security Policy**](https://cloud.tencent.com/document/product/685/18800#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AE.89.E5.85.A8.E7.AD.96.E7.95.A5).

## Adding a CC Protection Policy
1. Go to the [Aegis Anti-DDoS Console](https://console.cloud.tencent.com/gamesec), click **Advanced HTTP Anti-CC Defense Policy* in the left pane, and click **Add Policy**. After successful addition, click **Configuration** in the "Operation" column to enter the policy configuration page.
![1](https://i.imgur.com/yDiQsHG.png)
2. Configure options such as HTTP QPS request threshold, URL whitelist, IP blacklist and whitelist and custom anti-CC defense mode based on business characteristics and protection requirements. Click OK to finish adding the policy.
![2](https://i.imgur.com/mfY0Xyt.png)

## Binding an Anti-CC Defense Policy Directly to a Protected IP
1. Click **Advanced HTTP Anti-CC Defense Policy* in the left pane, and click a **Policy ID**.
![3](https://i.imgur.com/VYBlSMr.png)
2. Click **List of bound IPs** and click **Add IP**.
![4](https://i.imgur.com/Nj10vJm.png)

## Binding a DDoS Protective IP with an Anti-CC Defense Policy
1. Click **DDoS Protective IP** and select a protective IP to enter the DDoS protective IP details page.
![5](https://i.imgur.com/pAeeKuk.png)
2. Click "Advanced Configuration". Click **Bind**, select an anti-CC defense policy and click **OK**.
![6](https://i.imgur.com/i37QogR.png)

## Configuring an Anti-CC Defense Policy for a Protected IP Under a DDoS Protection Pack
1. Click **DDoS Protection Pack** and select a protection Pack ID to enter the DDoS protection pack details page.
![7](https://i.imgur.com/ME4OtML.png)
2. Click **Protected IP List**, select the IP to be configured and click "Configure HTTP anti-CC defense policy".
![8](https://i.imgur.com/E9k6P1r.png)
