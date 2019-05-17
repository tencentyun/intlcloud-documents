## 1. API Description
Automatically answers user questions with artificial intelligence.  
HTTP request method: GET.

## 2. Request Parameters
 | Name | Type | Required | Description|
 |------ |------|------ |----- |
 |appId	 | String | Yes| Application ID; available in the IASK Application Management Interface |
 |uuId   | String | Yes	| Unique ID of the user; maximum length: 20 characters |
 |channel|	Int	| Yes | API calling channel, 0: IASK API, 1: WeChat Official Account, 2: desktop website, 3: mobile website |
 |query	|String| Yes	| The input question |
 |time	|Int   | Yes	| Timestamp. Unit:second |
 |sign	|String| Yes | Signature of the API call. The signature is calculated by the parameters required for the API call and the SecretKey of the application. |


## 3. Response Parameters
 | Name | Type | Description |
 |:-----  |:-----|-----|
 |code|  Int | Code, 0 - normal; other values - Abnormal |
 |data|Object| The returned result |
 |msg |String| The returned message |

## 4. How to Access
 4.1 Get APPID and SecretKey from the IASK application;
 4.2 Ensure the values of all the parameters except *sign* is correct (no need to consider the parameters in `postbody`);
 4.3 Calculate parameter *sign*: Sort *APPID, oaID, openID, templateID and timestamp* in ascending order to get a string: `&appId=x&openId=x&templateId=x&timestamp=x`; Add SecretKey to the string header to get: `x&appId=x&openId= x&templateId=x&timestamp=x`. Generate an MD5 hash for the string.

 Example (PHP):
 ```
 $secret_key = xxx;  // SecretKey in IASK application configuration
     'appId' => 'xx'
     'time' => 1525339871,
     'channel' => 'xx',
     'uuId' => 'xx',
     'query' => 'xx',
 ];
 ksort($params);
 foreach ($params as $key => $value) {
     $secret_key.= '&' . $key . '=' . $value;
 }
 $sign = md5($secret_key);
 ```
## 5. Samples
### Request Sample
 ```
 iask.qq.com/aics/open/ask?
 appId=817c0cc4fb65b98022b73b56485a515d&uuId=aa
 &channel=1
 &query= Try again
 &time=1528012017
 &sign=dc0900e8209f1b3c16f4c0bb736d7a39
 ```
### Response Sample
 Directly returned result:
 ```
 {
     code: 0,
     data: {
         type => 'STRING',
         prefix => '',
         answer => 'xxxx', 
 		rel => [
             "xxx", 
             "xxx"
         ],
         suffix => '',
     },
     msg: "success"
 }
 ```

 Result returned after probing:
 ```
 {
         code: 0,
         data: {
             type => 'ARRAY',
             prefix => '',
             answer => [
                 "xxx" ,
                 "xxx" ,
             ], 
             rel => [],
             suffix => '',
         },
         msg: "success"
     }
 ```
