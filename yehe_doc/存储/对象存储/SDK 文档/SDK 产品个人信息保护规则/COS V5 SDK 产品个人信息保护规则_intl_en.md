## Introduction

QCloudCOSXML for iOS or COSXML for Android (the "SDK Product") is developed by Tencent Cloud Computing (Beijing) Co., Ltd. ("we", "us", or "our") with the registered address at 309, 3/F (West), No. 49, Zhichun Road, Haidian District, Beijing, China.

This Personal Information Protection Policy for COS SDK v5 ("Policy") is intended to inform developers and end users of the collection, use, and processing of end users' personal information by the SDK Product as necessary to implement its features.

**Please read this Policy carefully. If you are a developer, please acknowledge that you fully understand and agree to this Policy before integrating the SDK Product. If you do not consent to this Policy or agree to fulfill your obligations to protect end users' personal information in accordance with this Policy, you must immediately stop connecting to and using the SDK Product. You shall integrate the SDK Product and process end users' personal information only after obtaining their consent.**

## Notes

**If you are a developer,**
1. **You shall comply with applicable laws and regulations in connection with your collection, use, and processing of end users' personal information, including but not limited to developing and publishing a privacy policy governing personal information protection.**
2. **Before integrating the SDK Product, you shall inform end users of the collection, use, and processing of their personal information by the SDK Product and legally obtain their consent.**
3. **Unless otherwise required by laws and regulations, you shall not collect end users' personal information before obtaining their consent.**
4. **You shall provide an easy-to-use, legally compliant mechanism that allows end users to exercise their rights and explain to them how to query, copy, modify, delete, restrict the processing of, transfer, or get a copy of their personal information, withdraw their consent, and cancel their account.**
5. **You shall comply with the requirements specified in this Policy.**

If you have any questions or comments about the content of this Policy, feel free to contact us through the channels as provided in Article 8 of this Policy.

## 1. Information We Collect and How We Use It

#### 1.1 Personal information required to implement the features of the SDK Product

To implement the features of the SDK Product, we will collect from end users or developers the following personal information generated during the use of such features by end users:
<table>
<tbody>
<tr>
<td style="width: 15%;"><strong>OS</strong></td>
<td style="width: 15%;"><strong>Type of Personal Information</strong></td>
<td><strong>Purpose of Processing</strong></td>
<td style="width: 20%;"><strong>Method of Processing</strong></td>
</tr>
<tr>
<td>Android and iOS</td>
<td>Network status</td>
<td>Optimize the SDK based on requests under different network conditions.</td>
<td>Encrypted transfer</td>
</tr>
<tr>
<td>Android</td>
<td>IP address</td>
<td>Analyze whether network linkages are properly resolved when network requests are made.</td>
<td>Encrypted transfer</td>
</tr>
<tr>
<td>Android</td>
<td>System attributes</td>
<td>Optimize the SDK based on system version differences.</td>
<td>Encrypted transfer</td>
</tr>
<tr>
<td>Android</td>
<td>Multimedia files</td>
<td>Read local files and upload them to COS or download files stored in COS to the local file system. We cannot upload or download files without permission.</td>
<td>Encrypted transfer</td>
</tr>
<tr>
<td>iOS</td>
<td><strong>Clipboard</strong></td>
<td><strong>Agree on a string of characters with the user, so that when the agreed characters are present on the user's clipboard,</strong>
<strong>we can send the SDK logs to the App/SDK to help the user troubleshoot issues.</strong>
</td>
<td><strong>To be read only inside the SDK without transfer</strong></td>
</tr>
</tbody>
</table>

To implement the features of the SDK Product, we will embed the following third-party SDKs in the SDK Product:

<table>
<tbody>
<tr>
<td style="width: 10%;"><strong>OS</strong></td>
<td style="width: 15%;"><strong>Third-Party SDK</strong></td>
<td style="width: 20%;"><strong>Provider</strong></td>
<td style="width: 20%;"><strong>Type of Processed Personal Information</strong></td>
<td style="width: 15%;"><strong>Purpose</strong></td>
<td style="width: 20%;"><strong>Personal Information Protection Policy for Third-Party SDK</strong></td>
</tr>
<tr>
<td>Android</td>
<td>OkHttp v3</td>
<td>Square, Inc.</td>
<td>Not to collect</td>
<td>Network request</td>
<td>N/A (open-source library)</td>
</tr>
<tr>
<td>Android</td>
<td>Okio</td>
<td>Square, Inc.</td>
<td>Not to collect</td>
<td>Data read/write</td>
<td>N/A (open-source library)</td>
</tr>
<tr>
<td>Android</td>
<td>Bolt-task</td>
<td>Meta Platforms, Inc.</td>
<td>Not to collect</td>
<td>Job processing</td>
<td>N/A (open-source library)</td>
</tr>
<tr>
<td>Android</td>
<td>DataInsight</br>com.tencent.qmsp.sdk:qmsp-sdk-official</td>
<td>Shenzhen Tencent Computer System Co., Ltd.</td>
<td>Platform/Device manufacturer, device OS version, local language, time zone, and network status (Wi-Fi status)</td>
<td>Performance data reporting</td>
<td><a href="https://privacy.qq.com/document/preview/a19a8cf4f2354306b137a7db39d32024">Privacy Protection Policy for DataInsight SDK</a></td>
</tr>
<tr>
<td>Android</td>
<td>QIMEI<br>com.tencent.qmsp.oaid2</td>
<td>Shenzhen Tencent Computer System Co., Ltd.</td>
<td>Network type and IP address</td>
<td>Performance data reporting</td>
<td><a href="https://privacy.qq.com/document/preview/91754d6dd7824e3689f17782c580e06e">Personal Information Protection Policy for QIMEI SDK</a></td>
</tr>
<tr>
<td>iOS</td>
<td>DataInsight</td>
<td>Shenzhen Tencent Computer System Co., Ltd.</td>
<td>Network status</td>
<td>Performance reporting</td>
<td><a href="https://privacy.qq.com/document/preview/a19a8cf4f2354306b137a7db39d32024">Privacy Protection Policy for DataInsight SDK</a></td>
</tr>
</tbody>
</table>

#### 1.2 Permissions required to implement the features of the SDK Product

To implement the features of the SDK Product, we will request the required permissions through the application.

<table>
<tbody>
<tr>
<td style="width: 15%;"><strong>OS</strong></td>
<td style="width: 15%;"><strong>Permission</strong></td>
<td><strong>Purpose</strong></td>
<td style="width: 25%;"><strong>Required</strong></td>
</tr>
<tr>
<td>Android</td>
<td>Network permission</td>
<td>Allow access to the network to implement upload and download features.</td>
<td>Yes</td>
</tr>
<tr>
<td>Android</td>
<td>Storage permission</td>
<td>Read local files and upload them to COS or download files stored in COS to the local file system. We cannot upload or download files without permission.</td>
<td>No</td>
</tr>
<tr>
<td>Android</td>
<td>Bluetooth</td>
<td>Upload files transferred over Bluetooth.</td>
<td>No</td>
</tr>
<tr>
<td>iOS</td>
<td>Network permission</td>
<td>Allow access to the network to implement upload and download features.</td>
<td>Yes</td>
</tr>
<tr>
<td>iOS</td>
<td>Album permission</td>
<td>Upload images and videos from the app.</td>
<td>To be requested by the app but not the SDK</td>
</tr>
<tr>
<td>iOS</td>
<td>Bluetooth permission</td>
<td>Transfer and upload files over Bluetooth.</td>
<td>To be requested from the app if the files to be uploaded from the app are transferred over Bluetooth</td>
</tr>
<tr>
<td>iOS</td>
<td>Mic permission</td>
<td>Upload taken photos or videos.</td>
<td>To be requested from the app to upload taken photos or videos from the app</td>
</tr>
<tr>
<td>iOS</td>
<td>Camera permission</td>
<td>Upload taken videos.</td>
<td>To be requested from the app to upload taken videos from the app</td>
</tr>
</tbody>
</table>

Note that the permission display and disablement methods may vary by device and system and are subject to the used device and as further described in the operating system developers' instructions. By disabling a permission, end users deny the permission. In this case, we and developers will no longer collect and use the personal information corresponding to the permission and thus will not be able to provide the features that can be provided only if end users enable the permission.

#### 1.3 Exceptions to requiring user consent under laws and regulations

1. As necessary for the conclusion or performance of the contract with end users.
2. As necessary to fulfill our legal obligations.
3. As necessary to cope with public health emergencies or protect the health or property safety of end users in an emergency.
4. The reasonable processing of end users' personal information for news coverage or public opinion supervision in line with the public interest.
5. The reasonable processing of end users' personal information made public by themselves or otherwise legally made public in accordance with this Policy.
6. Other circumstances stipulated by laws and regulations.

Note: Any information collected by us that cannot identify end users alone or in combination with other information is not personal information within the meaning of the law.

#### 1.4 Automatic start or associated start by the SDK

In general, the SDK Product will not automatically start the app or be started along with the app. To make it easy for developers to debug bugs and to provide access to logs, the SDK Product for iOS will transfer its logs to the app when the string of characters on the end user's clipboard matches the string of characters agreed on with the end user. We offer developers the `shouldShowLog` API, which can be called to give end users the option to enable associated start. If you are a developer, click [here](https://github.com/tencentyun/qcloud-sdk-ios/blob/master/README.md) for instructions. In addition, you shall inform end users of the circumstances under which the SDK will automatically start the app or be started along with the app, and provide them the option to enable or disable associated start.

## 2. Data Processing by Third Parties and Public Disclosure of Information

To implement the features of the SDK Product, we will share personal information with third parties for the following purposes and in the following use cases:
<table>
<tbody>
<tr>
<td style="width: 13%;"><strong>OS</strong></td>
<td style="width: 15%;"><strong>Third Party Name</strong></td>
<td style="width: 10%;"><strong>Product/Type</strong></td>
<td style="width: 10%;"><strong>Information</strong></td>
<td style="width: 15%;"><strong>Purpose</strong></td>
<td style="width: 13%;"><strong>Use Case</strong></td>
<td style="width: 10%;"><strong>Sharing Method</strong></td>
<td style="width: 14%;"><strong>Third-Party Personal Information Protection Policy</strong></td>
</tr>
<tr>
<td>Android and iOS</td>
<td>Shenzhen Tencent Computer System Co., Ltd.</td>
<td>DataInsight SDK</td>
<td>Network status</td>
<td>Analyze the transfer performance under different network conditions.</td>
<td>COS API request</td>
<td>Encrypted transfer</td>
<td style="width: 33.476%;"><a href="https://privacy.qq.com/document/preview/a19a8cf4f2354306b137a7db39d32024">Privacy Protection Policy for DataInsight SDK</a></td>
</tr>
<tr>
<td>Android</td>
<td>Shenzhen Tencent Computer System Co., Ltd.</td>
<td>DataInsight SDK</td>
<td>IP address</td>
<td>Analyze whether network linkages are properly resolved when network requests are made.</td>
<td>COS API request</td>
<td>Encrypted transfer</td>
<td><a href="https://privacy.qq.com/document/preview/a19a8cf4f2354306b137a7db39d32024">Privacy Protection Policy for DataInsight SDK</a></td>
</tr>
<tr>
<td>Android</td>
<td>Shenzhen Tencent Computer System Co., Ltd.</td>
<td>DataInsight SDK</td>
<td>System attributes</td>
<td>Analyze the attributes of devices with poor performance.</td>
<td>COS API request</td>
<td>Encrypted transfer</td>
<td><a href="https://privacy.qq.com/document/preview/a19a8cf4f2354306b137a7db39d32024">Privacy Protection Policy for DataInsight SDK</a></td>
</tr>
</tbody>
</table>

We will not transfer end users' personal information to any companies, organizations, or individuals, except that:
1. We notify end users in advance of the type of personal information to be transferred about them and for what purpose, how, and to whom it will be transferred, and obtain their separate consent.
2. If we need to transfer personal information as part of a merger, division, dissolution, or bankruptcy, we will notify end users of the transferee's name and contact information and request the transferee to continue the fulfillment of the obligations as a personal information processor. We will request the transferee to obtain end users' consent again before changing the original purpose or method of processing.
 
We will not publicly disclose end users' personal information, except that:
1. We have notified end users of the type of personal information to be publicly disclosed about them and for what purpose, how, and to whom it will be disclosed, and have obtained their separate consent.
2. We are required by laws, regulations, legal proceedings, lawsuits, or any government authorities.

## 3. How End Users Manage Their Own Information

We attach great importance to end users' right to manage their personal information and endeavor to help them do so, including querying, copying, and deleting their personal information, canceling their account, and configuring the privacy feature, to safeguard their rights. If you are a developer, you must provide methods for end users to query, copy, modify, and delete their personal information, withdraw their consent, and cancel their account.

End users have the right to withdraw their consent to the processing of their personal information based on such consent. We offer developers the capabilities to disable the SDK Product as instructed in [Getting Started](https://intl.cloud.tencent.com/document/product/436/12159) for Android or [Getting Started](https://intl.cloud.tencent.com/document/product/436/11280) for iOS. As we cannot interact directly with end users through UIs, end users can directly contact developers and request them to stop using the SDK Product, or contact us through the channels as provided in Article 8 of this Policy. If you are an end user, you understand that specific business features or services can be implemented only if you provide the information required by such features or services. If you withdraw your consent, we will be unable to continue providing the corresponding features or services, nor will we further process your relevant personal information. Your decision to withdraw your consent does not affect our processing of your personal information previously collected based on such consent.


## 4. Information Storage

#### 4.1 Information storage location

We will store personal information collected and generated in the territory of China in the territory of China in accordance with laws and regulations.

#### 4.2 Information retention period

Generally, we retain end users' personal information only for the minimum period of time necessary to achieve the purposes as described in this Policy, except:
- To comply with applicable laws and regulations.
- To comply with court decisions, judgments, or other legal proceedings.
- To comply with the law enforcement requirements of applicable government authorities.

## 5. Information Security

We implement appropriate safeguards to protect end users' personal information from loss, improper use, or unauthorized access or disclosure.
We protect end users' personal information in strict accordance with laws and regulations.
We use various safeguards within a reasonable level of security to protect the security of information.
For example, we use encryption, anonymization, and other means to protect end users' personal information.
We have a rigorous management policy, process, and organization in place to guarantee the information security.
For example, we strictly limit the access to information to specific people, request them to comply with their confidentiality obligations, and review their compliance.
In the event of a security incident such as personal information leakage, we will launch the contingency plan to prevent the expansion of the incident and notify developers through such means as push notification and notice.

## 6. Minor Protection

The SDK Product is oriented to adults.

If you are a developer, and end users are minors under the age of 14 ("minors"), you must inform the minors' parents or legal guardians of this Policy and may not process the minors' personal information unless you have obtained the consent of their parents or legal guardians. If we find that you have provided the personal information of minors to us without the consent of their guardians, we will take action to delete such personal information as soon as possible.

If you are the guardian of a minor and have any questions or claims regarding the protection of the minor's personal information, you can contact developers or contact us through the channels as provided in Article 8 of this Policy.

## 7. Changes

We may revise this Policy from time to time.

If any revisions to this Policy will lead to the substantial derogation of end users' rights under this Policy, we will announce such revisions through website notices or other means before such revisions take effect. If you are a developer, and the updated Policy specifies changes in the processing of end users' personal information, you must update your privacy policy in due course, notify end users in the form of a pop-up window, and obtain their consent. If end users do not agree to accept this Policy, you must stop integrating the SDK Product.

## 8. Contact Us

We have set up a personal information protection team and a personal information protection officer. If you have any questions, complaints, or comments about this Policy or personal information protection, you can:
- Contact us through [Tencent Customer Service](https://kf.qq.com/);
- Email your questions to Dataprivacy@tencent.com; or
- Mail to Data Privacy Protection Department, Tencent Binhai Building, No. 33, Haitian 2nd Road, Nanshan District, Shenzhen, Guangdong, China, 518054.

We will review such questions, complaints, or comments and respond within 15 business days or such other period as may be specified by laws and regulations.
