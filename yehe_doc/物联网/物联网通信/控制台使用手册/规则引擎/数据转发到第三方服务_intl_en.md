## Overview

When forwarding a message field extracted through a rule to a third-party service, you can customize how to process the data. This is the most flexible way for you to process the message.

>!The third-party service must be HTTP- or HTTPS-based. To configure forwarding to a third-party service, you need to provide a URL and port number supporting HTTP or HTTPS. After successful forwarding by the rule engine, the third-party service will receive packets from `42.193.134.62`.

The figure below shows the entire process of forwarding data to a third-party service:
![](https://main.qcloudimg.com/raw/66880632e6d2e6fd0c43d1643546171e.png)

For more information on the content and format of the data to be forwarded, please see [Data Processing](https://intl.cloud.tencent.com/document/product/1105/41485).

## Entering Server Configuration

1. Log in to the [IoT Hub console](https://console.cloud.tencent.com/iotcloud) and select **Rule Engine** on the left sidebar.
2. Click the rule to be configured to enter the rule details page and click **Add Action**.
3. In the pop-up **Add Action** window, enter relevant information and click **Save**.
 - Select "forward" as the action type.
 - Enter your HTTP or HTTPS service address. IoT Hub will forward data reported by devices to this address.
 - Please select **Authentication Token** and enter the corresponding token of your service. You can enter any token for signature generation (this token will be compared with the token contained in the URL of the API for authentication).
   ![](https://main.qcloudimg.com/raw/c052c2aa73d7d31c61e6de3f1d4fc145.png)


## Verifying Message Source as IoT Hub

>!To ensure the stable use of your backend, please select **Authentication Token**.

### Request ID

If **Authentication Token** is selected for forwarding to the third-party service (i.e., HTTP forwarding), IoT Hub will add the following fields to the header of the HTTP or HTTPS request:

<table>
<thead>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Signature</td>
<td>`Signature` combines the `Token` parameter entered in **Add Action** and the `Timestamp` and `Nonce` parameters in the request</td>
</tr>
<tr>
<td>Timestamp</td>
<td>Timestamp</td>
</tr>
<tr>
<td>Nonce</td>
<td>Random number</td>
</tr>
</tbody></table>

1. The `Token`, `Timestamp`, and `Nonce` parameters are sorted in lexicographical order.
2. The three parameter strings are concatenated into one string for SHA1 encryption.
3. After getting the encrypted string, you can compare it with `Signature` and verify whether the request comes from IoT Hub.

The sample code used to verify `Signature` in PHP is as follows:
<dx-codeblock>
:::  PHP
private function checkSignature()
{
    $signature = $_GET["signature"];
    $timestamp = $_GET["timestamp"];
    $nonce = $_GET["nonce"];
	
    $token = TOKEN;
    $tmpArr = array($token, $timestamp, $nonce);
    sort($tmpArr, SORT_STRING);
    $tmpStr = implode( $tmpArr );
    $tmpStr = sha1( $tmpStr );
    
    if( $tmpStr == $signature ){
        return true;
    }else{
        return false;
    }
}
:::
</dx-codeblock>

For example, the relevant parameters of a request are as follows, and `Token` is set to `aaa`.
<dx-codeblock>
:::  HTTP
Nonce: IkOaKMDalrAzUTxC
Signature: c259ed29ec13ba7c649fe0893007401a36e70453
Timestamp: 1604458421
:::
</dx-codeblock>

The string after sorting is `1604458421IkOaKMDalrAzUTxCaaa`, and the final SHA1 result is calculated as `c259ed29ec13ba7c649fe0893007401a36e70453`.

**Service address verification**

1. When the rule engine is enabled, IoT Hub will send a GET request to the entered server URL, and the following fields will be added to the header of the GET request:
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Signature</td>
<td>`Signature` combines the `Token` parameter entered in **Add Action** and the `Timestamp` and `Nonce` parameters in the request</td>
</tr>
<tr>
<td>Timestamp</td>
<td>Timestamp</td>
</tr>
<tr>
<td>Nonce</td>
<td>Random number</td>
</tr>
<tr>
<td>Echostr</td>
<td>Random string</td>
</tr>
</tbody></table>
Sample message sent by IoT Hub to the third-party service:
<dx-codeblock>
:::  HTTP
GET / HTTP/1.1
Host: **.**.**.**:4443
User-Agent: Go-http-client/1.1
Content-Type: application/json
Echostr: UPWIAFASvDUFcTEE
Nonce: testrance
Signature: abb6c316a8134596d825c5a1295bfa6f7657664d
Timestamp: 1623149590
Accept-Encoding: gzip
:::
</dx-codeblock>
2. If the third-party service confirms that the GET request comes from IoT Hub, it needs to return the content of the `Echostr` parameter as-is in the `body`.
Sample message replied by the third-party service to IoT Hub:
<dx-codeblock>
:::  HTTP
HTTP/1.1 200 OK
Date: Tue, 08 Jun 2021 10:53:10 GMT
Content-Length: 16
Content-Type: text/plain; charset=utf-8

UPWIAFASvDUFcTEE
:::
</dx-codeblock>
3. IoT Hub verifies the content of the returned `Echostr` parameter to check whether the server URL is valid.

## Resending Mechanism

The resending mechanism is used to send the message again in case of a failure in the message forwarding process, which makes sure that the message is received. The details are as follows:
- If message forwarding fails, the system will retry forwarding at intervals of 1s, 3s, and 10s in sequence. If all three retries fail, the message will be discarded.
- If you have configured the forward error action, then after three unsuccessful retries, the message will be forwarded again according to the configured action. If forwarding still fails, the message will be discarded.
