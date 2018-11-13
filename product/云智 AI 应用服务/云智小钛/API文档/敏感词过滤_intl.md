## 1. API Description
 If the content entered by the user contains sensitive words, they will be replaced with \*\* for display. Sensitive words can be added on the conversation settings page in the IASK management console.
 Call protocol: HTTP/HTTPS GET request.

## 2. Request Parameters
 | Name | Type | Required | Description|
 |:----  |:---   |:----- |----- |
 |appId  |	String	| Yes	| Application ID; available in the IASK application management interface |
 |query	 | String	| Yes	| Text to be filtered |
 |time   |	Int	| Yes	| Timestamp in seconds |
 |sign   |	String	| Yes | Calling signature; generated based on the API calling parameters and the application SecretKey |

## 3. Response Parameters
 | Name	| Type	| Description |
 |---------|---------|------|
 |code	   |   Int	| Code, 0 - normal; other values - exceptional |
 |data	   |  String	| Filtered text returned |
 |msg	   |  String	| Returned message |

## 4. Access Process
 4.1. Obtain the appId and SecretKey from the IASK application;

 4.2. Confirm the values of the parameters except the sign parameter;

 4.3. Generate the sign parameter by splicing the appId, uuId, channel, query and time parameters into a string in ascending order to get `&appId=x&query=x&time=x` and adding SecretKey to the beginning of the string to get `x&appId=x&query=x&time=x`. Perform MD5 processing on this string to get the signature parameter (sign).

 sign parameter generation example (PHP):
 ```
 $secret_key = xxx;  // SecretKey in IASK application configuration
 $params = [
     'appId' => 'xx'
     'time' => 1525339871, 
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
 iask.qq.com /aics/open/filterSensitiveWord?
 appId=817c0cc4fb65b98022b73b56485a515d
 &query= Can you stop eating sour radish?
 &time=1528803562
 &sign=a96c71b1d0f192906310bbaccf8ce1d1
 ```

### Response Example

 ```
 {
     "code": 0,
     "data": "Can you *****?",
     "msg": "success"
 }
 ```
