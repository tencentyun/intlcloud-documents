Bot flow statistics is a module provided in bot traffic management. This feature identifies malicious users by monitoring and analyzing the traffic characteristics of your user groups.

## Prerequisites

You have purchased a WAF plan and subscribed to [bot traffic management](https://intl.cloud.tencent.com/document/product/627/47799#bot-.E8.A1.8C.E4.B8.BA.E7.AE.A1.E7.90.86.E4.BB.B7.E6.A0.BC.E8.AF.B4.E6.98.8E). Meanwhile, you have added a domain name to WAF.

## Protection Configuration
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-botconfig) and select **Configuration Center** > **Bot and Application Security** on the left sidebar.
2. On the page that appears, select a target region and click **Bot management**.
![](https://qcloudimg.tencent-cloud.cn/raw/0ce245727d7e77992b94c5df648ef8a8.png)
3. On the bot management page, click ![](https://qcloudimg.tencent-cloud.cn/raw/f05a86c4176526c2846a61f2a2207a37.png) in the bot flow statistics module.
![](https://qcloudimg.tencent-cloud.cn/raw/c1f85ac9e1901c95c63a592393bbd933.png)
4. On the page displayed, configure different feature metrics.
![](https://qcloudimg.tencent-cloud.cn/raw/ec756b3e2fc12c366f8c8b0eb0c123b2.png)

**Parameter description:**
  - Name/Description:
      - Referer type: Number of deduplicated Referers in a session request. In different detection modes, it is used to determine access requests as abnormal when its probability threshold reaches.
      - URL type: Number of deduplicated URLs in a session request. In different detection modes, it is used to determine access requests as abnormal when its probability threshold reaches.
      - User-Agent type: Number of deduplicated User-Agents in a session request. In different detection modes, it is used to determine access requests as abnormal when its probability threshold reaches.
      - Cookie type: Number of deduplicated Cookies in a session request. In different detection modes, it is used to determine access requests as abnormal when its probability threshold reaches.
      - Total sessions: Total number of sessions. In different detection modes, it is used to determine access requests as abnormal when its probability threshold reaches.
     - Average session speed: Average number of sessions per minute. In different detection modes, it is used to determine access requests as abnormal when its probability threshold reaches.
     - Session duration: Amount of time a session lasts. In different detection modes, it is used to determine access requests as abnormal when its probability threshold reaches.
  - Mode: The probability thresholds of the metrics vary with different detection modes.
	 - If the detection mode is quite strict, the detection rate is higher, but the detection accuracy is lower.
     - If the detection mode is quite loose, the detection rate is lower, but the detection accuracy is higher.
     - The Auto mode is a mode produced by bot traffic management using the historical website traffic patterns. This mode switches from Loose to Strict automatically according to the bot situation of the website.
    - On/Off: It controls whether to enable feature metrics. If one feature metric is disabled, it will not be counted toward the bot score.

## Best Practices
As the bot flow statistics module is built based on accumulated experience in bot defense, you are recommended to enable this feature regardless of the situation and set the mode to "Auto".

