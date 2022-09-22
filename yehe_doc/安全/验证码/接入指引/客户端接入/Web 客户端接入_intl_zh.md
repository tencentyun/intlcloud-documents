## 前提条件
客户端接入前，需完成新建验证，并在**验证列表**获取所需的 CaptchaAppId 以及 AppSecretKey。步骤如下：

1. 登录 [验证码控制台](https://console.cloud.tencent.com/captcha/graphical) ，左侧导航栏选择**图形验证** > **验证管理**，进入验证管理页面。
2. 单击**新建验证**，根据业务场景需求，设置验证名称等参数。
3. 单击**确定**，完成新建验证，即可在验证列表中查看验证码 CaptchaAppId 及 AppSecretKey。

## 代码示例

以下代码示例，单击**验证**，激活验证码，并弹窗展示验证结果。

>! 该示例未展示调用票据校验 API 的逻辑。业务客户端完成验证码接入后，业务服务端需二次核查验证码票据结果（未接入票据校验，会导致黑产轻易伪造验证结果，失去验证码人机对抗效果），详情请参见：[接入票据校验（Web 及 App）](https://intl.cloud.tencent.com/document/product/1159/49682)。

```

  <!DOCTYPE html>
  <html lang="en">
  
  <head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Web frontend access code sample</title>
    <!-- (Required) Dependency of the CAPTCHA program, which cannot be modified. If you use local caching or other methods to skip loading of the CAPTCHA, the CAPTCHA will not update and work properly, even triggering false positives. -->
    <script src="https://sg.captcha.qcloud.com/TCaptcha-global.js"></script>
  </head>
  
  <body>
    <button id="CaptchaId" type="button">Verify</button>
  </body>
  
  <script>
  
      // Define the callback function
      function callback(res) {
          // The callback output returned by the first passed parameter, which is as follows
          // ret         Int       Verification result. The value 0 indicates a successful verification. The value 2 indicates that the CAPTCHA is disabled by the user.
          // ticket      String    A verified ticket. The field value is not null only when ret = 0.
          // CaptchaAppId       String    ID of the CAPTCHA.
          // bizState    Any       The defined transparent transmission parameter.
          // randstr     String    The random string verified, which is required for subsequent ticket verification.
          console.log('callback:', res);
  
  
          // res（The user disables the CAPTCHA）= {ret: 2, ticket: null}
          // res（Verified） = {ret: 0, ticket: "String", randstr: "String"}
          // res（Return a disaster recovery ticket prefixed with "error_" when the verification request fails） = {ret: 0, ticket: "String", randstr: "String",  errorCode: Number, errorMessage: "String"}
          // Here is the code snippet of the verification result. Modify it based on the actual ticket and errorCode
          if (res.ret === 0) {
            // Copy result to clipboard
            var str = '【randstr】->【' + res.randstr + '】      【ticket】->【' + res.ticket + '】';
            var ipt = document.createElement('input');
            ipt.value = str;
            document.body.appendChild(ipt);
            ipt.select();
            document.execCommand("Copy");
            document.body.removeChild(ipt);
            alert('1. Return result（randstr、ticket）Copied successfully. You can press Ctrl+V to paste the result to view。2. Open the console from your browser and view the result returned。');
          }
      }
  
      // Define the function that handles TCaptcha-global.js loading errors
      function loadErrorCallback() {
        var appid = ''
        // Generate a disaster recovery ticket or execute other operations
        var ticket = 'terror_1001_' + appid + Math.floor(new Date().getTime() / 1000);
        callback({
          ret: 0,
          randstr: '@'+ Math.random().toString(36).substr(2),
          ticket: ticket,
          errorCode: 1001,
          errorMessage: 'jsload_error',
        });
      }
  
      // Define the event that triggers CAPTCHA
      window.onload = function(){
        document.getElementById('CaptchaId').onclick = function(){
          try {
            // Generate a CAPTCHA object
            // CaptchaAppId：Log in to the Captcha console and enter the [Manage CAPTCHA] page. If no CAPTCHAs has been created, create one first.
            //callback：Defined callback function
            var captcha = new TencentCaptcha('CaptchaAppId', callback, {});
            // Call the method to display the CAPTCHA
            captcha.show(); 
          } catch (error) {
            // Load error. Please call the  load error handling function
            loadErrorCallback();
            }
          }
      }
  </script>
  
  </html>
```
## 接入说明

### 步骤1：动态引入验证码 JS
Web 页面需动态引入验证码 JS，在业务需要验证时，唤起验证码进行验证。

```
<!-- 动态引入验证码JS示例 -->
<script src="https://sg.captcha.qcloud.com/TCaptcha-global.js"></script>
```

>! 必须动态引入验证码 JS。如通过其他手段规避动态加载，会导致验证码无法正常更新，对抗能力无法保证，甚至引起误拦截。

### 步骤2：创建验证码对象
引入验证码 JS 后，验证码会在全局注册一个`TencentCaptcha`类，业务方可以使用这个类自行初始化验证码，并对验证码进行显示或者隐藏。

>! 触发验证码的元素不要使用`id="TencentCaptcha"`，TencentCaptcha 属于系统默认 id，不可使用。 

#### 构造函数

```
new TencentCaptcha(CaptchaAppId, callback, options);
```

**参数说明**

<table>
<thead><tr>
<th>参数名</th><th>值类型</th><th>说明</th></tr>
</thead>
<tbody><tr><td>CaptchaAppId</td><td>String</td>
<td>验证码 CaptchaAppId：登录 <a href="https://console.cloud.tencent.com/captcha/graphical">验证码控制台</a>，在<strong>验证管理页面</strong>进行查看。如果未创建过验证，请先新建验证。</td></tr><tr><td>callback</td><td>Function</td><td>验证码回调函数，详情请参见 <a href="#hdhs">callback 回调函数</a>。</td>
</tr><tr><td>options</td><td>Object</td>
<td>验证码外观配置参数, 详情请参见 <a href="#pzcs">options 外观配置参数</a>。</td>
</tr></tbody></table>


[](id:hdhs)

#### callback 回调函数

验证结束后，会调用业务传入的回调函数，并在第一个参数中传入回调结果。回调结果字段说明如下：

| 字段名       | 值类型 | 说明                                                         |
| ------------ | ------ | ------------------------------------------------------------ |
| ret          | Int    | 验证结果，0：验证成功。2：用户主动关闭验证码。               |
| ticket       | String | 验证成功的票据，当且仅当 ret = 0 时 ticket 有值。            |
| CaptchaAppId | String | 验证码应用 ID。                                              |
| bizState     | Any    | 自定义透传参数。                                             |
| randstr      | String | 本次验证的随机串，后续票据校验时需传递该参数。               |
| errorCode    | Number | 错误 code ，详情请参见 [回调函数 errorCode 说明](#errorCode)。 |
| errorMessage | String | 错误信息。                                                     |

[](id:errorCode)
**回调函数errorCode说明**

| errorCode | 说明                       |
| --------- | -------------------------- |
| 1001      | TCaptcha-global.js加载错误 |
| 1002      | 调用 show 方法超时         |
| 1003      | 中间 js 加载超时           |
| 1004      | 中间 js 加载错误           |
| 1005      | 中间 js 运行错误           |
| 1006      | 拉取验证码配置错误/超时    |
| 1007      | iframe 加载超时            |
| 1008      | iframe 加载错误            |
| 1009      | jquery 加载错误            |
| 1010      | 滑块 js 加载错误           |
| 1011      | 滑块 js 运行错误           |
| 1012      | 刷新连续错误3次            |
| 1013      | 验证网络连续错误3次        |

[](id:pzcs)

#### options 外观配置参数

options 参数用于对验证码进行定制外观设置，默认可以设置为空。

>!
>- 验证码弹窗内部不支持调整样式大小，如果需要调整，可在弹窗最外层用 `class=tcaptcha-transform` 的元素设置 `transform:scale();`。验证码更新可能会改变元素的 id，class 等属性，请勿依赖其他验证码元素属性值覆盖样式。
>- 如果手机原生端有设置左右滑动手势，需在调用验证码 show 方法前禁用，验证完成后再打开，防止与验证码滑动事件冲突。


| 配置名         | 值类型                | 说明                                                         |
| :------------- | :-------------------- | :----------------------------------------------------------- |
| bizState       | Any                   | 自定义透传参数，业务可用该字段传递少量数据，该字段的内容会被带入 callback 回调的对象中。 |
| enableDarkMode | Boolean/String | 开启自适应深夜模式或强制深夜模式。<li>开启自适应深夜模式: {"enableDarkMode": true}</li><li>强制深夜模式: {"enableDarkMode": 'force'}</li> |
| ready          | Function              | 验证码加载完成的回调，回调参数为验证码实际的宽高：<br>{"sdkView": {<br>"width": number,<br>"height": number<br>}}<br>该参数仅为查看验证码宽高使用，**请勿使用此参数直接设定宽高**。 |
| needFeedBack   | String | 自定义帮助链接: {"needFeedBack": 'url地址' } |
|loading|Boolean|是否在验证码加载过程中显示loading框。不指定该参数时，默认显示loading框。<li>显示loading框: {"loading": true}</li><li>不显示loading框: {"loading": false}</li>|
| userLanguage   | String                | 指定验证码提示文案的语言，优先级高于控制台配置。<br/>支持传入值同 navigator.language 用户首选语言，大小写不敏感。<br/>详情参见 [userLanguage 配置参数](#userLanguage)。 |

[](id:userLanguage)

**userLanguage 配置参数**

| 参数名 | 说明                 |
| :----- | :------------------- |
| zh-cn  | 简体中文             |
| zh-hk  | 繁体中文（中国香港） |
| zh-tw  | 繁体中文（中国台湾） |
| en     | 英文                 |
| ar     | 阿拉伯语             |
| my     | 缅甸语               |
| fr     | 法语                 |
| de     | 德语                 |
| he     | 希伯来语             |
| hi     | 印地语               |
| id     | 印尼语               |
| it     | 意大利语             |
| ja     | 日语                 |
| ko     | 朝鲜语               |
| lo     | 老挝语               |
| ms     | 马来语               |
| pl     | 波兰语               |
| pt     | 葡萄牙语             |
| ru     | 俄语                 |
| es     | 西班牙语             |
| th     | 泰语                 |
| tr     | 土耳其语             |
| vi     | 越南语               |

### 步骤3：调用验证码实例方法

TencentCaptcha 的实例提供一些操作验证码的常用方法：

| 方法名    | 说明                       | 传入参数 | 返回内容                                 |
| --------- | -------------------------- | -------- | ---------------------------------------- |
| show      | 显示验证码，可以反复调用。 | 无       | 无                                       |
| destroy   | 隐藏验证码，可以反复调用。 | 无       | 无                                       |
| getTicket | 获取验证成功后的 ticket。   | 无       | `Object:{"CaptchaAppId":"","ticket":""}` |

### 步骤4：容灾处理

为保障验证码 Captacha 服务端异常时不阻塞客户网站正常业务流程，建议参考如下方式接入验证码。

1. 定义JS加载错误处理函数。
``` javascript
// 错误处理函数作用：在JS加载或初始化错误时，保障事件流程正常
// 函数定义需在script加载前
function loadErrorCallback() {
	var appid = ''
	// 生成容灾票据或自行做其它处理
	var ticket = 'terror_1001_' + appid + Math.floor(new Date().getTime() / 1000);
	callback({
		ret: 0,
        randstr: '@'+ Math.random().toString(36).substr(2),
        ticket,
        errorCode: 1001,
        errorMessage: 'jsload_error',
	});
}
```
2. 调用验证码实例catch到错误时，调用JS加载错误处理函数。
```javascript
try {
	// 生成一个验证码对象
	var captcha = new TencentCaptcha('你的验证码CaptchaAppId', callback, {});
	// 调用方法，显示验证码
	captcha.show(); 
} catch (error) {
	// 加载异常，调用验证码js加载错误处理函数
	loadErrorCallback();
}
```
3. 定义验证码callback回调函数时，根据 ticket 和 errorCode （而非 ret）的情况做处理。errorCode的定义参考步骤2中"回调函数errorCode说明"。
```javascript
function callback(res) {
	// res（用户主动关闭验证码）= {ret: 2, ticket: null}
	// res（验证成功） = {ret: 0, ticket: "String", randstr: "String"}
	// res（请求错误，返回terror_前缀的容灾票据） = {ret: 0, ticket: "String", randstr: "String",  errorCode: Number, errorMessage: "String"}
	if (res.ticket){
		//根据errorCode情况做特殊处理
        if(res.errorCode === xxxxx){
           //自定义容灾逻辑（例如跳过这次验证）
        }
      }
}
```

完整容灾方案，详情请见[业务容灾方案](https://intl.cloud.tencent.com/document/product/1159/49688)。

>! 业务客户端完成验证码接入后，服务端需二次核查验证码票据结果（未接入票据校验，会导致黑产轻易伪造验证结果，失去验证码人机对抗效果），详情请参见：[接入票据校验(Web及App)](https://intl.cloud.tencent.com/document/product/1159/49682)。

## 常见问题

详情参见 [接入相关问题](https://intl.cloud.tencent.com/document/product/1159/49692)。
