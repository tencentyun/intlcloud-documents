## Protection Description
"CC Protection" identifies and blocks CC attacks based on access attributes and connection status. It provides scenario-specific configurations to create protection rules, helping secure your business. It also supports the cleaning threshold setting.


## Prerequisites
You have purchased an [Anti-DDoS Advanced instance](https://intl.cloud.tencent.com/document/product/297/37241) and set the object to protect.

## Directions
1. Log in to the [Anti-DDoS console](https://console.cloud.tencent.com/ddos/antiddos-advanced/config/port) and select **Anti-DDoS Advanced (New)** > **Configurations** on the left sidebar. Open the **CC Protection** tab.
2. Select a domain name from the IP list.
 ![](https://qcloudimg.tencent-cloud.cn/raw/48b33703155d1418b3a1c3aab979e8f4.png)
3. To enable CC protection in the "CC Protection and Cleansing Threshold" section, click ![](https://qcloudimg.tencent-cloud.cn/raw/b56da8e70914bb5f6fce1900bcf81ef5.png) and set a cleansing threshold.
![](https://qcloudimg.tencent-cloud.cn/raw/48b33703155d1418b3a1c3aab979e8f4.png)
>?
>- This switch controls wether to enable CC protection. Only when it is on, all the CC protection policies take effect.
>- The cleansing threshold is the threshold for Anti-DDoS services to start cleansing traffic. If the number of HTTP requests sent to the specified domain name exceeds the threshold, CC protection will be triggered.
>- If the protection is enabled, your Anti-DDoS Advanced instance will use the default cleansing threshold after your business is connected, and the system will generate a baseline based on historical patterns of your business traffic. You can also set the cleansing threshold for your business needs.
>- If you have a clear concept about the threshold, set it as required. Otherwise please leave it to the default value. Anti-DDoS will automatically learn through AI algorithms and generate the default threshold for you.
