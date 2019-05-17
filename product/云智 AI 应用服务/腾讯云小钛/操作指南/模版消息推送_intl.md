## 1. API Description
API domain name: `iask.qq.com`  
This API (pushTemplateMsg) is used to push template message.  
HTTP request method: HTTPS POST  
Content format: application/JSON

## 2. Request Parameters
| Parameter name    | Type  | Required | Description                                       |
| :---------- | :------- | :------- | ---------------------------------------------- |
| appId       | String   | Yes       | Application ID; available in IASK Application Management Interface            |
| oaId        | String   | Yes       | The ID of the WeChat Official Account authorized for IASK                         |
| openId      | Int      | Yes       | The openid of the recipient                                   |
| templateId  | String   | Yes       | ID of the template                                       |
| url         | String   | No       | Redirection link of the template                                   |
| timestamp   | Int      | Yes       | Timestamp. Unit: second                                 |
| sign        | String   | Yes       | Signature of the API call. The signature is calculated by the parameters required for the API call and the SecretKey of the application.  |
| miniprogram | JSON     | No       | Should be passed to the post body, see [Sample 1](#miniprogram).      |
| data        | JSON     | Yes       | Should be passed to the post body, see [Sample 2](#data ).                   |
 
 
## 3. Response Parameters
 | Parameter name	| Type	| Description |
 |---------|---------|------|
 |code	   |   Int	| 0: Normal. Non-zero values: Abnormal|
 |data	   |  String	|The filtered text that has returned|
 |msg	   |  String	|The returned message|

## 4. How to Access
 4.1 Get APPID and SecretKey from the IASK application;
 4.2 Ensure the values of all the parameters except *sign* is correct (no need to consider the parameters in `postbody`);
 4.3 Calculate parameter *sign*: Sort *APPID, oaID, openID, templateID and timestamp* in ascending order to get a string: `&appId=x&openId=x&templateId=x&timestamp=x`; Add SecretKey to the string header to get: `x&appId=x&openId= x&templateId=x&timestamp=x`. Generate an MD5 hash for the string.

 Example (PHP):
 ```
$secret_key = xxx;  //SecretKey in the IASK application configuration
$params = [
    'appId' => 'xx'
    'openId' => 'xx'
    'timestamp' => 1525339871, 
    'oaId' => 'xx', 
    'templateId' => 'xx',
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
iask.qq.com/aics/open/pushTemplateMsg?
appId=be043fdb5e7d23041f0436a27ae3777d
&oaId=wxc300f0df2a16da43
&openId=ogud103JWOxWQmSKy2DR-NE6NTD4
&templateId=Jpdhk-mCTam7fQjbObwBgZW54g2ij8cjja7NYo_b8YU
&url=http://www.qq.com&timestamp=111&sign=xxx
```

Sample 1 (miniprogram)：<span id="miniprogram"></span>
 ```
 {
"appid":"xiaochengxuappid12345",   //APPID of the WeChat Mini Program
"pagepath":"index?foo=bar"    //Specific page path of the WeChat Mini Program 
}
```

Sample 2 (data)：<span id="data"></span>
 ```
 {
        "first": {
            "value":"Ticket Progress Notification",
            "color":"#173177"
        },
        "keyword1":{
            "value":"xxxx",
            "color":"#173177"
        },
        "keyword2": {
            "value":"xxx",
            "color":"#173177"
},
        "keyword3": {
            "value":"xxx",
            "color":"#173177"
        },
        "remark":{
            "value":"Click to view details." ,
            "color":"#173177"
        }
    }
``` 

### Response sample

 ```
 {
    "code": 0,
    "data": {
        "errcode": 0,			//The returned code from the push template message API
        "errmsg": "ok",		//The returned msg from the push template message API
        "msgid": 496146255857205248	//The returned msgId from the push template message API
    },
    "msg": "success"
}
 ```
