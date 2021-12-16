## Feature Description

If an API call fails, you can check the error information based on the error code list.

## Error Code List

### Error codes of SMS message sending

<table>
   <tr>
      <th nowrap="nowrap">Error Code</th>
      <th>Description</th>
      <th>Solution</th>
   </tr>
   <tr>
      <td>1001</td>
      <td>`sig` verification failed.</td>
      <td>Check the `sig` against the format requirements in the API.</td>
   </tr>
   <tr>
      <td>1002</td>
      <td>The SMS message contains sensitive words.</td>
      <td>Contact <a href="https://intl.cloud.tencent.com/document/product/382/3773">SMS Helper</a> for assistance.</td>
   </tr>
   <tr>
      <td>1003</td>
      <td>The request body has no `sig` field or the `sig` field is empty.</td>
      <td>Follow the API specification.</td>
   </tr>
   <tr>
      <td>1004</td>
      <td>Failed to parse the request packet. Usually, this is because that the API specification was not followed.</td>
       <td>For more information, see <a href="https://intl.cloud.tencent.com/document/product/382/9558">What should I do if error 1004 is returned?</a>.</td>
   </tr>
   <tr>
      <td>1006</td>
      <td>The request has no permissions.</td>
       <td>Check the error message for solution. If the problem persists, contact <a href="https://intl.cloud.tencent.com/document/product/382/3773">SMS Helper</a> and provide the failed mobile number for assistance.</td>
   </tr>
   <tr>
      <td>1007</td>
      <td>Other errors.</td>
       <td>Check the error message for solution. If the problem persists, contact <a href="https://intl.cloud.tencent.com/document/product/382/3773">SMS Helper</a> and provide the failed mobile number for assistance.</td>
   </tr>
   <tr>
      <td>1008</td>
      <td>The request to send an SMS message timed out.</td>
      <td>The probability of this error is very low. You can retry to solve it.</td>
   </tr>
   <tr>
      <td>1009</td>
      <td>The request IP is not on the allowlist.</td>
       <td>You have configured the verification of request source IP, but the current requesting IP is not on the configured allowlist. If necessary, contact <a href="https://intl.cloud.tencent.com/document/product/382/3773">SMS Helper</a> for assistance.</td>
   </tr>
   <tr>
      <td>1011</td>
      <td>This RESTful API does not exist.</td>
      <td>See the RESTful API description.</td>
   </tr>
   <tr>
      <td>1012</td>
      <td>The signature is in incorrect format or has not been approved.</td>
      <td>The signature can contain only 2–12 letters and digits. If its format is correct, check whether it has been approved.</td>
   </tr>
   <tr>
      <td>1013</td>
      <td>The SMS sending hits the sending frequency limit policy.</td>
       <td>You can adjust the policy in the console. If you have other requirements, contact <a href="https://intl.cloud.tencent.com/document/product/382/3773">SMS Helper</a> for assistance.</td>
   </tr>
   <tr>
      <td>1014</td>
      <td>The template content has not been approved or does not match the content of the approved template.</td>
       <td>For more information, see <a href="https://intl.cloud.tencent.com/document/product/382/9558">What should I do if error 1014 is returned?</a>.</td>
   </tr>
   <tr>
      <td>1015</td>
      <td>The mobile number is on the blocklist. Usually, this is because that the user unsubscribed or the carrier's blocklist was hit.</td>
       <td>Contact <a href="https://intl.cloud.tencent.com/document/product/382/3773">SMS Helper</a> for assistance.</td>
   </tr>
   <tr>
      <td>1016</td>
      <td>The format of the mobile number is incorrect.</td>
      <td>For more information, see <a href="https://intl.cloud.tencent.com/document/product/382/9558">What should I do if error 1016 is returned?</a>.</td>
   </tr>
   <tr>
      <td>1017</td>
      <td>The content of the requested SMS message is too long.</td>
       <td>For message length calculation rule, see <a href="https://intl.cloud.tencent.com/document/product/382/18052">SMS Length Calculation Rule</a>.</td>
   </tr>
   <tr>
      <td>1019</td>
      <td>The `sdkappid` does not exist.</td>
      <td>-</td>
   </tr>
   <tr>
      <td>1020</td>
      <td>The `sdkappid` has been disabled.</td>
       <td>This `sdkappid` is forbidden to provide services. If necessary, contact <a href="https://intl.cloud.tencent.com/document/product/382/3773">SMS Helper</a> for assistance.</td>
   </tr>
   <tr>
      <td>1021</td>
      <td>The request was initiated at an exceptional time. Usually, this is because that the time difference between your server and Tencent Cloud server exceeds 10 minutes.</td>
      <td>Check whether the server time and the time field in the API are correct.</td>
   </tr>
   <tr>
      <td>1022</td>
      <td>The number of SMS messages sent on the current day exceeds the set upper limit.</td>
      <td>You can adjust the SMS sending frequency limit policy in the console.</td>
   </tr>
   <tr>
      <td>1023</td>
      <td>The number of SMS messages sent to a single mobile number within 30 seconds exceeds the set upper limit.</td>
      <td>You can adjust the SMS sending frequency limit policy in the console.</td>
   </tr>
   <tr>
      <td>1024</td>
      <td>The number of SMS messages sent to a single mobile number within 1 hour exceeds the set upper limit.</td>
      <td>You can adjust the SMS sending frequency limit policy in the console.</td>
   </tr>
   <tr>
      <td>1025</td>
      <td>The number of SMS messages sent to a single mobile number on the current day exceeds the set upper limit.</td>
      <td>You can adjust the SMS sending frequency limit policy in the console.</td>
   </tr>
   <tr>
      <td>1026</td>
      <td>The number of identical SMS messages sent to a single mobile number exceeds the set upper limit.</td>
      <td>You can adjust the SMS sending frequency limit policy in the console.</td>
   </tr>
   <tr>
      <td>1029</td>
      <td>The marketing SMS sending time is incorrect.</td>
      <td>Marketing SMS messages can only be sent between 8:00 and 22:00 in order not to disturb recipients.</td>
   </tr>
   <tr>
      <td>1030</td>
      <td>The request is not supported.</td>
      <td>-</td>
   </tr>
   <tr>
      <td>1031</td>
      <td>The package balance is insufficient.</td>
       <td>Purchase an SMS package.</td>
   </tr>
   <tr>
      <td>1032</td>
      <td>Individual users do not have permission to send marketing SMS messages.</td>
      <td>See <a href="https://intl.cloud.tencent.com/document/product/382/40653">Differences in rights</a>.</td>
   </tr>
   <tr>
      <td>1033</td>
      <td>The service has been suspended due to overdue payments. </td>
      <td>You can log in to Tencent Cloud to make the payments.</td>
   </tr>
   <tr>
      <td>1034</td>
      <td>The group SMS request contains both Chinese mainland and global mobile numbers.</td>
      <td>Send SMS messages to Chinese mainland and global mobile numbers separately.</td>
   </tr>
   <tr>
      <td>1036</td>
      <td>There are more than 12 characters in a single template variable.</td>
       <td>There is no upper limit of variable characters for enterprise users. You can change your account identity type to enterprise as instructed in <a href="https://intl.cloud.tencent.com/document/product/378/37276">Identity Verification Change Guide</a>. The limit change will take effect in about one hour.</td>
   <tr>
   <tr>
      <td>1038</td>
      <td>For a verification code template, only 0–6 digits can be passed in as the template variable.</td>
       <td>-</td>
   <tr>
      <td>1045</td>
      <td>SMS sending to this region is not supported.</td>
      <td>-</td>
   </tr>	 
      <tr>
      <td>1046</td>
      <td>There are more than 200 mobile numbers submitted in a single call of the bulk SMS sending API.</td>
      <td>Follow the API specification.</td>
   </tr>	    	 
      <tr>
      <td>1047</td>
      <td>The number of global SMS messages that can be sent per day is limited.</td>
      <td>To adjust the limit, contact <a href="https://intl.cloud.tencent.com/document/product/382/3773">SMS Helper</a> for assistance.</td>
   </tr>	    
      <tr>
      <td>1048</td>
      <td>URLs are not allowed in template variables.</td>
      <td>-</td>
   </tr>
      <tr>
      <td>1049</td>
      <td>The number of Chinese mainland SMS messages sent on the current day exceeds the set upper limit.</td>
      <td>You can adjust the SMS sending frequency limit policy in the console.</td>
   </tr>
      <tr>
      <td>1050</td>
      <td>The number of global SMS messages sent on the current day exceeds the set upper limit</td>
      <td>You can adjust the SMS sending frequency limit policy in the console.</td>
   </tr>
      <tr>
      <td>1051</td>
      <td>The SMS sending target country/region is on the blocklist.</td>
      <td>You can adjust the SMS sending limit policy in the console.</td>
   </tr>
      <tr>
      <td>1052</td>
      <td>The number of SMS messages sent to the recipient's country/region on the current day exceeds the set upper limit</td>
      <td>You can adjust the SMS sending frequency limit policy in the console.</td>
   </tr>	
   <tr>
      <td>60008</td>
      <td>Request processing timed out.</td>
      <td>For more information, see <a href="https://intl.cloud.tencent.com/document/product/382/9558">What should I do if error 60008 is returned?</a>.</td>
   </tr>
   </tr>
</table>

### Error codes of receipt status

If the following errors occur, we recommend you contact the carrier for processing first. If you cannot find the details of an error code in the table below, contact [SMS Helper](https://intl.cloud.tencent.com/document/product/382/3773) for assistance. The table contains the following abbreviations/acronyms: CMCC (China Mobile), UNICOM (China Unicom), TELECOM (China Telecom), and MTU (China Mobile, China Telecom, and China Unicom).

| Error Code       | Category | Description     |
| ------------ | ---- | -------- |
| -106                 | MTU | The message is blocked by the carrier as it hits a keyword.                       |
| 002                  | MTU | The recipient's phone is powered off, out of service, unreachable, or out of area.      |
| 004                  | MTU | The recipient's mobile number is out of service, invalid, or suspended.             |
| BD:LSTO              | MTU | The carrier's gateway is exceptional.                         |
| BST-209 | MTU | The recipient is on the carrier's blocklist. |
| BST-210 | MTU | The message is blocked by the carrier as it hits a keyword. |
| BWLIST \_006 | MTU | The recipient is on the gateway's blocklist. |
| DB:0108 | MTU | The carrier's gateway is exceptional. |
| DB:13                | MTU | The recipient's phone has a reception exception.                           |
| DB00141 | MTU | The message is blocked by the carrier as it hits a keyword. |
| DELIVRD | MTU | The message is successfully delivered to the recipient. |
| DISTURB | MTU | Too many messages have been sent to the recipient. |
| ER:101               | MTU | The recipient is on the carrier's blocklist.                           |
| ERR:111              | MTU | The carrier's gateway is exceptional.                         |
| ERR-209 | MTU | The recipient is on the carrier's blocklist. |
| ERR-210 | MTU | The message is blocked by the carrier as it hits a keyword. |
| IB:0182 | MTU | The carrier's gateway is exceptional. |
| IC-0054 | MTU | The message is blocked by the carrier as it hits a keyword. |
| LN:9999              | MTU | The carrier's gateway is exceptional.                         |
| MB:1013              | MTU | The message is blocked by the carrier's gateway.                         |
| MX:0003 | MTU | The number of messages sent to one single mobile number on the current day exceeds the upper limit. |
| MX:0012 | MTU | The recipient's mobile number is on the unsubscription blocklist. |
| OVERDUE | MTU | The recipient's phone has a reception exception. |
| REJECTD | MTU | The message is rejected for some reason. |
| SC:0001 | MTU | The message is blocked by the carrier as it hits a keyword. |
| SME13 | MTU | The recipient is on the carrier's blocklist. |
| TD:0001 | MTU | The recipient is on the gateway's blocklist. |
| TD:0004 | MTU | The message is suspiciously phishing and should be checked. |
| TD:18 | MTU | The recipient's mobile number's carrier is unknown. |
| TD:19 | MTU | The recipient's mobile number is on the blocklist. |
| TE:0002 | MTU | Message submission to the gateway fails. |
| TE:0003 | MTU | The number of messages sent to one single mobile number on the current day exceeds the upper limit. |
| TE:0014 | MTU | Human review fails. |
| TSBLACK | MTU | The recipient is on the compliant blocklist. |
| TX:2000              | MTU | Signature subcode acquisition fails.                       |
| TX:2001              | MTU | Signature subcode acquisition times out.                       |
| TX:2002              | MTU | Signature subcode acquisition fails.                       |
| TX:2003              | MTU | Signature parsing fails.                           |
| TX:3000              | MTU | Sending submission fails.                           |
| TX:3001              | MTU | Sending times out.                               |
| TX:4099              | MTU | The carrier's gateway is exceptional.                         |
| TX:4100              | MTU | The carrier's gateway is exceptional.                         |
| TX:4151              | MTU | The carrier's gateway is exceptional.                         |
| WX-FAIL              | MTU | The recipient is on the carrier's blocklist.                           |
| UNDELIVRD | MTU | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.  |
| XZ:0000 | MTU | The message is blocked by the carrier as it hits a keyword. |
| YX:9006              | MTU | Message sending fails as the message contains multiple signatures.                             |
| YY:0206              | MTU | The carrier's gateway is exceptional.                         |
| XA:0001| MTU | The message is blocked by the carrier's gateway. |
| XA:0100| MTU | The frequency limit is reached. |
| XA:0139| MTU | The recipient is on the carrier's blocklist.   |
| -9990                | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off. |
| -9410                | CMCC | The recipient is on the carrier's blocklist.   |
| -9409                | CMCC | The recipient is on the carrier's blocklist.   |
| -9246                | CMCC | The recipient is on the carrier's blocklist.    |
| -9236                | CMCC | The carrier's frequency limit is reached.   |
| -9235                | CMCC | The carrier's frequency limit is reached.   |
| -9234                | CMCC | The carrier's frequency limit is reached.   |
| -9233                | CMCC | The carrier's frequency limit is reached.   |
| -9231                | CMCC | The carrier's frequency limit is reached.  |
| -9224                | CMCC | The carrier's gateway is exceptional.   |
| -9223                | CMCC | The message is blocked by the carrier as it hits a keyword.   |
| -9222                | CMCC | The message is blocked by the carrier as it hits a keyword.    |
| -9220                | CMCC | The recipient is on the carrier's blocklist.   |
| -9217                | CMCC | The carrier's gateway is exceptional.  |
| -9212                | CMCC | The recipient is on the carrier's blocklist.   |
| -9211                | CMCC | The message is blocked by the carrier as it hits a keyword.    |
| -9203                | CMCC | The recipient's mobile number does not exist.    |
| -9014                | CMCC | The recipient is on the carrier's blocklist.   |
| -9013                | CMCC | The recipient is on the carrier's blocklist.   |
| -9012                | CMCC | The recipient is on the carrier's blocklist.   |
| -9009                | CMCC | The carrier's gateway is exceptional. |
| -9000 | CMCC | The recipient's mobile number is exceptional as it is ported to another carrier. |
| -1050                | CMCC | The message is blocked by the carrier as it hits a keyword.  |
| -1033                | CMCC | Message sending fails as the recipient's mobile number is ported to another carrier. |
| -1023   | CMCC | Message sending fails as the recipient's mobile number is ported to another carrier. |
| -1021        | CMCC | The message is blocked by the carrier as it hits a keyword.          |
| -1017     | CMCC | The recipient's mobile number does not exist.       |
| -1016        | CMCC | The message is blocked by the carrier's gateway. |
| -1012 | CMCC | The recipient is on the carrier's blocklist. |
| -1005        | CMCC | The recipient is on the carrier's blocklist.   |
| -1000   | CMCC | The carrier's gateway is exceptional. |
| -127 | CMCC | The sent message contains garbled characters. |
| -108                 | CMCC | The recipient's mobile number does not exist.  |
| -104 | CMCC | The recipient is on the carrier's blocklist. |
| -100 | CMCC | The recipient's mobile number is out of area. |
| -96                  | CMCC | The message is blocked by the carrier as it hits a keyword.    |
| -94                  | CMCC | The carrier's frequency limit is reached.   |
| -14 | CMCC | The recipient is on the carrier's blocklist. |
| -13 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.  |
| 001          | CMCC | The recipient's phone has a reception exception.   |
| 00202                | CMCC | The recipient's mobile number does not exist.   |
| 03           | CMCC | The message is blocked by the carrier's gateway. |
| 7 | CMCC | The CMCC gateway is exceptional internally. |
| 76 | CMCC | The message is blocked as it hits a keyword. |
| 115 | CMCC | The message is blocked as it hits a keyword. |
| 144 | CMCC | The recipient is on the blocklist.  |
| 145                  | CMCC | The carrier's frequency limit is reached. |
| 188          | CMCC | The carrier's gateway is exceptional.           |
| 904                  | CMCC | The recipient's mobile number is out of service.   |
| 1077 | CMCC | The recipient is on the blocklist.  |
| 1243 | CMCC | The recipient's mobile number is exceptional as it is ported to another carrier. |
| 431025               | CMCC | The carrier's frequency limit is reached.   |
| 431037               | CMCC | Message sending fails as the recipient's mobile number is ported to another carrier. |
| 431082               | CMCC | The recipient is on the carrier's blocklist.  |
| 9992 | CMCC | The recipient's phone has a storage exception. The recipient is recommended to clear the inbox. |
| 9994 | CMCC | The recipient's phone has a reception exception. |
| 9997 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.  |
| 9998 | CMCC | The recipient's mobile number does not exist.  |
| 9999 | CMCC | Message sending fails as the recipient's mobile number is ported to another carrier. |
| ADTFAIL      | CMCC | The message is blocked by the carrier as it hits a keyword.          |
| AICHECK      | CMCC | The message is blocked by the carrier as it hits a keyword.          |
| AUDIT:F      | CMCC | The message is blocked by the carrier's gateway. |
| BADSIGN              | CMCC | The recipient's mobile number does not exist.                                    |
| BEYONDN | CMCC | An internal carrier error occurs. |
| BD:0000              | CMCC | The recipient's mobile number is ported to another carrier.                               |
| BD:0001      | CMCC | The frequency limit is reached.                 |
| BD:0002      | CMCC | The carrier's gateway is exceptional. |
| BD:0003 | CMCC | The message hits a carrier keyword. |
| BLACK0       | CMCC | The recipient's phone is powered off.                     |
| BLKLIST      | CMCC | The recipient is on the carrier's blocklist.   |
| BST--1       | CMCC | The recipient is on the carrier's blocklist.   |
| BST-204      | CMCC | The recipient is on the carrier's blocklist.   |
| BWLIST | CMCC | The recipient is on the gateway's blocklist. |
| C100100 | CMCC | The message hits a keyword. |
| C100106 | CMCC | The sending limit is exceeded. |
| CA:0051      | CMCC | The carrier's gateway is exceptional.           |
| CA:0052      | CMCC | The carrier's gateway is exceptional.           |
| CA:0054 | CMCC | An internal CMCC error occurs. |
| CA:0111      | CMCC | The carrier's gateway is exceptional.           |
| CA:8008      | CMCC | The message is blocked by the carrier's gateway. |
| CA:8027              | CMCC | The recipient is on the carrier's blocklist.                           |
| CA:9005      | CMCC | The message is blocked by the carrier's gateway. |
| CA:9023              | CMCC | The recipient is on the carrier's blocklist.                           |
| CB:0001      | CMCC | The recipient's mobile number does not exist or is out of service.           |
| CB:0002      | CMCC | The carrier's gateway is exceptional.           |
| CB:0005      | CMCC | The carrier's gateway is exceptional.           |
| CB:0007      | CMCC | The carrier's gateway is exceptional.           |
| CB:0010 | CMCC | The sending limit is exceeded. |
| CB:0013 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.  |
| CB:0015 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.  |
| CB:0016      | CMCC | The carrier's gateway is exceptional.           |
| CB:0018      | CMCC | The carrier's gateway is exceptional.           |
| CB:0022      | CMCC | The carrier's gateway is exceptional.           |
| CB:0047      | CMCC | The recipient's mobile number does not exist or is out of service.           |
| CB:0053      | CMCC | The recipient's mobile number does not exist or is out of service.           |
| CB:0054      | CMCC | The carrier's gateway is exceptional.           |
| CE:0211      | CMCC | The message is blocked by the carrier's gateway. |
| CE:0301      | CMCC | The recipient's phone has a storage exception.   |
| CE:0501      | CMCC | The message is blocked by the carrier's gateway. |
| CHECK        | CMCC | The message is blocked by the carrier as it hits a keyword.          |
| CL:105       | CMCC | The message is blocked by the carrier's gateway. |
| CL:116               | CMCC | The message is blocked by the carrier as it hits a keyword.                        |
| CJ:007       | CMCC | The frequency limit is reached.                 |
| CJ:0006      | CMCC | The frequency limit is reached.                 |
| CJ:0007      | CMCC | The message is blocked by the carrier as it hits a keyword.          |
| CJ:0008      | CMCC | The message is blocked by the carrier as it hits a keyword.          |
| CM:8003              | CMCC | The message is blocked by the carrier as it hits a keyword.                        |
| CMPP20ERR:   | CMCC | The carrier's gateway is exceptional.           |
| CMPP30ERR:   | CMCC | The recipient's mobile number does not exist or is out of service.           |
| CONTENT              | CMCC | The message is blocked by the carrier as it hits a keyword.                        |
| DA:0051      | CMCC | The carrier's gateway is exceptional.           |
| DA:0052      | CMCC | The carrier's gateway is exceptional.           |
| DA:0053 | CMCC | The CMCC gateway is exceptional internally. |
| DA:0054 | CMCC | Response times out. |
| DA:0084      | CMCC | The carrier's gateway is exceptional.           |
| DB:0000      | CMCC | The carrier's gateway is exceptional.           |
| DB:0001 | CMCC | The recipient's phone is exceptional. |
| DB:0002      | CMCC | The carrier's gateway is exceptional.           |
| DB:0003      | CMCC | The carrier's gateway is exceptional.           |
| DB:0004      | CMCC | The carrier's gateway is exceptional.           |
| DB:0006 | CMCC | The CMCC gateway is exceptional internally. |
| DB:0007 | CMCC | The CMCC gateway is exceptional internally. |
| DB:0008      | CMCC | The carrier's gateway is exceptional.           |
| DB:0009 | CMCC | The CMCC gateway is exceptional internally. |
| DB:0010 | CMCC | An internal carrier error occurs. |
| DB:0100 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.  |
| DB:0101 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.  |
| DB:0102 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.  |
| DB:0103 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.  |
| DB:0104      | CMCC | The recipient is on the carrier's blocklist.             |
| DB:0105      | CMCC | The carrier's gateway is exceptional.           |
| DB:0106 | CMCC | The service code is incorrect. |
| DB:0107 | CMCC | An internal carrier error occurs. |
| DB:0109      | CMCC | The carrier's gateway is exceptional.           |
| DB:0110      | CMCC | The carrier's gateway is exceptional.           |
| DB:0111      | CMCC | The recipient's mobile number does not exist or is out of service.           |
| DB:0112      | CMCC | The carrier's gateway is exceptional.           |
| DB:0113      | CMCC | The carrier's gateway is exceptional.           |
| DB:0114      | CMCC | The carrier's gateway is exceptional.           |
| DB:0115      | CMCC | The recipient's mobile number is suspended.                  |
| DB:0116      | CMCC | The recipient's mobile number is suspended.                  |
| DB:0117      | CMCC | The recipient's mobile number is suspended.                  |
| DB:0118      | CMCC | The recipient's mobile number is suspended.                  |
| DB:0119      | CMCC | The recipient's mobile number is suspended.                  |
| DB:0120      | CMCC | The carrier's gateway is exceptional.           |
| DB:0121      | CMCC | The carrier's gateway is exceptional.           |
| DB:0122      | CMCC | The carrier's gateway is exceptional.           |
| DB:0123      | CMCC | The carrier's gateway is exceptional.           |
| DB:0124      | CMCC | The carrier's gateway is exceptional.           |
| DB:0125      | CMCC | The carrier's gateway is exceptional.           |
| DB:0126 | CMCC | The recipient's mobile number is exceptional as it is ported to another carrier. |
| DB:0127      | CMCC | The recipient's mobile number is out of service.                     |
| DB:0128      | CMCC | The recipient's mobile number is out of service.                     |
| DB:0129 | CMCC | The recipient's mobile number is exceptional as it is ported to another carrier. |
| DB:0130      | CMCC | The recipient's mobile number does not exist or is out of service.           |
| DB:0131      | CMCC | The recipient's mobile number does not exist or is out of service.           |
| DB:0132      | CMCC | The recipient's mobile number does not exist or is out of service.           |
| DB:0133      | CMCC | The recipient's mobile number does not exist or is out of service.           |
| DB:0134      | CMCC | The recipient's mobile number does not exist or is out of service.           |
| DB:0135      | CMCC | The recipient's mobile number does not exist or is out of service.           |
| DB:0136      | CMCC | The carrier's gateway is exceptional.           |
| DB:0137      | CMCC | The carrier's gateway is exceptional.           |
| DB:0138      | CMCC | The recipient's mobile number does not exist or is out of service.           |
| DB:0139 | CMCC | The sending time period is non-compliant. |
| DB:0140      | CMCC | The recipient is on the carrier's blocklist.             |
| DB:0140 | CMCC | The CMCC gateway is exceptional internally. |
| DB:0141 | CMCC | The recipient is on the blocklist of China Mobile or MIIT due to repeated complaints. |
| DB:0142 | CMCC | The daily maximum number of sent MTs is exceeded. |
| DB:0143 | CMCC | The daily maximum number of sent MTs is exceeded. |
| DB:0144 | CMCC | The recipient is on the global blocklist. |
| DB:00144     | CMCC | The recipient is on the carrier's blocklist.             |
| DB:0145 | CMCC | The recipient is on the blocklist.  |
| DB:0146 | CMCC | The recipient is on the blocklist.  |
| DB:0147      | CMCC | The recipient's mobile number does not exist or is out of service.           |
| DB:0150      | CMCC | The carrier's gateway is exceptional.           |
| DB:0151      | CMCC | The carrier's gateway is exceptional.           |
| DB:0152 | CMCC | The CMCC gateway is exceptional internally. |
| DB:0153      | CMCC | The carrier's gateway is exceptional.           |
| DB:0154      | CMCC | The carrier's gateway is exceptional.           |
| DB:0155      | CMCC | The carrier's gateway is exceptional.           |
| DB:0156      | CMCC | The carrier's gateway is exceptional.           |
| DB:0164 | CMCC | The recipient is on the carrier's blocklist. |
| DB:0171      | CMCC | The carrier's gateway is exceptional.           |
| DB:0182      | CMCC | The recipient's mobile number is suspended.                  |
| DB:0309      | CMCC | The message is blocked by the carrier as it hits a keyword.          |
| DB:0318      | CMCC | The recipient's mobile number does not exist.                      |
| DB:0500      | CMCC | The carrier's gateway is exceptional.           |
| DB:0501 | CMCC | The CMCC gateway is exceptional internally. |
| DB:0502 | CMCC | The CMCC gateway is exceptional internally. |
| DB:0503      | CMCC | The carrier's gateway is exceptional.           |
| DB:0504 | CMCC | The CMCC gateway is exceptional internally. |
| DB:0505 | CMCC | An internal carrier error occurs. |
| DB:0506      | CMCC | The carrier's gateway is exceptional.           |
| DB:1150      | CMCC | The carrier's gateway is exceptional.           |
| DB:9001      | CMCC | The carrier's gateway is exceptional.           |
| DB:9006      | CMCC | The recipient is on the carrier's blocklist.             |
| DB:9005              | CMCC | The carrier's gateway is exceptional.                         |
| DB:9007      | CMCC | The frequency limit is reached.                 |
| DB:BACK              | CMCC | The recipient is on the carrier's blocklist.                           |
| DB:BLACK     | CMCC | The recipient is on the carrier's blocklist.             |
| DB00143              | CMCC | The carrier's frequency limit is reached.                         |
| DB00144 | CMCC | The recipient's mobile number is blocked by the global blocklist. |
| DBBLACK      | CMCC | The recipient is on the carrier's blocklist.             |
| DG:0001              | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off. |
| DG:0141              | CMCC | The recipient is on the carrier's blocklist.                           |
| DG:0142              | CMCC | The carrier's frequency limit is reached.                         |
| DI:0008      | CMCC | The frequency limit is reached.                 |
| DI:0029      | CMCC | The frequency limit is reached.                 |
| DI:0145      | CMCC | The frequency limit is reached.                 |
| DI:9402      | CMCC | The recipient is on the carrier's blocklist.             |
| DI:9403      | CMCC | The recipient is on the carrier's blocklist.             |
| DI:9413      | CMCC | The frequency limit is reached.                 |
| DI:9414      | CMCC | The carrier's gateway is exceptional.           |
| DI:9415      | CMCC | The message is blocked by the carrier as it hits a keyword.          |
| DI:9416      | CMCC | The message is blocked by the carrier as it hits a keyword.          |
| DI:9422      | CMCC | The message is blocked by the carrier as it hits a keyword.          |
| DI:9423      | CMCC | The message is blocked by the carrier as it hits a keyword.          |
| DI:9427      | CMCC | The message is blocked by the carrier as it hits a keyword.          |
| DI:9428      | CMCC | The message is blocked by the carrier as it hits a keyword.          |
| DI:9429      | CMCC | The message is blocked by the carrier as it hits a keyword.          |
| DI:9430      | CMCC | The carrier's gateway is exceptional.           |
| DI:9431      | CMCC | The message is blocked by the carrier as it hits a keyword.          |
| DI:9432      | CMCC | The frequency limit is reached.                 |
| DI:9433      | CMCC | The frequency limit is reached.                 |
| DI:9434      | CMCC | The frequency limit is reached.                 |
| DI:9501      | CMCC | The recipient's mobile number does not exist.                      |
| DI:9909      | CMCC | The frequency limit is reached.                 |
| E200020              | CMCC | The message is blocked by the carrier as it hits a keyword (an unsubscription method must be added in marketing SMS messages). |
| E200038              | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off. |
| E:BLACK | CMCC | The recipient is on the carrier's blocklist. |
| E:CF                 | CMCC | The carrier's frequency limit is reached.                         |
| E:CHAN | CMCC | The recipient's mobile number is exceptional as it is ported to another carrier. |
| E:OCDDL      | CMCC | The frequency limit is reached.       |
| E:OCDWL      | CMCC | The frequency limit is reached.       |
| E:ODDL       | CMCC | The frequency limit is reached.                 |
| E:ODML | CMCC | The CMCC gateway is exceptional internally. |
| E:RPTSD      | CMCC | The frequency limit is reached.                 |
| ERR:13               | CMCC | The recipient's phone has a reception exception.                           |
| ERR-204      | CMCC | The recipient is on the carrier's blocklist.   |
| ERR_NUM | CMCC | The recipient's mobile number is incorrect or restricted. |
| ERR_NUM_00   | CMCC | The recipient's mobile number does not exist.                      |
| ERR_NUM_006 | CMCC | The recipient's mobile number is incorrect or restricted. |
| ERRTIME      | CMCC | The frequency limit is reached.                 |
| ETOS:402     | CMCC | The recipient is on the carrier's blocklist.             |
| EXPIRED | CMCC | The message has expired. |
| EWTD                 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off. |
| F123                 | CMCC | The recipient is on the carrier's blocklist.                           |
| F1110 | CMCC | The recipient's mobile number range does not exist. |
| F1122                | CMCC | The recipient is on the carrier's blocklist.                           |
| F1123                | CMCC | The recipient is on the carrier's blocklist.                           |
| F11300               | CMCC | The carrier's frequency limit is reached.                         |
| F100007              | CMCC | The message is blocked by the carrier as it hits a keyword.                        |
| F1214B1              | CMCC | The message is blocked by the carrier as it hits a keyword.                        |
| F1214HN              | CMCC | The message is blocked by the carrier as it hits a keyword.                        |
| F1214JR | CMCC | The message hits a carrier keyword. |
| F132200 | CMCC | The recipient's mobile number does not exist.  |
| FAILD        | CMCC | The carrier's gateway is exceptional.           |
| FAIL_RE      | CMCC | The message is blocked by the carrier's gateway. |
| GB:0003      | CMCC | The frequency limit is reached.       |
| GB:0004      | CMCC | The signature is non-compliant.       |
| GB:0007 | CMCC | The carrier's gateway is exceptional. |
| GB:0008      | CMCC | The recipient is on the carrier's blocklist.   |
| GB:0010 | CMCC | The recipient's mobile number is out of service. |
| GB:0011 | CMCC | The recipient is on the carrier's blocklist. |
| GB:0012      | CMCC | The message is blocked by the carrier as it hits a keyword.          |
| GB:0013      | CMCC | The message is blocked by the carrier's gateway. |
| GB:0016              | CMCC | The message is blocked by the carrier as it hits a keyword (an unsubscription method must be added in marketing SMS messages). |
| GB:0024              | CMCC | The message is blocked by the carrier as it hits a keyword.                        |
| GB:0025              | CMCC | The carrier's gateway is exceptional.                         |
| GB:0026              | CMCC | The carrier's gateway is exceptional.                         |
| GB:0028              | CMCC | The recipient is on the carrier's blocklist.                           |
| GG:1000      | CMCC | The carrier's gateway is exceptional.           |
| GL:0000              | CMCC | The carrier's gateway is exceptional.                         |
| HAVBEEN      | CMCC | The recipient is on the carrier's blocklist.             |
| HD:0001      | CMCC | The recipient is on the carrier's blocklist.             |
| HD:19 | CMCC | The recipient is on the gateway's blocklist. |
| HD:29        | CMCC | The frequency limit is reached.                 |
| HIGRISK | CMCC | The recipient is on the carrier's blocklist. |
| HTTPERROR    | CMCC | The carrier's gateway is exceptional.           |
| HTTPEXCEPT   | CMCC | The carrier's gateway is exceptional.           |
| IA00054              | CMCC | The carrier's gateway is exceptional.                         |
| IA:0051 | CMCC | An internal carrier error occurs. |
| IA:0052      | CMCC | The carrier's gateway is exceptional.           |
| IA:0053 | CMCC | The CMCC gateway is exceptional internally. |
| IA:0054 | CMCC | Response times out. |
| IA:0057      | CMCC | The carrier's gateway is exceptional.           |
| IA:0073 | CMCC | An internal carrier error occurs. |
| IB:0001      | CMCC | The carrier's gateway is exceptional.           |
| IB:0002      | CMCC | The carrier's gateway is exceptional.           |
| IB:0003      | CMCC | The carrier's gateway is exceptional.           |
| IB:0004      | CMCC | The carrier's gateway is exceptional.           |
| IB:0005      | CMCC | The carrier's gateway is exceptional.           |
| IB:0006      | CMCC | The carrier's gateway is exceptional.           |
| IB:0007      | CMCC | The carrier's gateway is exceptional.           |
| IB:0008 | CMCC | An internal carrier error occurs. |
| IB:0009 | CMCC | An internal carrier error occurs. |
| IB:0010      | CMCC | The carrier's gateway is exceptional.           |
| IB:0011 | CMCC | The message hits a carrier keyword. |
| IB:0012 | CMCC | Message sending fails as the recipient's mobile number is ported to another carrier. |
| IB:0013 | CMCC | An internal carrier error occurs. |
| IB:0064 | CMCC | The recipient's phone is powered off. |
| IB:0070      | CMCC | The carrier's gateway is exceptional.           |
| IB:0079      | CMCC | The carrier's gateway is exceptional.           |
| IB:0100      | CMCC | The carrier's gateway is exceptional.           |
| IB:0113      | CMCC | The carrier's gateway is exceptional.           |
| IB:0168 | CMCC | Message sending fails as the recipient's mobile number is ported to another carrier. |
| IB:0169 | CMCC | The CMCC gateway is exceptional internally. |
| IB:0194 | CMCC | The recipient's phone is powered off. |
| IB:0225      | CMCC | The carrier's gateway is exceptional.           |
| IB:0255 | CMCC | An internal carrier error occurs. |
| IB-0013              | CMCC | The recipient's phone has a reception exception.                           |
| IB-0099              | CMCC | The recipient's phone has a reception exception.                           |
| IC:0001 | CMCC | The recipient's mobile number is out of service, or the recipient's phone is powered off. |
| IC:0015 | CMCC | An internal carrier error occurs. |
| IC:0055 | CMCC | An internal carrier error occurs. |
| IC:0062 | CMCC | The recipient's phone is exceptional. |
| IC:0151 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.  |
| IC:0154      | CMCC | The carrier's gateway is exceptional.           |
| ID:0000 | CMCC | The CMCC gateway is exceptional internally. |
| ID:0001 | CMCC | The CMCC gateway is exceptional internally. |
| ID:0002      | CMCC | The carrier's gateway is exceptional.           |
| ID:0003      | CMCC | The carrier's gateway is exceptional.           |
| ID:0004 | CMCC | The CMCC gateway is exceptional internally. |
| ID:0005      | CMCC | The carrier's gateway is exceptional.           |
| ID:0006 | CMCC | The CMCC gateway is exceptional internally. |
| ID:0007      | CMCC | The carrier's gateway is exceptional.           |
| ID:0008 | CMCC | The CMCC gateway is exceptional internally. |
| ID:0009      | CMCC | The carrier's gateway is exceptional.           |
| ID:0010      | CMCC | The carrier's gateway is exceptional.           |
| ID:0011      | CMCC | The carrier's gateway is exceptional.           |
| ID:0012 | CMCC | The billable address is incorrect. |
| ID:0013 | CMCC | An internal carrier error occurs. |
| ID:0014      | CMCC | The carrier's gateway is exceptional.           |
| ID:0020 | CMCC | The CMCC gateway is exceptional internally. |
| ID:0021 | CMCC | The CMCC gateway is exceptional internally. |
| ID:0043 | CMCC | The recipient's mobile number is exceptional as it is ported to another carrier. |
| ID:0044      | CMCC | The carrier's gateway is exceptional.           |
| ID:0045 | CMCC | The CMCC gateway is exceptional internally. |
| ID:0046 | CMCC | The CMCC gateway is exceptional internally. |
| ID:0047 | CMCC | The CMCC gateway is exceptional internally. |
| ID:0048 | CMCC | The CMCC gateway is exceptional internally. |
| ID:0049 | CMCC | The CMCC gateway is exceptional internally. |
| ID:0051      | CMCC | The carrier's gateway is exceptional.           |
| ID:0052      | CMCC | The carrier's gateway is exceptional.           |
| ID:0053      | CMCC | The carrier's gateway is exceptional.           |
| ID:0054 | CMCC | The recipient's phone has a reception exception. |
| ID:0055 | CMCC | The recipient's phone has a reception exception. |
| ID:0056 | CMCC | The recipient's phone has a reception exception. |
| ID:0061      | CMCC | The carrier's gateway is exceptional.           |
| ID:0062      | CMCC | The carrier's gateway is exceptional.           |
| ID:0063      | CMCC | The carrier's gateway is exceptional.           |
| ID:0064 | CMCC | The CMCC gateway is exceptional internally. |
| ID:0065 | CMCC | The CMCC gateway is exceptional internally. |
| ID:0066 | CMCC | The CMCC gateway is exceptional internally. |
| ID:0067 | CMCC | The CMCC gateway is exceptional internally. |
| ID:0068 | CMCC | The recipient's phone has a reception exception. |
| ID:0069 | CMCC | The recipient is on the blocklist.  |
| ID:0070 | CMCC | An internal carrier error occurs. |
| ID:0071      | CMCC | The carrier's gateway is exceptional.           |
| ID:0072      | CMCC | The carrier's gateway is exceptional.           |
| ID:0073 | CMCC | The recipient's phone has a reception exception. |
| ID:0074 | CMCC | The CMCC gateway is exceptional internally. |
| ID:0075 | CMCC | The CMCC gateway is exceptional internally. |
| ID:0076 | CMCC | The message is blocked as it hits a keyword. |
| ID:0077      | CMCC | The carrier's gateway is exceptional.           |
| ID:0078      | CMCC | The carrier's gateway is exceptional.           |
| ID:0079      | CMCC | The carrier's gateway is exceptional.           |
| ID:0080      | CMCC | The carrier's gateway is exceptional.           |
| ID:0081      | CMCC | The carrier's gateway is exceptional.           |
| ID:0082      | CMCC | The carrier's gateway is exceptional.           |
| ID:0083      | CMCC | The carrier's gateway is exceptional.           |
| ID:0084 | CMCC | The CMCC gateway is exceptional internally. |
| ID:0085 | CMCC | The CMCC gateway is exceptional internally. |
| ID:0086 | CMCC | The CMCC gateway is exceptional internally. |
| ID:0087 | CMCC | The CMCC gateway is exceptional internally. |
| ID:0077      | CMCC | The carrier's gateway is exceptional.           |
| ID:0078      | CMCC | The carrier's gateway is exceptional.           |
| ID:0079      | CMCC | The carrier's gateway is exceptional.           |
| ID:0080      | CMCC | The carrier's gateway is exceptional.           |
| ID:0081      | CMCC | The carrier's gateway is exceptional.           |
| ID:0082      | CMCC | The carrier's gateway is exceptional.           |
| ID:0088 | CMCC | The CMCC gateway is exceptional internally. |
| ID:0089 | CMCC | The CMCC gateway is exceptional internally. |
| ID:0096 | CMCC | The recipient is on the blocklist.  |
| ID:0097 | CMCC | The recipient is on the blocklist.  |
| ID:0100 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.  |
| ID:0101 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.  |
| ID:0102 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.  |
| ID:0103 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.  |
| ID:0104 | CMCC | The recipient's mobile number does not exist.  |
| ID:0105      | CMCC | The carrier's gateway is exceptional.           |
| ID:0106      | CMCC | The carrier's gateway is exceptional.           |
| ID:0107      | CMCC | The carrier's gateway is exceptional.           |
| ID:0108      | CMCC | The recipient's mobile number is suspended.                  |
| ID:0109      | CMCC | The carrier's gateway is exceptional.           |
| ID:0110      | CMCC | The carrier's gateway is exceptional.           |
| ID:0111      | CMCC | The carrier's gateway is exceptional.           |
| ID:0112      | CMCC | The carrier's gateway is exceptional.           |
| ID:0113      | CMCC | The carrier's gateway is exceptional.           |
| ID:0114      | CMCC | The carrier's gateway is exceptional.           |
| ID:0115      | CMCC | The recipient's mobile number is suspended.                  |
| ID:0116      | CMCC | The recipient's mobile number is suspended.                  |
| ID:0117      | CMCC | The recipient's mobile number is suspended.                  |
| ID:0118      | CMCC | The recipient's mobile number is suspended.                  |
| ID:0119      | CMCC | The recipient's mobile number is suspended.                  |
| ID:0120      | CMCC | The recipient's mobile number is suspended.                  |
| ID:0121      | CMCC | The recipient's mobile number is suspended.                  |
| ID:0122      | CMCC | The carrier's gateway is exceptional.           |
| ID:0123      | CMCC | The carrier's gateway is exceptional.           |
| ID:0124      | CMCC | The carrier's gateway is exceptional.           |
| ID:0125      | CMCC | The carrier's gateway is exceptional.           |
| ID:0126 | CMCC | The recipient's mobile number is exceptional as it is ported to another carrier. |
| ID:0127      | CMCC | The recipient's mobile number is out of service.                     |
| ID:0128      | CMCC | The recipient's mobile number is out of service.                     |
| ID:0129 | CMCC | The recipient's mobile number is exceptional as it is ported to another carrier. |
| ID:0131      | CMCC | The recipient's mobile number is out of service.                     |
| ID:0132      | CMCC | The recipient's mobile number does not exist.                      |
| ID:0133      | CMCC | The recipient's mobile number does not exist.                      |
| ID:0134      | CMCC | The recipient's mobile number does not exist.                      |
| ID:0135      | CMCC | The recipient's mobile number does not exist.                      |
| ID:0136      | CMCC | The carrier's gateway is exceptional.           |
| ID:0137      | CMCC | The carrier's gateway is exceptional.           |
| ID:0138      | CMCC | The carrier's gateway is exceptional.           |
| ID:0139      | CMCC | The carrier's gateway is exceptional.           |
| ID:0140      | CMCC | The recipient is on the carrier's blocklist.             |
| ID:0141 | CMCC | The recipient is on the blocklist.  |
| ID:0142 | CMCC | The sending limit is exceeded. |
| ID:0143 | CMCC | The sending limit is exceeded. |
| ID:0199 | CMCC | The recipient is on the blocklist.  |
| ID:0310      | CMCC | The carrier's gateway is exceptional.           |
| ID:0311 | CMCC | The sending limit is exceeded. |
| ID:0312      | CMCC | The carrier's gateway is exceptional.           |
| ID:0313      | CMCC | The carrier's gateway is exceptional.           |
| ID:0314      | CMCC | The carrier's gateway is exceptional.           |
| ID:0315      | CMCC | The carrier's gateway is exceptional.           |
| ID:0317      | CMCC | The carrier's gateway is exceptional.           |
| ID:0318 | CMCC | The message is blocked as it hits a keyword. |
| ID:1240      | CMCC | The carrier's gateway is exceptional.           |
| ID:1241      | CMCC | The carrier's gateway is exceptional.           |
| ID:1242 | CMCC | The carrier's gateway is exceptional. |
| ID:1243      | CMCC | The carrier's gateway is exceptional.           |
| ID:1244 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.  |
| ID:1245 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.  |
| ID:1246 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.  |
| ID:1247 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.  |
| ID:1248      | CMCC | The carrier's gateway is exceptional.           |
| ID:1249      | CMCC | The carrier's gateway is exceptional.           |
| ID:1250      | CMCC | The carrier's gateway is exceptional.           |
| ID:1251      | CMCC | The carrier's gateway is exceptional.           |
| ID:6150      | CMCC | The carrier's gateway is exceptional.           |
| ID:6151 | CMCC | The recipient's phone has a reception exception. |
| ID:6152 | CMCC | The recipient's phone has a reception exception. |
| ID:6153 | CMCC | The recipient's phone has a reception exception. |
| INCOMPL              | CMCC | The carrier's gateway is exceptional.                         |
| INVALID              | CMCC | The message is blocked by the carrier as it hits a keyword (an unsubscription method must be added in marketing SMS messages). |
| JL:0013      | CMCC | The recipient is on the carrier's blocklist.   |
| JL:0014 | CMCC | The message hits a carrier keyword. |
| JL:0017 | CMCC | The recipient's mobile number does not exist or is out of service. |
| JL:0026 | CMCC | The recipient is on the carrier's blocklist. |
| JL:0028 | CMCC | The recipient is on the carrier's blocklist. |
| KEY:FIL              | CMCC | The message is blocked by the carrier as it hits a keyword.                        |
| KEYWORD      | CMCC | The message is blocked by the carrier's gateway. |
| LIMIT        | CMCC | The frequency limit is reached.       |
| LK:9414              | CMCC | The message is blocked by the carrier as it hits a keyword.                        |
| LT:0036              | CMCC | Message sending fails as the recipient's mobile number is ported to another carrier. |
| LU:0002      | CMCC | The recipient's phone has a reception exception.             |
| LU:0003      | CMCC | The recipient is on the carrier's blocklist.             |
| M2:0043      | CMCC | The frequency limit is reached.       |
| M2:0045      | CMCC | The recipient is on the carrier's blocklist.   |
| MA:0001 | CMCC | An internal carrier error occurs. |
| MA:0002      | CMCC | The carrier's gateway is exceptional.           |
| MA:0003      | CMCC | The carrier's gateway is exceptional.           |
| MA:0004      | CMCC | The carrier's gateway is exceptional.           |
| MA:0005      | CMCC | The carrier's gateway is exceptional.           |
| MA:0006 | CMCC | The message hits a carrier keyword. |
| MA:0009      | CMCC | The carrier's gateway is exceptional.           |
| MA:0010      | CMCC | The carrier's gateway is exceptional.           |
| MA:0011      | CMCC | The carrier's gateway is exceptional.           |
| MA:0012      | CMCC | The carrier's gateway is exceptional.           |
| MA:0013      | CMCC | The carrier's gateway is exceptional.           |
| MA:0014      | CMCC | The carrier's gateway is exceptional.           |
| MA:0021      | CMCC | The recipient's mobile number does not exist.                      |
| MA:0022 | CMCC | An internal carrier error occurs. |
| MA:0023      | CMCC | The recipient is on the carrier's blocklist.             |
| MA:0026              | CMCC | The message is blocked by the carrier as it hits a keyword.                        |
| MA:0036      | CMCC | The message is blocked by the carrier's gateway. |
| MA:0039              | CMCC | The message is blocked by the carrier as it hits a keyword.                        |
| MA:0051 | CMCC | An internal carrier error occurs. |
| MA:0052      | CMCC | The carrier's gateway is exceptional.           |
| MA:0053 | CMCC | The recipient's phone has a reception exception. |
| MA:0054 | CMCC | An internal carrier error occurs. |
| MA:0054? | CMCC | The CMCC gateway is exceptional internally. |
| MA:0072      | CMCC | The carrier's gateway is exceptional.           |
| MA:0073 | CMCC | - |
| MA:0191      | CMCC | The carrier's gateway is exceptional.           |
| MA:0194      | CMCC | The carrier's gateway is exceptional.           |
| MB:0000 | CMCC | The recipient's phone has a reception exception. |
| MB:0001 | CMCC | The CMCC gateway is exceptional internally. |
| MB:0002      | CMCC | The carrier's gateway is exceptional.           |
| MB:0003      | CMCC | The carrier's gateway is exceptional.           |
| MB:0004      | CMCC | The carrier's gateway is exceptional.           |
| MB:0005      | CMCC | The carrier's gateway is exceptional.           |
| MB:0006      | CMCC | The carrier's gateway is exceptional.           |
| MB:0007 | CMCC | The CMCC gateway is exceptional internally. |
| MB:0008 | CMCC | The CMCC gateway is exceptional internally. |
| MB:0010      | CMCC | The carrier's gateway is exceptional.           |
| MB:0011      | CMCC | The carrier's gateway is exceptional.           |
| MB:0012      | CMCC | The carrier's gateway is exceptional.           |
| MB:0013      | CMCC | The carrier's gateway is exceptional.           |
| MB:0014      | CMCC | The carrier's gateway is exceptional.           |
| MB:0015      | CMCC | The carrier's gateway is exceptional.           |
| MB:0017      | CMCC | The carrier's gateway is exceptional.           |
| MB:0018      | CMCC | The carrier's gateway is exceptional.           |
| MB:0019 | CMCC | The recipient's phone has a reception exception. |
| MB:0020      | CMCC | The carrier's gateway is exceptional.           |
| MB:0022 | CMCC | The recipient is on the blocklist.  |
| MB:0027              | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off. |
| MB:0031              | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off. |
| MB:0032              | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off. |
| MB:0034              | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off. |
| MB:0051      | CMCC | The carrier's gateway is exceptional.           |
| MB:0052      | CMCC | The carrier's gateway is exceptional.           |
| MB:0069 | CMCC | The recipient's phone is powered off. |
| MB:0064      | CMCC | The carrier's gateway is exceptional.           |
| MB:0065      | CMCC | The carrier's gateway is exceptional.           |
| MB:0066      | CMCC | The carrier's gateway is exceptional.           |
| MB:0067      | CMCC | The carrier's gateway is exceptional.           |
| MB:0068      | CMCC | The carrier's gateway is exceptional.           |
| MB:0070      | CMCC | The carrier's gateway is exceptional.           |
| MB:0072      | CMCC | The carrier's gateway is exceptional.           |
| MB:0073      | CMCC | The carrier's gateway is exceptional.           |
| MB:0077      | CMCC | The carrier's gateway is exceptional.           |
| MB:0080      | CMCC | The carrier's gateway is exceptional.           |
| MB:0081      | CMCC | The carrier's gateway is exceptional.           |
| MB:0083      | CMCC | The carrier's gateway is exceptional.           |
| MB:0084      | CMCC | The carrier's gateway is exceptional.           |
| MB:0085      | CMCC | The carrier's gateway is exceptional.           |
| MB:0088 | CMCC | An internal carrier error occurs. |
| MB:0097      | CMCC | The carrier's gateway is exceptional.           |
| MB:0098      | CMCC | The carrier's gateway is exceptional.           |
| MB:0099      | CMCC | The carrier's gateway is exceptional.           |
| MB:0100      | CMCC | The carrier's gateway is exceptional.           |
| MB:0101      | CMCC | The carrier's gateway is exceptional.           |
| MB:0102      | CMCC | The carrier's gateway is exceptional.           |
| MB:0103      | CMCC | The carrier's gateway is exceptional.           |
| MB:0145      | CMCC | The carrier's gateway is exceptional.           |
| MB:0147      | CMCC | The carrier's gateway is exceptional.           |
| MB:0192      | CMCC | The carrier's gateway is exceptional.           |
| MB:0193      | CMCC | The carrier's gateway is exceptional.           |
| MB:0194      | CMCC | The carrier's gateway is exceptional.           |
| MB:0195      | CMCC | The carrier's gateway is exceptional.           |
| MB:0196      | CMCC | The carrier's gateway is exceptional.           |
| MB:0241      | CMCC | The carrier's gateway is exceptional.           |
| MB:0244      | CMCC | The carrier's gateway is exceptional.           |
| MB:0250      | CMCC | The carrier's gateway is exceptional.           |
| MB:0254 | CMCC | The recipient's phone is exceptional. |
| MB:0255 | CMCC | The CMCC gateway is exceptional internally. |
| MB:1016      | CMCC | The carrier's gateway is exceptional.           |
| MB:1024      | CMCC | The carrier's gateway is exceptional.           |
| MB:1025 | CMCC | The CMCC gateway is exceptional internally. |
| MB:1026 | CMCC | SMC operating parameters (such as MO speed, MT speed, number of messages, and number of message entities) reach the maximum limit of the license. |
| MB:1031 | CMCC | The SMS center returns a "maximum number of sent messages exceeded" error. The reason may be that the storage of the recipient's phone is full. |
| MB:1034 | CMCC | The CMCC gateway is exceptional internally. |
| MB:1035      | CMCC | The carrier's gateway is exceptional.           |
| MB:1036      | CMCC | The recipient's phone has a reception exception.             |
| MB:1037      | CMCC | The carrier's gateway is exceptional.           |
| MB:1038      | CMCC | The recipient's mobile number is suspended.                 |
| MB:1039      | CMCC | The carrier's gateway is exceptional.           |
| MB:1040      | CMCC | The recipient's mobile number is out of service.                     |
| MB:1041 | CMCC | The sending limit is exceeded. |
| MB:1042 | CMCC | The number of messages cached in the SMC memory to be sent to the recipient exceeds the maximum number of messages deliverable to the recipient. |
| MB:1043 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.  |
| MB:1044      | CMCC | The carrier's gateway is exceptional.           |
| MB:1045      | CMCC | The carrier's gateway is exceptional.           |
| MB:1046      | CMCC | The carrier's gateway is exceptional.           |
| MB:1047      | CMCC | The carrier's gateway is exceptional.           |
| MB:1048      | CMCC | The carrier's gateway is exceptional.           |
| MB:1049      | CMCC | The carrier's gateway is exceptional.           |
| MB:1050      | CMCC | The carrier's gateway is exceptional.           |
| MB:1051 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.  |
| MB:1052      | CMCC | The carrier's gateway is exceptional.           |
| MB:1056      | CMCC | The carrier's gateway is exceptional.           |
| MB:1057      | CMCC | The carrier's gateway is exceptional.           |
| MB:1058      | CMCC | The carrier's gateway is exceptional.           |
| MB:1060      | CMCC | The carrier's gateway is exceptional.           |
| MB:1061      | CMCC | The carrier's gateway is exceptional.           |
| MB:1062      | CMCC | The carrier's gateway is exceptional.           |
| MB:1063      | CMCC | The carrier's gateway is exceptional.           |
| MB:1064      | CMCC | The carrier's gateway is exceptional.           |
| MB:1065      | CMCC | The carrier's gateway is exceptional.           |
| MB:1069 | CMCC | The CMCC gateway is exceptional internally. |
| MB:1070 | CMCC | The sending limit is exceeded. |
| MB:1072 | CMCC | The CMCC gateway is exceptional internally. |
| MB:1073 | CMCC | The CMCC gateway is exceptional internally. |
| MB:1074 | CMCC | The CMCC gateway is exceptional internally. |
| MB:1075 | CMCC | The CMCC gateway is exceptional internally. |
| MB:1076 | CMCC | The recipient is on the blocklist.  |
| MB:1077 | CMCC | The recipient has a record of malicious complaints against China Mobile and thus is on the blocklist. |
| MB:1078 | CMCC | An internal carrier error occurs. |
| MB:1079 | CMCC | The message is rejected due to fraud. |
| MB:1080 | CMCC | The CMCC gateway is exceptional internally. |
| MB:1081 | CMCC | The CMCC gateway is exceptional internally. |
| MB:1082 | CMCC | The CMCC gateway is exceptional internally. |
| MB:1083 | CMCC | The message is rejected due to fraud. |
| MB:1086 | CMCC | The CMCC gateway is exceptional internally. |
| MB:1279 | CMCC | The CMCC gateway is exceptional internally. |
| MB:8000              | CMCC | The carrier's gateway is exceptional.                         |
| MC:0001 | CMCC | An unknown error occurs. |
| MC:0055 | CMCC | Message sending fails as the recipient's mobile number is out of area or the storage of the recipient's phone is full. |
| MC:0055_000 | CMCC | Message sending fails as the recipient's mobile number is out of area or the storage of the recipient's phone is full. |
| MC:0055_006 | CMCC | Message sending fails as the recipient's mobile number is out of area or the storage of the recipient's phone is full. |
| MC:0062 | CMCC | The recipient's mobile number is out of service. |
| MC:0151 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.  |
| MC00151 | CMCC | An internal carrier error occurs. |
| MC_T:55      | CMCC | The carrier's gateway is exceptional. |
| ME:-7        | CMCC | The message is blocked by the carrier's gateway. |
| MH:0004              | CMCC | The recipient is on the carrier's blocklist.                           |
| MH:0007              | CMCC | The message is blocked by the carrier as it hits a keyword.                        |
| MH:0008      | CMCC | The message is blocked by the carrier as it hits a keyword.          |
| MH:18        | CMCC | The recipient's mobile number does not exist.            |
| MH:19 | CMCC | The recipient is on the blocklist.  |
| MH:20        | CMCC | The recipient's phone has a reception exception.   |
| MH:999               | CMCC | The message is blocked by the carrier as it hits a keyword.                        |
| MI:XXXX | CMCC | China Mobile error codes start with M, which are mostly caused by problems with the recipient's mobile phone/number; for example, the mobile number is out of service, out of area, or invalid, or the phone is powered off or has poor reception. |
| MI:0000 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.  |
| MI:0001 | CMCC | The recipient's phone is powered off. |
| MI:0002 | CMCC | An internal carrier error occurs. |
| MI:0004 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.  |
| MI:0005 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.  |
| MI:0008 | CMCC | An internal CMCC gateway error occurs. |
| MI:0009              | CMCC | The recipient's phone is powered off.                                   |
| MI:0010 | CMCC | The recipient's mobile number has expired. |
| MI:0011 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.  |
| MI:0012 | CMCC | The recipient's phone is invalid. |
| MI:0013 | CMCC | The recipient's mobile number is out of service, or the recipient's phone is powered off. |
| MI:0015 | CMCC | The recipient's mobile number is out of service, or the recipient's phone is powered off. |
| MI:0017 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.  |
| MI:0020 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.  |
| MI:0022 | CMCC | An internal CMCC gateway error occurs. |
| MI:0023 | CMCC | An internal carrier error occurs. |
| MI:0024 | CMCC | The recipient's mobile number is out of service, or the recipient's phone is powered off. |
| MI:0029 | CMCC | The recipient's mobile number is out of service, or the recipient's phone is powered off. |
| MI:0030 | CMCC | An internal carrier error occurs. |
| MI:0036 | CMCC | An internal CMCC gateway error occurs. |
| MI:0038 | CMCC | An internal carrier error occurs. |
| MI:0041 | CMCC | An internal carrier error occurs. |
| MI:0044 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.  |
| MI:0043              | CMCC | The recipient's phone is powered off.                                   |
| MI:0045 | CMCC | An internal CMCC gateway error occurs. |
| MI:0048 | CMCC | An internal carrier error occurs. |
| MI:0050 | CMCC | The recipient's mobile number is out of service, or the recipient's phone is powered off. |
| MI:0051 | CMCC | The CMCC gateway is exceptional internally. |
| MI:0052 | CMCC | Roaming is restricted. |
| MI:0053 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.  |
| MI:0054 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.  |
| MI:0055 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.  |
| MI:0056 | CMCC | Response times out. |
| MI:0057 | CMCC | An internal carrier error occurs. |
| MI:0059 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.  |
| MI:0063 | CMCC | An internal carrier error occurs. |
| MI:0064 | CMCC | An internal carrier error occurs. |
| MI:0075 | CMCC | The recipient's phone has a reception exception. |
| MI:0080 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.  |
| MI:0081 | CMCC | An internal carrier error occurs. |
| MI:0083 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.  |
| MI:0084 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.  |
| MI:0089 | CMCC | An internal carrier error occurs. |
| MI:0090 | CMCC | VMSC returns a "remote address unreachable" error. |
| MI:0098 | CMCC | An internal carrier error occurs. |
| MI:0099 | CMCC | VMSC returns an "unexpected response received" error. |
| MI:0660 | CMCC | The CMCC gateway is exceptional internally. |
| MI:0999 | CMCC | The CMCC gateway is exceptional internally. |
| MI00000 | CMCC | The message has expired in the SMS center. |
| MI00020              | CMCC | The carrier's gateway is exceptional.                         |
| MI00022 | CMCC | The storage of the recipient's phone is full. |
| MI00029              | CMCC | The carrier's gateway is exceptional.                         |
| MI00036 | CMCC | An internal carrier error occurs. |
| MI0020 | CMCC | Message sending fails: ErrorinMS. |
| MILIMIT      | CMCC | The recipient's mobile number is out of service.           |
| MK00001 | CMCC | The recipient's mobile number does not exist. |
| MK00011              | CMCC | The recipient's mobile number is out of service.                                   |
| MK00013              | CMCC | The recipient's mobile number is out of service.                                   |
| MK:0000 | CMCC | The recipient's mobile number does not exist. |
| MK:0001 | CMCC | The recipient's mobile number is not found in HLR, and the SMS center returns a status of "unable to identify the number", which means that the number is incorrect. |
| MK:0002              | CMCC | The recipient's phone has a reception exception.                           |
| MK:0003 | CMCC | The recipient is invalid. Recipient authentication fails during this message sending. The reason may be that MSC believes that the authentication password of the recipient's mobile number is invalid. The error code in MSC is 3, which is defined as 9 in the ETSI GSM 0902 protocol. |
| MK:0004 | CMCC | The recipient's mobile number is out of service, or the recipient's phone is powered off. |
| MK:0005 | CMCC | The recipient's mobile number does not exist or is out of service or suspended. |
| MK:0006 | CMCC | An internal carrier error occurs. |
| MK:0007 | CMCC | The recipient's phone is invalid. |
| MK:0008 | CMCC | The recipient's region has poor reception, so the message cannot be received. |
| MK:0009 | CMCC | The recipient's mobile number is out of area: MWDSET |
| MK:0010 | CMCC | The recipient's mobile number is temporarily unreachable. |
| MK:0011 | CMCC | The recipient's mobile number is out of service, or the recipient's phone is powered off. |
| MK:0012 | CMCC | The recipient's mobile number does not exist.  |
| MK:0013 | CMCC | The recipient's mobile number does not exist.  |
| MK:0015 | CMCC | The recipient's phone experiences a software issue when receiving the sent message; for example, after the phone is restarted, some software programs for processing messages have not been initialized, so messages cannot be processed normally at this time. |
| MK:0016 | CMCC | The recipient's phone is invalid. |
| MK:0017 | CMCC | The storage of the recipient's phone is full. |
| MK:0018 | CMCC | The CMCC gateway is exceptional internally. |
| MK:0019 | CMCC | MS does not support the SMS termination service. |
| MK:0020 | CMCC | An internal carrier error occurs. |
| MK:0021 | CMCC | An internal carrier error occurs. |
| MK:0022 | CMCC | An internal carrier error occurs. |
| MK:0023 | CMCC | An internal carrier error occurs. |
| MK:0024 | CMCC | Message sending fails as the recipient's phone is powered off when the message is sent. |
| MK:0025 | CMCC | The CMCC gateway is exceptional internally. |
| MK:0029 | CMCC | The recipient's mobile number is temporarily unreachable. |
| MK:0030 | CMCC | The CMCC gateway is exceptional internally. |
| MK:0031 | CMCC | The CMCC gateway is exceptional internally. |
| MK:0032 | CMCC | The CMCC gateway is exceptional internally. |
| MK:0033 | CMCC | The CMCC gateway is exceptional internally. |
| MK:0034 | CMCC | The CMCC gateway is exceptional internally. |
| MK:0035 | CMCC | The CMCC gateway is exceptional internally. |
| MK:0036 | CMCC | An unknown error from MSC occurs. |
| MK:0037 | CMCC | The CMCC gateway is exceptional internally. |
| MK:0038              | CMCC | The carrier's gateway is exceptional.                         |
| MK:0040 | CMCC | The CMCC gateway is exceptional internally. |
| MK:0041 | CMCC | An internal carrier error occurs. |
| MK:0043              | CMCC | The recipient's phone is powered off.                                   |
| MK:0044 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off. |
| MK:0045 | CMCC | An internal carrier error occurs. |
| MK:0046 | CMCC | The CMCC gateway is exceptional internally. |
| MK:0051 | CMCC | An internal carrier error occurs. |
| MK:0052 | CMCC | The CMCC gateway is exceptional internally. |
| MK:0053 | CMCC | An internal carrier error occurs. |
| MK:0054 | CMCC | The CMCC gateway is exceptional internally. |
| MK:0055 | CMCC | An internal carrier error occurs. |
| MK:0056 | CMCC | An internal carrier error occurs. |
| MK:0057 | CMCC | An internal carrier error occurs. |
| MK:0058 | CMCC | The CMCC gateway is exceptional internally. |
| MK:0061 | CMCC | The CMCC gateway is exceptional internally. |
| MK:0062 | CMCC | The CMCC gateway is exceptional internally. |
| MK:0063 | CMCC | An internal carrier error occurs. |
| MK:0065 | CMCC | GIW response times out. |
| MK:0066 | CMCC | An internal carrier error occurs. |
| MK:0068 | CMCC | An internal carrier error occurs. |
| MK:0069 | CMCC | The CMCC gateway is exceptional internally. |
| MK:0075 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off. |
| MK:0077 | CMCC | The CMCC gateway is exceptional internally. |
| MK:0078 | CMCC | The CMCC gateway is exceptional internally. |
| MK:0079 | CMCC | The recipient's phone has a storage exception. The recipient is recommended to clear the inbox. |
| MK:0084 | CMCC | HLR returns an "unexpected response received" error. |
| MK:0088 | CMCC | VMSC returns a "potential version mismatch" error. |
| MK:0090 | CMCC | The recipient's mobile number is out of service or temporarily unreachable. |
| MK:93        | CMCC | The message is blocked by the carrier as it hits a keyword.          |
| MK:0098              | CMCC | The recipient's phone is powered off.                                   |
| MK:0099              | CMCC | The carrier's gateway is exceptional.                         |
| MK:0115 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.  |
| MK:0118 | CMCC | The message is blocked as it hits a keyword. |
| MK:0128 | CMCC | The recipient's phone is invalid. |
| MK:0130 | CMCC | The CMCC gateway is exceptional internally. |
| MK:0195 | CMCC | The CMCC gateway is exceptional internally. |
| MK:0196 | CMCC | The CMCC gateway is exceptional internally. |
| MK:0208 | CMCC | The CMCC gateway is exceptional internally. |
| MK:0209 | CMCC | The recipient's phone has a storage exception. The recipient is recommended to clear the inbox. |
| MK:0210 | CMCC| Message sending fails as the recipient's mobile number does not have the SMS feature activated. |
| MK:100C | CMCC | The recipient is on the carrier's blocklist. |
| MK:100D | CMCC | The recipient is on the carrier's blocklist. |
| MK:1002              | CMCC | The carrier's gateway is exceptional.                         |
| MK:1007              | CMCC | The carrier's gateway is exceptional.                         |
| MK:1009                | CMCC | The recipient's phone has a reception exception.                           |
| MK:1010 | CMCC | The recipient is on the carrier's blocklist. |
| ML:HMD       | CMCC | The frequency limit is reached.                 |
| ML:MBLJ                | CMCC | The recipient's phone has a reception exception.                           |
| ML:MYWG      | CMCC | The recipient's mobile number is not a Chinese mainland number.       |
| ML:SHLJ | CMCC | The message is blocked by the carrier's gateway. |
| MM:0000              | CMCC | The recipient's phone is powered off.                                   |
| MM:0064 | CMCC | The recipient is on the blocklist. |
| MN:XXXX | CMCC | China Mobile error codes start with M, which are mostly caused by problems with the recipient's mobile phone/number; for example, the mobile number is out of service, out of area, or invalid, or the phone is powered off or has poor reception. |
| MN:0000 | CMCC | The message is blocked as it hits a keyword. |
| MN00001 | CMCC | An internal carrier error occurs. |
| MN:0001 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off. |
| MN:0009 | CMCC | An internal carrier error occurs. |
| MN:0011 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off. |
| MN:0012 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off. |
| MN:0013 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off. |
| MN0013 | CMCC | The recipient's mobile number is out of service. |
| MN00013      | CMCC | The recipient's phone has a cache exception.   |
| MN:0017 | CMCC | The message is rejected. |
| MN:0019 | CMCC | An internal carrier error occurs. |
| MN:0020 | CMCC | An internal CMCC gateway error occurs. |
| MN:0021              | CMCC | The carrier's gateway is exceptional.                         |
| MN:0022 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off. |
| MN:0029 | CMCC | An internal carrier error occurs. |
| MN:0036 | CMCC | The recipient's mobile number is out of area. |
| MN:0041 | CMCC | The recipient's phone is powered off or unreachable. |
| MN:0044              | CMCC | The recipient's phone is powered off.                                   |
| MN:0045 | CMCC | The CMCC gateway is exceptional internally. |
| MN:0050 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off. |
| MN:0051 | CMCC | The recipient's mobile number does not exist. |
| MN:0052 | CMCC | An internal carrier error occurs. |
| MN:0053 | CMCC | An internal carrier error occurs. |
| MN:0054 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off. |
| MN:0055 | CMCC | An internal carrier error occurs. |
| MN:0056 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off. |
| MN:0059 | CMCC | The recipient's mobile number is out of area. |
| MN:0075 | CMCC | An internal carrier error occurs. |
| MN:0084              | CMCC | The recipient's phone is powered off.                                   |
| MN:0090              | CMCC | The recipient's phone is powered off.                                   |
| MN:0098 | CMCC | The CMCC gateway is exceptional internally. |
| MN:0099 | CMCC | The message is rejected by the carrier manually. |
| MN:0174 | CMCC | The message is blocked as it hits a keyword. |
| MN:0660      | CMCC | The recipient's phone has a storage exception.   |
| MN:0999 | CMCC | The message is blocked as it hits a keyword. |
| MO:0008 | CMCC | The message is blocked by the carrier as it hits a keyword. |
| MO:0013 | CMCC | The recipient's mobile number does not exist. |
| MO:0016              | CMCC | The carrier's gateway is exceptional.                         |
| MOBILE_ | CMCC | The recipient's mobile number does not exist. |
| MOBLLE_ | CMCC | The recipient is on the carrier's blocklist. |
| MS:1009 | CMCC | The carrier's gateway is exceptional. |
| MT:9414 | CMCC | The message is blocked by the carrier as it hits a keyword. |
| MUSTNOT | CMCC | The recipient's mobile number does not exist. |
| MX:0002 | CMCC | Message submission to the upper-level channel fails. |
| MX:0011 | CMCC | The message is blocked by the carrier's gateway. |
| NA:0001 | CMCC | A mobile number range identification error occurs. |
| NONE                 | CMCC | The carrier's gateway is exceptional.                         |
| NOTITLE | CMCC | The message is blocked by the carrier as it hits a keyword (an unsubscription method must be added in marketing SMS messages). |
| NOROUTE | CMCC | Route finding fails. |
| NO_ROUT              | CMCC | The recipient's mobile number does not exist. |
| NR-FAIL | CMCC | The message is blocked by the carrier as it hits a keyword. |
| ODDL | CMCC | The carrier's frequency limit is reached. |
| OVER_SE | CMCC | The gateway restricts the sending time (7:00–21:00). |
| PARAMS | CMCC | The message is blocked by the carrier as it hits a keyword. |
| PARAMS_              | CMCC | The recipient's mobile number does not exist. |
| PBLKP | CMCC | The message is blocked by the carrier as it hits a keyword. |
| PHONERR      | CMCC | The recipient's mobile number does not exist. |
| R1:0010      | CMCC | The carrier's gateway is exceptional.           |
| REJRCT | CMCC | The message is blocked by the carrier as it hits a keyword. |
| ROUTERR | CMCC | The message is blocked by the carrier's gateway. |
| RTE_ERR                | CMCC | The recipient's phone has a reception exception.                           |
| S:10000              | CMCC | The carrier's gateway is exceptional.                         |
| S::8 | CMCC | The CMCC gateway is exceptional internally. |
| S::13 | CMCC | The message is blocked as it hits a keyword. |
| S::15| CMCC | The message hits a carrier keyword. |
| S::16      | CMCC | The recipient's phone has a cache exception.   |
| S::37 | CMCC | The message is blocked by the carrier's gateway. |
| S::91 | CMCC | The recipient is on the carrier's blocklist. |
| S::92 | CMCC | The carrier's frequency limit is reached. |
| S::99        | CMCC | The recipient's mobile number is out of service. |
| S::FAIL (S::FAILED) | CMCC | The carrier's gateway is exceptional.                         |
| S::TIME              | CMCC | The carrier's gateway is exceptional.                         |
| SC:0003 | CMCC | The recipient is on the carrier's blocklist. |
| SC:0005 | CMCC | The recipient is on the carrier's blocklist. |
| SC:0006 | CMCC | The message hits a carrier keyword. |
| SC:0010 | CMCC | The message is blocked by the carrier's gateway. |
| SC:0011 | CMCC | The message is blocked by the carrier as it hits a keyword. |
| SC:0016 | CMCC | The recipient is on the carrier's blocklist. |
| SD:0070                | CMCC | The recipient's phone has a reception exception.                           |
| SENDERR      | CMCC | The carrier's gateway is exceptional. |
| SIGNATU | CMCC | The province is not identified. |
| SINLIM       | CMCC | The carrier's gateway is exceptional.           |
| SINPER | CMCC | The carrier's frequency limit is reached. |
| SMGP001 | CMCC | The message is blocked by the carrier as it hits a keyword. |
| SP_UNKN              | CMCC | The recipient's mobile number does not exist. |
| STATE:2                | CMCC | The recipient's phone has a reception exception.                           |
| TA:13                | CMCC | The recipient's mobile number does not exist. |
| TA:169 | CMCC | The recipient's mobile number does not exist. |
| TASNOOK              | CMCC | The carrier's gateway is exceptional.                         |
| TC:0001 | CMCC | The recipient's mobile number is on the blocklist. |
| TC:0007 | CMCC | The message contains a sensitive word. |
| TD:88 | CMCC | The recipient is on the carrier's blocklist. |
| TE:0008 | CMCC | The recipient's mobile number is ported to another carrier. |
| TE:0009 | CMCC | The message is blocked by the carrier as it hits a keyword. |
| TE:0011 | CMCC | The message is blocked by the carrier as it hits a keyword. |
| TE:0012 | CMCC | The recipient is on the carrier's blocklist. |
| TG:0013 | CMCC | The recipient's mobile number does not exist. |
| TE:0015 | CMCC | The recipient is on the carrier's blocklist. |
| TE:0016 | CMCC | The recipient's mobile number does not exist. |
| TREFUSE | CMCC | The message is blocked by the carrier as it hits a keyword. |
| TUIDING | CMCC | The recipient is on the carrier's blocklist. |
| UE:0003 | CMCC | The recipient is on the carrier's blocklist. |
| UE:0010 | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off. |
| UNDELIV | CMCC | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off. |
| UNKNOWN | CMCC | The message status is unknown. |
| USER_RE | CMCC | The message is blocked by the carrier as it hits a keyword. |
| VALVE:D | CMCC | The carrier's frequency limit is reached. |
| VALVE:H      | CMCC | The frequency limit is reached.       |
| VALVE:M      | CMCC | The frequency limit is reached.       |
| WBLIST | CMCC | The recipient is on the carrier's blocklist. |
| XA:0138 | CMCC | The recipient is on the carrier's blocklist. |
| XA:2040 | CMCC | Cross-network sending is not supported. |
| XA:2112 | CMCC | Cross-network sending is not supported. |
| XA:2138 | CMCC | The recipient is on the carrier's blocklist. |
| XA:2139 | CMCC | The recipient is on the carrier's blocklist. |
| XL:169 | CMCC | The recipient's mobile number does not exist. |
| XREJECT              | CMCC | The recipient's mobile number does not exist. |
| YF:031                | CMCC | The recipient's phone has a reception exception.                           |
| YF:032 | CMCC | The recipient is on the carrier's blocklist. |
| YF:0415 | CMCC | The carrier's frequency limit is reached. |
| YX:8007 | CMCC | The message is blocked by the carrier's gateway. |
| ZN:0418 | CMCC | The message is blocked by the carrier as it hits a keyword. |
| -201 | UNICOM | The carrier's gateway is exceptional. |
| -103 | UNICOM  | The recipient is on the carrier's blocklist. |
| -99                  | UNICOM | The recipient is on the carrier's blocklist. |
| -74 | UNICOM | An internal carrier error occurs. |
| -43 | UNICOM | The storage of the recipient's phone is full. |
| -37 | UNICOM | The recipient's phone is powered off. |
| -12                  | UNICOM | The recipient is on the carrier's blocklist. |
| -9 | UNICOM | The message hits a carrier keyword. |
| -8 | UNICOM | The carrier's gateway is exceptional. |
| -4                   | UNICOM | The recipient's phone has a reception exception.                           |
| -3 | UNICOM | The carrier's gateway is exceptional. |
| -1 | UNICOM | An internal carrier error occurs. |
| 0.089583             | UNICOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.                         |
| 0.103472             | UNICOM | The recipient's mobile number does not exist. |
| 0.1208 | UNICOM | The UNICOM gateway is exceptional internally. |
| 0.1299 | UNICOM  | The recipient is on the carrier's blocklist. |
| 0.150694444 | UNICOM  | The recipient is on the carrier's blocklist. |
| 0.209722     | UNICOM | The recipient's mobile number is out of service.                     |
| 0000001      | UNICOM | The recipient's mobile number does not exist. |
| 0000002      | UNICOM | The recipient's mobile number does not exist. |
| 0000003     | UNICOM | The recipient's mobile number is out of service.                     |
| 0000004 | UNICOM | The carrier's gateway is exceptional. |
| 0000005 | UNICOM | The recipient's mobile number is out of service, or the recipient's phone is powered off. |
| 0000008      | UNICOM | The recipient's mobile number does not exist. |
| 0000010                   | UNICOM | The recipient's phone has a reception exception.                           |
| 0000011              | UNICOM | The message is blocked by the carrier as it hits a keyword. |
| 0000012      | UNICOM | The recipient's mobile number does not exist. |
| 0000015 | UNICOM | The recipient's mobile number is out of service, or the recipient's phone is powered off. |
| 0000017 | UNICOM | The recipient's phone is powered off. |
| 0000023              | UNICOM | The recipient's mobile number is suspended. |
| 0000024     | UNICOM | The recipient's mobile number is out of service.                     |
| 0000029 | UNICOM | The recipient's phone is powered off. |
| 0000030 | UNICOM | The carrier's gateway is exceptional. |
| 0000046      | UNICOM | The recipient's mobile number does not exist. |
| 0000048              | UNICOM | The recipient's phone has a reception exception. |
| 0000055 | UNICOM | The carrier's gateway is exceptional. |
| 0000056 | UNICOM | The recipient's mobile number is out of service, or the recipient's phone is powered off. |
| 0000072 | UNICOM | The recipient's mobile number is out of service, or the recipient's phone is powered off. |
| 0000074              | UNICOM | The recipient's phone has a reception exception. |
| 0000079 | UNICOM  | The recipient is on the carrier's blocklist. |
| 0000086 | UNICOM  | The recipient is on the carrier's blocklist. |
| 0000088 | UNICOM | The recipient's mobile number is out of service, or the recipient's phone is powered off. |
| 0000089      | UNICOM | The recipient's mobile number does not exist. |
| 0000093     | UNICOM | The recipient's mobile number is out of service.                     |
| 0000097 | UNICOM  | The recipient is on the carrier's blocklist. |
| 0000099 | UNICOM  | The recipient is on the carrier's blocklist. |
| 1 | UNICOM | The recipient's mobile number does not exist. |
| 2 | UNICOM | An internal carrier error occurs.  |
| 3 | UNICOM | An internal carrier error occurs.  |
| 4 | UNICOM | The recipient's phone is powered off. |
| 5 | UNICOM | The recipient's mobile number is out of service. |
| 6                    | UNICOM | The carrier's gateway is exceptional.                         |
| 8 | UNICOM  | The message length is incorrect. |
| 9 | UNICOM | The serial number is invalid (duplicate, incorrect format, etc.). |
| 10 | UNICOM | The Src_ID is incorrect; for example, the recipient's mobile number does not exist or is restricted or forwarded to the China Unicom secretary service, or the recipient's phone is powered off. |
| 11 | UNICOM | An internal carrier error occurs.  |
| 12 | UNICOM | The billable address is incorrect; for example, the recipient's mobile number does not exist or is restricted or forwarded to the China Unicom secretary service, or the recipient's phone is powered off. |
| 13 | UNICOM | The service code is not assigned, and the corresponding declaration item cannot be found according to the access number and service code on the MT list. |
| 14 | UNICOM | An internal carrier error occurs.  |
| 15 | UNICOM | The recipient's mobile number is out of area. |
| 16 | UNICOM | The recipient's mobile number does not exist. |
| 17 | UNICOM | An internal carrier error occurs.  |
| 18 | UNICOM | The recipient does not subscribe to the message. |
| 19 | UNICOM | The recipient does not subscribe to the message. |
| 20 | UNICOM | The recipient's mobile number is temporarily out of service. |
| 21 | UNICOM | An internal carrier error occurs.  |
| 22 | UNICOM | An internal carrier error occurs.  |
| 23 | UNICOM | An internal carrier error occurs.  |
| 24 | UNICOM | The billable mobile number is invalid (out of service). |
| 27 | UNICOM | The recipient's phone does not support SMS. |
| 29 | UNICOM | The recipient's mobile number is incorrect. |
| 31 | UNICOM | The recipient's phone is invalid. |
| 32 | UNICOM | An internal carrier error occurs.  |
| 33 | UNICOM | The recipient's mobile number does not exist. |
| 34 | UNICOM  | The recipient is on the carrier's blocklist. |
| 35                   | UNICOM | The carrier's gateway is exceptional.                         |
| 36 | UNICOM | The recipient's mobile number is out of service. |
| 37 | UNICOM | The recipient's phone has a reception exception. |
| 38                   | UNICOM | The carrier's gateway is exceptional.                         |
| 40 | UNICOM | An internal carrier error occurs.  |
| 41                   | UNICOM | The carrier's gateway is exceptional.                         |
| 43 | UNICOM | The storage of the recipient's phone is full. |
| 44 | UNICOM | The recipient's phone does not have the SMS feature. |
| 45 | UNICOM | The recipient's mobile number is out of service. |
| 46 | UNICOM   | Contact [SMS Helper](https://intl.cloud.tencent.com/document/product/382/3773) for assistance. |
| 48 | UNICOM | An internal carrier error occurs.  |
| 49                   | UNICOM | The carrier's gateway is exceptional.                         |
| 50 | UNICOM | The recipient's mobile number is out of service. |
| 51           | UNICOM | The recipient's phone is exceptional.                 |
| 52 | UNICOM | The recipient's phone does not have the SMS feature. |
| 53 | UNICOM | The recipient's phone is powered off. |
| 54 | UNICOM | The recipient's phone is powered off. |
| 55 | UNICOM | The recipient's mobile number is out of area. |
| 56 | UNICOM | The recipient's mobile number is out of service. |
| 57 | UNICOM | An internal carrier error occurs.  |
| 58 | UNICOM | The recipient's phone has a reception exception. |
| 59 | UNICOM | An internal carrier error occurs.  |
| 61 | UNICOM | The recipient's mobile number does not exist. |
| 63           | UNICOM | The recipient's mobile number is suspended.                 |
| 64 | UNICOM | The recipient's mobile number is out of area. |
| 66                   | UNICOM | The carrier's gateway is exceptional.                         |
| 67 | UNICOM | The recipient's mobile number does not exist. |
| 69 | UNICOM | The recipient is on the blocklist. |
| 70 | UNICOM | The recipient's mobile number is out of area. |
| 72 | UNICOM | The recipient's mobile number in the 145 range does not exist. |
| 73 | UNICOM | An internal carrier error occurs.  |
| 75 | UNICOM | The recipient's mobile number is restricted. |
| 79 | UNICOM | The storage of the recipient's phone is full. |
| 83                   | UNICOM | The carrier's gateway is exceptional.                         |
| 85 | UNICOM  | The recipient's mobile number does not exist, or the recipient's phone is powered off.  |
| 86 | UNICOM | The recipient's mobile number is out of area. |
| 88 | UNICOM | The recipient's mobile number is out of area. |
| 89 | UNICOM | The recipient's mobile number is out of area. |
| 90 | UNICOM | An internal carrier error occurs.  |
| 92 | UNICOM   | Contact [SMS Helper](https://intl.cloud.tencent.com/document/product/382/3773) for assistance. |
| 93 | UNICOM | Monthly rent authentication fails as the recipient's mobile number is out of service or canceled. |
| 95 | UNICOM | Authentication fails as the recipient's mobile number does not exist or is canceled. |
| 98 | UNICOM | The recipient's mobile number is temporarily out of service. |
| 99 | UNICOM | The recipient's mobile number is temporarily out of service. |
| 100 | UNICOM   | Contact [SMS Helper](https://intl.cloud.tencent.com/document/product/382/3773) for assistance. |
| 100:97       | UNICOM  | The recipient is on the carrier's blocklist.             |
| 101 | UNICOM | The recipient's mobile number does not exist. |
| 102 | UNICOM | The recipient's mobile number is out of service. |
| 103 | UNICOM   | Contact [SMS Helper](https://intl.cloud.tencent.com/document/product/382/3773) for assistance. |
| 104 | UNICOM | An internal carrier error occurs.  |
| 105 | UNICOM | The recipient's mobile number is out of service, suspended, or forbidden. |
| 106 | UNICOM | Authentication fails as the fees are invalid. |
| 107 | UNICOM | The UNICOM gateway is exceptional internally. |
| 110 | UNICOM | An internal carrier error occurs.  |
| 114                  | UNICOM | The carrier's gateway is exceptional.                         |
| 116 | UNICOM | An internal carrier error occurs.  |
| 117 | UNICOM   | Contact [SMS Helper](https://intl.cloud.tencent.com/document/product/382/3773) for assistance. |
| 118 | UNICOM | The recipient's phone does not have the SMS feature. |
| 121                  | UNICOM | The carrier's gateway is exceptional.                         |
| 122 | UNICOM | The recipient's phone has a reception exception. |
| 124 | UNICOM | The recipient's phone is powered off, or the recipient's mobile number is suspended or forbidden. |
| 141                  | UNICOM | The carrier's gateway is exceptional.                         |
| 148 | UNICOM | An internal carrier error occurs.  |
| 164 | UNICOM   | Contact [SMS Helper](https://intl.cloud.tencent.com/document/product/382/3773) for assistance. |
| 174                  | UNICOM | The carrier's gateway is exceptional.                         |
| 181                  | UNICOM | The carrier's gateway is exceptional.                         |
| 182 | UNICOM | The recipient's mobile number is suspended. |
| 193                  | UNICOM | The carrier's gateway is exceptional.                         |
| 194                  | UNICOM | The recipient's phone has a reception exception.                           |
| 210                  | UNICOM | The carrier's gateway is exceptional.                         |
| 213 | UNICOM | The recipient's mobile number is out of service, suspended, or forbidden. |
| 219 | UNICOM | The message cannot be received as the recipient's mobile number is out of service or temporarily unreachable, or the recipient's phone is powered off. |
| 222 | UNICOM | The message is blocked as it contains a sensitive word. |
| 227                  | UNICOM | The carrier's gateway is exceptional.                         |
| 230                  | UNICOM | The carrier's gateway is exceptional.                         |
| 237 | UNICOM | The recipient is on the blocklist.  |
| 239                  | UNICOM | The carrier's gateway is exceptional.                         |
| 245                  | UNICOM | The recipient's mobile number does not exist.                                   |
| 253                  | UNICOM | The recipient's phone has a reception exception.                           |
| 254                  | UNICOM | The carrier's gateway is exceptional.                         |
| 255 | UNICOM   | Contact [SMS Helper](https://intl.cloud.tencent.com/document/product/382/3773) for assistance. |
| 706                  | UNICOM | The recipient's mobile number does not exist.                                   |
| 43497 | UNICOM | The recipient's mobile number does not exist, or the recipient is on the blocklist.  |
| 2-67 | UNICOM | The message is blocked by the carrier. |
| 2-68 | UNICOM | The UNICOM gateway is exceptional internally. |
| 2:01 | UNICOM | The recipient's mobile number does not exist. |
| 2:05 | UNICOM | The recipient's phone is powered off. |
| 2:3 | UNICOM | The recipient's phone is powered off. |
| 2:4          | UNICOM | The recipient's mobile number is out of service, or the recipient's phone is powered off. |
| 2:8                   | UNICOM | The recipient's phone has a reception exception.                           |
| 2:10 | UNICOM | The recipient's mobile number is out of service. |
| 2:11                   | UNICOM | The recipient's phone has a reception exception.                           |
| 2:12 | UNICOM | The recipient's mobile number does not exist. |
| 2:13 | UNICOM | The recipient's mobile number is out of service. |
| 2:15                   | UNICOM | The recipient's phone has a reception exception.                           |
| 2:17                 | UNICOM | The recipient's phone has a cache exception.   |
| 2:18 | UNICOM | The recipient's phone is powered off. |
| 2:19 | UNICOM | The recipient's mobile number does not exist. |
| 2:20                 | UNICOM | The recipient's mobile number is out of service. |
| 2:21 | UNICOM | The recipient's mobile number does not exist. |
| 2:22 | UNICOM | The carrier's gateway is exceptional. |
| 2:23 | UNICOM | The recipient's mobile number is out of service. |
| 2:24                   | UNICOM | The recipient's phone has a reception exception.                           |
| 2:36                 | UNICOM | The recipient's mobile number is out of service. |
| 2:38                   | UNICOM | The recipient's phone has a reception exception.                           |
| 2:40 | UNICOM | The carrier's gateway is exceptional. |
| 2:41                   | UNICOM | The recipient's phone has a reception exception.                           |
| 2:44             | UNICOM | The recipient's mobile number is suspended. |
| 2:46 | UNICOM | The recipient's mobile number does not exist. |
| 2:53 | UNICOM | The recipient's phone is powered off. |
| 2:55                   | UNICOM | The recipient's phone has a reception exception.                           |
| 2:56 | UNICOM | The recipient's mobile number is out of service. |
| 2:63 | UNICOM | The recipient's mobile number is out of service. |
| 2:86                   | UNICOM | The recipient's phone has a reception exception.                           |
| 2:72                   | UNICOM | The recipient's phone has a reception exception.                           |
| 2:75                   | UNICOM | The recipient's phone has a reception exception.                           |
| 2:79 | UNICOM | The recipient's phone has a storage exception.   |
| 2:83                   | UNICOM | The recipient's phone has a reception exception.                           |
| 2:89 | UNICOM | The recipient's mobile number does not exist. |
| 2:93         | UNICOM | The recipient's mobile number is out of service. |
| 2:95 | UNICOM | The carrier's gateway is exceptional. |
| 2:98                 | UNICOM | The recipient's mobile number is out of service. |
| 2:100                   | UNICOM | The recipient's phone has a reception exception.                           |
| 2:182        | UNICOM | The recipient's mobile number is out of service. |
| 2:211 | UNICOM | The carrier's gateway is exceptional. |
| 2:213                | UNICOM | The recipient's mobile number is out of service. |
| 2:242                   | UNICOM | The recipient's phone has a reception exception.                           |
| 2:23000          | UNICOM | The recipient's mobile number is out of service, or the recipient's phone is powered off. |
| 2:24000      | UNICOM | The recipient's mobile number is out of service. |
| 2:50000      | UNICOM | The recipient's mobile number does not exist. |
| 100:23               | UNICOM | The recipient's mobile number does not exist. |
| 100:29          | UNICOM | The recipient's mobile number is out of service, or the recipient's phone is powered off. |
| 100:101 | UNICOM | The recipient's mobile number does not exist. |
| BLACK | UNICOM  | The recipient is on the carrier's blocklist. |
| BWLISTS | UNICOM | The recipient's mobile number does not exist. |
| CJ:0005 | UNICOM  | The recipient is on the carrier's blocklist. |
| CU:0020              | UNICOM | The message is blocked by the carrier as it hits a keyword. |
| DB:0005 | UNICOM | The recipient's phone is powered off. |
| DB00108 | UNICOM | The carrier's gateway is exceptional. |
| DJ:0141 | UNICOM  | The recipient is on the carrier's blocklist. |
| DJ:0255              | UNICOM | The message is blocked by the carrier as it hits a keyword. |
| E:DISPR | UNICOM | The recipient's mobile number does not exist. |
| E:ONSUB | UNICOM | The carrier's network fails. |
| ERR:000              | UNICOM | The recipient's mobile number is out of service. |
| ERR:004              | UNICOM | The message is blocked by the carrier as it hits a keyword. |
| ERR:005              | UNICOM | The recipient's mobile number is out of service.                     |
| ERR:008              | UNICOM | The recipient's phone is powered off. |
| ERR:010              | UNICOM | The recipient's mobile number does not exist. |
| ERR:012 | UNICOM | The recipient's mobile number is out of service. |
| ERR:017 | UNICOM | The recipient's mobile number is out of service. |
| ERR:032              | UNICOM | The message is blocked by the carrier as it hits a keyword. |
| ERROR                | UNICOM  | The recipient is on the carrier's blocklist.                           |
| FAIL_BL      | UNICOM  | The recipient is on the carrier's blocklist.   |
| FAIL_IN | UNICOM | The recipient's mobile number does not exist. |
| FAIL_MO              | UNICOM | The recipient's phone is powered off.                                   |
| FF:0001 | UNICOM | The recipient's mobile number does not exist. |
| GB:0006 | UNICOM | The recipient's mobile number does not exist. |
| GB:0015 | UNICOM | The carrier's gateway is exceptional. |
| HONGZHA | UNICOM  | The recipient is on the carrier's blocklist. |
| LT:0 | UNICOM | Message sending succeeds. |
| LT:0000 | UNICOM | The recipient's mobile number is suspended. |
| LT:0001 | UNICOM | The recipient's mobile number does not exist. |
| LT:0002 | UNICOM | A China Unicom failure occurs due to poor reception. If batch failures occur, the reason may be that the message contains a sensitive word. In this case, you need to confirm with the carrier. |
| LT:0003 | UNICOM | The recipient's mobile number is invalid. |
| LT:0004 | UNICOM | The recipient's mobile number is out of service. |
| LT:0005 | UNICOM | The message is blocked by the gateway. |
| LT:0006      | UNICOM | The message is blocked by the carrier's gateway. |
| LT:0008 | UNICOM | The storage of the recipient's phone is full. |
| LT:0009 | UNICOM | The recipient's mobile number is invalid. |
| LT:00-1 | UNICOM | The message is blocked by the gateway. |
| LT:00-4 | UNICOM | The recipient's phone has a reception exception. |
| LT:00-9 | UNICOM | The recipient's mobile number does not exist. |
| LT:0010 | UNICOM | The recipient's mobile number does not exist. |
| LT:0011 | UNICOM | The recipient's phone is powered off. |
| LT:0012 | UNICOM | The recipient's mobile number does not exist. |
| LT:0013 | UNICOM | The recipient's mobile number is out of service. |
| LT:0015 | UNICOM | The message is blocked by the gateway. |
| LT:0016      | UNICOM | The recipient's phone has a reception exception.   |
| LT:0017 | UNICOM | The message is blocked by the gateway. |
| LT:0020 | UNICOM | The message is blocked by the gateway. |
| LT:0022 | UNICOM | The message is blocked by the gateway. |
| LT:0023 | UNICOM | The recipient's mobile number does not exist. |
| LT:0024 | UNICOM | The recipient's phone is powered off. |
| LT:0027 | UNICOM | The recipient's phone is powered off. |
| LT:0029 | UNICOM | The recipient's phone is powered off. |
| LT:0031 | UNICOM | The recipient's phone has a reception exception. |
| LT:0040 | UNICOM | The recipient's mobile number does not exist. |
| LT:0044 | UNICOM | The message is blocked by the gateway. |
| LT:0046 | UNICOM | The message is blocked by the gateway. |
| LT:0048 | UNICOM | Call fails. |
| LT:0050 | UNICOM | The recipient's mobile number is temporarily unreachable. |
| LT:0051 | UNICOM | The recipient's mobile number is temporarily unreachable. |
| LT:0052      | UNICOM | The recipient's mobile number does not exist.           |
| LT:0053 | UNICOM | The recipient's mobile number is temporarily unreachable. |
| LT:0054 | UNICOM | The recipient's phone is powered off. |
| LT:0055 | UNICOM  | Inbound call is restricted. |
| LT:0057 | UNICOM | The message is blocked by the gateway. |
| LT:0059 | UNICOM | The recipient's phone is powered off. |
| LT:0061 | UNICOM  | The message is blocked. |
| LT:0069 | UNICOM | A China Unicom failure occurs. |
| LT:0075      | UNICOM | The recipient's mobile number does not exist.           |
| LT:0079 | UNICOM | The message is blocked by the gateway. |
| LT:0086 | UNICOM | The message is blocked by the gateway. |
| LT:0089 | UNICOM | The recipient's mobile number is invalid. |
| LT:0090 | UNICOM | The message is blocked by the gateway. |
| LT:0092 | UNICOM | The message is blocked by the gateway. |
| LT:0093 | UNICOM | The message is blocked by the gateway. |
| LT:0098 | UNICOM | The message is blocked by the gateway. |
| LT:0100 | UNICOM | The recipient's mobile number does not exist. |
| LT:0104 | UNICOM | The recipient's phone is invalid. |
| LT:0106 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:0117 | UNICOM | The message is blocked by the gateway. |
| LT:0122 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:0-37 | UNICOM | The recipient's mobile number does not exist. |
| LT:0-74 | UNICOM | The recipient's mobile number is out of service. |
| LT:1 | UNICOM | The recipient's mobile number is invalid. |
| LT:5 | UNICOM | The recipient's phone has a reception exception. |
| LT:6 | UNICOM | The recipient's phone is invalid. |
| LT:9 | UNICOM | The recipient's phone is invalid. |
| LT:11 | UNICOM | Message sending fails as the recipient's mobile number is ported to another carrier. |
| LT:12 | UNICOM | The recipient's phone is invalid. |
| LT:13 | UNICOM | Call is forbidden. |
| LT:23 | UNICOM | Message sending fails as the recipient's mobile number is ported to another carrier. |
| LT:27 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:31 | UNICOM | The recipient's phone has a reception exception. |
| LT:32 | UNICOM | The recipient's phone has a reception exception. |
| LT:34 | UNICOM | The recipient's phone has a reception exception. |
| LT:35 | UNICOM | The recipient's phone has a reception exception. |
| LT:36 | UNICOM | The recipient's phone has a reception exception. |
| LT:52 | UNICOM | The recipient's phone has a reception exception. |
| LT:61 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:67 | UNICOM | The recipient is on the blocklist. |
| LT:86 | UNICOM | The recipient is on the blocklist. |
| LT:90 | UNICOM | The recipient's phone is faulty. |
| LT:91 | UNICOM | The recipient's phone does not have the SMS feature. |
| LT:92 | UNICOM | The storage of the recipient's phone is full. |
| LT:100 | UNICOM | The recipient's phone has a reception exception. |
| LT:101 | UNICOM | The recipient's phone is powered off. |
| LT:102 | UNICOM | The recipient's phone has a reception exception. |
| LT:103 | UNICOM | The recipient's mobile number does not exist. |
| LT:104 | UNICOM | The recipient's mobile number is invalid. |
| LT:106 | UNICOM | The recipient's phone has a reception exception. |
| LT:107 | UNICOM | The recipient's mobile number is invalid. |
| LT:110 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:111 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:112 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:113 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:114 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:115 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:116 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:117 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:118 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:119 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:120 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:121 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:122 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:181 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:182 | UNICOM | The operation is forbidden. |
| LT:21 | UNICOM | The recipient's phone does not have the SMS feature. |
| LT:215 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:217 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:218 | UNICOM | The recipient's number is invalid. |
| LT:219 | UNICOM | The recipient's number is invalid. |
| LT:220 | UNICOM | The recipient's phone is powered off. |
| LT:221 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:222 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:223 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:225 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:226 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:227 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:228 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:229 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:230 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:231 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:232 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:233 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:234 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:235 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:236 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:237 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:238 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:239 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:240 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:241 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:242 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:243 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:244 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:245 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:246 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:247 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:248 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:249 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:250 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:251 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:252 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:253 | UNICOM | An internal UNICOM gateway error occurs. |
| LT:254 | UNICOM | An internal UNICOM gateway error occurs. |
| MA:0038              | UNICOM | The carrier's frequency limit is reached.                         |
| MAXFREQ              | UNICOM | The carrier's frequency limit is reached.                         |
| MC:000 | UNICOM | The recipient's phone is powered off. |
| MK:-108              | UNICOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.                         |
| MK:-74               | UNICOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.                         |
| MK:-43               | UNICOM | The recipient's phone has a reception exception.                           |
| MK:-37               | UNICOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.                         |
| MK:-9                | UNICOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.                         |
| MK:                  | UNICOM | The carrier's gateway is exceptional.                         |
| MK:1         | UNICOM | The recipient's mobile number is out of service.                     |
| MK:2                 | UNICOM | The recipient's phone has a reception exception.                           |
| MK:3                 | UNICOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.                         |
| MK:5                 | UNICOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.                         |
| MK:7                 | UNICOM | The recipient's phone has a reception exception.                           |
| MK:8                 | UNICOM | The recipient's phone has a reception exception.                           |
| MK:9                 | UNICOM | The recipient's mobile number is out of service.                                   |
| MK:10                | UNICOM | The recipient's phone has a reception exception.                           |
| MK:11                | UNICOM | The recipient's phone has a reception exception.                           |
| MK:12                | UNICOM | The recipient's phone has a reception exception.                           |
| MK:13                | UNICOM | The recipient's phone has a reception exception.                           |
| MK:15                | UNICOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.                         |
| MK:17                | UNICOM | The recipient's phone has a reception exception.                           |
| MK:19                | UNICOM | The recipient's phone has a reception exception.                           |
| MK:20                | UNICOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.                         |
| MK:21                | UNICOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.                         |
| MK:23                | UNICOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.                         |
| MK:24                | UNICOM | The recipient's mobile number does not have the SMS feature enabled.                         |
| MK:25                | UNICOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.                         |
| MK:27                | UNICOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.                         |
| MK:29                | UNICOM | The recipient's phone has a reception exception.                           |
| MK:44                | UNICOM | The recipient's phone has a reception exception.                           |
| MK:53                | UNICOM | The recipient's phone has a reception exception.                           |
| MK:54                | UNICOM | The recipient's phone has a reception exception.                           |
| MK:55                | UNICOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.                         |
| MK:56                | UNICOM | The recipient's phone has a reception exception.                           |
| MK:57                | UNICOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.                         |
| MK:63                | UNICOM | The recipient's phone has a reception exception.                           |
| MK:75                | UNICOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.                         |
| MK:90                | UNICOM | The recipient's phone has a reception exception.                           |
| MK:92                | UNICOM | The recipient's phone has a reception exception.                           |
| MK:100               | UNICOM | The recipient's phone has a reception exception.                           |
| MK:122               | UNICOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.                         |
| MK:1000 | UNICOM | The recipient's phone has a reception exception. |
| MN:0082      | UNICOM | The recipient's mobile number is suspended.                 |
| MO:0001              | UNICOM | The recipient's mobile number does not exist.                                   |
| MO:0032      | UNICOM | The carrier's gateway is exceptional. |
| MO:0254 | UNICOM | The carrier's gateway is exceptional. |
| MO:0084              | UNICOM  | The recipient is on the carrier's blocklist.                           |
| MO:0086              | UNICOM | The carrier's frequency limit is reached.                         |
| MO:0094              | UNICOM | The recipient's phone is powered off.                                   |
| MO:0247              | UNICOM | The carrier's gateway is exceptional.                         |
| MS:0005              | UNICOM | The recipient's mobile number does not exist.                                   |
| MS:1005              | UNICOM | The recipient's mobile number does not exist.                                   |
| MS:1007 | UNICOM | The recipient's mobile number is out of service, or the recipient's phone has a reception exception. |
| MX:0001      | UNICOM | The message is blocked by the carrier as it hits a keyword. |
| MX:0004      | UNICOM  | The recipient is on the carrier's blocklist.             |
| MX:0005      | UNICOM | The carrier's gateway is exceptional.           |
| MX:0006      | UNICOM | The message is blocked by the carrier as it hits a keyword. |
| MX:0007      | UNICOM  | The recipient is on the carrier's blocklist.             |
| MX:0008      | UNICOM | The message is blocked by the carrier as it hits a keyword. |
| MX:0009      | UNICOM  | The recipient is on the carrier's blocklist.             |
| MX:0010      | UNICOM | The recipient's mobile number does not exist.                     |
| MX:0013      | UNICOM  | The recipient is on the carrier's blocklist.             |
| QM_FAIL      | UNICOM | The message is blocked by the carrier's gateway. |
| R:00002      | UNICOM | The recipient's phone is powered off.                     |
| R:00003      | UNICOM | The recipient's mobile number does not exist.                     |
| R:00004      | UNICOM | The recipient's mobile number does not exist.                     |
| R:00009      | UNICOM | The recipient's phone is powered off.                     |
| R:00014      | UNICOM | The recipient's mobile number does not exist.                     |
| R:00017      | UNICOM | The recipient's phone is powered off.                     |
| R:00018      | UNICOM | The recipient's phone has a reception exception.             |
| R:00019      | UNICOM | The recipient's phone is powered off.                     |
| R:00020      | UNICOM | The recipient's phone is powered off.                     |
| R:00022      | UNICOM | The recipient's phone is powered off.                     |
| R:00027      | UNICOM | The recipient's phone is powered off.                     |
| R:00029      | UNICOM | The recipient's mobile number does not exist.                     |
| R:00033      | UNICOM | The recipient's mobile number does not exist.                     |
| R:00035      | UNICOM | The recipient's phone is powered off.                     |
| R:00036      | UNICOM | The frequency limit is reached.                 |
| R:00041      | UNICOM | The recipient's phone is powered off.                     |
| R:00044      | UNICOM | The recipient's phone is powered off.                     |
| R:00045      | UNICOM | The recipient's phone is powered off.                     |
| R:00048      | UNICOM | The recipient's phone is powered off.                     |
| R:00050      | UNICOM | The recipient's phone is powered off.                     |
| R:00051      | UNICOM | The recipient's phone is powered off.                     |
| R:00053      | UNICOM | The recipient's phone is powered off.                     |
| R:00054      | UNICOM | The recipient's phone is powered off.                     |
| R:00055      | UNICOM | The recipient's phone is powered off.                     |
| R:00057      | UNICOM | The recipient's phone is powered off.                     |
| R:00058      | UNICOM | The recipient's phone is powered off.                     |
| R:00059      | UNICOM | The recipient's phone is powered off.                     |
| R:00064      | UNICOM | The recipient's phone is powered off.                     |
| R:00067      | UNICOM | The recipient's phone is powered off.                     |
| R:00068      | UNICOM | The recipient's phone is powered off.                     |
| R:00069      | UNICOM | The recipient's phone is powered off.                     |
| R:00070      | UNICOM | The recipient's phone is powered off.                     |
| R:00072      | UNICOM | The recipient's phone is powered off.                     |
| R:00073      | UNICOM | The recipient's phone is powered off.                     |
| R:00075      | UNICOM | The recipient's phone is powered off.                     |
| R:00079      | UNICOM | The recipient's phone is powered off.                     |
| R:00083      | UNICOM | The recipient's phone is powered off.                     |
| R:00085      | UNICOM | The recipient's phone is powered off.                     |
| R:00086      | UNICOM | The recipient's phone is powered off.                     |
| R:00088      | UNICOM | The recipient's phone is powered off.                     |
| R:00089      | UNICOM | The recipient's phone is powered off.                     |
| R:00090      | UNICOM | The recipient's phone has a reception exception.             |
| R:00092      | UNICOM | The recipient's phone is powered off.                     |
| R:00093      | UNICOM | The recipient's phone is powered off.                     |
| R:00096      | UNICOM | The recipient's phone is powered off.                     |
| R:00098      | UNICOM | The recipient's phone is powered off.                     |
| R:00099      | UNICOM | The recipient's phone is powered off.                     |
| R:00106      | UNICOM | The recipient's phone is powered off.                     |
| R:00124      | UNICOM | The recipient's phone is powered off.                     |
| R:00181      | UNICOM | The recipient's phone is powered off.                     |
| R:00182      | UNICOM | The recipient's mobile number is out of service.                     |
| R:00210      | UNICOM | The recipient's phone is powered off.                     |
| R:00230      | UNICOM | The recipient's phone is powered off.                     |
| R:00242      | UNICOM | The recipient's mobile number does not exist.                     |
| R:00245      | UNICOM | The recipient's phone is powered off.                     |
| R:00253      | UNICOM | The recipient's phone is powered off.                     |
| R:00254      | UNICOM | The recipient's phone is powered off.                     |
| R:00605      | UNICOM | The recipient's phone is powered off.                     |
| R:00612      | UNICOM | The recipient's phone is powered off.                     |
| R:00613      | UNICOM | The recipient's phone is powered off.                     |
| R:00614      | UNICOM | The recipient's phone is powered off.                     |
| R:00615      | UNICOM | The recipient's phone is powered off.                     |
| R:00616      | UNICOM | The carrier's gateway is exceptional.           |
| R:00617      | UNICOM | The recipient's phone is powered off.                     |
| R:00619      | UNICOM | The recipient's phone is powered off.                     |
| R:00627      | UNICOM | The recipient's phone is powered off.                     |
| R:00634      | UNICOM | The recipient's phone is powered off.                     |
| R:00636      | UNICOM | The recipient's phone is powered off.                     |
| R:00640      | UNICOM | The recipient's mobile number does not exist.                     |
| R:00650      | UNICOM | The recipient's phone is powered off.                     |
| R:00680      | UNICOM | The recipient's phone is powered off.                     |
| R:00701      | UNICOM | The recipient's mobile number does not exist.                     |
| R:00702      | UNICOM | The recipient's phone is powered off.                     |
| R:00704      | UNICOM | The recipient's phone is powered off.                     |
| R:00705      | UNICOM | The recipient's mobile number is out of service.                     |
| R:00706      | UNICOM | The recipient's phone is powered off.                     |
| R:00707      | UNICOM | The recipient's phone is powered off.                     |
| R:00708      | UNICOM | The recipient's phone is powered off.                     |
| R:00711      | UNICOM | The recipient's phone is powered off.                     |
| R:00713      | UNICOM | The recipient's phone is powered off.                     |
| R:00714      | UNICOM | The recipient's phone is powered off.                     |
| R:00718      | UNICOM | The recipient's phone is powered off.                     |
| R:00721      | UNICOM | The recipient's phone is powered off.                     |
| R:00726      | UNICOM | The recipient's phone is powered off.                     |
| R:00760      | UNICOM | The recipient's phone is powered off.                     |
| R:00761      | UNICOM | The recipient's phone is powered off.                     |
| R:00762      | UNICOM | The recipient's phone is powered off.                     |
| R:00763      | UNICOM | The recipient's phone is powered off.                     |
| R:00764      | UNICOM | The recipient's phone is powered off.                     |
| R:00765      | UNICOM | The recipient's phone is powered off.                     |
| R:00771      | UNICOM | The recipient's phone is powered off.                     |
| R:00779      | UNICOM | The recipient's phone is powered off.                     |
| R:00801      | UNICOM | The recipient's mobile number does not exist.                     |
| R:00802      | UNICOM | The recipient's phone is powered off.                     |
| R:00814      | UNICOM | The recipient's phone is powered off.                     |
| R:00815      | UNICOM | The recipient's phone is powered off.                     |
| R:00817      | UNICOM | The recipient's phone is powered off.                     |
| R:00827      | UNICOM | The recipient's phone is powered off.                     |
| R:00869      | UNICOM | The recipient's mobile number does not exist.                     |
| R:00875      | UNICOM | The recipient's phone is powered off.                     |
| R:00899      | UNICOM | The recipient's phone is powered off.                     |
| R:00980      | UNICOM | The recipient's phone is powered off.                     |
| R:00999      | UNICOM | The frequency limit is reached.                 |
| R:04300      | UNICOM | The recipient's mobile number is out of service.                     |
| R:04414      | UNICOM | The recipient's mobile number does not exist.                     |
| R:04442      | UNICOM | The recipient's phone is powered off.                     |
| R:04701      | UNICOM | The recipient's mobile number does not exist.                     |
| R1:0013      | UNICOM | The recipient's mobile number does not exist.                     |
| R1:0043      | UNICOM | The recipient's mobile number does not exist.                     |
| R1:1011      | UNICOM | The recipient's mobile number does not exist.                     |
| R2:0010      | UNICOM | The carrier's gateway is exceptional.           |
| R2:0011      | UNICOM | The carrier's gateway is exceptional.           |
| S::-19       | UNICOM | The recipient's phone is powered off.           |
| S::-9 | UNICOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off. |
| S::-6        | UNICOM | Message sending fails as the recipient's mobile number is ported to another carrier. |
| S::1                 | UNICOM | The recipient's mobile number does not exist.                                   |
| S::9                 | UNICOM | The message is blocked by the carrier as it hits a keyword. |
| S::43                | UNICOM | The carrier's gateway is exceptional.                         |
| SGIP:-74             | UNICOM | The recipient's mobile number is out of service.                                   |
| SGIP:-37     | UNICOM | The recipient's phone is powered off.                     |
| SGIP:0               | UNICOM | The recipient's phone has a reception exception.                           |
| SGIP:1 | UNICOM | The recipient's mobile number does not exist. |
| SGIP:2               | UNICOM | The recipient's phone has a reception exception.                           |
| SGIP:3               | UNICOM | The recipient's phone has a reception exception.                           |
| SGIP:4       | UNICOM | The recipient's mobile number is out of service, or the recipient's phone is powered off.      |
| SGIP:5       | UNICOM | The recipient's mobile number is out of service.           |
| SGIP:7               | UNICOM | The recipient's phone has a reception exception.                           |
| SGIP:8       | UNICOM | The recipient's mobile number does not exist.           |
| SGIP:9       | UNICOM | The carrier's gateway is exceptional.           |
| SGIP:11      | UNICOM | The recipient's mobile number is out of service.           |
| SGIP:12      | UNICOM | The recipient's mobile number does not exist.           |
| SGIP:13      | UNICOM | The recipient's mobile number is out of service.           |
| SGIP:15              | UNICOM | The recipient's mobile number is out of service, or the recipient's phone is powered off.                              |
| SGIP:24              | UNICOM | The recipient's mobile number is out of service, or the recipient's phone is powered off.                              |
| SGIP:27              | UNICOM | The recipient's phone has a reception exception.                           |
| SGIP:29              | UNICOM | The recipient's mobile number does not exist.                                   |
| SGIP:51              | UNICOM | The recipient's phone has a reception exception.                           |
| SGIP:54              | UNICOM | The recipient's phone has a reception exception.                           |
| SGIP:57              | UNICOM | The carrier's gateway is exceptional.                         |
| SGIP:75      | UNICOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off. |
| SGIP:81      | UNICOM | The carrier's gateway is exceptional.           |
| SGIP:82      | UNICOM | The carrier's gateway is exceptional.           |
| SGIP:83      | UNICOM | The frequency limit is reached.                 |
| SGIP:84      | UNICOM | The carrier's gateway is exceptional.           |
| SGIP:85      | UNICOM | The carrier's gateway is exceptional.           |
| SGIP:86      | UNICOM | The carrier's gateway is exceptional.           |
| SGIP:87      | UNICOM | The carrier's gateway is exceptional.           |
| SGIP:88      | UNICOM | The carrier's gateway is exceptional.           |
| SGIP:89      | UNICOM | The carrier's gateway is exceptional.           |
| SGIP:90 | UNICOM | The message is blocked by the carrier. |
| SGIP:91      | UNICOM | The carrier's gateway is exceptional.           |
| SGIP:92      | UNICOM | The carrier's gateway is exceptional.           |
| SGIP:93      | UNICOM | The carrier's gateway is exceptional.           |
| SGIP:94      | UNICOM | The carrier's gateway is exceptional.           |
| SGIP:98      | UNICOM | The recipient's mobile number is out of service.                     |
| SGIP:100             | UNICOM | The recipient's mobile number does not exist or is out of service.                              |
| SK:8210 | UNICOM | The recipient's mobile number is exceptional as it is ported to another carrier. |
| SME-9        | UNICOM | The recipient's mobile number does not exist.           |
| TE:0013 | UNICOM  | The recipient is on the carrier's blocklist. |
| U:-108               | UNICOM | The recipient's mobile number is out of service.                                   |
| U:-75                | UNICOM | The carrier's frequency limit is reached.                         |
| U:-74                | UNICOM | The recipient's mobile number is suspended.                               |
| U:-37                | UNICOM | The recipient's phone is powered off.                                   |
| U:-17                | UNICOM | The recipient's phone is powered off.                                   |
| U:1                  | UNICOM | The recipient's mobile number does not exist.                                   |
| U:2                  | UNICOM | The carrier's gateway is exceptional.                         |
| U:3                  | UNICOM | The carrier's gateway is exceptional.                         |
| U:4                  | UNICOM | The recipient's phone is powered off.                                   |
| U:5                  | UNICOM | The recipient's mobile number is out of service.                                   |
| U:7                  | UNICOM | The carrier's gateway is exceptional.                         |
| U:8 | UNICOM | The message length exceeds the limit. |
| U:9                  | UNICOM | The recipient's mobile number does not exist.                                   |
| U:10                 | UNICOM | The recipient's mobile number does not exist.                                   |
| U:11                 | UNICOM | The carrier's gateway is exceptional.                         |
| U:12                 | UNICOM | The carrier's gateway is exceptional.                         |
| U:13                 | UNICOM | The carrier's gateway is exceptional.                         |
| U:15                 | UNICOM | The recipient's phone has a reception exception.                           |
| U:17                 | UNICOM | The carrier's gateway is exceptional.                         |
| U:18                 | UNICOM | The carrier's gateway is exceptional.                         |
| U:20                 | UNICOM | The recipient's mobile number is out of service.                                   |
| U:22                 | UNICOM | The carrier's gateway is exceptional.                         |
| U:23                 | UNICOM | The carrier's gateway is exceptional.                         |
| U:24                 | UNICOM | The recipient's mobile number does not exist.                                   |
| U:29                 | UNICOM | The recipient's mobile number does not exist.                                   |
| U:31                 | UNICOM | The recipient's phone has a reception exception.                           |
| U:36                 | UNICOM | The recipient's mobile number is out of service.                                   |
| U:40                 | UNICOM | The carrier's gateway is exceptional.                         |
| U:44                 | UNICOM | The recipient's mobile number is suspended.                               |
| U:48                 | UNICOM | The carrier's gateway is exceptional.                         |
| U:51                 | UNICOM | The recipient's phone is powered off.                                   |
| U:53                 | UNICOM | The recipient's phone is powered off.                                   |
| U:54                 | UNICOM | The recipient's phone is powered off.                                   |
| U:58                 | UNICOM | The recipient's phone has a storage exception.   |
| U:59                 | UNICOM | The carrier's gateway is exceptional.                         |
| U:69                 | UNICOM  | The recipient is on the carrier's blocklist.                           |
| U:75                 | UNICOM | The carrier's frequency limit is reached.                         |
| U:76                 | UNICOM | The carrier's gateway is exceptional.                         |
| U:98                 | UNICOM | The recipient's mobile number is out of service.                                   |
| U:100                | UNICOM | The carrier's gateway is exceptional.                         |
| U:115                | UNICOM | The carrier's gateway is exceptional.                         |
| U:122                | UNICOM | The carrier's gateway is exceptional.                         |
| U2:-108 | UNICOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off. |
| U2:-82               | UNICOM | The recipient's phone is powered off.                                   |
| U2:-75       | UNICOM | The recipient's phone has a reception exception.   |
| U2:-74 | UNICOM | The recipient's mobile number is out of service. |
| U2:-62               | UNICOM | The recipient's mobile number is out of service.                                   |
| U2:-37 | UNICOM | The recipient's mobile number is suspended. |
| U2:-29               | UNICOM | The recipient's phone has a reception exception.                           |
| U2:-26               | UNICOM | The recipient's phone is powered off.                                   |
| U2:-19 | UNICOM | The recipient is on the blocklist.  |
| U2:-17               | UNICOM | The recipient's phone is powered off.                                   |
| U2:-9                | UNICOM | The recipient's mobile number does not exist.                                   |
| U2:-2 | UNICOM | The recipient's mobile number is out of service, or the recipient's phone is powered off. |
| U2:-3 | UNICOM | The recipient's phone is powered off. |
| U2:1 | UNICOM | The recipient's mobile number does not exist. |
| U2:2 | UNICOM | The UNICOM gateway is exceptional internally. |
| U2:3 | UNICOM | The UNICOM gateway is exceptional internally. |
| U2:4 | UNICOM | The recipient's phone is powered off. |
| U2:5 | UNICOM | The recipient's mobile number is out of service. |
| U2:6 | UNICOM  | The recipient is on the carrier's blocklist. |
| U2:7 | UNICOM | Message sending exceeds the limit. |
| U2:8 | UNICOM | The message length exceeds the limit. |
| U2:9 | UNICOM | The recipient's phone has a reception exception. |
| U2:10 | UNICOM | The recipient's mobile number does not exist. |
| U2:11 | UNICOM | The UNICOM gateway is exceptional internally. |
| U2:12 | UNICOM | The UNICOM gateway is exceptional internally. |
| U2:13 | UNICOM | The UNICOM gateway is exceptional internally. |
| U2:15 | UNICOM | The recipient's mobile number is out of area. |
| U2:16 | UNICOM  | The recipient is on the carrier's blocklist. |
| U2:17 | UNICOM | The UNICOM gateway is exceptional internally. |
| U2:18        | UNICOM | The recipient's phone is powered off.                     |
| U2:20 | UNICOM | The recipient's mobile number is out of service. |
| U2:21                | UNICOM | The recipient's mobile number is out of service.                                   |
| U2:22 | UNICOM | The UNICOM gateway is exceptional internally. |
| U2:23 | UNICOM | The UNICOM gateway is exceptional internally. |
| U2:24 | UNICOM | The recipient's mobile number does not exist. |
| U2:27 | UNICOM | The recipient's phone is powered off. |
| U2:29 | UNICOM | The recipient's mobile number does not exist. |
| U2:30 | UNICOM | The carrier's gateway is exceptional. |
| U2:31 | UNICOM | The recipient's phone is exceptional. |
| U2:32 | UNICOM | The carrier's gateway is exceptional. |
| U2:35 | UNICOM | The recipient's mobile number is out of service. |
| U2:36 | UNICOM | The recipient's mobile number is out of service. |
| U2:38 | UNICOM | The carrier's gateway is exceptional. |
| U2:40                | UNICOM | The carrier's gateway is exceptional.                         |
| U2:43                | UNICOM | The recipient's mobile number is out of service.                                   |
| U2:44                | UNICOM | The recipient's phone has a reception exception.                           |
| U2:45 | UNICOM | The recipient's mobile number is out of service. |
| U2:46                | UNICOM | The recipient's phone has a reception exception.                           |
| U2:48 | UNICOM | The recipient's mobile number does not exist. |
| U2:50 | UNICOM | The recipient's mobile number is out of service. |
| U2:51 | UNICOM | The UNICOM gateway is exceptional internally. |
| U2:52 | UNICOM | The recipient's phone does not have the SMS feature. |
| U2:53 | UNICOM | The recipient's phone is powered off. |
| U2:54 | UNICOM | The recipient's phone is powered off. |
| U2:55 | UNICOM | The recipient's mobile number is out of area. |
| U2:56 | UNICOM | The recipient's phone is powered off. |
| U2:57 | UNICOM | The UNICOM gateway is exceptional internally. |
| U2:58 | UNICOM | The recipient's phone is exceptional. |
| U2:59 | UNICOM | The UNICOM gateway is exceptional internally. |
| U2:61 | UNICOM  | The recipient's mobile number does not exist, or the recipient's phone is powered off.  |
| U2:63 | UNICOM | The carrier's gateway is exceptional. |
| U2:66                | UNICOM | The recipient's phone has a storage exception.   |
| U2:67 | UNICOM | The recipient's mobile number does not exist. |
| U2:69                | UNICOM  | The recipient is on the carrier's blocklist.                           |
| U2:72 | UNICOM | The recipient's mobile number does not exist. |
| U2:73 | UNICOM | The carrier's gateway is exceptional. |
| U2:74 | UNICOM | The recipient's phone is powered off. |
| U2:75 | UNICOM | The carrier's frequency limit is reached. |
| U2:79 | UNICOM | The recipient's mobile number is exceptional. |
| U2:80 | UNICOM | The recipient's phone is powered off. |
| U2:83 | UNICOM | The carrier's gateway is exceptional. |
| U2:86                | UNICOM | The recipient's phone has a cache exception.                          |
| U2:88        | UNICOM | The recipient's phone has a reception exception.             |
| U2:89 | UNICOM | The recipient's phone has a reception exception. |
| U2:90 | UNICOM | The carrier's gateway is exceptional. |
| U2:92 | UNICOM | The recipient's phone has a cache exception. |
| U2:93 | UNICOM | The carrier's gateway is exceptional. |
| U2:95 | UNICOM | The carrier's gateway is exceptional. |
| U2:98 | UNICOM | The recipient's mobile number is out of service. |
| U2:99 | UNICOM | The recipient's mobile number is out of service. |
| U2:100 | UNICOM | The UNICOM gateway is exceptional internally. |
| U2:106 | UNICOM | The recipient's mobile number is out of service. |
| U2:115 | UNICOM | The carrier's gateway is exceptional. |
| U2:116       | UNICOM | The recipient's phone has a reception exception.   |
| U2:117 | UNICOM | The carrier's gateway is exceptional. |
| U2:121       | UNICOM | The recipient's phone has a reception exception.   |
| U2:122 | UNICOM | The recipient's phone is exceptional. |
| U2:182               | UNICOM | The recipient's mobile number is out of service.                                   |
| U2:247               | UNICOM | The recipient's mobile number is out of service.                                   |
| U2:252 | UNICOM | The carrier's gateway is exceptional. |
| W-BLACK      | UNICOM  | The recipient is on the carrier's blocklist.             |
| XY:0000              | UNICOM  | The recipient is on the carrier's blocklist.                           |
| 006                  | TELECOM | The message is blocked by the carrier as it hits a keyword.                       |
| 010                  | TELECOM | The recipient's phone has a reception exception.                          |
| 13-19        | TELECOM | The carrier's gateway is exceptional.           |
| 23-29        | TELECOM | The carrier's gateway is exceptional.           |
| 112-116     | TELECOM | The carrier's gateway is exceptional.           |
| 128-255      | TELECOM | The carrier's gateway is exceptional.           |
| 650(660\99   | TELECOM | The frequency limit is reached.                 |
| 702                  | TELECOM | The recipient's mobile number is out of service.                                   |
| 705          | TELECOM | The recipient's mobile number is suspended.                 |
| 708                  | TELECOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.                         |
| 711                  | TELECOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.                          |
| 712                  | TELECOM | The carrier's gateway is exceptional.                         |
| 713                  | TELECOM | The message is blocked by the carrier as it hits a keyword.                       |
| 714                  | TELECOM | The recipient's mobile number is out of service, or the recipient's phone is powered off.                              |
| 716                  | TELECOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.                          |
| 717                  | TELECOM | The recipient's phone has a reception exception.                          |
| 718                  | TELECOM | The recipient's phone has a reception exception.                          |
| 726                  | TELECOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.                          |
| 731                  | TELECOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.                          |
| 760                  | TELECOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.                          |
| 762                  | TELECOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.                          |
| 771                  | TELECOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.                          |
| 779                  | TELECOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.                          |
| 999                  | TELECOM | The recipient's phone has a reception exception.                          |
| 1000         | TELECOM | The carrier's gateway is exceptional.           |
| 1107         | TELECOM | The carrier's gateway is exceptional. |
| 1509949              | TELECOM | The recipient's phone is powered off.                                    |
| ACCEPTD | TELECOM | The message has been received by the recipient. |
| BLACKMB      | TELECOM | The recipient is on the carrier's blocklist.             |
| BLACKWD              | TELECOM | The recipient is on the carrier's blocklist.                           |
| BWLISTSS163S | TELECOM | The recipient is on the carrier's blocklist. |
| DB:0612              | TELECOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.                          |
| DB:0613              | TELECOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.                          |
| DB:0614              | TELECOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.                          |
| DB:0615              | TELECOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.                          |
| DB:0618              | TELECOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.                          |
| DB:0620              | TELECOM | The recipient's phone has a reception exception.                          |
| DB:0622              | TELECOM | The carrier's gateway is exceptional.                         |
| DB:0627              | TELECOM | The carrier's gateway is exceptional.                         |
| DB:0636              | TELECOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.                          |
| DB:0640              | TELECOM | The recipient's mobile number does not exist.                                   |
| DB:0650              | TELECOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.                          |
| DB:0899              | TELECOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.                          |
| DB:0999              | TELECOM | The recipient's phone has a reception exception.                          |
| DB:1037              | TELECOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.                          |
| DELIVER      | TELECOM | The recipient's mobile number does not exist.                     |
| E:ODSL               | TELECOM | The carrier's frequency limit is reached.                         |
| ERR:601 | TELECOM | The recipient's mobile number is out of service.  |
| ERR:602              | TELECOM | The recipient's phone is powered off.                                    |
| ERR:612              | TELECOM | The message is blocked by the carrier as it hits a keyword.                       |
| ERR:613              | TELECOM | The recipient's mobile number does not exist.                                   |
| ERR:615              | TELECOM | The recipient's phone is powered off.                                    |
| ERR:617              | TELECOM | The recipient's phone has a reception exception.                          |
| ERR:618              | TELECOM | The recipient's phone has a reception exception.                          |
| ERR:627              | TELECOM | The recipient's phone has a reception exception.                          |
| ERR:640              | TELECOM | The recipient's mobile number does not exist.                                   |
| ERR:660              | TELECOM | The recipient's phone has a reception exception.                          |
| EXPIRED_76   | TELECOM | The recipient's mobile number is suspended.                 |
| EXPIREDS001S | TELECOM | The recipient's phone has a cache exception. |
| EXPIREDS010S | TELECOM | The recipient's phone is powered off.  |
| EXPIREDS601S | TELECOM | The recipient's mobile number is out of service.  |
| EXPIREDS602S | TELECOM | The recipient's phone is powered off.  |
| EXPIREDS608S | TELECOM | The recipient's phone is powered off.  |
| EXPIREDS612S | TELECOM | The recipient's phone has a reception exception.|
| EXPIREDS613S | TELECOM | The recipient's phone has a reception exception.|
| EXPIREDS614S         | TELECOM | The recipient's phone has a reception exception.                          |
| EXPIREDS615S | TELECOM | The recipient's phone has a reception exception.|
| EXPIREDS616S | TELECOM | The recipient's phone has a reception exception.  |
| EXPIREDS617S | TELECOM | The recipient's phone has a reception exception.|
| EXPIREDS618S | TELECOM | The recipient's phone has a reception exception.|
| EXPIREDS619S         | TELECOM | The recipient's phone has a reception exception.                          |
| EXPIREDS622S         | TELECOM | The recipient's phone has a reception exception.                          |
| EXPIREDS636S | TELECOM | The recipient's phone has a reception exception.  |
| EXPIREDS640S | TELECOM | The recipient's mobile number does not exist. |
| EXPIREDS650S | TELECOM | The recipient's phone has a reception exception.|
| EXPIREDS660S | TELECOM | The recipient's phone is powered off.  |
| EXPIREDS702S | TELECOM | The recipient's phone is powered off.  |
| EXPIREDS705S | TELECOM | The recipient's mobile number is out of service.  |
| EXPIREDS711S | TELECOM | The recipient's mobile number does not exist.                     |
| EXPIREDS712S         | TELECOM | The recipient's phone has a reception exception.                          |
| EXPIREDS713S         | TELECOM | The recipient's phone has a storage exception.                           |
| EXPIREDS714S | TELECOM | No acknowledgment information is received. The recipient is recommended to clear the phone cache. |
| EXPIREDS716S | TELECOM | The recipient's phone has a reception exception.  |
| EXPIREDS717S | TELECOM | The recipient's phone has a reception exception.  |
| EXPIREDS726S         | TELECOM | The recipient's phone has a reception exception.                          |
| EXPIREDS731S | TELECOM | The recipient's phone has a reception exception.  |
| EXPIREDS760S | TELECOM | The recipient's mobile number does not exist. |
| EXPIREDS765S | TELECOM | The recipient's mobile number does not exist. |
| EXPIREO      | TELECOM | The recipient's mobile number does not exist.                     |
| F000039      | TELECOM | The carrier's gateway is exceptional.           |
| F1120                | TELECOM | The recipient is on the carrier's blocklist.                           |
| F1121                | TELECOM | The message is blocked by the carrier as it hits a keyword.                       |
| F121420              | TELECOM | The message is blocked by the carrier as it hits a keyword.                       |
| F1214H1              | TELECOM | The message is blocked by the carrier as it hits a keyword.                       |
| F1214HY              | TELECOM | The message is blocked by the carrier as it hits a keyword.                       |
| FAILED       | TELECOM | The carrier's gateway is exceptional. |
| GB:0002      | TELECOM | The frequency limit is reached.       |
| GB:0014              | TELECOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.                          |
| MBBLACK      | TELECOM | The recipient is on the carrier's blocklist.             |
| ME:-3        | TELECOM | The recipient's phone is powered off.            |
| MK:1006              | TELECOM | The carrier's gateway is exceptional.                         |
| MO:0009              | TELECOM | The message is blocked by the carrier as it hits a keyword.                       |
| MOBILEBLAC   | TELECOM | The recipient is on the carrier's blocklist.             |
| MS:0002 | TELECOM | The carrier's frequency limit is reached. |
| MS:219               | TELECOM | The recipient's phone has a reception exception.                          |
| MS:1106 | TELECOM | The recipient's phone is powered off. |
| NOPASS | TELECOM | The message is blocked by the carrier manually. |
| PBDQ                 | TELECOM | The carrier's gateway is exceptional.                         |
| RDBLACK              | TELECOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.                          |
| R:00000      | TELECOM | The recipient's mobile number does not exist.                     |
| R:00001      | TELECOM | The recipient's mobile number does not exist.                     |
| R:00005      | TELECOM | The recipient's mobile number is suspended.                 |
| R:00006      | TELECOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.           |
| R:00008      | TELECOM | The recipient's mobile number does not exist.                     |
| R:00011      | TELECOM | The recipient's phone is powered off.                      |
| R:00012      | TELECOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.           |
| R:00013      | TELECOM | The recipient's mobile number is out of service.                      |
| R:00023      | TELECOM | The recipient's phone is powered off.                      |
| R:00056      | TELECOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.           |
| R:00061      | TELECOM | The recipient's mobile number is suspended.                 |
| R:00102      | TELECOM | The recipient's mobile number is out of service.                      |
| R:00104      | TELECOM | The recipient's mobile number does not exist.                     |
| R:00168      | TELECOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.           |
| R:00601      | TELECOM | The recipient's mobile number is suspended.                 |
| R:00602      | TELECOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.           |
| R:00660      | TELECOM | The recipient's mobile number does not exist.                     |
| REFUSED      | TELECOM | The frequency limit is reached.                 |
| REJECT | TELECOM | The message is rejected by the carrier manually. |
| REJECTDS174S | TELECOM | The recipient's phone has a reception exception.    |
| REJECTDS255S         | TELECOM | The recipient's phone has a reception exception.                          |
| REJECTDS706S | TELECOM | The recipient's phone is powered off, which causes data retention. |
| REJECTDS726S | TELECOM | The recipient's phone has a reception exception.|
| REJECTDS900S | TELECOM | The recipient's phone has a cache exception.             |
| REJECTE | TELECOM | The message is blocked by the carrier manually. |
| ROUTEERR     | TELECOM | The carrier's gateway is exceptional.           |
| S::TIMEOUT | TELECOM | Submission times out. |
| SGIP:10      | TELECOM | The recipient's phone is powered off.            |
| SMGP601      | TELECOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.           |
| SMGP602      | TELECOM | The recipient's phone is powered off.                      |
| SMGP603      | TELECOM | The recipient's phone is powered off.                      |
| SMGP609      | TELECOM | The carrier's gateway is exceptional.           |
| SMGP614      | TELECOM | The recipient's phone has a reception exception.            |
| SMGP615      | TELECOM | The recipient's phone has a reception exception.            |
| SMGP624      | TELECOM | The frequency limit is reached.                 |
| SMGP627      | TELECOM | The recipient's phone has a reception exception.            |
| SMGP628      | TELECOM | The recipient's mobile number is suspended.                 |
| SMGP634      | TELECOM | The recipient's mobile number is suspended.                 |
| SMGP640      | TELECOM | The recipient's mobile number does not exist.                     |
| SMGP660      | TELECOM | The carrier's gateway is exceptional.           |
| SMGP701      | TELECOM | The recipient's mobile number does not exist.                     |
| SMGP702      | TELECOM | The recipient's phone is powered off.                      |
| SMGP703      | TELECOM | The recipient's phone is powered off.                      |
| SMGP704      | TELECOM | The carrier's gateway is exceptional.           |
| SMGP705      | TELECOM | The recipient's mobile number is out of service.                      |
| SMGP713      | TELECOM | The recipient's phone has a reception exception.            |
| SMGP714      | TELECOM | The recipient's phone has a cache exception.             |
| SMGP726      | TELECOM | The recipient's phone is exceptional.                 |
| SMGP728      | TELECOM | The recipient's phone is exceptional.                  |
| SMGP730      | TELECOM | The recipient's phone is exceptional.                  |
| SMGP801      | TELECOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.           |
| SMGP802      | TELECOM | The recipient's phone is powered off.                      |
| SMGP815      | TELECOM | The recipient's mobile number is out of service.                      |
| SMGP840      | TELECOM | The recipient's mobile number does not exist.                     |
| SMGPERR:1    | TELECOM | The recipient's phone is exceptional.                  |
| SMGPERR:10   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:11   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:12   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:13   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:14   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:15   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:16   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:17   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:18   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:19   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:2    | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:20   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:21   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:22   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:23   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:24   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:25   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:26   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:27   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:28   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:29   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:3    | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:30   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:31   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:32   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:33   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:34   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:35   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:36   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:37   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:38   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:39   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:4    | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:40   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:43   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:44   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:45   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:46   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:47   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:48   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:49   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:50   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:51   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:52   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:53   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:54   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:55   | TELECOM | The carrier's gateway is exceptional.           |
| SMGPERR:56   | TELECOM | The carrier's gateway is exceptional.           |
| SPMSERR:10   | TELECOM | The recipient's mobile number does not exist.                     |
| SPMSERR:11   | TELECOM | The recipient's mobile number is suspended.                 |
| SPMSERR:12   | TELECOM | The carrier's gateway is exceptional.           |
| SPMSERR:13   | TELECOM | The carrier's gateway is exceptional.           |
| SPMSERR:14   | TELECOM | The carrier's gateway is exceptional.           |
| SPMSERR:15   | TELECOM | The carrier's gateway is exceptional.           |
| SPMSERR:16   | TELECOM | The carrier's gateway is exceptional.           |
| SPMSERR:25   | TELECOM | The carrier's gateway is exceptional.           |
| SPMSERR:30   | TELECOM | The carrier's gateway is exceptional.           |
| SPMSERR:31   | TELECOM | The carrier's gateway is exceptional.           |
| SPMSERR:99   | TELECOM | The carrier's gateway is exceptional.           |
| SUBFAIL      | TELECOM | The carrier's gateway is exceptional.           |
| SUPERWD              | TELECOM | The recipient's mobile number does not exist or is out of service, or the recipient's phone is powered off.                          |
| SWITCH | TELECOM | China Telecom does not support sending marketing SMS. |
| TIMEUP               | TELECOM | The carrier's gateway is exceptional.                         |
| UNDELIV_60   | TELECOM | The recipient's mobile number is suspended.                 |
| UNDELIV_64   | TELECOM | The recipient's mobile number does not exist.                     |
| UNDELIV_70   | TELECOM | The recipient's mobile number is suspended.                 |
| UNDELIV_80   | TELECOM | The recipient's mobile number is suspended.                 |
| UNDELIVS001S | TELECOM | The recipient's mobile number does not exist. |
| UNDELIVS010S | TELECOM | The recipient's phone is powered off.  |
| UNDELIVS601S | TELECOM | The recipient's mobile number does not exist. |
| UNDELIVS602S | TELECOM | The recipient's phone is powered off.  |
| UNDELIVS606S | TELECOM | The message is blocked by the carrier's gateway. |
| UNDELIVS608S | TELECOM | The carrier is exceptional internally. |
| UNDELIVS612S | TELECOM | The recipient's phone has a reception exception. The recipient is recommended to restart the phone. |
| UNDELIVS613S | TELECOM | The recipient's phone has a reception exception.|
| UNDELIVS614S | TELECOM | No acknowledgment information is received. The recipient is recommended to clear the phone cache. |
| UNDELIVS615S | TELECOM | The recipient's phone has a reception exception.|
| UNDELIVS616S         | TELECOM | The recipient's phone has a reception exception.                          |
| UNDELIVS617S | TELECOM | The recipient's phone has a reception exception.|
| UNDELIVS618S | TELECOM | The recipient's phone has a reception exception.|
| UNDELIVS619S | TELECOM | The recipient's phone has a reception exception.|
| UNDELIVS620S | TELECOM | The recipient's phone has a reception exception.|
| UNDELIVS622S | TELECOM | The recipient's phone has a reception exception.|
| UNDELIVS625S         | TELECOM | The recipient's phone has a reception exception.                          |
| UNDELIVS627S | TELECOM | The recipient's phone has a reception exception.|
| UNDELIVS634S | TELECOM | The recipient's phone has a reception exception.|
| UNDELIVS636S | TELECOM | The recipient's phone has a reception exception.|
| UNDELIVS640S | TELECOM | The recipient's mobile number does not exist. |
| UNDELIVS650S | TELECOM | The recipient's phone has a reception exception.|
| UNDELIVS660S | TELECOM | The message is blocked as it hits a keyword. |
| UNDELIVS680S | TELECOM | The recipient's mobile number is out of service.  |
| UNDELIVS701S | TELECOM | The recipient's mobile number does not exist or is out of service. |
| UNDELIVS702S | TELECOM | The recipient's phone has a reception exception.  |
| UNDELIVS704S | TELECOM | The recipient's mobile number does not exist.           |
| UNDELIVS705S | TELECOM | The recipient's mobile number is out of service.  |
| UNDELIVS706S | TELECOM | The recipient's phone is powered off.            |
| UNDELIVS707S | TELECOM | The recipient's phone has a reception exception.|
| UNDELIVS711S | TELECOM | The recipient's phone has a reception exception.|
| UNDELIVS712S | TELECOM | The recipient's phone has a reception exception.|
| UNDELIVS713S | TELECOM | No acknowledgment information is received. The recipient is recommended to clear the phone cache. |
| UNDELIVS714S | TELECOM | The recipient's phone has a reception exception.|
| UNDELIVS716S | TELECOM | The recipient's phone has a reception exception.|
| UNDELIVS717S | TELECOM | The recipient's phone has a reception exception.|
| UNDELIVS718S | TELECOM | The recipient's phone has poor reception when the message is sent. |
| UNDELIVS719S | TELECOM | The recipient's phone has a reception exception.  |
| UNDELIVS721S | TELECOM | The recipient's phone has a reception exception.            |
| UNDELIVS726S | TELECOM | The recipient's phone has a reception exception.|
| UNDELIVS730S | TELECOM | The recipient's phone has a reception exception.|
| UNDELIVS731S | TELECOM | No acknowledgment information is received. The recipient is recommended to clear the phone cache. |
| UNDELIVS761S | TELECOM | The recipient's phone has a reception exception.  |
| UNDELIVS762S | TELECOM | The recipient's phone has a reception exception.|
| UNDELIVS764S | TELECOM | The recipient's phone is powered off. |
| UNDELIVS765S | TELECOM | The recipient's mobile number does not exist. |
| UNDELIVS766S | TELECOM | The recipient's phone is powered off.  |
| UNDELIVS767S         | TELECOM | The recipient's mobile number is out of service, or the recipient's phone is powered off.                              |
| UNDELIVS768S         | TELECOM | The recipient's phone has a reception exception.                          |
| UNDELIVS771S | TELECOM | The recipient's mobile number does not exist. |
| UNDELIVS779S | TELECOM | The recipient's phone has a reception exception.|
| UNDELIVS801S | TELECOM | The recipient's mobile number is out of service.  |
| UNDELIVS802S | TELECOM | The recipient's phone is powered off.  |
| UNDELIVS812S | TELECOM | The recipient's phone has a reception exception.|
| UNDELIVS813S         | TELECOM | The recipient's phone has a reception exception.                          |
| UNDELIVS814S | TELECOM | The recipient's phone is powered off when the message is sent. |
| UNDELIVS815S | TELECOM | The recipient's phone is exceptional.  |
| UNDELIVS817S | TELECOM | The recipient's phone has a reception exception.|
| UNDELIVS819S | TELECOM | The recipient's phone has a reception exception.  |
| UNDELIVS822S         | TELECOM | The recipient's phone has a reception exception.                          |
| UNDELIVS827S | TELECOM | The recipient's phone has a reception exception.  |
| UNDELIVS836S | TELECOM | The recipient's phone has a reception exception.  |
| UNDELIVS860S | TELECOM | The recipient's mobile number does not exist. |
| UNDELIVS869S | TELECOM | The recipient's mobile number is out of service.  |
| UNDELIVS870S         | TELECOM | The recipient's mobile number does not exist.                                   |
| UNDELIVS880S | TELECOM | The recipient's phone is exceptional. The recipient is recommended to clear the cache and try again. |
| UNDELIVS899S | TELECOM | No response is returned when the message is sent. |
| UNDELIVS908S | TELECOM | Message sending is jammed during peak hours. |
| UNDELIVS999S | TELECOM | The recipient's phone is powered off.  |
| UNKNOWNS879S | TELECOM | The recipient's phone has a reception exception.  |
| WZ:9413      | TELECOM | The frequency limit is reached.                 |
| ZZ:9023 | TELECOM | The carrier's frequency limit (one message every three days) is reached. |
