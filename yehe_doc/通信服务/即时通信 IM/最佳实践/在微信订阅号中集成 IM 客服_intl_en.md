This article describes the process of developing a customer service demo using Node.js in order to integrate Tencent Cloud IM with a WeChat subscription account.
> This demo is for reference only. There are many other factors to consider, such as load balancing, API rate limits and persistent data storage, before bringing this to the production environment. These are not covered by this article. You should implement them to suit your needs.

## Use Case and Demo Images
The use case is described as follows:
1. You are a online clothing seller and a customer use the WeChat subscription account to make an inquiry: “when are you getting new children clothing?”.
2. The inquiry is transferred to your customer service agent through Tencent Cloud IM.
3. The agent replies "We are getting new arrivals in May. Please follow our updates." The message is pushed to the customer through Tencent Cloud IM and WeChat.

The following figure illustrates what a customer sees:
![](https://main.qcloudimg.com/raw/155fe5984115665314d9305c53b0a619.jpg)
The following figure illustrates what a customer agent sees:
![](https://main.qcloudimg.com/raw/f69848510053e9ee1ebf046854229fd6.png)
The following figure is a flowchart of the use case;
![](https://main.qcloudimg.com/raw/00c46f548d19ab7e3a5335d902ecd0f7.png)

## Considerations
- If the message transfer link is long, it may take longer to send and receive messages.
- Subscription accounts registered by individuals cannot use the [customer service message] API of the WeChat Official Accounts Platform to push messages to subscribers.

## Prerequisites

- You have prepared a public network development server or a CVM instance that is capable of running Node.js.
- You have [registered](https://mp.weixin.qq.com/cgi-bin/registermidpage?action=index&lang=zh_CN&token=) a WeChat subscription account or service account.
- You have read the [developer documentation for the WeChat Official Accounts Platform](https://developers.weixin.qq.com/doc/offiaccount/Basic_Information/Access_Overview.html).
- You have created an [IM app](https://intl.cloud.tencent.com/document/product/1047/34577).
- You have imported IM user accounts, such as user0 and user1, through [one-by-one import](https://intl.cloud.tencent.com/document/product/1047/34953) or [batch import](https://intl.cloud.tencent.com/document/product/1047/34954).

## References

- [API documentation](https://intl.cloud.tencent.com/document/product/1047/34620)
- [Third-party callback](https://intl.cloud.tencent.com/document/product/1047/34354)
- [Developer Guide for the WeChat Official Accounts Platform](https://developers.weixin.qq.com/doc/offiaccount/Getting_Started/Overview.html)
- [Express framework tutorial](https://expressjs.com/zh-cn/)

## Directions

### Step 1: create a project and install dependencies

```javascript
npm init -y

// express framework
npm i express@latest --save 

// Encryption module
npm i crypto@latest --save

// xml parsing tool
npm i xml2js@latest --save

// Initiate an HTTP request.
npm i axios@latest --save

// Calculate userSig.
npm i tls-sig-api-v2@latest --save
```

### Step 2: enter IM app information and calculate the UserSig

<pre>
// ------------ IM ------------
const IMAxios = axios.create({
  timeout: 10000,
  headers: {
    'Content-Type': 'application/x-www-form-urlencoded;charset=UTF-8',
  },
});

// The user ID mapping table imported into the IM account system is not persistently stored and used only for indexing in the demo. For production environments, use another technical solution.
const importedAccountMap = new Map();
// IM app and app administrator information can be obtained from the <a href="https://console.cloud.tencent.com/im">IM console</a>.
const SDKAppID = 0; // Enter the SDKAppID of the IM app.
const secrectKey = ''; // Enter the key of the IM app.
const AppAdmin = 'user0'; // Set user0 as the app admin account.
const kfAccount1 = 'user1'; // Set user1 as a customer service agent account.
// Calculate UserSig, which will be used when calling RESTful APIs. For more information, refer to documentation on <a href="https://github.com/tencentyun/tls-sig-api-v2-node">GitHub</a>.
const api = new TLSSigAPIv2.Api(SDKAppID, secrectKey);
const userSig = api.genSig(AppAdmin, 86400*180);
console.log('userSig:', userSig);
</pre>

### Step 3: configure the URL and token
> This guide document was written with reference to the Developer Guide for the WeChat Official Accounts Platform. In case of any change, the latest information can be found in the [Access Guide](https://mp.weixin.qq.com/wiki).

1. Log in to the management backend of the subscription account.
2. Select **Basic Configuration** and select the checkbox to agree to become a developer.
3. Click **Modify Configuration** and enter the following:
 - URL: the API URL for receiving WeChat messages and events. Required.
 - Token: user-defined string for generating a signature. The token will be compared with the token contained in the API URL for authentication. Required.
 - EncodingAESKey: manually entered or randomly generated. This is used as the key for message encryption and decryption. Optional.

### Step 4: enable the web service listening port and correctly respond to the token authentication request by WeChat

<pre>
const express = require('express'); // express framework 
const crypto =  require('crypto'); // Encryption module
const util = require('util');
const xml2js = require('xml2js'); // Parse xml.
const axios = require('axios'); // Initiate an HTTP request.
const TLSSigAPIv2 = require('tls-sig-api-v2'); // Calculate userSig.

// ------------ Web service ------------
var app = express();
// The token is set in **Subscription Account Management Backend** -> **Basic Configuration**.

// Process all GET requests from port 80.
app.get('/', function(req, res) {
  // ------------ Accessing the WeChat Official Accounts Platform ------------
  // For more information, see the <a href="https://developers.weixin.qq.com/doc/offiaccount/Basic_Information/Access_Overvie">WeChat official documentation</a>. 
  // Obtain signature, timestamp, nonce, and echostr from the WeChat server GET request.
  var signature = req.query.signature; // WeChat encrypted signature
  var timestamp = req.query.timestamp; // Timestamp
  var nonce = req.query.nonce; // Random number
  var echostr = req.query.echostr; // Random character string

  // Sort the token, timestamp, and nonce parameters in a lexicographical order.
  var array = [myToken, timestamp, nonce];
  array.sort();

  // Concatenate the character strings of the three parameters into one for sha1 encryption.
  var tempStr = array.join('');
  const hashCode = crypto.createHash('sha1'); // Create an encryption type. 
  var resultCode = hashCode.update(tempStr,'utf8').digest('hex'); // Encrypt the character string.

  // After obtaining the encrypted character string, the developer can compare it with signature and flag the request as being from WeChat.
  if (resultCode === signature) {
    res.send(echostr);
  } else {
    res.send('404 not found');
  }
});

// Listen to port 80.
app.listen(80);
</pre>

### Step 5: implement the service logic on the developer server

- When receiving subscription events from WeChat, call the [Importing a Single Account](https://intl.cloud.tencent.com/document/product/1047/34953) or [Batch Importing Accounts](https://intl.cloud.tencent.com/document/product/1047/34954) API to import accounts into the system.
- When receiving subscription events from WeChat, passively reply to the message.
- When receiving unsubscription events from WeChat, call the [Deleting Accounts](https://intl.cloud.tencent.com/document/product/1047/34955) API to delete the account from the system.
- When receiving a common message pushed by WeChat, call the [Sending a One-to-One Message](https://intl.cloud.tencent.com/document/product/1047/34919) API to send a one-to-one message to the agent account.

```javascript
const genRandom = function() {
  return  Math.floor(Math.random() * 10000000);
}

// Generate the wx text reply xml.
const genWxTextReplyXML = function(to, from, content) {
  let xmlContent = '<xml><ToUserName><![CDATA[' + to + ']]></ToUserName>'
  xmlContent += '<FromUserName><![CDATA[' + from + ']]></FromUserName>'
  xmlContent += '<CreateTime>' + new Date().getTime() + '</CreateTime>'
  xmlContent += '<MsgType><![CDATA[text]]></MsgType>'
  xmlContent += '<Content><![CDATA[' + content + ']]></Content></xml>';

  return xmlContent;
}

/**
 * Import users into the IM account system.
 * @param {String} userID ID of the user to be imported
 */
const importAccount = function(userID) {
  console.log('importAccount:', userID);
  return new Promise(function(resolve, reject) {
    var url = util.format('https://console.tim.qq.com/v4/im_open_login_svc/account_import?sdkappid=%s&identifier=%s&usersig=%s&random=%s&contenttype=json',
      SDKAppID, AppAdmin, userSig, genRandom());
    console.log('importAccount url:', url);
    IMAxios({
      url: url,
      data: {
        "Identifier": userID
      },
      method: 'POST'
    }).then((res) => {
      if (res.data.ErrorCode === 0) {
        console.log('importAccount ok.', res.data);
        resolve();
      } else {
        reject(res.data);
      }
    }).catch((error) => {
      console.log('importAccount failed.', error);
      reject(error);
    })
  });
}

/**
 * Delete users from the IM account system.
 * @param {String} userID ID of the user to be deleted
 */
const deleteAccount = function(userID) {
  console.log('deleteAccount', userID);
  return new Promise(function(resolve, reject) {
    var url = util.format('https://console.tim.qq.com/v4/im_open_login_svc/account_delete?sdkappid=%s&identifier=%s&usersig=%s&random=%s&contenttype=json',
      SDKAppID, AppAdmin, userSig, genRandom());
    console.log('deleteAccount url:', url);
    IMAxios({
      url: url,
      data: {
        "DeleteItem": [
          {
            "UserID": userID,
          },
        ]
      },
      method: 'POST'
    }).then((res) => {
      if (res.data.ErrorCode === 0) {
        console.log('deleteAccount ok.', res.data);
        resolve();
      } else {
        reject(res.data);
      }
    }).catch((error) => {
      console.log('deleteAccount failed.', error);
      reject(error);
    })
  });
}

/**
 * Send a one-to-one message.
 */
const sendC2CTextMessage = function(userID, content) {
  console.log('sendC2CTextMessage:', userID, content);
  return new Promise(function(resolve, reject) {
    var url = util.format('https://console.tim.qq.com/v4/openim/sendmsg?sdkappid=%s&identifier=%s&usersig=%s&random=%s&contenttype=json',
      SDKAppID, AppAdmin, userSig, genRandom());
    console.log('sendC2CTextMessage url:', url);
    IMAxios({
      url: url,
      data: {
        "SyncOtherMachine": 2, // The message will not be synchronized to the sender. If you want to synchronize the message to the From_Account, set SyncOtherMachine to 1.
        "To_Account": userID,
        "MsgLifeTime":60, // Messages are retained for 60 seconds.
        "MsgRandom": 1287657,
        "MsgTimeStamp": Math.floor(Date.now() / 1000), // The unit is second and must be an integer.
        "MsgBody": [
          {
            "MsgType": "TIMTextElem",
            "MsgContent": {
              "Text": content
            }
          }
        ]
      },
      method: 'POST'
    }).then((res) => {
      if (res.data.ErrorCode === 0) {
        console.log('sendC2CTextMessage ok.', res.data);
        resolve();
      } else {
        reject(res.data);
      }
    }).catch((error) => {
      console.log('sendC2CTextMessage failed.', error);
      reject(error);
    });
  });
}

// Process WeChat post requests.
app.post('/', function(req, res) {
  var buffer = [];
  // Listen for data events in order to receive data.
  req.on('data', function(data) {
    buffer.push(data);
  });
  // Listen for end events in order to process received data.
  req.on('end', function() {
    const tmpStr = Buffer.concat(buffer).toString('utf-8');
    xml2js.parseString(tmpStr, { explicitArray: false }, function(err, result) {
      if (err) {
        console.log(err);
        res.send("success");
      } else {
        if (!result) {
          res.send("success");
          return;
        }
        console.log('wx post data:', result.xml);
        var wxXMLData = result.xml;
        var toUser = wxXMLData.ToUserName; // Recipient's WeChat
        var fromUser = wxXMLData.FromUserName;// Sender's WeChat
        if (wxXMLData.Event) {  // Process the event type.
          switch (wxXMLData.Event) {
            case "subscribe": // Subscribe.
              res.send(genWxTextReplyXML(fromUser, toUser, 'Thanks for following XX. We want to offer you the best service.'));
              importAccount(fromUser).then(() => {
                // Record the ID of the imported user.
                importedAccountMap.set(fromUser, 1);
              });
              break;
            case "unsubscribe": // Unsubscribe.
              deleteAccount(fromUser).then(() => {
                importedAccountMap.delete(fromUser);
              });
              res.send("success");
              break;
          }
        } else { // Process the message type.
          switch (wxXMLData.MsgType) {
            case "text":
              // Process text messages.
              sendC2CTextMessage(kfAccount1, 'Inquiry from a WeChat subscription account: ' + wxXMLData.Content).then(() => {
                console.log('C2C message sent successfully');
              }).catch((error) => {
                console.log('C2C message failed to sent');
              });
              break;
            case "image":
              // Process image messages.
              break;
            case "voice":
              // Process voice messages.
              break;
            case "video":
              // Process video messages.
              break;
            case "shortvideo":
              // Process short video messages.
              break;
            case "location":
              // Process locations.
              break;
            case "link":
              // Process link messages.
              break;
            default:
              break;  
          }
          res.send(genWxTextReplyXML(fromUser, toUser, 'Transferring you to a customer service agent, please wait.'));
        }
      }
    })
  });
});
```

### Step 6: register and process IM third-party callbacks

<pre>
// Process POST requests from IM third-party callbacks.
app.post('/imcallback', function(req, res) {
  var buffer = [];
  // Listen for data events in order to to receive data.
  req.on('data', function(data) {
    buffer.push(data);
  });
  // Listen to end events in order to process received data.
  req.on('end', function() {
    const tmpStr = Buffer.concat(buffer).toString('utf-8');
    console.log('imcallback', tmpStr);
    const imData = JSON.parse(tmpStr);
    // Push the message sent by kfAccount1 to the customer.
    if (imData.From_Account === kfAccount1) {
      // Package the message and push it using the **customer service message** API of WeChat to the specified user.
      // Note: subscription accounts registered by individuals cannot use this API. For more information, refer to <a href="https://developers.weixin.qq.com/doc/offiaccount/Message_Management/Service_Center_messages.html">Customer Service Messages</a>. 
    }

    res.send({
      "ActionStatus":"OK",
      "ErrorInfo":"",
      "ErrorCode": 0 // 0: not muted. 1: muted.
    });
  });
});
</pre>
