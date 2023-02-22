## Overview
Tencent is the earliest and biggest instant messaging developer in China. In conformity with the trend of industrial digital transformation, Tencent now shares its high-concurrency and highly reliable instant messaging capabilities as SDKs and RESTful APIs and launches the Tencent Cloud product Instant Massaging (IM). You can integrate the IM SDKs provided by Tencent Cloud into your apps in a simple way. By calling RESTful APIs on the server side, you can easily have powerful instant communication capabilities. The following figure shows the interaction between the IM service and your apps.
![](https://qcloudimg.tencent-cloud.cn/raw/2e57bf9cbb3a1855efe7abdfd7d8beab.png)
For developer requirements and scenarios in different phases, the Instant Messaging (IM) team provides a series of solutions, including the Android, iOS, Windows, and web SDK components, as well as capabilities for integrating [RESTful APIs](https://intl.cloud.tencent.com/document/product/1047/34620) and [Webhooks](https://intl.cloud.tencent.com/document/product/1047/34354) on the server. With these components and capabilities, developers can construct reliable and stable IM products for free and global communication.

## Architecture
IM features a comprehensive suite of solutions including global access, one-to-one chat, group chat, message push, profile and relationship chain hosting, and account authentication. It also provides complete app access and backend management APIs.
![](https://main.qcloudimg.com/raw/6537f6e705289419963ee647ae851c94.png)
## Services
### Access service
The access service provides IM with highly interconnected, reliable, and secure global network connection channels and proprietary multi-level optimal addressing algorithms to implement scheduling across private and public networks. Technologies including intelligent compatibility for passing through gateway policies, persistent connection multiplexing, transport-layer protocol optimization, and channel encryption allow businesses to establish simple and reliable communication with business backends without concerns about network details.
When terminals log in, the IM SDK connects to the nearest access nodes. IM access nodes include the following:

- China: South China, North China, East China, Hong Kong, Taiwan, etc.
- Other regions:
 - Asia: Singapore, Indonesia, UAE, Thailand, Malaysia, Japan, Vietnam, India, South Korea, and Philippines
 - Europe: United Kingdom, Netherlands, France, Germany, Italy, Norway, France, Russia, and Spain
 - South America: Brazil
 - North America: United States, Canada, and Mexico
 - Oceania: Australia
 - Africa: South Africa and Nigeria

### IDC
IM provides IDCs in China, South Asia (India), Southeast Asia (Singapore), Northeast Asia (Seoul, South Korea), and Europe (Frankfurt, Germany) for you to choose from. Your business data is stored in the IDC you selected when creating the app, and each IDC can be accessed globally.

### One-to-one chat
One-to-one chat supports various message types including text, emojis, locations, images, audio, short video, and custom message. It provides special features such as red packets, chatbots, read receipt, and message recall as well as services such as offline messages and roaming messages. For more information, see [One-to-One Messages](https://intl.cloud.tencent.com/document/product/1047/33523).

### Group chat
A group chat involves multiple participants. IM supports the following five group types based on group joining and organization management methods to meet the requirements of different group chat scenarios.

- **Work group (Work)**: After a work group is created, users can join the group only by being invited by group members. The invitation does not need to be accepted by the invitee or approved by the group owner.
- **Public group (Public)**: After a public group is created, the group owner can designate group admins. To join the group, a user needs to search for the group ID and send a request, and the request needs to be approved by the group owner or an admin before the user can join the group.
- A **meeting group (Meeting)** allows users to join and exit freely and supports viewing message history from before the user joined the group. Meeting groups are ideal for scenarios that integrate Tencent Real-Time Communication (TRTC), such as audio and video conferences and online education.
- **Audio-video group (AVChatRoom)**: Allows users to join and exit freely, supports an unlimited number of members, and does not store message history. Audio-video groups can be used with Cloud Streaming Services (CSS) to support on-screen comment chat scenarios.
- **Community group (Community)**: Allows users to join and exit freely and is ideal for ultra-large community group chat scenarios, such as knowledge sharing and game communication
>?The community feature is supported by the SDK of the Enhanced edition on v5.8.1668 or later and the SDK for web on v2.17.0 or later. You need to purchase the Ultimate edition, go to the [**console**](https://console.cloud.tencent.com/im/qun-setting), select **Group feature configuration**, and enable **Community**.

Groups are highly customizable, supporting custom group types, group fields, group member fields, group IDs, and event callbacks. You can fully customize your group based on the needs of your app. For more information, see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529).
>!Although audio-video groups (AVChatRoom) support unlimited group members, if a spike in group members is expected within a short time (in scenarios such as large online events where the number of members in a single group reaches 50,000 or above), contact the [channel manager](https://cloud.tencent.com/about/connect) in advance and report service resource usage by providing the SDKAppID and the scheduled event time.



### Profile and relationship chain hosting
IM provides a holistic solution for profile and relationship chain management, storing user profiles (for example, nicknames, profile photos, and custom profile fields), friend lists, blocklists, and other information. IM's profile and relationship chain hosting service provides a backup service with up to 12 copies and multi-data center remote deployment to improve service quality and disaster recovery performance. For more information, see [Profile Management](https://intl.cloud.tencent.com/document/product/1047/33520) and [Relationship Chain Management](https://intl.cloud.tencent.com/document/product/1047/33521).

### Account authentication
Data security is ensured with asymmetric encryption ECDSA-SHA256 and hash encryption HMAC-SHA256 (HMAC-SHA256 is recommended). Developers can directly use the app’s own account to quickly integrate IM services, freeing themselves from tedious account mapping work. With simple SDK integration and convenient API calls, it is easy to authenticate user accounts (UserID) and passwords (UserSig). For more information, see [Login Authentication](https://intl.cloud.tencent.com/document/product/1047/33517).

## Management and Monitoring
In addition to basic instant messaging features, IM provides a convenient and easy-to-use console, which allows you to create apps, download IM SDKs, query app configurations, perform joint app testing, and integrate instant messaging capabilities. IM console also supports various features such as backend message delivery, group management, and statistics. For more information, see [Console Guide](https://intl.cloud.tencent.com/document/product/1047/34577).

## Advanced Features
### RESTful APIs
RESTful APIs are HTTP management APIs that provide the app backend with a management entry at the backend. For the list of RESTful APIs currently supported by IM, see [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

In addition to RESTful APIs, IM Console also provides simple features such as data management and one-to-one and one-to-many messaging. Developers can manage, view, and test data in IM Console. In contrast, RESTful APIs are less user-friendly, but they can provide more powerful management capabilities.


### Third-party callbacks
When IM initiates a [third-party callback](https://intl.cloud.tencent.com/document/product/1047/34354), it sends requests to the app backend before or after an event. Then, the app backend synchronizes data accordingly or intervenes in the subsequent processing of the event.
IM provides a diverse set of webhook events, which are free of charge. For more information, see the [Webhook Command List](https://intl.cloud.tencent.com/document/product/1047/34355).

## Private Deployment
Private deployment allows an enterprise to deploy systems directly to its own servers and save data locally. IM provides the private deployment feature to assist enterprises in the deployment, implementation, and Ops of the private version. If needed, apply for the [IM private service](https://cloud.tencent.com/apply/p/kotpgwc3vq).
>?To apply for the IM private service, you need to log in with your root account of Tencent Cloud.

## Security and Compliance
Compliance is the foundation for the development of Tencent Cloud IM, which meets the compliance requirements of different countries and industries. In addition to ensuring the **security, compliance, availability, confidentiality, and privacy** of the services it provides, IM also provides relevant support for its customers to **meet their and their customers' compliance requirements, reduce repeated investment in audit work, and improve auditing and management efficiency**.

<b>IM has passed SOC 1, SOC 2, and SOC 3 audits, meets the requirements of China's Cybersecurity Classified Protection 2.0 (Level 3), and is certified to ISO 9001, ISO 20000, ISO 27001, ISO 27017, ISO 27018, ISO 27701, ISO 29151, CSA STAR, NIST CSF, BS 10012, and K-ISMS.</b>

<style>
    .card-container {
        width: 380px;
				height:
        display: block;
        float: left;
        padding-left: 15px;
        padding-right: 15px;
        box-sizing: border-box;
    }

    .card {
        border-radius: 10px;
        padding-top: 10px;
        padding-left: 10px;
        padding-right: 10px;
        padding-bottom: 10px;
        margin-top: 30px;
        border: 1px solid #ebeef5;
        background-color: #fff;
        overflow: hidden;
        box-shadow: 0 2px 12px 0 rgb(0 0 0 / 10%);
        text-align: left;
    			height:260px;
    }
    
    .markdown-text-box img {
        box-shadow: none;
    }


    .titlename {
                color:#191919;f
        position: relative;
        top: -2px;
                font-weight: bolder;
                font-size: larger;
    }
        
        @media (max-width: 768px){
                .card-container,
                .scene-card-container{
                        width: 100%;
                }
                .scene-card > div{
                        width: 100%!important;
                        margin-left: 0!important;
                }
                img {
        box-shadow: none;
    }
        }
</style>

<div style="position: relative; box-sizing: border-box;  padding-bottom: 10px; margin-bottom: 10px; overflow:hidden">
    <div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/7c288e0b31526692c16a8e4fe641d6db.jpg" data-nonescope="true">
                                <p class="titlename">  <a href="https://intl.cloud.tencent.com/document/product/363/11543">SOC 1 Type II Report</a> </p>
																<p style="color:#586376;">This audit report describes the internal controls of Tencent Cloud's service system and is conducted in accordance with the section AT-C 320 of AICPA's Statement on Standards for Attestation Engagements No. 18 (SSAE No. 18).</p>
            </div>
</div>
 <div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/7c288e0b31526692c16a8e4fe641d6db.jpg" data-nonescope="true">
                                <p class="titlename">  <a href="https://intl.cloud.tencent.com/document/product/363/11543">SOC 2 Type II Report</a> </p>
                                <p style="color:#586376;">This audit report describes the security, availability, and confidentiality of Tencent Cloud's service system and is conducted in accordance with the section AT-C 205 of AICPA's SSAE No. 18 and TSP Section 100 (2017 version).</p>
            </div>
</div>
<div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;"src="https://qcloudimg.tencent-cloud.cn/raw/7c288e0b31526692c16a8e4fe641d6db.jpg" data-nonescope="true">
                                <p class="titlename">  <a href="https://intl.cloud.tencent.com/document/product/363/11543">SOC 3 Type II Report</a> </p>
																<p style="color:#586376;">This is a general use report describing the security, availability, and confidentiality of Tencent Cloud's service system and is conducted in accordance with the section AT-C 205 of AICPA's SSAE No. 18 and TSP Section 100 (2017 version).</p>
            </div>
</div>
<div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;"src="https://qcloudimg.tencent-cloud.cn/raw/7e62e559319afa51562101026009f0e3.png" data-nonescope="true">
                                <p class="titlename">  <a href="https://www.tencentcloud.com/document/product/363/2487">Cybersecurity Classified Protection 2.0 </a></p>
																<p style="color:#586376;">Tencent’s fintech solutions are registered for level 4 protection, and our public cloud services are registered for level 3 protection.</p>
            </div>
</div>
 <div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;"src="https://qcloudimg.tencent-cloud.cn/raw/be5a02d7027805cec66391d24d5382d6.png" data-nonescope="true">
                                <p class="titlename">  <a href="https://intl.cloud.tencent.com/document/product/363/2410">ISO 9001 Standard for Quality Management Systems</a>
																<p style="color:#586376;">Tencent Cloud is China’s first cloud computing service provider accredited by both CNAS (China National Accreditation Service for Conformity Assessment) and ANAB (ANSI-ASQ National Accreditation Board) in accordance with ISO 9001. We implement effective quality control processes to deliver quality cloud services.</p></p>
            </div>
</div>
<div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/0f2f62361c7420c58bfeab74c42373da.png" data-nonescope="true">
                                <p class="titlename">  <a href="https://intl.cloud.tencent.com/document/product/363/2409">ISO 20000 Standard for IT Service Management Systems</a> </p><p style="color:#586376;">With strictly followed IT service management processes, Tencent Cloud is China’s first cloud computing service provider certified to ISO 20000-1:2018.</p>
            </div>
</div>
<div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/b3b88a42e294d602d7af7d42aa343b4d.png" data-nonescope="true">
                                <p class="titlename">  <a href="https://intl.cloud.tencent.com/document/product/363/2408">ISO 27001 Standard for Information Security Management Systems</a></p><p style="color:#586376;">ISO/IEC 27001:2015 is a supplement to ISO/IEC 27002:2013. The certification is a testament to the effectiveness of Tencent Cloud’s information security controls.</p>
            </div>
</div>
 <div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/4934c5489f0cb35f8e1e16614fc07593.png" data-nonescope="true">
                                <p class="titlename">  <a href="https://intl.cloud.tencent.com/document/product/363/33541">ISO 27017 Guidelines for Information Security Controls of Cloud Services</a> </p><p style="color:#586376;">ISO/IEC 27017:2015 is a supplement to ISO/IEC 27002:2013. The certification is a testament to the effectiveness of Tencent Cloud’s information security controls.</p>
            </div>
 </div>
 <div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/c5b246657205e0023ea89b19d95b6753.png" data-nonescope="true">
                                <p class="titlename">  <a href="https://intl.cloud.tencent.com/document/product/363/14031">ISO 27018 Standard for Personal Data Protection in Public Clouds</a></p><p style="color:#586376;">Tencent Cloud is committed to building a sound personal information management system and using different technologies to protect the personal data of each user.</p>
            </div>
</div>
 <div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;"src="https://qcloudimg.tencent-cloud.cn/raw/0b37fbf8d1bfa04031db30ed15d76f9b.png" data-nonescope="true">
                                <p class="titlename">  <a href="https://intl.cloud.tencent.com/document/product/363/33540">ISO 27701 Standard for Data Privacy Controls</a> <p style="color:#586376;">Tencent Cloud is the world’s first cloud service provider to become ISO/IEC 27701 certified. We have implemented an effective data privacy management system which we continue to improve.</p></p>
            </div>
</div>
 <div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;"src="https://qcloudimg.tencent-cloud.cn/raw/f652574979d9db78c8a991ca4b8a78fc.png" data-nonescope="true">
                                <p class="titlename">  <a 
            </div>
        </div>
<div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;"src="https://qcloudimg.tencent-cloud.cn/raw/32d85d30e2129e5f22259918ff1d6619.png" data-nonescope="true">
                                <p class="titlename">  <a href="https://intl.cloud.tencent.com/document/product/363/7249">CSA STAR Certification</a> </p><p style="color:#586376;">CSA STAR certification is an internationally recognized cloud security certification program. Tencent Cloud has been awarded a Gold rating by STAR and continues to strengthen its security posture.</p>
            </div>
</div>
 <div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/a18be30e18d5f87d324094f9353083d0.png" data-nonescope="true">
                                <p class="titlename">  <a href="https://intl.cloud.tencent.com/document/product/363/45469">NIST Cybersecurity Framework</a> </p><p style="color:#586376;">The NIST Cybersecurity Framework was released by the US National Institute of Standards and Technology in response to Executive Order 13636 "Improving Critical Infrastructure Cybersecurity". The framework emphasizes the use of business drivers to guide cybersecurity activities.</p>
            </div>
</div>
<div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;"src="https://qcloudimg.tencent-cloud.cn/raw/23115be55af090caf230525be53b883d.png" data-nonescope="true">
                                <p class="titlename">  <a href="https://intl.cloud.tencent.com/document/product/363/34542">K-ISMS Certification</a> </p><p style="color:#586376;">Tencent Cloud is China’s first K-ISMS certified cloud computing provider. The certification is an assurance that Tencent Cloud’s information security management system and capabilities comply with relevant laws and standards in South Korea.</p>
            </div>
</div>
<div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;"  src="https://qcloudimg.tencent-cloud.cn/raw/eac6c9f40236f5ad1028ddbb34a2c5cb.png" data-nonescope="true">
                                <p class="titlename">  <a 
            </div>
</div>
</div>
