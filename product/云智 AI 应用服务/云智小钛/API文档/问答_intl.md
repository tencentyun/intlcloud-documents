## 1. API Description
 This API is used to intelligently answer user questions.
 Call protocol: HTTP/HTTPS GET request.

## 2. Request Parameters
 | Name | Type | Required | Description|
 |------ |------|------ |----- |
 |appId	 | String | Yes| Application ID; available in the IASK application management interface |
 |uuId   | String | Yes	| User's unique ID; maximum length: 20 characters |
 |channel|	Int	| Yes | API calling channel, 0: IASK API, 1: WeChat Official Account, 2: desktop website, 3: mobile website |
 |query	|String| Yes	| User's question |
 |time	|Int   | Yes	| Timestamp in seconds |
 |sign	|String| Yes | Calling signature; generated based on the API calling parameters and the application SecretKey |


## 3. Response Parameters
 | Name | Type | Description |
 |:-----  |:-----|-----|
 |code|  Int | Code, 0 - normal; other values - exceptional |
 |data|Object| Returned result |
 |msg |String| Returned message |

## 4. Access Process
 4.1. Obtain the appId and SecretKey from the IASK application; 

 4.2. Confirm the values of the parameters except the sign parameter;

 4.3. Generate the sign parameter by splicing the appId, uuId, channel, query and time parameters into a string in ascending order to get `&appId=x&channel=x&query=x&time=x&uuId=x` and adding SecretKey to the beginning of the string to get `x&appId=x&channel=x&query=x&time=x&uuId=x`. Perform MD5 processing on this string to get the signature parameter (sign).

 sign parameter generation example (PHP):
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
## 5. Examples
### Request Example
 ```
 iask.qq.com/aics/open/ask?
 appId=817c0cc4fb65b98022b73b56485a515d&uuId=aa
 &channel=1
 &query= Try again
 &time=1528012017
 &sign=dc0900e8209f1b3c16f4c0bb736d7a39
 ```
### Response Example
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
