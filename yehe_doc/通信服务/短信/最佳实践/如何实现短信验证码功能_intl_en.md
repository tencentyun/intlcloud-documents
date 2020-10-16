Sending verification codes through SMS is the most popular and securest way to verify user identities. Currently, SMS verification codes are widely used in various application scenarios such as user registration, password reset, login protection, identity verification, random password generation, and transaction confirmation.
This document uses developing a verification code-based login and signup service based on [SCF](https://intl.cloud.tencent.com/document/product/583) as an example to describe how to implement the SMS verification code feature.

## Preparations
- You have [signed up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and verified your organizational identity.
- You have purchased an SMS package.
- Prepare SMS signature owner qualification certificates.
 This document takes a business license as a qualification certificate for example.
- Understand the SMS body content review standards.
- Get the `SDKAppID` of the SMS application.

## Relevant Materials
- [Demo source code](https://github.com/qcloudsms/smsLogin)
- Other products' documentation
 - [VPC documentation](https://intl.cloud.tencent.com/document/product/215)
 - [TencentDB for MySQL documentation](https://intl.cloud.tencent.com/document/product/236)
 - [NAT Gateway documentation](https://intl.cloud.tencent.com/document/product/1015)
 - [SCF documentation](https://intl.cloud.tencent.com/document/product/583)



<span id="Step1"></span>
## Step 1. Configure the SMS content
After an SMS signature or body template is submitted, it will be reviewed within two hours generally. You can [configure alarm contacts](https://intl.cloud.tencent.com/document/product/382/35470) to receive review result notifications.

<span id="Step1_1"></span>
### Step 1.1. Create a signature

1. Log in to the [SMS Console](https://console.cloud.tencent.com/smsv2).
2. Select **Mainland China SMS** > **Signature Management** on the left sidebar and click **Create Signature**.
3. Set the following parameters as needed:
 <table>
     <tr>
         <th width="20%">Parameter</th>  
         <th>Sample Value</th>  
     </tr>
	 <tr>      
       <td>Signature use</td>   
	     <td>For self-use (the signature is a company name, website, product name, or something else verified under the current account)</td>   
     </tr> 
	 <tr>      
       <td>Signature type</td>   
	     <td>Application</td>   
     </tr> 
	 <tr>      
       <td>Signature content</td>   
	     <td>Test demo</td>   
     </tr> 
	 <tr>      
       <td>Certificate type</td>   
	     <td>Screenshot of WeChat Mini Program settings page</td>   
     </tr> 
	 <tr>      
       <td>Certificate upload</td>   
	<td><img src="https://main.qcloudimg.com/raw/48ad431a784461465054160737b9b166.png" width=400/></td>    
     </tr> 
</table>
3. Click **OK**.
 Wait for signature review. The SMS signature will be available only after its status changes to **approved**.


<span id="Step1_2"></span>
### Step 1.2. Create a body template
1. Log in to the [SMS Console](https://console.cloud.tencent.com/smsv2).
2. Select **Mainland China SMS** > **Template Management** on the left sidebar and click **Create Body Template**.
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
	     <td>General SMS</td>   
     </tr> 
	 <tr>      
        <td>SMS content</td>   
	     <td>Your signup verification code is {1}. Please enter it within {2} minutes. If the signup was not initiated by you, please ignore this message.</td>   
     </tr> 
</table>
4. Click **OK**.
 Wait for body template review. The body template will be available only after its status changes to **approved**. Please note down the template ID.

<span id="Step2"></span>
## Step 2. Set the SMS sending frequency limit (optional)
>!Individual users have no permission to modify the frequency limit. To use this feature, change "Individual Identity" to "Organizational Identity".

To ensure business and channel security and minimize potential financial losses caused by malicious calls of SMS APIs, you are recommended to [set the sending frequency limit](https://intl.cloud.tencent.com/document/product/382/35469#.E8.AE.BE.E7.BD.AE.E5.8F.91.E9.80.81.E9.A2.91.E7.8E.87.E9.99.90.E5.88.B6). In addition, you can use Tencent Cloud Captcha to maximize the protection of your business security.
This document uses the default SMS sending frequency limit policy as an example.

- For SMS messages with the same content, a maximum of one such message can be sent to the same mobile number within 30 seconds.
- A maximum of 10 messages can be sent to the same mobile number on a calendar day.

<span id="Step3"></span>
## Step 3. Configure the VPC and subnet
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

<span id="Step4"></span>
## Step 4. Configure a TencentDB for MySQL instance
The region and subnet AZ of the TencentDB for MySQL instance must be the same as those of the VPC configured in [step 3](#Step3).

1. Purchase a TencentDB for MySQL instance. For detailed directions, please see [Purchase Methods](https://intl.cloud.tencent.com/document/product/236/5160).
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
	     <td>MySQL 5.7</td>   
     </tr> 
	 <tr>      
        <td>Architecture</td>   
	     <td>High-Availability Edition</td>   
     </tr> 
	 <tr>      
        <td>Master AZ</td>   
	     <td>Guangzhou Zone 3</td>   
     </tr> 
	 <tr>      
        <td>Slave AZ</td>   
	     <td>Guangzhou Zone 4</td>   
     </tr> 
	 <tr>      
        <td>Instance specification</td>   
	     <td>4-core 8,000 MB MEM</td>   
     </tr> 
	 <tr>      
        <td>Disk</td>   
	     <td>200 GB</td>   
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
2. Initialize the TencentDB for MySQL instance. For detailed directions, please see [Initializing TencentDB for MySQL Instance](https://intl.cloud.tencent.com/document/product/236/3128).
 <table>
     <tr>
         <th width="20%">Parameter</th>  
         <th>Sample Value</th>  
     </tr>
	 <tr>      
        <td>Supported character set</td>   
	     <td>UTF-8</td>   
     </tr> 
	 <tr>      
        <td>Table name case sensitivity</td>   
	     <td>Yes</td>   
     </tr> 
	 <tr>      
        <td>Custom port</td>   
	     <td>3306</td>   
     </tr> 
	 <tr>      
        <td>Root account and password</td>   
	     <td>Set as needed</td>   
     </tr> 
	 <tr>      
        <td>Confirm password</td>   
	     <td>Enter the password again</td>   
     </tr> 
</table>
3. Log in to the TencentDB for MySQL instance. For detailed directions, please see [Logging in to phpMyAdmin](https://intl.cloud.tencent.com/document/product/236/32341).
4. Create a table and fields for storing information such as user phone numbers, profile photos, and nicknames as needed. For detailed directions, please see [Creating Database and Table](https://intl.cloud.tencent.com/document/product/236/8465).

<span id="Step5"></span>
## Step 5. Create a function
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

<span id="Step6"></span>
## Step 6. Enable public network access (optional)
- Functions deployed in a VPC before April 29, 2020 are isolated from the public network by default. If you want them to have access to both private network and public network, you can do so by enabling public network access.
 Log in to the [SCF Console](https://console.cloud.tencent.com/scf/index?rid=1), select **Function Service**, click the name of the target function in the function list to enter the function configuration page. Click **Edit**, check **Public Network Access**, and click **Save** to save the configuration.
- Functions deployed on or after April 29, 2020 have public network access enabled by default, and no additional operations are required.


<span id="Step7"></span>
## Step 7. Deploy the SMS SDK
1. Run the following command to install the SDK:
```
npm install tencentcloud-sdk-nodejs --save
```
2. Import the SMS module code into your code.
3. Configure the core logic for sending SMS messages.
<pre>
/*
 * Feature: using SDK to send SMS messages
 * Parameter: mobile number and SMS verification code
 */
async function sendSms(phone, code) {
  const tencentcloud = require('tencentcloud-sdk-nodejs');
  const SmsClient = tencentcloud.sms.v20190711.Client;
  const Credential = tencentcloud.common.Credential;
  const ClientProfile = tencentcloud.common.ClientProfile;
  const HttpProfile = tencentcloud.common.HttpProfile;
  // `secretId` and `secretKey` of Tencent Cloud account, which should not be disclosed
  const secretId = "secretId";// Set it to your real `secretId`
  const secretKey = "secretKey";// Set it to your real `secretKey`

  let cred = new Credential(secretId, secretKey);
  let httpProfile = new HttpProfile();
  httpProfile.endpoint = "sms.tencentcloudapi.com";
  let clientProfile = new ClientProfile();
  clientProfile.httpProfile = httpProfile;
  let client = new SmsClient(cred, "ap-guangzhou", clientProfile);
  phone = "+86" + phone;// Mobile number in Mainland China

  let req = {
      PhoneNumberSet: [phone],// Mobile number to which the SMS message is sent
      TemplateID: "",// ID of the template created and recorded in <a href="#Step1_2">step 1.2</a>
      Sign: "",// Signature created in <a href="#Step1_1">Step 1.1</a>
      TemplateParamSet: [code],// Random verification code
      SmsSdkAppid: ""// SMS application ID
  }

  function smsPromise() {
      return new Promise((resolve, reject) => {
          client.SendSms(req, function(errMsg, response) {
              if (errMsg) {
                  reject(errMsg)
              } else {
                  if(response.SendStatusSet && response.SendStatusSet[0] && response.SendStatusSet[0].Code === "Ok") {
                      resolve({
                          errorCode: 0,
                          errorMessage: response.SendStatusSet[0].Message,
                          data: {
                              codeStr: response.SendStatusSet[0].Code,
                              requestId: response.RequestId
                          }
                      })
                  } else {
                      resolve({
                          errorCode: -1003,// SMS verification code sending failed
                          errorMessage: response.SendStatusSet[0].Message,
                          data: {
                              codeStr: response.SendStatusSet[0].Code,
                              requestId: response.RequestId
                          }
                          
                      })
                  }
              }                
          });
      })
  }
  let queryResult = await smsPromise()
  return queryResult
}
</pre>

<span id="Step8"></span>
## Step 8. Verify the core logic of verification code sending
Verification codes have a high requirement for timeliness. You can store verification codes in the memory or TencentDB for Redis and use the mobile number as a key to store information such as sending time, verification code, number of verification attempts, and verification result. For the sake of security, you are recommended to set a limit on the number of verification attempts to prevent brute force attacks. In this document, a maximum of three attempts is used as an example.
```
/*
 * Feature: getting SMS verification code based on mobile number
 */
async function getSms(queryString) {
  const code = Math.random().toString().slice(-6);// Generate a random 6-digit verification code
  const sessionId = Math.random().toString().slice(-8);// Generate a random 8-digit verification code
  const sessionCode = {
      code: code,
      sessionId: sessionId,
      sendTime: new Date().getTime(),
      num: 0,// Number of verification attempts, which can be up to 3
      used: 1// 1: not used; 2: used
  }
  clearCacheCode()

  cacheCode[queryString.phone] = sessionCode
```

<span id="Step9"></span>
## Step 9. Configure the login module
The login module is mainly used for user signup or login. It stores user information such as mobile number, username, profile photo, and signup time upon the first login (i.e., signup).
```
/*
* Feature: login
*/
async function loginSms(queryString) {
  const connection = mysql.createConnection({
    host: '', // TencentDB instance IP address
    user: '', // TencentDB instance username, such as `root`
    password: '', // TencentDB instance password
    database: '' // TencentDB database name
  });
  connection.connect();

  if(queryString.token) {
    return await verifyToken(connection, queryString)
  }

  if(!queryString.code || !queryString.sessionId) {
    return {
        errorCode: -1001,
        errorMessage: "Missing parameter"
    }
  }

  let result = cacheCode[queryString.phone]
  if(!result || result.used === 2 || result.num >= 3) {
    return {
      errorCode: -1100,
      errorMessage: "The verification code has expired"
    }
  }
  if(result.sessionId !== queryString.sessionId) {
    return {
      errorCode: -1103,
      errorMessage: "Unmatched sessionId"
    }
  }
  
  if(result.code == queryString.code) {
    cacheCode[queryString.phone].used = 2;// Update the verification code status to "used"
    const queryInfoSql = `select * from info where phone = ?`
    let queryInfoResult = await wrapPromise(connection, queryInfoSql, [queryString.phone])
    if(queryInfoResult.length === 0) {// No records are found. The user has not signed up.
      return await generateInfo(connection, queryString)
    } else {
      let infoResult = queryInfoResult[0]
      return {
        errorCode: 0,
        errorMessage: "Logged in successfully",
        data: {
          phone: infoResult.phone,
          token: getToken(infoResult.userId, infoResult),
          name: infoResult.name,
          avatar: infoResult.avatar,
          userId: infoResult.userId.toString()
        }
      }
    }
  } else {
    updateCacheCode(queryString.phone, result)
    return {
      errorCode: -1102,
      errorMessage: "The verification code is incorrect. Please enter again."
    }
  }
}
```

In addition, to make login easier, you can use the JSON web token standard to generate a token, which can be used to maintain the login status, so that the user can stay logged in for a short time period with no need to enter a new SMS verification code.

```
/*
* Feature: using JSON web token to distribute token
*/
function getToken(userId, infoResult) {
  return jwt.sign({
    phone: infoResult.phone,
    userId: userId,
    name: infoResult.name,
    avatar: infoResult.avatar
  }, privateKey, {expiresIn: tokenExpireTime});
}
```


