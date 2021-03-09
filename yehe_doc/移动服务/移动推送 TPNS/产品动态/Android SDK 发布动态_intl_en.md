## January 2021
   <table>
<tr>
    <th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
</tr>
<tr>
        <td>SDK v1.2.2.4 is released.</td>
<td><li>The special character handling issue in Intent strings of FCM notifications is fixed.<li>Other known issues are fixed.</td>
        <td>2021-01-18</td>
        <td><a href="https://console.cloud.tencent.com/tpns/sdkdownload">SDK Download</a></td>
    </tr>
</table>

## December 2020

<table>
<tr>
    <th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
</tr>
<tr>
        <td>SDK v1.2.2.1 is released.</td>
<td>The Intent redirection component permission vulnerability is fixed. `TpnsActivity` is modified to be non-exported.</td>
        <td>2020-12-10</td>
        <td>-</td>
    </tr>
</table>


## November 2020

<table>
<tr>
    <th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
</tr>
<tr>
        <td>SDK v1.2.2.0 is released.</td>
       <td><li> The naming convention is unified for account and tag operation APIs.<li> SDK error code reporting is optimized.<li> The FCM channel protocol is upgraded, and the display of notifications sent through the FCM channel is taken over by the system.<li> Badge coloring is supported for messages sent through the TPNS channel.<li> Gzip compression is supported during network communication.<li>The exception of service unbinding that might occur in multi-thread environments is fixed.</td>
        <td>2020-11-26</td>
        <td>-</td>
    </tr>
        <tr>
        <td>SDK v1.2.1.3 is released.</td>
       <td><li>The internal logic is optimized.<li>Huawei Push SDK v5 is officially supported staring this version. Update the integration configuration as instructed in <a href="https://intl.cloud.tencent.com/document/product/1024/37176">Huawei Channel v5 Integration</a>.</td>
        <td>2020-11-11</td>
        <td>-</td>
    </tr>
</table>


## October 2020

<table>
<tr>
    <th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
</tr>
        <tr>
        <td>SDK v1.2.1.1 is released.</td>
				<td><li><b>User attribute</b> APIs are added for personalized push.</li> <li>The <b>in-app message</b> feature and several in-app message templates are added.</li><li>The SO files are optimized and updated.</li><li>The SDK is optimized internally.</li></td>
        <td>2020-10-12</td>
        <td>-</td>
    </tr>
</table>




## July 2020

<table>
<tr>
    <th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
</tr>
        <tr>
        <td>SDK v1.2.0.3 is released</td>
       <td>Known issues are fixed. </td>
        <td>2020-07-30</td>
        <td>-</a></td>
    </tr>
<tr>
        <td>SDK v1.2.0.2 is released.</td>
       <td>The internal logic is optimized. </td>
        <td>2020-07-01</td>
        <td>-</td>
    </tr>
</table>

## June 2020

<table>
<tr>
    <th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
</tr>
<tr>
        <td>SDK v1.2.0.1 is released.</td>
       <td><li> Statistics of vendor channel notification click events can be collected. </li> <li> More custom notification styles are added.</li> <li> The SDK for OPPO PUSH is upgraded to v2.1.0.</li> </td>
        <td>2020-06-23</td>
        <td>This version involves package name changes. Please modify relevant configurations as instructed in <a href="https://intl.cloud.tencent.com/document/product/1024/30713">SDK Integration</a>:
<li>Automatic integration: pay attention to the obfuscation configuration.</li>
<li>Manual integration: pay attention to the SO files, manifest file, and obfuscation configuration.</li></td>
    </tr>
    <tr>
        <td>SDK v1.1.6.3 is released.</td>
        <td>Third-party vendor channel integration is optimized.</td>
        <td>2020-06-04</td>
        <td><a href="https://console.cloud.tencent.com/tpns/sdkdownload">-</a></td>
    </tr>
</table>

## April 2020

<table>
<tr>
    <th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
</tr>
    <tr>
        <td>SDK v1.1.6.1 is released.</td>
        <td>The vulnerability with HTTPS certificate verification is fixed.</td>
        <td>2020-04-28</td>
        <td>-</a></td>
    </tr>
    <tr>
        <td>SDK v1.1.6.0 is released.</td>
        <td><li> The encryption protocol is optimized. </li> <li> Network connection is optimized.</li> <li> Badge can now be configured for the Huawei channel.</li> <li> The SDK v3.7.5 for Mi Push and SDK v3.9.0 for Meizu Push are upgraded. </li><li> Realme and Black Shark channels are supported.</li><li> The call of Beacon to get QIMEI information is removed.</li></td>
        <td>2020-04-21</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/1024/35828">Badge Adaptation Guide</a></td>
    </tr>
    <tr>
        <td>SDK v1.1.5.5 is released.</td>
        <td>The issue where DCL violation occurred when an application was released in Google Play is fixed.</li></td>
        <td>2020-04-02</td>
        <td>-</td>
    </tr>
</table>

## March 2020
<table>
<tr>
    <th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
</tr>
    <tr>
        <td>SDK v1.1.5.4 is released.</td>
        <td><li> Network connection is optimized.</li> <li>Account types are added. </li> <li> Issues with security alarming are fixed. </li> <li> TPNS is now compatible with XG Platform version upgrade. </li><li> The feature to get QIMEI information is added.</li> </td>
        <td>2020-03-06</td>
        <td>-</td>
    </tr>
</table>



## January 2020

<table>
<tr>
    <th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
</tr>
    <tr>
        <td>SDK v1.1.5.3 is released.</td>
        <td><li> Network is optimized.</li> <li> Security alarming is optimized.</li></td>
        <td>2020-01-14</td>
        <td>-</td>
    </tr>
</table>

## December 2019

<table>
<tr>
    <th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
</tr>
    <tr>
        <td>SDK v1.1.5.2 is released.</td>
        <td>Error monitoring is optimized.</td>
        <td>2019-12-19</td>
        <td>-</td>
    </tr>
    <tr>
        <td>SDK v1.1.5.1 is released.</td>
        <td>Crash monitoring is optimized.</td>
        <td>2019-12-12</td>
        <td>-</td>
    </tr>
    <tr>
        <td>SDK v1.1.5.0 is released.</td>
        <td><li> Huawei push is optimized.</li> <li> SDK v2.0.2 for OPPO PUSH is optimized.</li></td>
        <td>2019-12-04</td>
        <td>-</td>
    </tr>
</table>

## November 2019

<table>
<tr>
    <th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
</tr>
    <tr>
        <td>SDK v1.1.4.0 is released.</td>
        <td><li> Internal error reporting is added.</li> <li> TPNS is now compatible with Huawei Push v3.</li> <li> TPNS is now compatible with OnePlus devices.</li></td>
        <td>2019-11-21</td>
        <td>-</td>
    </tr>
    <tr>
        <td>SDK v1.1.3.2 is released.</td>
        <td>Statistics are optimized.</td>
        <td>2019-11-13</td>
        <td>-</td>
    </tr>
    <tr>
        <td>SDK v1.1.3.1 is released.</td>
        <td>Network is optimized.</td>
        <td>2019-11-11</td>
        <td>-</td>
    </tr>
</table>

## October 2019

<table>
<tr>
    <th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
</tr>
    <tr>
        <td>SDK v1.1.3.0 is released.</td>
        <td><li> Data reporting is optimized.</li> <li> Logging is optimized to add the local log reporting feature.</li> <li> API chaining call is added.</li> <li> The system is optimized internally to improve resource release.</li></td>
        <td>2019-10-31</td>
        <td>-</td>
    </tr>
</table>

## September 2019

<table>
<tr>
    <th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
</tr>
    <tr>
        <td>SDK v1.1.2.1 is released.</td>
        <td><li> The notification bar display is optimized.</li> <li> Some APIs are optimized.</li> <li> Audio rich media is now supported.</li> <li> The SDK is optimized internally.</li></td>
        <td>2019-09-27</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/1024/30713#.E9.9B.86.E6.88.90.E6.96.B9.E6.B3.95">Usage of audiovisual rich media</a></td>
    </tr>
</table>

