
Aegis Anti-DDoS provides advanced security protection policies against DDoS attacks. You can bind the policies to protective IPs or IPs protected by protection packs based on the needs of your business platform, and then use features such as protocol disabling, port disabling, IP blacklist/whitelist, message characteristic filtering policies and null session prevention to achieve targeted protection capabilities for the platform. For more information on the configuration, see [**Custom Advanced Security Policy**](https://intl.cloud.tencent.com/document/product/685/18800#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AE.89.E5.85.A8.E7.AD.96.E7.95.A5).

## Adding an Advanced Security Policy
1. Go to the [Aegis Anti-DDoS Console](https://console.cloud.tencent.com/gamesec), click **Advanced Anti-DDoS Policy* in the left pane, and click **Add Policy**. After successful addition, click **Configuration** in the "Operation" column to enter the policy configuration page.
![1](https://i.imgur.com/Wl3AkVR.png)
2. Select the disabled protocol and port to be configured, set the IP blacklist/whitelist, and filter the message characteristics. You can optionally enable the prevention against traffic from outside China and null sessions. Click OK to finish adding the policy.
![2](https://i.imgur.com/yavb9sQ.png)

## Binding an Advanced Security Policy Directly to a Protected IP
1. Click **Advanced Anti-DDoS Policy* in the left pane, and click a **Policy ID**.
![3](https://i.imgur.com/RAyf1eu.png)
2. Click **List of bound IPs** and click **Add IP**.
![4](https://i.imgur.com/npch7l6.png)

## Binding a DDoS Protective IP with an Advanced Security Policy
1. Click **DDoS Protective IP** and click "Protective IP".
![5](https://i.imgur.com/XvPmr7Q.png)
2. Click **Advanced configuration** on the **DDoS Protective IP** page. Click **Bind**, select an advanced anti-DDoS policy in the "Configure Advanced Anti-DDoS Policy" pop-up and click **OK**.
![6](https://i.imgur.com/2q7m1qI.png)

## Configuring an Advanced Security Policy for a Protected IP Under a DDoS Protection Pack
1. Click **DDoS Protection Pack** and click a protection pack ID.
![7](https://i.imgur.com/8Oo1qt0.png)
2. On the DDoS protection pack details page, click **Protected IP List**, select the IP to be configured and click "Configure advanced security policy".
![8](https://i.imgur.com/t0TdZN8.png)
