
Bot and application security supports bot management where you can enable and configure the provided modules, which can be used together with bot traffic analysis and access logs to protect the core APIs of your website from bots. Meanwhile, you can create fine-grained protection rules based on the session status provided by bot traffic analysis.

Bot management allows you to manage bots in a fine-grained manner with the following modules: client risk identification (browser bot defense), threat intelligence, AI evaluation, bot flow statistics, action scores, custom rules, token configuration, and legitimate bots. 

### Client risk identification (browser bot defense)
It applies dynamic security verification technology to generate a unique client ID that can be used to detect potential malicious bot behaviors in the client access to web or H5 pages.

### Threat intelligence
Relying on Tencent's nearly 20 years of network security experience and big data intelligence, it accurately identifies malicious IP and IDC access by monitoring the IP status in real time and adopting a risk scoring system, while intelligently identifying malicious bot characteristics to block access initiated by malicious bots, distributed bots, proxies, credential stuffing, and bargain hunting.

### AI evaluation
It applies AI models, built based on AI technology and Tencent’s rich experience in risk control and defense against cyber crime, along with big data analysis of access traffic to quickly identify and combat access behaviors from advanced persistent threat bots and hidden threat bots.

### Bot flow statistics
Leveraging big data analysis and statistics, it automatically identifies malicious traffic according to the traffic characteristics of your user group, modifies the malicious traffic threshold to stop the access from common bots and high-frequency bots, and adjusts the statistical model to block most bot bypassing behaviors.


### Action setting
A bot score is given based on the access requested detected by the threat intelligence, AI evaluation, bot flow statistics modules. The score range is 0-100. The higher the score, the higher the likelihood that the request is initiated by a bot and the greater the harm caused to the website. Based on the bot score, you can specify an action within a score range to block malicious access accurately.

### Session management
Different access behaviors of the same IP can be distinguished and abnormal user access can be accurately controlled without affecting other users by the specified location of the session token.

### Legitimate bots
It allows legitimate bots (such as search engines and feed bots) to obtain website data, so that the websites can be indexed normally.

### Custom rules
 Custom rules are rule that you can create to handle access requests initiated by specific bots.
