
Aegis Anti-DDoS provides advanced protection policies against HTTP CC attacks. The anti-CC defense policy triggers CC protection when the number of HTTP requests exceeds the set QPS value. For more information on the configuration, see [**Custom Advanced Security Policy**](https://intl.cloud.tencent.com/document/product/685/18800#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AE.89.E5.85.A8.E7.AD.96.E7.95.A5).

## Adding a CC Protection Policy
1. Go to the [Aegis Anti-DDoS Console](https://console.cloud.tencent.com/gamesec), click **Advanced HTTP Anti-CC Defense Policy* in the left pane, and click **Add Policy**. After successful addition, click **Configuration** in the "Operation" column to enter the policy configuration page.
![1](https://main.qcloudimg.com/raw/a32eaf1467ef22fd27cac77a7ce4b15f.png)
2. Configure options such as HTTP QPS request threshold, URL whitelist, IP blacklist and whitelist and custom anti-CC defense mode based on business characteristics and protection requirements. Click OK to finish adding the policy.
![2](https://main.qcloudimg.com/raw/5b6359d8248c3b1e34aedb073691a9fa.png)

## Binding an Anti-CC Defense Policy Directly to a Protected IP
1. Click **Advanced HTTP Anti-CC Defense Policy* in the left pane, and click a **Policy ID**.
![3](https://main.qcloudimg.com/raw/3d663831885c74d52b19c9377852d24d.png)
2. Click **List of bound IPs** and click **Add IP**.
![4](https://main.qcloudimg.com/raw/de18a5e19a794f66e789d3c39d8f77b1.png)

## Binding a DDoS Protective IP with an Anti-CC Defense Policy
1. Click **DDoS Protective IP** and select a protective IP to enter the DDoS protective IP details page.
![5](https://main.qcloudimg.com/raw/997da26bb158592f5b42a515e53406bc.png)
2. Click "Advanced Configuration". Click **Bind**, select an anti-CC defense policy and click **OK**.
![6](https://main.qcloudimg.com/raw/daa015ef589070bb7921909e113fa0f0.png)

## Configuring an Anti-CC Defense Policy for a Protected IP Under a DDoS Protection Pack
1. Click **DDoS Protection Pack** and select a protection Pack ID to enter the DDoS protection pack details page.
![7](https://main.qcloudimg.com/raw/c83a7d6e01ee0bc9e70ec1372b75c952.png)
2. Click **Protected IP List**, select the IP to be configured and click "Configure HTTP anti-CC defense policy".
![8](https://main.qcloudimg.com/raw/8913f39b80a97f0edb55fc90795232f9.png)
