## 1. API Description
 The sensitive words contained in user-generated content will be shown as \*\*. To customize sensitive words, go to the setting page of *conversation* in IASK management console.
 
HTTP request method: HTTP/HTTPS GET.

## 2. Request Parameters
 | Name | Type | Required | Description|
 |:----  |:---   |:----- |----- |
 |appId  |	String	| Yes	| Application ID; available in IASK Application Management Interface |
 |query	 | String	| Yes	| Text to be filtered |
 |time   |	Int	| Yes	| Timestamp. Unit: second |
 |sign   |	String	| Yes |  Signature of the API call. The signature is calculated by the parameters required for the API call and the SecretKey of the application.|

## 3. Response Parameters
 | Name	| Type	| Description |
 |---------|---------|------|
 |code	   |   Int	| Code, 0 - normal; other values - Abnormal |
 |data	   |  String	| The filtered text that has returned |
 |msg	   |  String	| The returned message |

## 4. How to Access
 4.1 Get APPID and SecretKey from the IASK application;
 4.2 Ensure the values of all the parameters except *sign* is correct (no need to consider the parameters in `postbody`);
 4.3 Calculate parameter *sign*: Sort *APPID, oaID, openID, templateID and timestamp* in ascending order to get a string: `&appId=x&openId=x&templateId=x&timestamp=x`; Add SecretKey to the string header to get: `x&appId=x&openId= x&templateId=x&timestamp=x`. Generate an MD5 hash for the string.

 Example (PHP):
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

## 5. Samples
### Request sample
 ```
 iask.qq.com /aics/open/filterSensitiveWord?
 appId=817c0cc4fb65b98022b73b56485a515d
 &query= Can you stop eating sour radish?
 &time=1528803562
 &sign=a96c71b1d0f192906310bbaccf8ce1d1
 ```

### Response sample

 ```
 {
     "code": 0,
     "data": "Can you *****?",
     "msg": "success"
 }
 ```
