## Feature Overview
### Overview
The web protection feature provides application layer protection for sites using the HTTP/HTTPS protocol. It also contains 500+ rules managed in the rules library and AI engine.
>?The EdgeOne console is not yet fully available. To access the console, please [contact us](https://intl.cloud.tencent.com/contact-us) for activation.

### Web/Bot action description[](id:explain)
The web protection and bot protection features allows you to set actions based on your business scenarios. There are three actions available:
- Block: The traffic to forward will be blocked. Meanwhile, a block page will be returned and attacks will be recorded.
- Observe: The traffic will be observed, while attacks will be recorded.
- Allow: The traffic will be allowed, while attacks will not be recorded.

## Basic Web Protection
This feature provides protection rules developed by Tencent Cloud over the years, delivering very low false negative and false positive rates, and fast responses to 0day threats.
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Select **Attack Defense** > **Web Protection** on the left sidebar.
2. Select a site. Turn on/off the switch ![](https://qcloudimg.tencent-cloud.cn/raw/7d363152eb0ea6c823ae278c4d118dc6.png) in the basic web protection module. If it’s off, all traffic detected will be allowed, while your configurations will not be deleted.
![](https://qcloudimg.tencent-cloud.cn/raw/34b9d6d62e6dfa6269cb462d788a8e9b.png)
2. To configure and modify the module, click **Set**.
![](https://qcloudimg.tencent-cloud.cn/raw/8be83ae2e94b0bad3446b6a8b636eef5.png)
3. The defense mode, defense level and rule list are editable.
![](https://qcloudimg.tencent-cloud.cn/raw/957d9f01f9377f651e38dae3a2a804e1.png)

**Parameter description:**
 - Defense mode: Select "Block" or "Observe".
   - In the Block mode, attack traffic detected will be blocked and attacks will be recorded. This mode is used by default when basic web protection is enabled.
   - In the Observe mode, attack traffic detected will be allowed and attacks will be recorded, helping observe false positives incurred by your policies. To block the attack traffic, you can switch to the Block mode after your policy tuning.
 - Defense level: There are four defense levels, namely, "Super strict", "Strict", "Normal", and "Loose". With a stricter mode enabled, the ability to identify and block suspicious attack traffic is stronger, which may cause false positives more easily. However, in a less strict mode, only obviously suspicious traffic will be identified and blocked with much lower false positives, though it provides lower security.
 - A rule list contains the following configuration items:
    - Rule ID: The unique identifier of a rule, which is used to track attack logs for analysis.
    - Attack type: It describes the type of attacks.
    - Rule level: The defense level of a rule. Policies with the same rule level can be enabled/disabled at a time.
    - Rule description: It describes the defense role of a rule.
    - On/Off: Turn the switch on/off to enable/disable a rule.

## Custom Rule
This feature allows you to create custom rules for a number of business use cases, such as allowing/blocking specific traffic.

### Adding a rule
1. On the web protection page, select a site. Click **Set** in the custom rule module.
![](https://qcloudimg.tencent-cloud.cn/raw/048acd0f93bd44c900dc1efbd32ae7f6.png)
2. On the custom rule page, click **Add Rule**. Set the rule name, matching method, action, and priority.
![](https://qcloudimg.tencent-cloud.cn/raw/a62e6c213fc0be1a13270aa901f58fae.png)

**Parameter description:**
 - Rule name: It consists of letters, digits and underscores. A rule name will be generated automatically if this parameter is left empty. Note that a rule name must be unique.
 - Matching method: It consists of configuration items such as the protocol field (http/https) and the logical operator (include/equal to). Up to 5 conditions per rule are allowed, and the relation among conditions is "AND". Note that the same field can only be configured once in each rule.
 - Actions: It provides three options: Allow, Block and Observe.
    - Allow: Traffic that matches the specified rule will be allowed without any checks.
    - Block: Traffic that matches the specified rule will be blocked. Meanwhile, attacks will be recorded and a block page will be returned.
    - Observe: Traffic that matched the specified rule will be allowed, while attacks will be recorded.
 - Priority: Execution order of a rule. Custom rules with higher priority (a larger priority value) take precedence over those with lower priority (a smaller priority value). For custom rules with the same priority, the later-added one will be executed first.
3. Click **OK**.

### Enabling a rule
1. On the web protection page, select a site. Click **Set** in the custom rule module.
![](https://qcloudimg.tencent-cloud.cn/raw/733fb44fd9a77d4668df5c5ca831caa9.png)
2. On the custom rule page, you can enable one or more rules.
  - To enable a single rule, turn on the switch ![](https://qcloudimg.tencent-cloud.cn/raw/171fbbf6fe32c80aba5be84541814e23.png) on the right of the rule.
  - To enable multiple rules, click **Enable** after you select rules you want to enable.
![](https://qcloudimg.tencent-cloud.cn/raw/7266c688b6a95ead8335e2c53d9afb4d.png)

### Disabling a rule
1. On the web protection page, select a site. Click **Set** in the custom rule module.
![](https://qcloudimg.tencent-cloud.cn/raw/048acd0f93bd44c900dc1efbd32ae7f6.png)
2. On the custom rule page, you can disable one or more rules.
  - To disable a single rule, turn off the switch ![](https://qcloudimg.tencent-cloud.cn/raw/057134e300a8daaed49b0d60348921e3.png) on the right of the rule.
  - To disable multiple rules, click **Disable** after you select rules you want to disable.
![](https://qcloudimg.tencent-cloud.cn/raw/0a82b8152c87a64baf8c9904e3a443c1.png)

### Deleting a rule
1. On the web protection page, select a site. Click **Set** in the custom rule module.
![](https://qcloudimg.tencent-cloud.cn/raw/048acd0f93bd44c900dc1efbd32ae7f6.png)
2. On the custom rule page, select a rule you want to delete, and click **Delete** on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/2188375abcf255e2b366053266ea6b1b.png)
3. In the pop-up window, click **Delete**.


## Rate Limit
This feature enables you to limit the frequency of a source IP accessing third-level domain names. If the access frequency is exceeded, the source IP will be blocked for a period of time.

### Adding a rule
1. On the web protection page, select a site. Click **Set** in the rate limit module.
![](https://qcloudimg.tencent-cloud.cn/raw/733fb44fd9a77d4668df5c5ca831caa9.png)
2. On the rate limit page, click **Add Rule**. Set the rule name, matching method, access frequency, action, penalty duration, and priority.
![](https://qcloudimg.tencent-cloud.cn/raw/62fe8b2ccfa8327a26b53e1104aa952a.png)

**Parameter description:**
 - Rule name: It consists of letters, digits and underscores. A rule name will be generated automatically if this parameter is left empty. Note that a rule name must be unique.
 - Matching method: It consists of configuration items such as the protocol field (http/https) and the logical operator (include/equal to). Up to 5 conditions per rule are allowed, and the relation among conditions is "AND". Note that the same field can only be configured once in each rule.
 - Access frequency: The frequency of a source IP accessing the current third-level domain name.
 - Actions: It provides three options: Allow, Block and Observe.
    - Block: Traffic that matches the specified rule will be blocked. Meanwhile, attacks will be recorded and a block page will be returned.
    - Observe: Traffic that matched the specified rule will be allowed, while attacks will be recorded.
 - Penalty duration: The amount of time used to observe/block the source IP when the action is triggered.
 - Priority: Execution order of a rule. Custom rules with higher priority (a larger priority value) take precedence over those with lower priority (a smaller priority value). For custom rules with the same priority, the later-added one will be executed first.

3. Click **OK**.

### Enabling a rule
1. On the web protection page, select a site. Click **Set** in the rate limit module.
![](https://qcloudimg.tencent-cloud.cn/raw/733fb44fd9a77d4668df5c5ca831caa9.png)
2. On the rate limit page, you can enable one or more rules.
  - To enable a single rule, turn on the switch ![](https://qcloudimg.tencent-cloud.cn/raw/171fbbf6fe32c80aba5be84541814e23.png) on the right of the rule.
  - To enable multiple rules, click **Enable** after you select rules you want to enable.
![](https://qcloudimg.tencent-cloud.cn/raw/7266c688b6a95ead8335e2c53d9afb4d.png)



### Disabling a rule
1. On the web protection page, select a site. Click **Set** in the custom rule module.
![](https://qcloudimg.tencent-cloud.cn/raw/048acd0f93bd44c900dc1efbd32ae7f6.png)
2. On the rate limit page, you can disable one or more rules.
  - To disable a single rule, turn off the switch ![](https://qcloudimg.tencent-cloud.cn/raw/eff5ccb39d4480475860ffb0b1ab0267.png) on the right of the rule.
  - To disable multiple rules, click **Disable** after you select rules you want to disable.
![](https://qcloudimg.tencent-cloud.cn/raw/0a82b8152c87a64baf8c9904e3a443c1.png)


### Deleting a rule
1. On the web protection page, select a site. Click **Set** in the custom rule module.
![](https://qcloudimg.tencent-cloud.cn/raw/048acd0f93bd44c900dc1efbd32ae7f6.png)
2. On the rate limit page, select a rule you want to delete, and click **Delete** on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/2188375abcf255e2b366053266ea6b1b.png)
3. In the pop-up window, click **Delete**.
