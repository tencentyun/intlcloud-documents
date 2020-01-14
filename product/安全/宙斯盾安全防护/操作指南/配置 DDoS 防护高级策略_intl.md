
Aegis Anti-DDoS provides advanced security protection policies against DDoS attacks. You can bind the policies to protective IPs or IPs protected by protection packs based on the needs of your business platform, and then use features such as protocol disabling, port disabling, IP blacklist/whitelist, message characteristic filtering policies and null session prevention to achieve targeted protection capabilities for the platform. For more information on the configuration, see [**Custom Advanced Security Policy**](https://intl.cloud.tencent.com/document/product/685/18800#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AE.89.E5.85.A8.E7.AD.96.E7.95.A5).

## Adding an Advanced Security Policy
1. Go to the [Aegis Anti-DDoS Console](https://console.cloud.tencent.com/gamesec), click **Advanced Anti-DDoS Policy* in the left pane, and click **Add Policy**. After successful addition, click **Configuration** in the "Operation" column to enter the policy configuration page.
![1](https://main.qcloudimg.com/raw/11e9043e9091e22122ba494483f272d4.png)
2. Select the disabled protocol and port to be configured, set the IP blacklist/whitelist, and filter the message characteristics. You can optionally enable the prevention against traffic from outside China and null sessions. Click OK to finish adding the policy.
![2](https://main.qcloudimg.com/raw/6a9ed6826316038298b2bd4d9ccf3c14.png)

## Binding an Advanced Security Policy Directly to a Protected IP
1. Click **Advanced Anti-DDoS Policy* in the left pane, and click a **Policy ID**.
![3](https://main.qcloudimg.com/raw/4817bd463538640d1ef1fe22cac202df.png)
2. Click **List of bound IPs** and click **Add IP**.
![4](https://main.qcloudimg.com/raw/d9823cf1e24d5787828ef61d0e93e542.png)

## Binding a DDoS Protective IP with an Advanced Security Policy
1. Click **DDoS Protective IP** and click "Protective IP".
![5](https://main.qcloudimg.com/raw/73e8199885af3acb65055fc32698cf60.png)
2. Click **Advanced configuration** on the **DDoS Protective IP** page. Click **Bind**, select an advanced anti-DDoS policy in the "Configure Advanced Anti-DDoS Policy" pop-up and click **OK**.
![6](https://main.qcloudimg.com/raw/fec960c5d75c5f86c8f7dec2a8b69aa0.png)

## Configuring an Advanced Security Policy for a Protected IP Under a DDoS Protection Pack
1. Click **DDoS Protection Pack** and click a protection pack ID.
![7](https://main.qcloudimg.com/raw/e063a0b9d0a19da4e51134400664c6ed.png)
2. On the DDoS protection pack details page, click **Protected IP List**, select the IP to be configured and click "Configure advanced security policy".
![8](https://main.qcloudimg.com/raw/447920da62277b2e5bac787b58be27c4.png)
