
With bot and application security, you can enable and configure modules in bot management, observe and analyze traffic through bot traffic analysis and access logs. Then, you can set refined policies based on the session status to protect core website APIs and businesses from bot attacks.

Bot management supports configuration of bot scenario types, client risk identification (browser bot defense module), threat intelligence module, AI evaluation module, bot flow statistics module, action score, custom rules, token configuration, and legitimate bots. You can configure these modules for refined bot management. 

### Scenario-based bot configuration
Leveraging Tencent Cloud's years of expertise in bot governance, this feature offers client risk identification (browser bot defense module), threat intelligence module, AI policy module, bot analytics module, action score, session management, legitimate bots, and custom rules specifically for flash sales, price/content crawling, and login scenarios. It simplifies configuration and makes everything easy to use.


### Client Risk Identification (Browser Bot Defense Module)
This feature uses the dynamic identity verification technology and generates a unique ID for each client's business request to detect possible bots and malicious crawlers in the access to websites or HTML5 pages.

### Threat Intelligence Module
This feature is built on Tencent's nearly 20 years of experience in cybersecurity and big data intelligence. It determines the status of an IP in real time and uses a scoring mechanism to quantify a risk. It precisely identifies the access from a malicious dynamic IP and IDC. In addition, it intelligently identifies the features of a malicious crawler to cope with risky access requests from malicious crawlers, distributed crawlers, proxies, credential stuffing, and bargain hunting.

### AI Evaluation Module
This feature builds AI evaluation models from AI technologies and Tencent's experiences in controlling risks and fighting cybercrimes. Through big data analysis and AI modeling of access traffic, it quickly identifies malicious requesters and defends against risky access requests from APT and hidden threat bots.

### Bot Flow Statistics Module
Based on big data analysis, this feature automatically classifies customer traffic by characteristic and identifies abnormal and malicious traffic. It automatically adjusts the malicious traffic threshold and handles risky access requests from general and high-frequency bots. With auto-adjustment modeling, it resolves most of the bot behavior bypasses.

### Action Setting
This feature leverages the threat intelligence module, AI evaluation module, and bot flow statistics module to provide a comprehensive score ranging from 0 to 100 for the risk level of an access request to a website. The higher the score, the more likely it is from a bot, and the higher the risk level. With the score provided by bot analytics, the risk level of an access request is intelligently identified, and you can precisely block a risky access request based on actions configured for different score ranges.

In addition, it supports configuring a scope so that request data covered by the scope can be handled precisely.

### Session Management
This feature allows you to configure the token location of a session to differentiate between access behaviors of different users through the same IP. Therefore, you can precisely handle a user with abnormal access behavior without affecting other users.

### Legitimate Bots
This feature allows legitimate bots (such as search engines and feed bots) to get website data so that the website can be normally indexed.

### Custom Rules
This feature allows you to precisely handle compliant crawlers and access requests with different characteristics.

In addition, it supports configuring a scope so that request data covered by the scope can be handled precisely.

### Bot allowlist
This feature allows you to add the access requests from specified public network users to the allowlist based on the combination of different features, such as HTTP packet session feature, request feature, cookie, HTTP header, scope, IP feature, User-Agent, Referer, and session settings.

Priority from high to low: Bot allowlist > Scenario 1 (priority 1) > Scenario 2 (priority 2) > ... > Scenario n (priority m).