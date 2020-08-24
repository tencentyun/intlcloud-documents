Before using LVB, you need to know the following use limits:

<table>
    <tr><th width="15%">Item</th><th width="75%">Description</th></tr>
    <tr>
        <td>LVB domain name</td>
        <td>Multiple playback and push domain names can be created under an account by default. A domain name to be added must get an ICP filing from the MIIT for service in Mainland China, and the current filing information must be normal and available.</td>
    </tr>
    <tr>
        <td>LVB push</td>
        <td>The LVB push service does not limit the push bitrate and supports common resolutions and corresponding bitrates. To avoid push lag, you are recommended to keep the bitrate below 4 Mbps.</td>
    </tr>
    <tr>
        <td>LVB playback</td>
        <td><ul style="margin-bottom:0">
            	<li>Only when the `StreamName` of the playback address is the same as that of the push address can the corresponding stream be played back.
            	<li>The number of live streaming viewers is not limited, and you can set a bandwidth limit.
            </ul></td>
    </tr>
    <tr>
        <td>Template configuration</td>
        <td>After the association with a template is successfully configured, it will take effect in 5–10 minutes.</td>
    </tr>
    <tr>
        <td>Daily billing mode switch</td>
        <td>You can select bill-by-traffic or bill-by-bandwidth for daily billing, and you can switch the billing mode only once per day (the switch will take effect on the next day).</td>
    </tr>
		    <tr>
        <td>Supported push protocols</td>
				<td>LVB supports the RTMP output protocols. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/267/7968">FAQs</a>.</td>
    </tr>
		    <tr>
        <td>Supported playback protocols</td>
        <td>LVB supports the RTMP, FLV, and HLS playback protocols. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/267/7968">FAQs</a>.</td>
    </tr>
    <tr>
        <td>Live director</td>
        <td><ul style="margin-bottom:0">
            	<li>You can create only one live director instance under one account. Only after the existing instance is deleted can a new one be added. To add multiple instances, please <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> for application. 
            	<li>You can add up to five VOD files to the VOD input playback list. 
            	<li>You can relay a stream to up to three third-party vendors.
            </ul>
        </td>
    </tr>
</table>
