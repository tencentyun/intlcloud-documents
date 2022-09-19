AI evaluation is a module provided in bot traffic management. This feature applies AI models, built based on AI technology and Tencent's experiences in controlling risks and fighting cyber crimes, to quickly identify and deal with malicious access from sophisticated bots, advanced persistent threat bots and distributed bots.

## Prerequisites
You have purchased a WAF plan and subscribed to [bot traffic management](https://intl.cloud.tencent.com/document/product/627/47799). Meanwhile, you have added a domain name to WAF.

## Protection Configuration
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-botconfig) and select **Configuration Center** > **Bot and Application Security** on the left sidebar.
2. On the page that appears, select a target domain name and click **Bot management**.
![](https://qcloudimg.tencent-cloud.cn/raw/078651f75b12336ea8f1efcfc27808f7.png)
3. In the bot management section, click ![](https://qcloudimg.tencent-cloud.cn/raw/25ee88daf408bcac2a80287e314e669c.png) in the AI evaluation module.
![](https://qcloudimg.tencent-cloud.cn/raw/a6b3c43f7ec6f0624b1e47245532c4d6.png)
4. If a false positive that requests are falsely blocked occurs, you can click **Add to allowlist** and add the specific URL.
![](https://qcloudimg.tencent-cloud.cn/raw/259ca9ed22c140e21f0988106d802ae5.png)
5. Repeated access requests will be blocked before your core business is affected. To prevent false positives, you can add related URLs to the allowlist.
>?This allowlist only takes effect on the AI evaluation module.

![](https://qcloudimg.tencent-cloud.cn/raw/d63cd19ef79d99a1da8d5ea1c847e55e.png)

   **Parameter description:**
   - Policy name: Name of the policy. This parameter does not affect the AI evaluation result.
   - Rule description: Description of the policy. This parameter does not affect the AI evaluation result.
   - Allowed URL: Path that is allowed by the module. This parameter can affect the AI evaluation result.
   - On/Off: Switch of the module allowlist. When it is on, URLs that hit the allowlist will be allowed, but not counted toward the bot score. You can check the bot score in the threat intelligence and bot flow statistics modules.


## Best Practices
With rich experience in bot defense, the AI evaluation module can detect malicious bots quickly. Therefore, we recommend enabling this feature regardless of the situation and adding business callback APIs to the allowlist.

