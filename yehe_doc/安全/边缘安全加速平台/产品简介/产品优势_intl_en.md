## Integrated Platform
EdgeOne is an integrated edge security and acceleration platform offering 3D protection from layers 3 to 7.
- Anti-DDoS: It detects and cleanses DDoS attack traffic and guarantees the business availability based on diverse measures, for example, IP blocklist/allowlist and port blocking policies. Up to 2 Tbps protection bandwidth is provided.
- Rate limit: It uses mechanisms such as HTTP field match and access frequency monitoring to effectively cleanse CC attack traffic. Up to 70K QPS is provided.
- Web security protection: It effectively prevents top 10 OWASP web ricks like SQL injection and cross-site scripting (XSS) and quickly identifies and blocks bot behaviors.
- API security protection: It guarantees API access security based on a secure and reliable access authentication mechanism.

![](https://qcloudimg.tencent-cloud.cn/raw/a8aca67f5c50a8cd9efaf08890a8e54b.png)

## Web or Bot Attack Protection 
#### Bot recognition and protection
Based on the characteristics of protocols, IP intelligence, and custom sessions, it can accurately recognize and block various bots. In addition, it leverages data and threat intelligence to comprehensively analyze and learn crawler behaviors to build a crawler recognition model, which effectively solves problems of malicious crawler passthrough and benign crawler kill.

#### Web attack protection
It has an extensive attack characteristic library covering common OWASP security threats to effectively block web business security problems, including web attacks, intrusion vulnerability exploits, trojans, and backdoors. It also prevents zero-day vulnerabilities and adopts syntax analysis and AI smart detection engine to further improve the detection accuracy and reduce false positives.

 #### Around-the-clock active monitoring and response
Tencent Security team monitors your business security 24/7 to discover and respond to problems actively, greatly improving the responsiveness.

## Smart Protection
A smarter automatic protection service is developed based on multiple years of experience in attack backtracking.

#### Smart captcha
Based on many years of experience in CC attack prevention and research on cutting-edge trends in CC attack defense, the CC attack prevention system forms an effective client marking and identification solution. It continuously tracks clients to effectively solve problems of attack passthrough and normal user traffic kill in intense attack defense scenarios.

 
#### Automatic API recognition
An accurate automatic API recognition model is set up based on characteristic comparison in multiple dimensions such as UA, root directory, and CGI through in-depth analysis of big data. It can automatically recognize APIs to avoid mistakenly killing normal APIs and apps, greatly improving the API protection capabilities.

#### Attack backtracking
As an important component in response during and after security events, attack backtracking analyzes and collects evidence from the attack traffic to reveal the attack means used by attackers and get important information like attack source IPs and attack methods. This helps with subsequent protection policy adjustment and attack source tracing to avoid secondary attacks.

The system captures and analyzes the exception/attack event packets to extract the attack sources and packets as key evidence for attack backtracking. In addition, EdgeOne offers an all-around monitoring page to display a wide variety of information, including attack types, sources, ports, and traffic, which serves as the basis for you to adjust protection policies.

## Accurate Attack Source Positioning
The fingerprint recognition solution pinpoints attack sources to prevent your business from being affected.

#### Protocol flood attack protection
Attackers randomly forge large amounts of traffic over seldom used protocols. The system uses basic protection policies such as protocol blocking, regional traffic blocking, blocklist/allowlist, and network ACL, as well as the proprietary fingerprint recognition solution to perform in-depth recognition and match for diverse protocol characteristic fields, cleanse the flood attack traffic over all types of protocol, and thus prevent your business from being affected.

#### Accurate attack source positioning through fingerprint algorithm
Based on passive analysis of massive amounts of traffic and characteristics of multiple parameters such as TCP option, timestamp, and TTL, EdgeOne automatically determines the client operating system, application type, and device UID to accurately recognize attack sources. This helps effectively tackle different industry challenges like CC attack protection passthrough.
