Sending verification codes through SMS is the most popular and securest way to verify user identities. Currently, SMS verification codes are widely used in various application scenarios such as user registration, password reset, login protection, identity verification, random password generation, and transaction confirmation.
This document uses developing a verification code-enabled login and signup service based on [SCF](https://Intl.cloud.tencent.com/document/product/583) as an example to describe how to implement the SMS verification code feature.

In addition to SCF, you can also use the [SendSms](https://intl.cloud.tencent.com/document/product/382/34859) API for this purpose.

## Preparations
- You have [signed up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and [verified your organizational identity](https://intl.cloud.tencent.com/document/product/378/10496).
- You have purchased an SMS package.
- Prepare SMS signature owner qualification certificates.
 This document takes a business license as a qualification certificate for example.
- Understand the SMS body content review standards.
- Get the `SDKAppID` of the SMS application.

## Relevant Documents
- [Demo source code](https://github.com/tencentyun/scf-demo-repo/tree/master/Nodejs8.9-SmsVerificationCode)
- Other products' documentation
 - [VPC documentation](https://intl.cloud.tencent.com/document/product/215)
 - [TencentDB for Redis documentation](https://intl.cloud.tencent.com/document/product/239/3205)
 - [SCF documentation](https://intl.cloud.tencent.com/zh/document/product/583)

## Step 1. Configure SMS content[](id:Step1)
After an SMS signature or body template is submitted, it will be reviewed within two hours generally. You can [configure alarm contacts](https://intl.cloud.tencent.com/document/product/382/35470) and set template/signature review notifications to receive review result notifications.

### Step 1.1. Create a signature[](id:Step1_1)

1. Log in to the [SMS console](https://console.cloud.tencent.com/smsv2).
2. Select **Chinese Mainland SMS** > **Signatures** on the left sidebar and click **Create Signature**.
3. Set the following parameters as needed:
 <table>
     <tr>
         <th width="20%">Parameter</th>  
         <th>Sample Value</th>  
     </tr>
	 <tr>      
       <td>Signature purpose</td>   
	     <td>For self-use (the signature is a company name, website, product name, or something else verified under the current account)</td>   
     </tr> 
	 <tr>      
       <td>Signature type</td>   
	     <td>App</td>   
     </tr> 
	 <tr>      
       <td>Signature content</td>   
	     <td>Test demo</td>   
     </tr> 
	 <tr>      
       <td>Certificate type</td>   
	     <td>Screenshot of WeChat Mini Program settings page</td>   
     </tr> 
</table>
3. Click **OK**.
Wait for signature review. The SMS signature will be available only after its status changes to **approved**.


### Step 1.2. Create a body template[](id:Step1_2)
1. Log in to the [SMS console](https://console.cloud.tencent.com/smsv2).
2. Select **Chinese Mainland SMS** > **Body Templates** on the left sidebar and click **Create Body Template**.
3. Set the following parameters as needed:
 <table>
     <tr>
         <th width="20%">Parameter</th>  
         <th>Sample Value</th>  
     </tr>
	 <tr>      
        <td>Template name</td>   
	     <td>Verification code SMS</td>   
     </tr> 
	 <tr>      
        <td>SMS type</td>   
	     <td>Regular SMS</td>   
     </tr> 
	 <tr>      
        <td>SMS content</td>   
	     <td>Your signup verification code is {1}. Please enter it within {2} minutes. If the signup was not initiated by you, please ignore this message.</td>   
     </tr> 
</table>
4. Click **OK**.
Wait for body template review. The body template will be available only after its status changes to **approved**. Please note down the template ID.

## Step 2. Set the SMS delivery rate limit (optional)[](id:Step2)
>!Individual users have no permission to modify the rate limit. To use this feature, change "Individual Identity" to "Organizational Identity".

To ensure business and channel security and minimize potential financial losses caused by malicious calls of SMS APIs, you are recommended to [set the delivery rate limit](https://intl.cloud.tencent.com/document/product/382/35469). In addition, you can use Tencent Cloud Captcha to maximize the protection of your business security.
This document uses the default SMS delivery rate limit policy as an example.

- For SMS messages with the same content, a maximum of one such message can be sent to the same mobile number within 30 seconds.
- A maximum of 10 messages can be sent to the same mobile number on a calendar day.

## Step 3. Configure the VPC and subnet[](id:Step3)
By default, SCF is deployed in the public network and can access public network only. If you need to access Tencent Cloud resources such as TencentDB instances, you need to build a VPC to ensure data and connection security.

1. [Plan the network design](https://intl.cloud.tencent.com/document/product/215/31795) as needed.
2. Create a VPC. For detailed directions, please see [Creating VPC](https://intl.cloud.tencent.com/document/product/215/31805).
 >!The CIDRs of the VPC and subnet cannot be modified after creation.
 >
 <table>
     <tr>
         <th width="20%">Parameter</th>  
         <th>Sample Value</th>  
     </tr>
	 <tr>      
        <td>Region</td>   
	     <td>	South China (Guangzhou)</td>   
     </tr> 
	 <tr>      
        <td>Name</td>   
	     <td>Demo VPC</td>   
     </tr> 
	 <tr>      
        <td>IPv4 CIDR</td>   
	     <td>10.0.0.0/16</td>   
     </tr> 
	 <tr>      
        <td>Subnet name</td>   
	     <td>Demo subnet</td>   
     </tr> 
	 <tr>      
        <td>IPv4 CIDR</td>   
	     <td>10.0.0.0/16</td>   
     </tr> 
	 <tr>      
        <td>AZ</td>   
	     <td>Guangzhou Zone 3</td>   
     </tr> 
</table>

## Step 4. Configure a TencentDB for Redis instance[](id:Step4)
The region and subnet AZ of the TencentDB for Redis instance must be the same as those of the VPC configured in [step 3](#Step3).

1. Purchase a TencentDB for Redis instance. For detailed directions, please see [Creating TencentDB for Redis Instance](https://intl.cloud.tencent.com/document/product/239/37712).
 <table>
     <tr>
         <th width="20%">Parameter</th>  
         <th>Sample Value</th>  
     </tr>
	 <tr>      
        <td>Billing mode</td>   
	     <td>	Pay-as-you-go</td>   
     </tr> 
	 <tr>      
        <td>Region</td>   
	     <td>Guangzhou</td>   
     </tr> 
	 <tr>      
        <td>Database version</td>   
	     <td>Redis 4.0	</td>   
     </tr> 
	 <tr>      
        <td>Architecture</td>   
	     <td>Standard architecture</td>   
     </tr> 
	 <tr>      
        <td>Network</td>   
	     <td>Demo VPC and demo subnet</td>   
     </tr> 
	 <tr>      
        <td>Instance name</td>   
	     <td>Demo database</td>   
     </tr> 
	 <tr>      
        <td>Purchase quantity</td>   
	     <td>1</td>   
     </tr> 
</table>

## Step 5. Create a function[](id:Step5)
SCF currently supports development in Python, Node.js, PHP, Java, and Go. This document uses Node.js as an example.

1. Create a function in the region of the VPC created in [step 3](#Step3). For detailed directions, please see [Writing Function](https://intl.cloud.tencent.com/document/product/583/32742).
  <table>
     <tr>
         <th width="20%">Parameter</th>  
         <th>Sample Value</th>  
     </tr>
	 <tr>      
        <td>Function name</td>   
	     <td>Demo</td>   
     </tr> 
	 <tr>      
        <td>Runtime environment</td>   
	     <td>Node.js 8.9</td>   
     </tr> 
	 <tr>      
        <td>Creation method</td>   
	     <td>Template function: helloworld</td>   
     </tr> 
</table>
2. Deploy the function and set **API Gateway Trigger** as the trigger. For detailed directions, please see [Deploying Function](https://intl.cloud.tencent.com/document/product/583/32742).

## Step 6. Enable public network access (optional)[](id:Step6)
- Functions deployed in a VPC before April 29, 2020 are isolated from the public network by default. If you want them to have access to both private network and public network, you can do so by enabling public network access.
 Log in to the [SCF console](https://console.cloud.tencent.com/scf/index?rid=1), select **Function Service**, click the name of the target function in the function list to enter the function configuration page. Click **Edit**, check **Public Network Access**, and click **Save** to save the configuration.
- Functions deployed on or after April 29, 2020 have public network access enabled by default, and no additional operations are required.

## Step 7. Deploy the SMS demo[](id:Step7)
1. Go to the [SCF console](https://console.cloud.tencent.com/scf/) and select the SMS demo to deploy it.


2. Set the environment variables of the demo in **Advanced Configuration**.



| Field | Description |
| ----- | ----- |
| REDIS_HOST| Redis database address. |
|REDIS_PASSWORD| Redis database password. |
| SMS_TEMPLATE_ID| Template ID. You must enter the ID of an approved template, which can be viewed in the [SMS console](https://console.cloud.tencent.com/smsv2). |
| SMS_SIGN| Content of the SMS signature, which should be encoded in UTF-8. You must enter an approved signature, which can be viewed in the [SMS console](https://console.cloud.tencent.com/smsv2). Note: this parameter is required for Chinese Mainland SMS. |
| SMS_SDKAPPID| SMS `SdkAppid` actually generated after an application is added in the [SMS console](https://console.cloud.tencent.com/smsv2), such as 1400006666. |


3. Set the same VPC environment as the Redis database in **Advanced Configuration**.



4. Set the permissions of SCF **execution role** in **Advanced Configuration**.

You need to associate the `QcloudSMSFullAccess` policy with the `SCF_QcsRole` role in the [CAM console](https://console.cloud.tencent.com/cam/role).

In this way, the ``TENCENTCLOUD_SECRETID`, `TENCENTCLOUD_SECRETKEY`, and `TENCENTCLOUD_SESSIONTOKEN` environment variables can be obtained in the code, which will be used by the SMS SDK.

5. Click **Complete** to deploy the function.

6. Create an SCF **API Gateway trigger** and request the trigger address to use SMS capabilities.


## Step 8. Use the features
Verification codes have a high requirement for timeliness. You can store verification codes in the memory or TencentDB for Redis and use the mobile number as a key to store information such as sending time, verification code, number of verification attempts, and verification result.

### Features
#### Sending SMS verification code
Request parameters:

| Field | Type | Description |
| ----- | ----- | ----- |
| method|string| Request method, whose value is `getSms` |
|phone|string| Mobile number in the format of area code + mobile number, such as 86185662466** |

#### Verifying verification code (login)
Request parameters:

| Field | Type | Description |
| ----- | ----- | ----- |
| method|string| Request method, whose value is `login` |
|phone|string| Mobile number in the format of area code + mobile number, such as 86185662466** |
| code|string| 6-digit verification code |

### Error codes
| Field | Description |
| ----- | ----- |
| InValidParam| Missing parameter |
| MissingCode| Missing verification code parameter |
| CodeHasExpired| The verification code has expired |
| CodeHasValid| The verification code is invalid |
| CodeIsError| Please check whether the mobile number and verification code are correct |
