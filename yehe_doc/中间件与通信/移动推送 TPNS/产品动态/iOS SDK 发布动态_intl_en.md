## September 2021

<table>
 <tr>
 <th width=20%>Update</th>
 <th width=44%>Description</th>
 <th width=16%>Release Date</th>
 <th width=20%>Documentation</th>
 </tr>
<tr>
 <td>SDK v1.3.4.1 release</td>
 <td>  
  <li> Improves the accuracy of notification bar status.</li>
  <li> Modifies the in-app messaging API.</li>
 </td>
 <td>September 10, 2021</td>
 <td><a href="https://console.cloud.tencent.com/tpns/sdkdownload">SDK Download</a></td>
 </tr>
</table>

## August 2021

<table>
 <tr>
	 <th width=20%>Update</th>
	 <th width=44%>Description</th>
	 <th width=16%>Release Date</th>
	 <th width=20%>Documentation</th>
 </tr>
 <tr>
	 <td>SDK v1.3.4.0 release</td>
	 <td>  
		 <li> Fixes the issue where the network connection occasionally fails after a persistent connection is reconnected many times.</li>
		 <li> Fixes the occasional issue of inaccurate TPNS online status caused by app redirection.</li>
		 <li> Adds support for supplementary push via in-app messages. </li>
	 </td>
	 <td>August 26, 2021</td>
	 <td><li><a href="https://console.cloud.tencent.com/tpns/sdkdownload">SDK Download</a></li>
		<li><a href="https://intl.cloud.tencent.com/document/product/1024/40597">Upgrade Guide</a></li>
	 </td>
 </tr>
 </table>


## July 2021

<table>
 <tr>
	 <th width=20%>Update</th>
	 <th width=44%>Description</th>
	 <th width=16%>Release Date</th>
	 <th width=20%>Documentation</th>
 </tr>
 <tr>
	 <td>SDK v1.3.3.0 release</td>
	 <td>  
		<li> Fixes the issue where cluster switching does not take effect in real time.</li>
		<li> Fixes the issue of inaccurate binding when tag APIs are called frequently.</li>
		<li> Upgrades the SDK deployment target to version 9.0.</li>
		<li> Improves the performance of account binding and registration callback.</li>
		<li> Adds support for the `show_type` field of RESTful APIs. This field can be used to configure not to display notifications when the app is running in the foreground.</li>
		<li> Adds support for SSL in persistent connections.</li>
		<li> Supports the feature of identifying whether an app start is triggered by notification clicking.</li>
	 </td>
	 <td>July 06, 2021</td>
	 <td><a href="https://console.cloud.tencent.com/tpns/sdkdownload">SDK Download</a></td>
 </tr>
 </table>

## July 2021

<table>
 <tr>
	 <th width=20%>Update</th>
	 <th width=44%>Description</th>
	 <th width=16%>Release Date</th>
	 <th width=20%>Documentation</th>
 </tr>
	 <tr>
	 <td>SDK v1.3.2.1 release</td>
	 <td>  
			<li>Fixes the compatibility issue of referencing `TPNSInAppMessage.framework` under Xcode v12.5.</li>
			<li>Fixes the issue where two devices have the same TPNS token during iCloud backup and restoration.</li>
			<li>Optimizes the logic to make sure that after a user switches access points, the logs of the original access point will not be reported.</li>
			<li>Adds the API for binding mobile numbers to send ordinary and intelligent SMS messages.</li>
			<li>The demo demonstrates the "License Agreement" before the method of push notification pop-up window.</li>
			<li>Supports log prompt when the `startXGWithAccessID` API is incorrectly called.</li>
			<li>Supports log prompt when a hook conflict between the third-party SDK and `AppDelegate` occurs.</li>
			<li>Deletes unnecessary log prompts in production environments.</li>
	 </td>
	 <td>June 1, 2021</td>
	 <td><a href="https://intl.cloud.tencent.com/document/product/1024/40597">Upgrade Guide</a></td>
 </tr>
 </table>

## April 2021

<table>
 <tr>
	 <th width=20%>Update</th>
	 <th width=44%>Description</th>
	 <th width=16%>Release Date</th>
	 <th width=20%>Documentation</th>
 </tr>
 <tr>
	 <td>SDK v1.3.1.1 release</td>
	 <td>Fixes the issue where the GCDAsync library may cause compilation conflicts.</td>
	 <td>April 19, 2021</td>
	 <td>-</li> </td>
 </tr>
 <tr>
	 <td>SDK v1.3.1.0 release</td>
	 <td>  
		<li>Fixes the issue where the audio playback rules of TPNS and APNs channels are inconsistent.</li>
		<li>Fixes the issue where the encrypted fields delivered via the cloud control emergency solution become invalid during cluster switching.</li>
		<li>Fixes the issue where sometimes statistical log reporting fails.</li>
		<li>Fixes the issue where it might fail to overwrite notifications that carried `thread-id`.</li>
		<li>Optimizes the prompts of some error logs.</li>
		<li>Improves the accuracy of the terminal's environmental verification of TPNS token.</li>
		<li>Supports automatic reissue of the badge number set when the TPNS network connection fails.</li>
		<li>Improves the arrival and reporting of silent messages to make them more timely.</li>
		<li>Supports querying tags.</li>
		<li>Supports callbacks for notification permission applications.</li>
		<li>TPNS channel supports `thread_id` message grouping.</li>
		<li>Adds sample code for global cluster switching to the demo.</li>
		<li>Adds support for callbacks for successful TPNS network connection and disconnection.</li>
	</td>
	 <td>April 12, 2021</td>
	 <td>-</td>
 </tr>
 </table>

## January 2021

<table>
 <tr>
 <th width=20%>Update</th>
 <th width=44%>Description</th>
 <th width=16%>Release Date</th>
 <th width=20%>Documentation</th>
 </tr>
 <tr>
 <td>SDK v1.3.0.0 release</td>
 <td> <li> Fixes crashes in multi-thread and low-memory scenarios.
<li>Reduces unnecessary MQTT network timeout detection.
<li>Supports a higher performance report mode for arrival.
<li>Reduces the size of the in-app message plugin package.
<li>Encrypts the request that obtains the TPNS token.
<li>Adds parameter checking logic and error callback for account, tag, and user attributes.
<li>Deletes account type enumeration and makes it customizable. 
</td>
 <td>January 25, 2021</td>
 <td>-</li> </td>
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
 <td>SDK v1.2.9.0 release</td>
 <td> <li>Fixes the image download issue for rich media push.
 <li>Fixes the TPNS channel online issue when the app runs in the background.
 <li>Fixes TPNS token repeated issue that might occur in v1.2.5.2 or earlier.
 <li>Fixes persistent connection establishment issues.
 <li>Fixes conflicting names between "in-app message" and some SDKs.
 <li>Optimizes local cache performance.
 <li>Optimizes the report time of the app notification switch status.
 <li>Optimizes the persistent connection processing mechanism in weak network scenarios.
 <li>Optimizes account APIs.
 <li>Optimizes TPNS demo code.
 <li>Adds the local notification feature.
 <li>Supports IPv6.
 <li>Deletes the compatible code of the free version. </td>
 <td>November 25, 2020</td>
 <td> - </td>
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
 <td>SDK v1.2.8.1 release</td>
 <td>Fixed known issues. </td>
 <td>October 29, 2020</td>
 <td>- </td>
 </tr>
 </table>



## September 2020

<table>
<tr>
    <th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
</tr>
    <tr>
        <td>SDK v1.2.8.0 release</td>
				<td><li>Adds <b>user attribute</b> APIs for personalized push.</li><li>Adds the <b>in-app message</b> feature and several in-app message templates.</li><li>Supports message delivery via the TPNS channel.</li><li>Fixes known issues.</li></td>
        <td>September 27, 2020</td>
        <td>-</li></td>
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
        <td>SDK v1.2.7.2 release</td>
        <td><li>Adds the custom event report feature.</li><li>Improves the success rate of reporting the number of arrivals.</li><li>Fixes known issues.</li></td>
        <td>July 23, 2020</td>
        <td>-</a></li></td>
    </tr>        
</table>



## May 2020

<table>
<tr>
    <th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
</tr>
    <tr>
        <td>SDK v1.2.6.1 release</td>
        <td><li>Improves stability and fixes known issues.</li><li>Optimizes integration and adds the registration callback method.</li><li>Adds the TPNS channel and supports message delivery via the TPNS channel when message delivery via the APNs channel fails.</li><li>Optimizes data statistics.</li></td>
        <td>May 06, 2020</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/1024/30726">Registration Callback Method</a></li></td>
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
        <td>SDK v1.2.5.4 release</td>
        <td>Improves stability and fixes known issues.</li></td>
        <td>April 22, 2020</td>
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
        <td>SDK v1.2.5.3 release</td>
        <td><li>Supports unregistering free TPNS clusters to avoid repeated pushes.</li><li>Supports replacing repeated messages in the notification extension.</li></td>
        <td>March 19, 2020</td>
        <td>Unregisters the XG platform service.</a></td>
    </tr>
    <tr>
        <td>SDK v1.2.5.2 release</td>
        <td><li>Improves push precision and adds account type enumeration.</li><li>Improves stability, optimizes log I/O, and fixes message receiving callback issue for iOS 10.</li></td>
        <td>March 06, 2020</td>
        <td>-</td>
    </tr>
</table>


## February 2020

<table>
<tr>
    <th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
</tr>
    <tr>
        <td>SDK v1.2.5.1 release</td>
        <td><li>Simplifies the integration. Deletes report APIs and uses SDK auto-processing.</li><li>Improves stability and fixes crashes caused by the caching module.</li></td>
        <td>February 20, 2020</td>
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
        <td>SDK v1.2.4.9 release</td>
        <td><li>Improves stability. Fixes crashes triggered by message statistics and a memory leak issue.</li> <li>Improves SDK compatibility.</li></td>
        <td>January 06, 2020</td>
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
        <td>SDK v1.2.4.8 release</td>
        <td>Improves stability and fixes crashes triggered by message statistics.</li></td>
        <td>December 24, 2019</td>
        <td>-</td>
    </tr>
    <tr>
        <td>SDK v1.2.4.7 release</td>
        <td> Improves stability and fixes crashes triggered by message statistics and log record.</li></td>
        <td>December 19, 2019</td>
        <td>-</td>
    </tr>
    <tr>
        <td>SDK v1.2.4.6 release</td>
        <td><li>Optimizes the SDK registration process and improves the registration success rate.</li><li>Optimizes rich media push. Supports non-suffixed resources.</li><li>Fixes known issues.</li></td>
        <td>December 16, 2019</td>
        <td>-</td>
    </tr>
    <tr>
        <td>SDK v1.2.4.5 release</td>
        <td><li>Adds crash monitoring.</li> <li>Optimizes arrival data statistics.</li><li>Optimizes the statistics of accumulated number of devices.</li><li>Optimizes SDK I/O performance.</li><li>Optimizes SDK stability.</li></td>
        <td>December 12, 2019</td>
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
        <td>SDK v1.2.4.4 release</td>
        <td>Optimizes SDK registration process. Improves message delivery.</li></td>
        <td>November 28, 2019</td>
        <td>-</td>
    </tr>
    <tr>
        <td>SDK v1.2.4.3 release</td>
        <td>Optimizes SDK compatibility.</li></td>
        <td>November 26, 2019</td>
        <td>-</td>
    </tr>
    <tr>
        <td>SDK v1.2.4.2 release</td>
        <td>Fixes the TPNS token obtaining issue via the SDK.</li></td>
        <td>November 22, 2019</td>
        <td>-</td>
    </tr>
    <tr>
        <td>SDK v1.2.4.1 release</td>
        <td><li>Adds log upload APIs.</li><li>Optimizes SDK stability.</li><li>Optimizes SDK compatibility.</li></td>
        <td>November 13, 2019</td>
        <td>-</td>
    </tr>
    <tr>
        <td>SDK v1.2.4.0 release</td>
        <td><li>Fixes the single-account binding callback issue.</li><li> Improves the compatibility between SDK and third parties.</li><li> Separates device push environments to optimize statistics.</li><li>Optimizes the caching logic for replacing app information.</li><li>Improves the SDK registration success rate.</li></td>
        <td>November 12, 2019</td>
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
        <td>SDK v1.2.3.0 release</td>
        <td>Fixes the issue that occurs when the device token changes.</li></td>
        <td>October 21, 2019</td>
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
        <td>SDK v1.2.2.1 release</td>
        <td>Fixes the network connection issue that occurs when an API is called during the SDK launch.</li></td>
        <td>September 29, 2019</td>
        <td>-</td>
    </tr>
</table>


## August 2019

<table>
<tr>
    <th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
</tr>
    <tr>
        <td>SDK v1.2.2.0 release</td>
        <td><li>Fixes the registration issue for iOS 13.</li><li>Fixes the network connection issue that occurs when the app status changes.</li></td>
        <td>August 28, 2019</td>
        <td>-</td>
    </tr>
    <tr>
        <td>SDK v1.2.1.2 release</td>
        <td><li>Fixes the statistic clicking issue.</li><li>Fixes the tag binding API issue that occurs when the network condition changes.</li></td>
        <td>August 19, 2019</td>
        <td>-</td>
    </tr>
    <tr>
        <td>SDK v1.2.1.0 release</td>
        <td><li>Adds APIs to query TPNS-generated tokens.</li><li>Fixes the single-account binding issue.</li></td>
        <td>August 08, 2019</td>
        <td>-</td>
    </tr>
</table>


## July 2019

<table>
<tr>
    <th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
</tr>
    <tr>
        <td>SDK v1.2.0.0 release</td>
        <td><li>Adds the independent statistic report SDK.</li><li>Optimizes the client register service.</li><li>Updates the parsing logic of `DeviceToken`.</li></td>
        <td>July 30, 2019</td>
        <td>-</td>
    </tr>
    <tr>
        <td>SDK v1.1.0.1 release</td>
        <td><li>Fixes the verification logic of username and password.</li><li>Fixes the SDK dynamic loading issue.</li></td>
        <td>July 25, 2019</td>
        <td>-</td>
    </tr>
    <tr>
        <td>SDK v1.1.0.0 release</td>
        <td><li>Adds the PushKit plugin.</li><li>Optimizes the SDK launch time.</li></td>
        <td>July 18, 2019</td>
        <td>-</td>
    </tr>
    <tr>
        <td>SDK v1.0.1.0 release</td>
        <td><li>Adds persistent connection push.</li><li>Improves the support for the PushKit plugin. Currently, registration, unregistration, and report are supported.</li></td>
        <td>July 11, 2019</td>
        <td>-</td>
    </tr>
    <tr>
        <td>SDK v1.0.0.0 release</td>
        <td>Initial version</li></td>
        <td>July 05, 2019</td>
        <td>-</td>
    </tr>
</table>

