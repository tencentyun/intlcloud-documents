## February 2021
<table>
	<tr>
		<th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
	</tr>
	<tr>
        <td>Released SDK 1.2.3.1</td><td>Fixed a logic error of the Huawei disable component.</td>
        <td>2021-02-04</td><td><a href="https://console.cloud.tencent.com/tpns/sdkdownload">SDK Download</a></td>
    </tr>
<tr>
</table>

## January 2021
   <table>
<tr>
    <th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
</tr>
        <td>Released SDK v1.2.3.0</td>
<td><li>Optimized the network communication protocol to support secondary message encryption.
<li>Simplified APIs for client account, tag, and attribute settings.
<li>Added the `traceId` and `templateId` fields to notification callback.
<li>Added badge logic support for new Honor phones.
<li>Fixed the ANR issue that occasionally occurred during network connection checks.</td>
        <td>2021-01-27</td>
        <td>-</td>
    </tr>
<tr>
        <td>Released SDK v1.2.2.4</td>
<td><li>Fixed the special character handling issue in Intent strings of FCM notifications.<li>Fixed other known issues.</td>
        <td>2021-01-18</td>
        <td>-</a></td>
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
        <td>Released SDK v1.2.2.0</td>
       <td><li> Unified the naming convention for account and tag operation APIs.<li> Optimized SDK error code reporting.<li> Upgraded the FCM channel protocol to enable the FCM system to take over the display of notifications sent through the FCM channel.<li> Added the support for badge coloring for messages sent through the TPNS channel.<li> Added the support for Gzip compression during network communication.<li>Fixed the exception of service unbinding that might occur in multi-thread environments.</td>
        <td>2020-11-26</td>
        <td>-</td>
    </tr>
        <tr>
        <td>Released SDK v1.2.1.3</td>
       <td><li>Optimized the internal logic.<li>Officially added the support for Huawei Push SDK v5 starting this version. Update the integration configuration as instructed in <a href="https://intl.cloud.tencent.com/document/product/1024/37176">Huawei Channel v5 Integration</a>.</td>
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
        <td>Released SDK v1.2.1.1</td>
				<td><li><b>Added user attribute</b> APIs for personalized push.</li> <li>Added the <b>in-app message</b> feature and several in-app message templates.</li><li>Optimized and updated the SO files.</li><li>Optimized the SDK internally.</li></td>
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
        <td>Released SDK v1.2.0.3</td>
       <td>Fixed known issues. </td>
        <td>2020-07-30</td>
        <td>-</a></td>
    </tr>
<tr>
        <td>Released SDK v1.2.0.2</td>
       <td>Optimized the internal logic. </td>
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
        <td>Released SDK v1.2.0.1</td>
       <td><li> Added the support for collecting statistics on vendor channel notification click events. </li> <li> Added more custom notification styles.</li> <li> Upgraded the OPPO PUSH SDK to v2.1.0.</li> </td>
        <td>2020-06-23</td>
        <td>This version involves package name changes. Please modify relevant configurations as instructed in <a href="https://intl.cloud.tencent.com/document/product/1024/30713">SDK Integration</a>:
<li>Automatic integration: pay attention to the obfuscation configuration.</li>
<li>Manual integration: pay attention to the SO files, manifest file, and obfuscation configuration.</li></td>
    </tr>
    <tr>
        <td>Released SDK v1.1.6.3</td>
        <td>Optimized third-party vendor channel integration.</td>
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
        <td>Released SDK v1.1.6.1</td>
        <td>Fixed the vulnerability with HTTPS certificate verification.</td>
        <td>2020-04-28</td>
        <td>-</a></td>
    </tr>
    <tr>
        <td>Released SDK v1.1.6.0</td>
        <td><li> Optimized the encryption protocol. </li> <li> Optimized network connection.</li> <li> Added the support for badge configuration for the Huawei channel.</li> <li> Upgraded the SDK v3.7.5 for Mi Push and SDK v3.9.0 for Meizu Push. </li><li> Added the support for Realme and Black Shark channels.</li><li> Removed the call of Beacon to get QIMEI information.</li></td>
        <td>2020-04-21</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/1024/35828">Badge Adaptation Guide</a></td>
    </tr>
    <tr>
        <td>Released SDK v1.1.5.5</td>
        <td>Fixed the issue where DCL violation occurred when an application was released in Google Play.</li></td>
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
        <td>Released SDK v1.1.5.4</td>
        <td><li> Optimized network connection.</li> <li>Added account types. </li> <li> Fixed issues with security alarming. </li> <li> Added the compatibility with XG Platform version upgrade. </li><li> Added the feature of getting QIMEI information.</li><li>Added the feature of disabling session keep-alive.</li></td>
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
        <td>Released SDK v1.1.5.3</td>
        <td><li> Optimized the network.</li> <li> Optimized security alarming.</li></td>
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
        <td>Released SDK v1.1.5.2</td>
        <td>Optimized error monitoring.</td>
        <td>2019-12-19</td>
        <td>-</td>
    </tr>
    <tr>
        <td>Released SDK v1.1.5.1</td>
        <td>Optimized crash monitoring.</td>
        <td>2019-12-12</td>
        <td>-</td>
    </tr>
    <tr>
        <td>Released SDK v1.1.5.0</td>
        <td><li> Optimized the TPNS SDK support for Huawei push.</li> <li> Upgraded the OPPO PUSH SDK to v2.0.2.</li></td>
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
        <td>Released SDK v1.1.4.0</td>
        <td><li> Added internal error reporting.</li> <li> Added the compatibility with Huawei Push v3.</li> <li> Added the compatibility with OnePlus devices.</li></td>
        <td>2019-11-21</td>
        <td>-</td>
    </tr>
    <tr>
        <td>Released SDK v1.1.3.2</td>
        <td>Optimized statistics collection.</td>
        <td>2019-11-13</td>
        <td>-</td>
    </tr>
    <tr>
        <td>Released SDK v1.1.3.1</td>
        <td>Optimized the network.</td>
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
        <td>Released SDK v1.1.3.0</td>
        <td><li> Optimized data reporting.</li> <li> Optimized logging to add the local log reporting feature.</li> <li> Added API call chaining.</li> <li> Optimized the system internally to improve resource release.</li></td>
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
        <td>Released SDK v1.1.2.1</td>
        <td><li> Optimized the notification bar display.</li> <li> Optimized some APIs.</li> <li> Added the support for audio rich media.</li> <li> Optimized the SDK internally.</li></td>
        <td>2019-09-27</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/1024/30713#.E9.9B.86.E6.88.90.E6.96.B9.E6.B3.95">Usage of audiovisual rich media</a></td>
    </tr>
</table>

