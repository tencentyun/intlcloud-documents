This document describes how to configure the bot flow statistics module in the bot analytics section of bot traffic management. Using big data analytics and statistics and AI technology, it automatically identifies malicious users based on characteristics of user traffic.

## Prerequisites
You have purchased a WAF instance and [bot traffic management extra pack](https://intl.cloud.tencent.com/document/product/627/47799#bot-.E8.A1.8C.E4.B8.BA.E7.AE.A1.E7.90.86.E4.BB.B7.E6.A0.BC.E8.AF.B4.E6.98.8E) and enabled bot analysis for WAF-connected domain names.

## Protection Configuration
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-botconfig) and select **Configuration center** > **Bot and application security** on the left sidebar.
2. On the **Bot and application security** page, select the target domain name in the top-left corner and click **Bot management**.
![](https://qcloudimg.tencent-cloud.cn/raw/0ce245727d7e77992b94c5df648ef8a8.png)
3. In **Global settings**, click **Configure now** in the **Bot flow statistics module** section.
![](https://qcloudimg.tencent-cloud.cn/raw/c1f85ac9e1901c95c63a592393bbd933.png)
4. On the **Bot flow statistics module** page, you can configure the detection level of different features.
![](https://qcloudimg.tencent-cloud.cn/raw/ec756b3e2fc12c366f8c8b0eb0c123b2.png)

**Parameter description:**
   - Name/Description:
      - Referer type: The number of deduped Referers in a session request is detected, with different thresholds for detecting an access request with a higher value than the corresponding threshold.
      - Total URL types: The number of deduped URLs in a session request is detected, with different thresholds for detecting an access request with a higher value than the corresponding threshold.
      - User-Agent type: The number of deduped User-Agents in a session request is detected, with different thresholds for detecting an access request with a higher value than the corresponding threshold.
      - Cookie type: The number of deduped cookies in a session request is detected, with different thresholds for detecting an access request with a higher value than the corresponding threshold.
      - Total sessions: The total number of sessions is detected, with different thresholds for detecting an access request with a higher value than the corresponding threshold.
     - Average speed: The average number of sessions per minute is detected, with different thresholds for detecting an access request with a higher value than the corresponding threshold.
     - Session duration: The session duration is detected, with different thresholds for detecting an access request with a higher value than the corresponding threshold.

   - Mode: Different detection levels correspond to different thresholds, which fluctuate with the number of website access requests.
	 - A higher detection level indicates a higher detection rate with a lower detection accuracy.
     - A lower detection level indicates a lower detection rate with a higher detection accuracy.
     - Intelligent recommendation automatically learns the historical traffic of your website to generate a recommended detection level in Tencent Security bot traffic management. The detection level is either loose or medium according to the current bot situation at your website.
        - On/Off: You can enable or disable the detection type of the current option. After this option is disabled, the detection item will not contribute to the bot score.

5. After the configuration, click the configuration page of a certain scenario, and click ![](https://qcloudimg.tencent-cloud.cn/raw/7fc653737ff3f26b04fbb43c7754a8d7.png) of the **Bot flow statistics module**.

## Best Practices of Bot Flow Statistics Module
The bot flow statistics module leverages the bot defense experience and accumulation of the bot attack/defense lab to quickly identify abnormal access behaviors. Therefore, we recommend you enable it and set **Rule level** to **Intelligent recommendation** under any circumstances.