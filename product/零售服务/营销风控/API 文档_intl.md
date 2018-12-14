## Request Parameters

| Parameter | Required | Type | Description |
| ------------------- | -------- | ------ | ---------------------------------------- |
| accountType         | Yes       | Uint   | User account type <br/>1: QQ open account <br/>2: WeChat open account <br/>4: Mobile number (currently only Chinese mobile numbers are supported) <br/>10004: Mobile number MD5 |
| uid                 | Yes       | String | User ID value, e.g., WeChat/QQ openid or mobile number like 15912345687 |
| userIP              | Yes       | String | The real public IP used by the user to claim the reward                           |
| postTime            | Yes       | Uint   | User operation timestamp in seconds (Greenwich time, accurate to seconds, such as 1501590972)       |
|                     | Yes       | String | Information of the purchased item                                   |
| EncryptedCode       | No (entering is recommended) | String | Unique encryption code of the reward redemption code (to protect data security by using the encryption code and ensuing the ID is unique)        |
| Share | No (entering is recommended) | Uint | The number of users allowed for claiming for a single shared red packet <br/>For example: <br/>1: A single red packet supports claiming by only 1 user (exclusive red packet) <br/>2: A single red packet supports claiming by 2 users |
| Daytimes            | No (entering is recommended) | Uint   | The maximum number of reward claims allowed for a single account per day                      |
| Totaltimes          | No (entering is recommended) | Uint   | The maximum number of reward claims allowed for a single account in the entire campaign period                   |
| phoneNumber         | No (entering is recommended) | String | If accountType is not mobile number and the mobile number can be obtained, enter the corresponding mobile number (e.g., 15912345687) |
| Address             | No (entering is recommended) | String | Information of the location where the user participates in the campaign. For example, the specific latitude and longitude information can be entered and converted into the specific address information |
| Latitude            | No (entering is recommended) | Float  | Latitude; a floating point number in the range between 90 and -90 |
| Longitude           | No (entering is recommended) | Float  | Longitude; a floating point number in the range between 180 and -180 |
| Imei                | No       | String | Mobile phone device number                                    |
| referer             | No       | String | referer value of the user's HTTP request                        |
| typeID (for internal use to differentiate ecommerce and FMCG) | -       | Uint   | 0: Traditional anti-cheating APIs <br/>1: APIs for FMCG and new retail                      |
| loginType           | No       | UInt   | Login type <br/> 0: Other<br/> 1: Manual input of account name and password <br/> 2: Login with dynamic SMS code <br/> 3: Login by scanning QR code |
| loginSource         | No       | UInt   | Login source <br/> 0: Other <br/>1: PC webpage <br/> 2: Mobile webpage   3: App <br/> 4: WeChat Official Account    |

## Response parameters

| Parameter              | Type     | Description                                       |
| ------------------ | ------ | ---------------------------------------- |
| code               | Int    | Return code                                      |
| codeDesc           | String | Error code description <br/>Success: Success is returned <br/>Error: A specified error reason is returned       |
| message            | String | UTF-8 encoding; error message                             |
| Nonce              | UInt   | A random positive integer used to prevent replay attacks along with Timestamp (a common parameter)   |
| postTime (corresponding to the input parameter)  | String | Operation timestamp in seconds                                |
| uid (corresponding to the input parameter)       | String | Different user ID accountType values correspond to different user IDs. <br/>If it is a QQ or WeChat user, enter the corresponding openId |
| userIp (corresponding to input parameters)    | String | Public IP of the operation source                              |
| Level (importance: risk value)     | Int    | 0: Non-malicious <br/>1-4: Malicious level in ascending order                      |
| riskType (importance: risk tag) | Array  | Risk type; for details, see **Detailed Description of risktype** below                               |
| associateAccount   | String | If accountType is QQ or WeChat open account, this is used to identify the account ID of the associated business after logging in by the QQ or WeChat user |

## Detailed Description of risktype

<table>
<tbody>
<tr><th>Risk type</th><th>Risk details</th><th >Risk code</th><th >Explanation</th></tr>
<tr>
<td rowspan= '3'>Account risk</td>
<td >Low account credit score</td>
<td >1</td>
<td >The account has been penalized, inactive or reported for violations recently</td>
</tr>
<tr>
<td >Junk account</td>
<td >2</td>
<td >The account is likely an alternate account created by batch registration or has committed severe violations or been reported extensively for violations recently</td>
</tr>
<tr>
<td >Invalid account</td>
<td >3</td>
<td >The submitted account parameter failed to be parsed. If it is a WeChat/QQ openid, please check if the data submitted is correct</td>
</tr>
<tr>
<td rowspan= '3' >Behavior risk</td>
<td >Batch operation</td>
<td >101</td>
<td >Exceptional aggregation in factors such as IP, device or environment</td>
</tr>
<tr>
<td >Automaton</td>
<td >102</td>
<td >Suspected batch requests by an automaton</td>
</tr>
<tr>
<td >Exceptional code scan</td>
<td >103</td>
<td >Exceptional code scanning behaviors such as frequent scans or scans of many discarded codes</td>
</tr>
<tr>
<td rowspan= '2' >Environment risk</td>
<td >Exceptional environment</td>
<td >201</td>
<td >The operating IP, device or environment is exceptional, for example, the current IP is not the frequently-used IP or in a malicious IP address range</td>
</tr>
<tr>
<td >Exceptional JS reporting</td>
<td >202</td>
<td >You need to deploy JS on the frontend to make the reporting valid</td>
</tr>
</tbody>
</table>
