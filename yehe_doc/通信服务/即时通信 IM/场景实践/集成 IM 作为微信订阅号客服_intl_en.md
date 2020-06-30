This document describes how to use Node.js to develop a simple and common customer service agent demo as an example to describe the basic procedure of integrating Tencent Cloud IM with WeChat subscription accounts.
> The demo is for reference only. Many aspects, such as server load balancing, concurrent API control, and persistent information storage, need to be further improved before launch. Such improvements are not covered in this document. Developers can make improvements based on their actual needs.

## Basic Procedure and Effects of the Demo
The basic procedure of the demo described in this document is as follows:
1. A customer inquires "When will the children's clothing be available?" through a clothing and apparel e-commerce subscription account.
2. The customer's inquiry is transferred to the customer service agent of the clothing and apparel e-commerce account through Tencent Cloud IM.
3. The customer service agent replies "New clothing will be available in May. Please follow our updates." The message is pushed to the customer through Tencent Cloud IM and WeChat.
   

## Precautions
- If the message transfer link is long, it may take longer to send and receive messages.
- Subscription accounts registered by individuals cannot use the [customer service message] API of the WeChat Official Account Platform to push messages to subscribers.

## Prerequisites

- You have prepared a public network development server or CVM instance that can run Node.js.
- You have [registered](https://mp.weixin.qq.com/cgi-bin/registermidpage?action=index&lang=zh_CN&token=) a WeChat subscription account or service account.
- You have carefully read the [development document for the WeChat Official Account Platform](https://developers.weixin.qq.com/doc/offiaccount/Basic_Information/Access_Overview.html).
- You have created an [IM app](https://intl.cloud.tencent.com/document/product/1047/34577).
- You have imported IM user accounts, such as user0 and user1, through [one-by-one import](https://intl.cloud.tencent.com/document/product/1047/34953) or [batch import](https://intl.cloud.tencent.com/document/product/1047/34954) in advance.

## References

- [API Document](https://intl.cloud.tencent.com/document/product/1047/34620)
- [Third-Party Callback](https://intl.cloud.tencent.com/document/product/1047/34354)
- [Development Overview of the WeChat Official Account Platform](https://developers.weixin.qq.com/doc/offiaccount/Getting_Started/Overview.html)
- [Express Framework Tutorial](https://expressjs.com/zh-cn/)

## Directions

### Step 1: Create a development project and install dependencies

```javascript
npm init -y

// Express framework
npm i express@latest --save 

// Encryption module
npm i crypto@latest --save

// XML parser
npm i xml2js@latest --save

// Initiate an HTTP request.
npm i axios@latest --save

// Calculate the UserSig.
npm i tls-sig-api-v2@latest --save
```

### Step 2: Enter the IM app information and calculate the UserSig

<pre><code><span class="hljs-comment">// ------------ IM ------------</span>
<span class="hljs-keyword">const</span> IMAxios = axios.create({
  <span class="hljs-attr">timeout</span>: <span class="hljs-number">10000</span>,
  <span class="hljs-attr">headers</span>: {
    <span class="hljs-string">'Content-Type'</span>: <span class="hljs-string">'application/x-www-form-urlencoded;charset=UTF-8'</span>,
  },
});

<span class="hljs-comment">// The user ID mapping table imported into the IM account system is not persistently stored and used only for quick demo retrieval. For production environments, use another technical solution.</span>
<span class="hljs-keyword">const</span> importedAccountMap = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Map</span>();
<span class="hljs-comment">// IM app and app admin information can be obtained from the <a href="https://console.cloud.tencent.com/im">IM console</a>.</span>
<span class="hljs-keyword">const</span> SDKAppID = <span class="hljs-number">0</span>; <span class="hljs-comment">// Enter the SDKAppID of the IM app.</span>
<span class="hljs-keyword">const</span> secrectKey = <span class="hljs-string">''</span>; <span class="hljs-comment">// Enter the secret key of the IM app.</span>
<span class="hljs-keyword">const</span> AppAdmin = <span class="hljs-string">'user0'</span>; <span class="hljs-comment">// Set user0 as the app admin account.</span>
<span class="hljs-keyword">const</span> kfAccount1 = <span class="hljs-string">'user1'</span>; <span class="hljs-comment">// Set user1 as a customer service agent account.</span>
<span class="hljs-comment">// Calculate the UserSig, which will be used when calling RESTful APIs. For more information, see <a href="https://github.com/tencentyun/tls-sig-api-v2-node">Github</a>.</span>
<span class="hljs-keyword">const</span> api = <span class="hljs-keyword">new</span> TLSSigAPIv2.Api(SDKAppID, secrectKey);
<span class="hljs-keyword">const</span> userSig = api.genSig(AppAdmin, <span class="hljs-number">86400</span>*<span class="hljs-number">180</span>);
<span class="hljs-built_in">console</span>.log(<span class="hljs-string">'userSig:'</span>, userSig);</code></pre>

### Step 3: Configure the URL and token
> This document was written with reference to the Development Guide for the WeChat Official Account Platform. In case of any change, the latest information can be found in the [Access Guide](https://mp.weixin.qq.com/wiki).

1. Log in to the management backend of the subscription account.
2. Select **Basic Configuration** and select the protocol to become a developer.
3. Click **Modify Configuration** and complete the following relevant information.
 - URL: indicates the server address. This is the API URL for receiving WeChat messages and events. It is a required parameter.
 - Token: indicates a user-defined token. This is used to generate a signature. The token will be compared with the token contained in the API URL for security verification. It is a required parameter.
 - EncodingAESKey: is the manually entered or randomly generated key used for message body encryption. It is an optional parameter.

### Step 4: Enable the web service listening port and correctly respond to the token verification sent by WeChat

<pre><code><span class="hljs-keyword">const</span> express = <span class="hljs-keyword">require</span>(<span class="hljs-string">'express'</span>); <span class="hljs-comment">// Express framework</span>
<span class="hljs-keyword">const</span> crypto =  <span class="hljs-keyword">require</span>(<span class="hljs-string">'crypto'</span>); <span class="hljs-comment">// Encryption module</span>
<span class="hljs-keyword">const</span> util = <span class="hljs-keyword">require</span>(<span class="hljs-string">'util'</span>);
<span class="hljs-keyword">const</span> xml2js = <span class="hljs-keyword">require</span>(<span class="hljs-string">'xml2js'</span>); <span class="hljs-comment">// XML parser</span>
<span class="hljs-keyword">const</span> axios = <span class="hljs-keyword">require</span>(<span class="hljs-string">'axios'</span>); <span class="hljs-comment">// Initiate an HTTP request.</span>
<span class="hljs-keyword">const</span> TLSSigAPIv2 = <span class="hljs-keyword">require</span>(<span class="hljs-string">'tls-sig-api-v2'</span>); <span class="hljs-comment">// Calculate the UserSig.</span>

<span class="hljs-comment">// ------------ Web service ------------</span>
<span class="hljs-keyword">var</span> app = express();
<span class="hljs-comment">// You need to set the token by choosing **Subscription Account Management Backend** &gt; **Basic Configuration**.</span>

<span class="hljs-comment">// Process all GET requests that reach port 80.</span>
app.get(<span class="hljs-string">'/'</span>, <span class="hljs-function"><span class="hljs-keyword">function</span><span class="hljs-params">(req, res)</span> </span>{
  <span class="hljs-comment">// ------------ Accessing the WeChat Official Account Platform ------------</span>
  <span class="hljs-comment">// For more information, see the <a href="https://developers.weixin.qq.com/doc/offiaccount/Getting_Started/Overview.html">WeChat official document</a>.</span>
  <span class="hljs-comment">// Obtain the `signature`, `timestamp`, `nonce`, and `echostr` parameters from the GET request of the WeChat server.</span>
  <span class="hljs-keyword">var</span> signature = req.query.signature; <span class="hljs-comment">// WeChat encrypted signature</span>
  <span class="hljs-keyword">var</span> timestamp = req.query.timestamp; <span class="hljs-comment">// Timestamp</span>
  <span class="hljs-keyword">var</span> nonce = req.query.nonce; <span class="hljs-comment">// A radom number</span>
  <span class="hljs-keyword">var</span> echostr = req.query.echostr; <span class="hljs-comment">// A random string</span>

  <span class="hljs-comment">// Sort the `token`, `timestamp`, and `nonce` parameters in lexicographical order.</span>
  <span class="hljs-keyword">var</span> <span class="hljs-keyword">array</span> = [myToken, timestamp, nonce];
  <span class="hljs-keyword">array</span>.sort();

  <span class="hljs-comment">// Concatenate the strings of the three parameters into one for SHA1 encryption.</span>
  <span class="hljs-keyword">var</span> tempStr = <span class="hljs-keyword">array</span>.join(<span class="hljs-string">''</span>);
  <span class="hljs-keyword">const</span> hashCode = crypto.createHash(<span class="hljs-string">'sha1'</span>); <span class="hljs-comment">// Create an encryption type.</span>
  <span class="hljs-keyword">var</span> resultCode = hashCode.update(tempStr,<span class="hljs-string">'utf8'</span>).digest(<span class="hljs-string">'hex'</span>); <span class="hljs-comment">// Encrypt the input string.</span>

  <span class="hljs-comment">// After obtaining the encrypted string, the developer can compare it with the signature, and flag the request to indicate that the request comes from WeChat.</span>
  <span class="hljs-keyword">if</span> (resultCode === signature) {
    res.send(echostr);
  } <span class="hljs-keyword">else</span> {
    res.send(<span class="hljs-string">'404 not found'</span>);
  }
});

<span class="hljs-comment">// Listen to port 80.</span>
app.listen(<span class="hljs-number">80</span>);</code></pre>

### Step 5: Implement the service logic on the developer's server

- When receiving a followed event pushed by WeChat, call the API for [importing a single account](https://intl.cloud.tencent.com/document/product/1047/34953) or [batch importing accounts](https://intl.cloud.tencent.com/document/product/1047/34954) to import accounts into the account system.
- When receiving a followed event pushed by WeChat, passively reply to the message.
- When receiving an unfollowed event pushed by WeChat, call the API for [deleting accounts](https://intl.cloud.tencent.com/document/product/1047/34955) to delete the account from the account system.
- When receiving a common message pushed by WeChat, call the API for [sending one-to-one chat messages](https://intl.cloud.tencent.com/document/product/1047/34919) to send a one-to-one chat message to the customer service agent account.

```javascript
const genRandom = function() {
  return  Math.floor(Math.random() * 10000000);
}

// Generate the XML file for the wx text reply.
const genWxTextReplyXML = function(to, from, content) {
  let xmlContent = '<xml><ToUserName><![CDATA[' + to + ']]></ToUserName>'
  xmlContent += '<FromUserName><![CDATA[' + from + ']]></FromUserName>'
  xmlContent += '<CreateTime>' + new Date().getTime() + '</CreateTime>'
  xmlContent += '<MsgType><![CDATA[text]]></MsgType>'
  xmlContent += '<Content><![CDATA[' + content + ']]></Content></xml>';

  return xmlContent;
}

/**
 * Import users to the IM account system.
 * @param {String} userID - ID of the user to be imported
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
 * Delete a user from the IM account system.
 * @param {String} userID - ID of the user to be deleted
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
 * Send a one-to-one chat message.
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
        "SyncOtherMachine": 2, // The message will not be synchronized to the sender. If you want it to be synchronized to `From_Account`, set `SyncOtherMachine` to 1.
        "To_Account": userID,
        "MsgLifeTime":60, // The message will be retained for 60 seconds.
        "MsgRandom": 1287657,
        "MsgTimeStamp": Math.floor(Date.now() / 1000), // The unit is second and the value must be an integer.
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

// Process POST requests from WeChat.
app.post('/', function(req, res) {
  var buffer = [];
  // Monitor data events, which are used to receive data.
  req.on('data', function(data) {
    buffer.push(data);
  });
  // Monitor end events, which are used to process the received data.
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
        var toUser = wxXMLData.ToUserName; // Recipient’s WeChat ID
        var fromUser = wxXMLData.FromUserName;// Sender’s WeChat ID
        if (wxXMLData.Event) {  // Process the event type.
          switch (wxXMLData.Event) {
            case "subscribe": // Follow the subscription account.
              res.send(genWxTextReplyXML(fromUser, toUser, 'Thanks for following XX. We will offer you the best service.'));
              importAccount(fromUser).then(() => {
                // Record the ID of the imported user.
                importedAccountMap.set(fromUser, 1);
              });
              break;
            case "unsubscribe": // Unfollow the account.
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
              sendC2CTextMessage(kfAccount1, 'Inqury from the WeChat subscription account:' + wxXMLData.Content).then(() => {
                console.log('Sent the C2C message successfully');
              }).catch((error) => {
                console.log(Failed to send the 'C2C message');
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
              // Process location sending messages.
              break;
            case "link":
              // Process link clicking messages.
              break;
            default:
              break;  
          }
          res.send(genWxTextReplyXML(fromUser, toUser, 'Transferring to a customer service agent, please wait'));
        }
      }
    })
  });
});
```

### Step 6: Register and process IM third-party callbacks

<pre><code><span class="hljs-comment">// Process POST requests from IM third-party callbacks.</span>
app.post(<span class="hljs-string">'/imcallback'</span>, <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">req, res</span>) </span>{
  <span class="hljs-keyword">var</span> buffer = [];
  <span class="hljs-comment">// Monitor data events, which are used to receive data.</span>
  req.on(<span class="hljs-string">'data'</span>, <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">data</span>) </span>{
    buffer.push(data);
  });
  <span class="hljs-comment">// Monitor end events, which are used to process the received data.</span>
  req.on(<span class="hljs-string">'end'</span>, <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>) </span>{
    <span class="hljs-keyword">const</span> tmpStr = Buffer.concat(buffer).toString(<span class="hljs-string">'utf-8'</span>);
    <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'imcallback'</span>, tmpStr);
    <span class="hljs-keyword">const</span> imData = <span class="hljs-built_in">JSON</span>.parse(tmpStr);
    <span class="hljs-comment">// Push the message sent by kfAccount1 to the user.</span>
    <span class="hljs-keyword">if</span> (imData.From_Account === kfAccount1) {
      <span class="hljs-comment">// Package the message and push it through the **customer service message** API of WeChat to the specified user.</span>
      <span class="hljs-comment">// Note: subscription accounts registered by individuals are not allowed to use this API. For more information, see <a href="https://developers.weixin.qq.com/doc/offiaccount/Message_Management/Service_Center_messages.html">Customer Service Messages</a>.</span>
    }

    res.send({
      <span class="hljs-string">"ActionStatus"</span>: <span class="hljs-string">"OK"</span>,
      <span class="hljs-string">"ErrorInfo"</span>: <span class="hljs-string">""</span>,
      <span class="hljs-string">"ErrorCode"</span>: <span class="hljs-number">0</span> <span class="hljs-comment">// 0: not muted. 1: muted.</span>
    });
  });
});</code></pre>
