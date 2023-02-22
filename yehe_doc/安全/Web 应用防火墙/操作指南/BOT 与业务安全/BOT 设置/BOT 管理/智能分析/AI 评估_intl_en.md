This document describes the AI policy module in bot traffic management. This feature is built on Tencent's nearly 20 years of experience in cybersecurity and bot defense. It applies AI models, built based on AI technology and Tencent's experiences in controlling risks and fighting illegal activities, to quickly identify malicious requests and fight against previous, APT, and distributed bots.

## Prerequisites
You have purchased a WAF instance and [bot traffic management extra pack](https://www.tencentcloud.com/document/product/627/47799#bot-.E8.A1.8C.E4.B8.BA.E7.AE.A1.E7.90.86.E4.BB.B7.E6.A0.BC.E8.AF.B4.E6.98.8E) and enabled bot rule management for WAF-connected domain names.

## Protection Configuration
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-botconfig) and select **Configuration center** > **Bot and application security** on the left sidebar.
2. On the **Bot and application security** page, select the target domain name in the top-left corner and click **Bot management**.
![](https://qcloudimg.tencent-cloud.cn/raw/078651f75b12336ea8f1efcfc27808f7.png)
3. In global settings, click **Configure now** in the **Browser bot defense module** section.
![](https://qcloudimg.tencent-cloud.cn/raw/a6b3c43f7ec6f0624b1e47245532c4d6.png)
4. Click **Add to allowlist** to add certain URLs to the allowlist to reduce false positives detected by AI.
![](https://qcloudimg.tencent-cloud.cn/raw/259ca9ed22c140e21f0988106d802ae5.png)
5. On the AI policy page, you can add URLs to the allowlist, so that core business will not be blocked due to frequent access to core business/callback business. You can also add certain URLs to the allowlist so that they will not be blocked by mistake.
>? Here, the allowlist applies only to the AI policy module but not other modules.


**Parameter description:**
  - **Policy name**: Policy name.
  - **Rule description**: Policy description.
  - **Allowed URL**: URL allowed by the AI policy module, which affects the score of the AI policy module.
  - **On/Off**: You can enable/disable an allowlist in the AI policy module. When this option is on, the AI policy module will not add the score of the URL that hits the allowlist. The score will be provided by the threat intelligence module and bot flow statistics module.
6. After configuring the AI policy module, click the configuration page of a certain scenario and click ![](https://qcloudimg.tencent-cloud.cn/raw/c9174793080a26017ba65359b80ddde0.png) of the AI policy module.

## Best practices
The AI policy module leverages the bot defense experience and the accumulation of the bot attack/defense lab to quickly identify general and APT bots. Therefore, we recommend you enable it and add the business callback API to the allowlist under any circumstances.