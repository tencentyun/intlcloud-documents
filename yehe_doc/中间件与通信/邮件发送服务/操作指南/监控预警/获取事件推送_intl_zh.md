## 获取事件推送
**创建 URL**

事件推送是接收具体发送情况的渠道。在您通过 API 向腾讯云 DMS 发送邮件发送的请求之后，腾讯云会把「请求结果」同步返回，而邮件的「发送结果」和「其他事件结果」是通过事件推送异步返回的。

当某事件发生, 就会触发腾讯云 DMS 向您设置的 URL 发送数据 ( POST )。您在收到数据后，可以解析出事件和相应数据，做后续的处理。

目前支持的事件包括：请求、送达、无效、软退信、举报、打开和点击。具体事件的消息格式，请参考[事件推送相关问题](https://intl.cloud.tencent.com/document/product/1070/38236)。

获取事件推送，您需要：
1.  登录[腾讯云 DMS 控制台](https://console.cloud.tencent.com/dms)。
2.  在左侧导航栏中单击 【事件推送】，单击 【添加推送规则】。
3.  在添加推送规则弹窗中输入配置好能够正确响应 GET 和 POST 请求，并返回 HTTP 200 的 URL。
4.  单击 【验证】，验证成功后单击 【确定】 完成添加。
> 注意：目前事件推送仅支持一个URL，您可以在收到事件推送后做相应的处理。如果您需要添加多个 URL，请前往[提交工单](https://console.cloud.tencent.com/workorder) 。


**签名验证**
为了确保消息的来源身份是腾讯云 DMS，你可以选择对 POST 数据的来源进行安全认证。（您也可以选择不验证，直接对 POST 数据进行解析）

安全认证的方法如下:

-   点击 【发送密钥】 操作获取 `APP KEY`，腾讯云 DMS 会将 `APP KEY` 发送到您注册账号使用的邮箱
-   解析出 POST 数据中的 `token`，`timestamp` 和 `signature`
-   使用 `APP KEY`，`token` 和 `timestamp` 生成签名 `signature`，与 POST 数据中的 `signature` 进行校验 ( 签名算法: [SHA256](http://en.wikipedia.org/wiki/SHA-2))

**python 代码示例**

```
import hashlib, hmac
def verify(appkey, token, timestamp, signature):
    return signature == hmac.new(
        key=appkey,
        msg='{}{}'.format(timestamp, token),
        digestmod=hashlib.sha256).hexdigest()

```

**Java 代码示例** (依赖 [apache codec](http://commons.apache.org/proper/commons-codec/download_codec.cgi))

```
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;

import org.apache.commons.codec.binary.Hex;

public boolean verify(String appkey, String token, long timestamp,
            String signature) throws NoSuchAlgorithmException, InvalidKeyException {
    Mac sha256HMAC = Mac.getInstance("HmacSHA256");
    SecretKeySpec secretKey = new SecretKeySpec(appkey.getBytes(),"HmacSHA256");
    sha256HMAC.init(secretKey);
    StringBuffer buf = new StringBuffer();
    buf.append(timestamp).append(token);
    String signatureCal = new String(Hex.encodeHex(sha256HMAC.doFinal(buf
            .toString().getBytes())));
    return signatureCal.equals(signature);
}

```

**php 代码示例**

```
function verify($appkey,$token,$timestamp,$signature){
    $hash="sha256";
    $result=hash_hmac($hash,$timestamp.$token,$appkey);
    return strcmp($result,$signature)==0?1:0;
}
```

**重试机制**

如果遇到 URL 访问错误或超时，腾讯云 DMS 最多会重试 6 次。每次重试的时间间隔最快为 3min、10min、30min、1h、6h、12h、24h。即在消息丢失前，你有足够的时间来修复 URL。

如果超过重试次数，腾讯云 DMS 将会把消息丢弃。

每次事件处理，数据解析，您需要在 3s 内返回状态码 200，否则腾讯云 DMS 将会重发该条消息。