## September 2021

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> 
<tr>
    <td> SDK 5.7.1435 release (enhanced edition)</td>
    <td><ul style="margin:0">
        <li> Fixed the issue where local data was not updated in time after custom group profile fields were modified.</li>
    	<li> Fixed the synchronization issue that occurred when multiple conversations were pined on top.</li>
    	<li> Fixed the issue where Android device timeout signaling did not contain the custom data entered during invitation.</li>
    	<li> Fixed the issue where empty profiles overwrote local profiles due to network request failures during non-friend profile pulling.</li>
    	<li> Fixed the issue where historical group messages could be pulled after a user left the group and then joined the group again.</li>
    	<li> Fixed the issue where the callback event `onFriendListDeleted` was called twice after a friend was deleted.</li>
    	<li> Fixed the issue where the friend remarks of the last message of a conversation were empty.</li>
    	<li> Fixed the issue where, after the IM SDK was initialized, there was no callback for a `getConversationList` API call by a user that has not logged in.</li>
    	<li> Fixed the issue where, if failed messages were sent in a group conversation after the network was disconnected, there was no unread message count displayed when the first message was received in the conversation after the network connection was restored.</li>
	<li> For more information about updates, see <a href="https://intl.cloud.tencent.com/document/product/1047/34282">Update Log (Native)</a>.</li>
    </ul></td>
    <td> September 30, 2021</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.66 release (basic edition)</td>
    <td><ul style="margin:0">
        <li> Removed the feature of getting Wi-Fi information.</li>
    </ul></td>
    <td> September 22, 2021</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.6.1202 release (enhanced edition)</td>
    <td><ul style="margin:0">
        <li> Fixed the issue where, after a user left a group and then joined the same group again, the system included the messages that were not received during this period into the unread message count of the conversation.</li>
    	<li> Fixed the issue of the failure to delete group messages that failed to be sent by muted users.</li>
    	<li> Fixed the issue where, when historical messages were pulled, the nicknames and profile photos of message senders were occasionally restored to previous ones.</li>
    	<li> Added support for setting whether to support unread message count in meeting groups.</li>
    	<li> Added support for connecting the international websites of Singapore, South Korea, and Germany to acceleration domain names.</li>
    	<li> Fixed the issue where received image messages occasionally were in incorrect image formats.</li>
    	<li> Fixed the issue where, when video messages were sent in Windows, thumbnail sending occasionally failed.</li>
    	<li> Optimized the report of the success rate of receiving ordinary group messages.</li>
    	<li> Fixed the issue where, after group members are muted in an audio-video group, the muting period obtained through getting the group member profile is 0.</li>
    </ul></td>
    <td> September 10, 2021</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
</table>

## August 2021

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> 
<tr>
    <td> SDK 5.6.1200 release (enhanced edition)</td>
    <td><ul style="margin:0">
        <li> Improved login speed.</li>
    	<li> Added support for the international websites of Singapore, South Korea, and Germany.</li>
    	<li> Added support for commercial HTTP DNS.</li>
    	<li> Optimized the group attribute logic to solve the concurrency issue that occurred when group attributes were modified on multiple devices at the same time.</li>
    	<li> Improved the message database query speed.</li>
    	<li> Improved the network connection policy.</li>
    	<li> Optimized the search of image, video, and voice messages.</li>
    	<li> Reduced the time for getting the conversation list via `getConversationList` API calls.</li>
    	<li> Removed the feature of read reporting for audio-video groups.</li>
    	<li> Unified login error codes.</li>
    	<li> Changed the friend search callback parameter `V2TIMFriendInfo` to `V2TIMFriendInfoResult` so that the friend relationship can be determined based on `relationType`.</li>
    	<li> Added the API for getting offline push configuration for the message object.</li>
    	<li> Fixed the occasional database crash during the update of user profiles.</li>
        <li> For more information about updates, see <a href="https://intl.cloud.tencent.com/document/product/1047/34282">Update Log (Native)</a>.</li>
    </ul></td>
    <td> August 31, 2021</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
</table>

## July 2021

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> 
<tr>
    <td> SDK 5.5.897 release (enhanced edition)</td>
    <td><ul style="margin:0">
	<li>Fixed occasional data reporting crashes.</li>
        <li>Removed the call of `getSimOperatorName()` for getting the carrier name.</li>
    </ul></td>
    <td> July 29, 2021 </td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.65 release (basic edition)</td>
    <td><ul style="margin:0">
        <li>Removed the call of `getSimOperatorName()` for getting the carrier name.</li>
    </ul></td>
    <td> July 29, 2021 </td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.5.892 release (enhanced edition)</td>
    <td><ul style="margin:0">
        <li> Added support for message search by multiple keywords in the logical relationship of AND or OR.</li>
    	<li> Added support for message search by sender account.</li>
    	<li> Added support for pulling historical messages of a certain time range.</li>
    	<li> Added support for pulling historical group messages by sequence.</li>
    	<li> Added notifications for message modifications by a third-party callback.</li>
    	<li> Added the API for getting the maximum number of group members allowed to the group profile.</li>
    	<li> Added the `orderKey` field for sorting conversation objects to facilitate sorting conversations without the last message at the app layer.</li>
    	<li> Optimized the audio-video group message receiving latency by making the backend complete account conversion in advance.</li>
    	<li> Upgraded the network connection scheduling protocol to reduce the network connection time outside the Chinese mainland.</li>
    	<li> Optimized the conversation list pulling logic.</li>
    	<li> Optimized the group member pulling logic and enabled local cache.</li>
    	<li> Fixed the issue where log callback was not triggered when the log level was lower than Debug.</li>
	<li> Fixed the issue where group member profiles obtained did not include friend remarks.</li>
    	<li> Fixed the issue where the obtained list of groups the user has joined contained groups to be approved by the group owner.</li>
    	<li> Fixed the stability issue reported online.</li>
    </ul></td>
    <td> July 14, 2021 </td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
</table>

## June 2021

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> 
<tr>
    <td> SDK 5.4.666 release (enhanced edition)</td>
    <td><ul style="margin:0">
        <li> Changed the name of lite edition SDK to enhanced edition SDK.</li>
    	<li> Added support for message, group, and friend search (available for the Flagship edition only).</li>
    	<li> Added a parameter to specify whether to update the last message of the conversation during message sending.</li>
    	<li> Added support for clearing the roaming messages of a conversation while retaining the conversation.</li>
    	<li> Added support for concurrent multi-device login on the same platform (available for the Flagship edition only).</li>
    	<li> Reduced the time for network connection and login.</li>
    	<li> Optimized the data reporting feature.</li>
    	<li> Optimized the offline push logic to support disabling offline push globally.</li>
    	<li> Optimized the offline push logic to allow setting the message classification field `classification` for vivo phone offline push.</li>
    	<li> Fixed the occasional incorrectness of the unread message count of one-to-one conversations.</li>
    	<li> Optimized the historical message pulling speed.</li>
    	<li> Added support for adding emojis and locations to multi-element messages.</li>
    	<li> Fixed the issue where, if an offline user changed the nickname of a group, the nickname of the corresponding conversation was not updated in a timely manner after the user logged in the next time.</li>
    	<li> Fixed the issue where the 20005 error code was occasionally reported when read messages of one-to-one conversations were reported.</li>
    </ul></td>
    <td> June 03, 2021</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
</table>

## May 2021

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> 
<tr>
    <td> SDK 5.3.435 release (lite edition)</td>
    <td><ul style="margin:0">
        <li>Added the API for deleting roaming messages in conversations.</li>
    	<li>Fixed the issue where some Android phones could not receive network status change notifications over persistent connections.</li>
    	<li>Optimized the logic for pulling user profiles to avoid requesting the backend every time when strangers request for user profiles.</li>
     	<li>Fixed the issue where group profiles and historical messages could not be obtained when the groups were deleted but conversations were retained.</li>
	<li>Fixed the issue where conversations were out of order when you got them via the API for getting conversation list.</li>
    	<li>Added the API for getting the total message unread count in conversations.</li>
    	<li>Fixed the issue where group conversations in Mute Notifications mode were filtered out when getting the total message unread count.</li>
    	<li>Fixed the occasional crashes caused by iOS HTTP requests.</li>
    </ul></td>
    <td>May 20, 2021</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.62 release (standard edition)</td>
    <td><ul style="margin:0">
        <li>Fixed known issues.</li>
    </ul></td>
    <td>May 20, 2021</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
</table>

## April 2021

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> 
<tr>
    <td> SDK 5.3.425 release (lite edition)</td>
    <td><ul style="margin:0">
        <li>Added support for pinning a conversion to the top.</li>
    	<li>Added support for setting the Mute Notifications option for one-to-one messages.</li>
    	<li>Added support for sending messages that are not counted as unread.</li>
     	<li>Added support for getting local conversation and message data when there is no network connection or your login fails.</li>
	<li>Added XCFramework (supporting Mac Catalyst) to the SDK for iOS.</li>
    	<li>Added the API for getting the total message unread count in conversations.</li>
    	<li>Added the `birthday` field to personal profiles.</li>
    	<li>Fixed the issue where, when group @ messages were recalled, the conversations of the @ target users still contained the group @ notifications.</li>
    	<li>Fixed the issue where, for some Android phones, the network would be disconnected and connected again after a successful initial network connection during persistent connections.</li>
    	<li>Fixed the issue where users could not set custom fields when creating a group in the SDK for iOS.</li>
    	<li>Fixed the issue where users with special accounts could not search for local messages via `findMessage`.</li>
    </ul></td>
    <td>April 19, 2021</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.2.212 release (lite edition)</td>
    <td><ul style="margin:0">
        <li>Fixed the issue where the SDK may be rejected by the App Store for using IDFA related keywords.</li>
    </ul></td>
    <td>April 06, 2021</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.60 release (standard edition)</td>
    <td><ul style="margin:0">
        <li>Fixed the issue where the SDK may be rejected by the App Store for using IDFA related keywords.</li>
    </ul></td>
    <td>April 06, 2021</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
</table>

## March 2021

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> 
<tr>
	<td> SDK 5.2.210 release (lite edition)</td>
	<td><ul style="margin:0">
	    <li>Added support for forwarding multiple messages as a combined single message.</li>
	    <li>Optimized the logic of persistent connections, improving the quality of connections outside Chinese mainland.</li>
	    <li>Specified login error codes in a detailed way to distinguish whether the network is normal during login.</li>
	    <li>Optimized the logic of COS upload, providing better experience of sending rich media messages.</li>
	    <li>Added the advanced API for getting historical messages.</li>
	    <li>Added the API for getting conversations in batches.</li>
		<li>Added the API for checking friend relationships in batches.</li>
		<li>For more information about updates, see <a href="https://intl.cloud.tencent.com/document/product/1047/34282">Update Log</a>.</li>
	</ul></td>
	<td>March 12, 2021</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
	<td> SDK 5.1.56 release (standard edition)</td>
	<td><ul style="margin:0">
	    <li>Fixed the issue of the Windows SDK where the client thread might block the SDK logic thread when a new message callback was triggered.</li>
	    <li>Replaced the log component of the Android SDK to improve stability.</li>
	    <li>Optimized the logic of persistent connections, improving the quality of connections outside Chinese mainland.</li>
	    <li>Optimized data reporting and specified error codes related to network timeout in a detailed way.</li>
	    <li>Fixed occasional failures of extracting logs in the iOS SDK.</li>
	    <li>Fixed several stability issues.</li>
	</ul></td>
	<td>March 03, 2021</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
</table>
## January 2021
<table>
<tr>
    <th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr>
<tr>
    <td> SDK 5.1.138 release (lite edition)</td>
    <td>
        <ul style="margin:0">
            <li>Optimized logging.</li>
	    <li>Optimized the policy of persistent connections, improving the quality of connections outside Chinese mainland.</li>
	    <li>Fixed the issue where sometimes the last message was incorrect when multiple C2C messages were sent or received in the same second.</li>
	    <li>Fixed the issue where sometimes there was be no callback for querying the conversation list.</li>
	    <li>Fixed the issue where sometimes the sequence number of a C2C message was incorrect.</li>
	    <li>Fixed the issue where sometimes a negative upload progress was displayed when a video greater than 24 MB was sent on the Android platform.</li>
	    <li>Fixed occasional crashes on the Android platform when messages were sent.</li>
        </ul>
    </td>
    <td>February 05, 2021</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.50 release (standard edition)</td>
    <td>
        <ul style="margin:0">
            	<li>V2 APIs added the `random` field for message objects.</li>
	    	<li>Added support for recalling the `lastMsg` message in a conversation.</li>
		<li>Fixed occasional exceptions in the status of the last message obtained via the `getMessage` API.</li>
		<li>Fixed the issue where messages were delayed when user profiles were frequently pulled after messages were received.</li>
		<li>Fixed the issue where deleting the account might cause the failure to pull the group member list.</li>
		<li>Fixed the issue where the message might not be found when `findMessage` was called after `insertLocalMessage`.</li>
		<li>Fixed the issue where a conversation update callback was triggered when a conversation was deleted.</li>
		<li>Fixed the issue of the Android version where the nicknames of historical group messages were not timely updated.</li>
		<li>Improved the database stability of the iOS version.</li>
		<li>For more information about updates, see <a href="https://intl.cloud.tencent.com/document/product/1047/34282">Update Log</a>.</li>
        </ul>
    </td>
    <td>February 05, 2021</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.137 release (lite edition)</td>
    <td>
        <ul style="margin:0">
            <li>Fixed the issue where sometimes there was no callback for the login API when a user logged in to the same account repeatedly on multiple iOS devices or Android devices.</li>
	    <li>Fixed occasional crashes when a low-end Android device tried to obtain the log path.</li>
        </ul>
    </td>
    <td>January 29, 2021</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.136 release (lite edition)</td>
    <td>
        <ul style="margin:0">
            <li>V2 APIs added the API for log callbacks.</li>
	    <li>Fixed the issue where the UserID of the @ target user in the group @ message was empty.</li>
	    <li>Fixed the issue where sometimes audio-video group messages could not be received.</li>
	    <li>Fixed the occasional issue of incorrect login status in the case of frequent network reconnections.</li>
	    <li>Fixed the issue where sometimes users failed to log in again after going offline and being kicked off.</li>
	    <li>Fixed occasional crashes during DNS resolution.</li>
        </ul>
    </td>
    <td>January 27, 2021</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.132 release (lite edition)</td>
    <td>
        <ul style="margin:0">
            <li>Added support for overload protection in the network module.</li>
	    <li>Fixed the issue where sometimes some sessions were lost when the standard edition was upgraded to the lite edition.</li>
	    <li>Fixed the issue where the `onUserSigExpired` callback could not be received after the login information expired.</li>
	    <li>Fixed the issue where a member received the `onMemberKicked` callback after being kicked out of a group and joining the group again.</li>
        </ul>
    </td>
    <td>January 22, 2021</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.131 release (lite edition)</td>
    <td>
        <ul style="margin:0">
            <li>Added the API for forwarding a single message.</li>
	    <li>Optimized the logic of receiving audio-video group messages. When an audio-video group receives a message, the sender's nickname and profile photo are no longer queried.</li>
	    <li>Fixed the issue where there was no conversation update notification when the last message in a conversation was deleted.</li>
	    <li>Fixed the issue where sometimes the unread messages count in C2C conversations was cleared when the C2C messages were synchronized after login.</li>
	    <li>Fixed the issue where the last message in a conversation was not updated when the conversation list was synchronized after a user went offline and then online.</li>
	    <li>Fixed the issue on the Android platform where the settings of the custom message field `description` and personal profile fields `level` and `role` did not take effect.</li>
	    <li>Fixed occasional crashes on the Android platform during deinitialization.</li>
        </ul>
    </td>
    <td>January 19, 2021</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.21 release (standard edition)</td>
    <td>
        <ul style="margin:0">
            <li>Improved internationalization support by eliminating the issue where there were Chinese characters in the English version.</li>
						<li>Fixed the issue on the Android platform where custom messages with the extended field `extension` failed to be sent.</li>
        </ul>
    </td>
    <td>January 15, 2021</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.129 release (lite edition)</td>
    <td>
        <ul style="margin:0">
            <li>Fixed the issue where a conversation update callback was triggered when a user tried to get the conversation list and there was no conversation update.</li>
            <li>Fixed the issue where the last message in a conversation was not cleared when a user tried to delete all the messages in the conversation.</li>
            <li>Fixed the issue on the iOS platform where the returned information was not `nil` when a non-signaling message was passed in using the `getSignallingInfo` method.</li>
            <li>Fixed occasional crashes on the Android platform caused by JNI local reference table exceeding the limit.</li>
        </ul>
    </td>
    <td>January 13, 2021</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.125 release (lite edition)</td>
    <td>
        <ul style="margin:0">
            <li>V2 APIs added the `random` field for message objects.</li>
            <li>V2 APIs added the `description` and `extension` fields for custom messages.</li>
            <li>V2 APIs added the `role` and `level` fields for user profile objects.</li>
            <li>Fixed the database compatibility issue in the upgrade from versions below 4.8.1 to the lite edition.</li>
            <li>Fixed the issue where sometimes users received the callbacks of messages sent by themselves.</li>
            <li>Fixed the issue where there was no callback when users tried to get the list of groups that they had joined when they hadn't joined any group.</li>
            <li>Fixed the issue where there was no conversation update callback when setting group message receiving options.</li>
            <li>Fixed the issue where sometimes there was no end callback for conversion synchronization.</li>
            <li>Fixed occasional crashes during conversion synchronization.</li>
        </ul>
    </td>
    <td>January 08, 2021</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.20 release (standard edition)</td>
    <td>
        <ul style="margin:0">
            <li>V2 custom messages added the `desc` and `ext` fields.</li>
            <li>V2 user profile APIs added the `role` and `level` fields.</li>
            <li>Optimized V2 APIs. Whether your login is successful or not, you can get the data of the local conversation list and local historical messages.</li>
            <li>V2 added the `getHistoryMessageList` API to support getting cloud or local messages and getting messages sent before or after a specific time.</li>
            <li>Optimized the issue in getting the profile photos of C2C messages.</li>
            <li>Optimized the security and renewal of rich media message file upload.</li>
            <li>Fixed the issue where the local paths of sent rich media messages were empty.</li>
            <li>Fixed the issue where when a local message was inserted into a group, the previous message was displayed as the `lastMessage` of the conversation after users logged out and logged back in.</li>
            <li>Fixed the issue where when a local message was inserted into a group, the previous message was displayed as the `lastMessage` of the conversation after users logged out and logged back in.</li>
            <li>For more information about updates, see <a href="https://intl.cloud.tencent.com/document/product/1047/34282">Update Log</a>.</li>
        </ul>
    </td>
    <td>January 08, 2021</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
</table>

## December 2020

<table>
<tr>
    <th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr>
<tr>
    <td> SDK 5.1.123 release (lite edition)</td>
    <td>
        <ul style="margin:0">
            <li> Fixed the issue where the Android edition cannot receive custom group system messages sent via the RESTful API.</li>
            <li> Optimized the method of generating the value of the `random` field for a message.</li>
            <li> Optimized log printing to facilitate troubleshooting.</li>
            <li> Fixed the issue of occasional crashes in the network module.</li>
        </ul>
    </td>
    <td>December 31, 2020</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.122 release (lite edition)</td>
    <td>
        <ul style="margin:0">
            <li> Fixed the issue where there might be no callbacks for setting conversion drafts.</li>
            <li> Fixed the issue where the message sender information was not completed when searching for messages via `findMessage`.</li>
            <li> Fixed the issue where it might fail to search for messages via `findMessage` after inserting local messages.</li>
            <li> Fixed the issue where conversation objects were not updated when setting group message receiving options.</li>
            <li> Fixed the issue where conversation change notifications were not sent when personal or group nicknames or profile photos were changed.</li>
            <li> Fixed the issue where the last message of a conversation was not updated when inserting local messages.</li>
            <li> Enabled the on-cloud control of personal profile update cycle.</li>
            <li> Fixed the issue of occasional crashes caused by improper dictionary or array operations on the iOS platform.</li>
            <li> Fixed the issue of occasional crashes when deleting messages on the Android platform.</li>
        </ul>
    </td>
    <td>December 25, 2020</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.121 release (lite edition)</td>
    <td>
        <ul style="margin:0">
            <li> Optimized the logic of pulling group profiles, so you don’t need to pull the group member information for audio-video groups.</li>
            <li> Improved log printing and added the device type field.</li>
            <li> Fixed the issue where the status of the last message in a C2C conversation was not updated when the conversation received a message recall notification.</li>
            <li> Fixed the issue where the delay of long polling messages in audio-video groups was too long.</li>
            <li> Fixed the issue where the message long polling module did not update messages and pull the key after a user logged in to the same account repeatedly and joined the same audio-video group.</li>
            <li> Fixed the issue of crashes during parsing on the signaling module of the receiver when a custom message field passed in a JSON array on the iOS platform.</li>
            <li>Fixed occasional crashes when setting conversation drafts on the Android platform.</li>
        </ul>
    </td>
    <td>December 18, 2020</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.118 release (lite edition)</td>
    <td>
        <ul style="margin:0">
            <li> Optimized the message deduplication logic and fixed the issue where repeated callbacks were triggered for the same message.</li>
            <li> Added an API for the local insertion of C2C messages.</li>
            <li> Fixed the issue where the unread group message count did not decrease when unread group messages were deleted or recalled.</li>
            <li> Fixed the issue where messages that failed to be sent could not be deleted.</li>
            <li> Fixed the issue where the deletion failure callback was triggered when a user attempted to delete a conversation for a group that the user had left or a group that had been deleted.</li>
            <li> Fixed the issue where the setting failure callback was triggered when a user attempted to enable reporting for read group messages for a group that the user had left or a group that had been deleted.</li>
            <li> Fixed the issue where setting a signature in personal profiles failed.</li>
            <li> Fixed the issue where adding a friend to a blocklist occasionally led to crashes.</li>
            <li> Fixed the issue where no message ID was returned when a message was sent.</li>
        </ul>
    </td>
    <td>December 11, 2020</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.115 release (lite edition)</td>
    <td>
        <ul style="margin:0">
            <li> Optimized the signaling timeout threshold and server time synchronization.</li>
            <li> Fixed occasional failures in establishing connections on a weak network.</li>
            <li> iOS: completed API header files.</li>
            <li> Android: fixed crashes by replacing Gson with JSON.</li>
        </ul>
    </td>
    <td>December 04, 2020</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.10 release (standard edition)</td>
    <td>
        <ul style="margin:0">
            <li> V2 APIs: added support for custom group fields and multi-element messages.</li>
            <li> V2 APIs: added an API for local insertion of C2C messages.</li>
            <li> Mitigated the issue of message loss for ordinary groups and audio-video groups.</li>
            <li> Fixed the issue where messages that failed to be sent could not be deleted.</li>
            <li> Fixed the C2C conversation issue where, if the first message was sent online, the read receipt was not received.</li>
            <li> Fixed the issue where, after a recalled message was returned through the API for pulling historical messages, the message status was incorrect.</li>
            <li> Fixed the failure to return all friend list information when ‘null’ was entered as the friend list name in the API request for obtaining friend list information on iOS.</li>
            <li> Fixed a stability issue.</li>
        </ul>
    </td>
    <td>December 04, 2020</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.111 release (lite edition)</td>
    <td>
        <ul style="margin:0">
            <li> Improved log printing.</li>
            <li> Fixed several stability issues.</li>
        </ul>
    </td>
    <td>December 01, 2020</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
</table>


## November 2020

<table>
<tr>
    <th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr>
<tr>
    <td> SDK 5.1.110 release (lite edition)</td>
    <td>
        <ul style="margin:0">
            <li> Supplemented all V2 APIs.</li>
            <li> Supplemented the conversation feature.</li>
            <li> Supplemented the relationship chain feature.</li>
            <li> Added the group @ feature.</li>
            <li> iOS now allows users to be online on both their iPhones and iPads at the same time.</li>
            <li> Added support for multi-element message sending.</li>
            <li> Supplemented custom fields in group profiles.</li>
            <li> Fixed several stability issues.</li>
        </ul>
    </td>
    <td>November 26, 2020</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.2 release (standard edition)</td>
    <td>
        <ul style="margin:0">
            <li> iOS now allows users to be online on both their iPhones and iPads at the same time.</li>
            <li> Mac added support for the ARM64 architecture.</li>
            <li> Fixed a stability issue in the Android edition.</li>
            <li> Substituted the standard TRTC dependency package.</li>
        </ul>
    </td>
    <td>November 12, 2020</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.1 release (standard edition)</td>
    <td>
        <ul style="margin:0">
            <li> Added an API to obtain the number of online users in an audio-video group (AVChatRoom).</li>
            <li> Added an API to query messages by unique ID.</li>
            <li> Added an API to obtain the server calibration timestamp.</li>
            <li> Optimized the login speed.</li>
            <li> Added support for group members to input <code>@All</code>.</li>
            <li> Added international support for TUIKit components.</li>
            <li> Added support for a small livestreaming window in group livestreaming.</li>
        </ul>
        For more information about updates, see <a href="https://intl.cloud.tencent.com/document/product/1047/34282">Update Log</a>.
    </td>
    <td>November 05, 2020</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
</table>


## October 2020

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>SDK 5.0.108 release (lite edition)</td>
<td>
    <li>Fixed a stability issue in the iOS edition.</li>
    <li>Fixed the occasional message callback failure issue for the Android edition.</li>
</td>
<td>October 23, 2020</td>
<td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a> </td>
</tr><tr>
<td> SDK 5.0.10 release (standard edition)</td>
<td><ul style="margin:0">
    <li> Optimized signaling APIs to support the setting of onlineUserOnly for online messages and offlinePushInfo for offline push messages.</li>
    <li> Optimized the async callback for the API used to obtain a single conversation.</li>
    <li> Added an API for obtaining group types for conversations to facilitate display filtering of the conversation list.</li>
    <li> Added group livestreaming features, such as co-anchoring, gifts, beauty filter, and voice changing.</li>
    <li> Added live rooms that support co-anchoring, PK, likes, gifts, beauty filter, on-screen comments, following friends, and other features.</li>
    <li> Optimized the recognition of audio and video signaling.</li>
</ul></td>
<td>October 15, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
</table>


## September 2020

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td> SDK 5.0.106 release (Android & iOS lite edition)</td>
<td>Fixed a known stability issue.</td>
<td>September 21, 2020</td>
<td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a> </td>
</tr><tr>
<td> SDK 5.0.6 release (standard edition)</td>
<td><ul style="margin:0">
    <li> Added the group @ feature.</li>
    <li>Added the deleteMessages API for iOS and Android, which will simultaneously delete local and roaming messages.</li>
    <li>When deleting a conversation, the deleteConversation API also deletes local and roaming messages.</li>
    <li>API 2.0 added APIs for setting and obtaining custom fields for user profiles, friend profiles, and group member profiles.</li></ul>
For more information about updates, see <a href="https://intl.cloud.tencent.com/document/product/1047/34282">Update Log</a>.</td>
<td>September 18, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr><tr>
<td> SDK 5.0.102 release (Android & iOS lite edition)</td>
<td><ul style="margin:0">
    <li>Released the Android & iOS lite edition SDK.</li>
    <li>Compared with the standard edition SDK, the lite edition SDK removed the friend and conversation capabilities and optimized some service logic to ensure higher execution efficiency and a smaller installation package size.</li>
</ul></td>
<td>September 04, 2020</td>
<td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download </td>
</tr>
</table>

## July 2020

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>SDK 4.9.1 release (Android, iOS, and Windows)</td>
<td><ul style="margin:0;">
    <li>Optimized login outside Chinese mainland.</li>
    <li>Fixed file upload failures in some regions outside Chinese mainland.</li>
    <li>Fixed file upload failures for accounts containing the @ symbol.</li>
    <li>Fixed occasional errors with C2C unread count.</li>
    <li>Fixed occasional exceptions in conversation showName display.</li>
    <li>Added an API for obtaining the download URL of file messages.</li>
    <li>iOS: fixed the issue where there was no callback when users attempted to obtain C2C messages without a network connection.</li>
    <li>Android: fixed occasional crashes of signaling parsing APIs.</li>
    <li>Android: fixed occasional crashes when obtaining offline push information in messages.</li>
    <li>Android: fixed the issue of no callback when API2.0 getFriendApplicationList carried no data, and fixed the issue of no callback when non-members were specified for getGroupMembersInfo.</li>
    <li>Windows: added detailed group information when users obtain the list of groups joined.</li>
    <li>Windows: fixed the failure to send small files.</li>
    <li>Windows: fixed error 6002 reported by logs.</li>
    <li>iOS Demo & Android Demo: added push of offline voice and video calls and enabled redirection to the call answering interface.</li>
    <li>iOS: fixed failure to delete or recall custom messages.</li>
    <li>iOS: changed the voice and video code swift -> oc to substantially reduce third-party dependent libraries.</li>
    <li>iOS: added support for TUIKit pod integration of two types of voice and video dependent libraries: LiteAV_TRTC and LiteAV_Professional.</li>
    <li>Android: optimized the offline push of the demo and upgraded the push SDK version for each vendor.</li>
</ul></td>
<td>July 24, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK download</a></td>
</tr> </table>


## June 2020

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>SDK 4.8.50 release (Android, iOS, and Windows)</td>
<td><ul style="margin:0;">
    <li>Fixed the API 2.0 issue where the onMemberEnter callback was not triggered when someone entered a audio-video group (AVChatRoom).</li>
    <li>Added the groupID parameter to the onGroupInfoChanged and onMemberInfoChanged callbacks of API 2.0.</li>
    <li>Fixed the issue where there was no conversation update callback after a C2C message was sent successfully.</li>
    <li>Fixed the issue where a user failed to receive messages after switching accounts and joining the same audio-video group (AVChatRoom).</li>
    <li>Fixed the issue of occasional incorrect callback sequence during unread message synchronization after login.</li>
    <li>Added signaling APIs.</li>
    <li>Added the custom group attribute API for audio-video groups (AVChatRoom).</li>
    <li>Fixed known crashes.</li>
    <li>Changed the default log storage location to /sdcard/Android/data/package name/files/log/tencent/imsdk to be compatible with Android Q versions.</li>
    <li>The Windows platform fixed group member role issues during group creation.</li>
    <li>TUIKit replaced API 2.0.</li>
    <li>Integrated TRTC to realize the voice and video call feature.</li>
    <li>iOS TUIKit added the deep-color mode.</li>
    <li>Added support for AndroidX.</li>
</ul></td>
<td>June 22, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK download</a></td>
</tr> </table>

## May 2020

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>SDK 4.8 release (Android, iOS, and Windows)</td>
<td><ul style="margin:0;">
    <li>iOS & Android launched all-new API 2.0.</li>
    <li>iOS and Android support IPv6.</li>
    <li>Audio-video groups (AVChatRoom) support dynamic updates of the group member list.</li>
    <li>Fixed xlog crashes.</li>
    <li>Fixed the failure of iOS to send big files.</li>
    <li>Fixed the exceptions that occurred when the sender’s friend remark was pulled from iOS messages.</li>
    <li>IM SDK supports AndroidX.</li>
    <li>Fixed the crashes of Android devices caused by network permission issues.</li>
</ul></td>
<td>May 15, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK download</a></td>
</tr> </table>


## March 2020

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>SDK 2.6 release (Mini Program and Web)</td>
<td><ul style="margin:0">
    <li>Web: added support for creating and sending video messages of up to 100 MB.</li>
    <li>Added the <code>nick</code> and <code>avatar</code> properties to Message to display the nickname and profile photo of the message sender in audio-video chat rooms (AVChatRoom). (updateMyProfile must be called in advance.)</li>
    <li>Web: when an account logs in on multiple instances, the C2C message recall notification can be synchronized across these instances.</li>
    <li>After updateGroupProfile is called to successfully modify custom group fields, group members can receive group prompts and obtain related content: Message.payload.newGroupProfile.groupCustomField.</li>
    <li>Deprecated the TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVED API, and replaced it with MESSAGE_RECEIVED.</li>
    <li>Fixed an occasional error that occurred when calling getGroupList.</li></ul></td>
<td>March 30, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK download</a></td>
</tr><tr>
<td>SDK 4.7 release (Android, iOS, and Windows)</td>
<td><ul style="margin:0;">
    <li>Optimized the local log size.</li>
    <li>Improved login speed.</li>
    <li>Fixed an issue with unread count synchronization across multiple devices.</li>
    <li>Added getFriendList to get single friends.</li>
    <li>You can now set the message title and content to display on the push notifications bar on iOS and Android devices respectively.</li>
</ul></td>
<td>March 23, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK download</a></td>
</tr> </table>

## February 2020

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>SDK 4.6 improvements (Android, iOS, and Windows)</td>
<td><ul style="margin:0;">
    <li>Increased the upper limit for file uploads to 100 MB.</li>
    <li>Optimized COS uploads.</li>
    <li>Improved the logic for processing pending requests for groups.</li></ul></td>
<td>February 28, 2020</td>
<td>-</td>
</tr><tr>
<td>SDK 2.5 release (Mini Program and Web)</td>
<td><ul style="margin:0;">
    <li>Added the network status change event TIM.EVENT.NET_STATE_CHANGE, which enables the access side to provide prompts and instructions.</li>
    <li>Added support for running in WeChat Mini Program plug-in environments.</li>
    <li>Reduced and optimized error codes.</li>
    <li>Fixed the issue where, after an audio-video chat room (AVChatRoom) was created in the console and a group owner was specified, messages sent by other group members would be repeated on the group owner side after the group owner joined the group.</li>
    <li>Fixed the issue where, when groups were frequently created and terminated in the console or through RESTful APIs, the SDK did not deliver the TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVED event.</li>
    <li>Fixed an occasional issue where getMessageList would fail to pull group message lists.</li></ul></td>
<td>February 28, 2020</td>
<td>-</td>
</tr> </table>

## January 2020

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>SDK 2.4 release (Mini Program and Web)</td>
<td><ul style="margin:0;">
    <li>Added the revokeMessage API to recall messages.</li>
    <li>Added the isRevoked property in Message, which identifies a recalled message when its value is true.</li>
    <li>Added TIM.EVENT.MESSAGE_REVOKED, which is the event notification for message recalls.</li>
    <li>Added force offline types of “force offline due to multi-device login” and “force offline due to UserSig expiration” in the force offline event notification TIM.EVENT.KICKED_OUT.</li>
    <li>Increased the file upload limit for createFileMessage from 20 MB to 100 MB.</li>
    <li>Group prompts msgMemberInfo and shutupTime will be deprecated. Use memberList and muteTime instead.</li>
    <li>Added the IM smart customer service entry in the console.</li>
    <li>Fixed the issue where calling the off API could not cancel listening events.</li>
    <li>Fixed the issue where the value and type of the `isRead` property in Message were incorrect.</li>
    <li>Fixed the issue where the error code and error message were incorrect when the video file in a sent video message exceeded the maximum size.</li>
    <li>Fixed an occasional issue where the field content was inaccurate after custom fields were updated.</li>
    <li>Fixed the issue where the JOIN_STATUS_ALREADY_IN_GROUP event occasionally occurred when a user logged in and joined an audio-video chat room.</li>
    <li>Fixed potential performance issues caused by core-js.</li></ul></td>
<td>January 03, 2020</td>
<td>-</td>
</tr> </table>

## December 2019
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>SDK 4.6 improvements (Android, iOS, and Windows)</td>
<td><ul style="margin:0;">
    <li>Improved the network connection quality to quickly detect changes in network quality.</li>
    <li>Optimized AVChatRoom message handling.</li>
    <li>Added the getSenderNickname API for messages.</li>
    <li>TUIKit/Demo: profile photos displayed in conversation lists can be set to have rounded corners.</li></ul></td>
<td>December 23, 2019</td>
<td>-</td>
</tr><tr>
<td>SDK 2.3 release (Mini Program and Web)</td>
<td><ul style="margin:0;">
    <li>createImageMessage and createFileMessage APIs added support for passing in File objects.</li>
    <li>Added createFaceMessage to create emoji messages.</li>
    <li>Optimized the message notification efficiency of TIM.TYPES.GRP_AVCHATROOM groups to greatly improve the user experience.</li>
    <li>Adjusted the actual error codes and error messages returned by the SDK when messages fail to be sent.</li>
    <li>Addressed the issue where, when logout was called, only the message channel of the current instance was logged out.</li>
    <li>When a callback function passed in by the access side is encapsulated for security purposes and the logic of the callback function is incorrect, errors can be captured and located quickly.</li>
    <li>The SDK provides Chinese error information when IM server-side error codes are received.</li>
    <li>Fixed the issue where messages were occasionally lost when the WeChat Mini Program went to the foreground after remaining in the background for a long time.</li>
    <li>Fixed the issue where sending a message triggered TIM.EVENT.CONVERSATION_LIST_UPDATED multiple times.</li>
    <li>Fixed the issue where the SDK reported errors when files, such as images, were uploaded and registerPlugin was not called or incorrect parameters were entered.</li>
    <li>Fixed the issue where long polling did not stop after a TIM.TYPES.GRP_AVCHATROOM group was deleted.</li>
    <li>Fixed the issue where, when "multi-instance" or "multi-client" login was enabled, other instances or clients failed to receive messages after a web instance was logged out.</li>
    <li>Fixed the issue where the SDK occasionally reported errors due to the structure of conversation lists that were pulled.</li></ul></td>
<td>December 13, 2019</td>
<td>-</td>
</tr> </table>

## November 2019
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>SDK 2.2 release (Mini Program and Web)</td>
<td><ul style="margin:0;">
    <li>Mini Programs support createVideoMessage for creating and sending video messages. Video messages can be synced across platforms (you need to update to the latest versions of the TUIKit and SDK).</li>
    <li>Added the getGroupMemberProfile API for querying group members’ profiles.</li>
    <li>Compatible with audio and file messages sent by Native IM v3.x.</li>
    <li>Added GeoPayload for receiving location messages.</li>
    <li>Fixed the issue where long polling of TIM.TYPES.GRP_AVCHATROOM groups continued after logout.</li>
    <li>Fixed the issue where the group contact cards in message instances of TIM.TYPES.GRP_AVCHATROOM groups did not have values.</li>
    <li>Fixed the issue where the Internet Explorer 10 browser would report errors.</li>
    <li>Fixed the issue where anonymous users could not join groups.</li></ul></td>
<td>November 21, 2019</td>
<td>-</td>
</tr><tr>
<td>SDK 4.6 release (Android, iOS, and Windows)</td>
<td><ul style="margin:0;">
    <li>Roaming message recalls are now supported.</li>
    <li>iOS/Mac: added OPPOChannelID settings to fix the issue where OPPO mobile phones running Android 8.0 or later failed to receive iOS push messages.</li>
    <li>iOS/Mac: optimized the annotations of objects returned by getGrouplist.</li>
    <li>The channelID for offline push of OPPO mobile phones (Android 8.0 or higher is required) can now be set in the console.</li>
    <li>TUIKit/Demo: added the video call feature.</li>
    <li>TUIKit/Demo: added 3x3 grid display of group profile photos and optimized the conversation list, contacts, and chat UI.</li></ul></td>
<td>November 13, 2019</td>
<td>-</td>
</tr><tr>
<td>Fixed pricing for message history storage</td>
<td>With fixed pricing, message history storage is easier and more cost-efficient to use.</td>
<td>November 04, 2019</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/34350">Pricing</a></td>
</tr> </table>

## October 2019
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>Launch of a new console</td>
<td>Officially launched a new edition of the IM console.</td>
<td>October 22, 2019</td>
<td><ul style="margin:0;">
    <li><a href="https://intl.cloud.tencent.com/document/product/1047/34577">Creating and Upgrading Applications</a></li>
    <li><a href="https://intl.cloud.tencent.com/document/product/1047/34540">Basic Configuration</a></li>
    <li><a href="https://intl.cloud.tencent.com/document/product/1047/34419">Feature Configuration</a></li>
    <li><a href="https://intl.cloud.tencent.com/document/product/1047/34578">Group Management</a></li>
    <li><a href="https://intl.cloud.tencent.com/document/product/1047/34520">Callback Configuration</a></li>
    <li><a href="https://intl.cloud.tencent.com/document/product/1047/34579">Statistics and Analysis</a></li>
    <li><a href="https://intl.cloud.tencent.com/document/product/1047/34580">Development Tools</a></li></ul></td>
</tr><tr>
<td>SDK 4.5 improvements (Android, iOS, and Windows)</td>
<td><ul style="margin:0;">
    <li>Added file format extension to the URL generated upon sending a file message.</li>
    <li>Added a notification callback after custom group fields are modified.</li>
    <li>Local user and group information can be obtained before login by calling the initStorage method.</li>
    <li>Android: optimized the return types of getElementCount.</li>
    <li>Windows: improved the network reconnection speeds of different platforms across platform libraries.</li>
    <li>Windows: added JVM configurations to cross-platform libraries to facilitate passing jvm from an Android environment.</li></ul></td>
<td>October 16, 2019</td>
<td>-</td>
</tr><tr>
<td>SDK 2.1 release (Mini Program and Web)</td>
<td><ul style="margin:0;">
    <li>Added support for receiving audio and video messages.</li>
    <li>Changed the maximum number of messages that can be pulled by a single call to the getMessageList API to 15.</li>
    <li>Deprecated TIM.TYPES.MSG_SOUND and replaced it with TIM.TYPES.MSG_AUDIO.</li>
    <li>Fixed the issue where the getMessageList API could not pull messages in deleted group chats.</li>
    <li>Fixed the issue where group system notifications did not show group names.</li>
    <li>Fixed the issue where a conversation created after receiving a new message did not have the profile of the message sender.</li></ul></td>
<td>October 16, 2019</td>
<td>-</td>
</tr> </table>

## September 2019
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>SDK 2.0 release (Mini Program and Web)</td>
<td>The new IM SDK for Mini Program and IM SDK for Web offer better module stability and overall connection experience, as well as visualized Demo for convenient and easy try-out by customers.</td>
<td>September 19, 2019</td>
<td>-</td>
</tr><tr>
<td>SDK 4.5 improvements (Android, iOS, and Windows)</td>
<td><ul style="margin:0;">
    <li>Android: added read receipts.</li>
    <li>Improved network connection quality.</li>
    <li>Optimized the logic for pulling custom group/group member fields.</li></ul></td>
<td>September 18, 2019</td>
<td>-</td>
</tr> </table>

## August 2019
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>SDK 4.5 release (Android, iOS, and Windows)</td>
<td><ul style="margin:0;">
    <li>Added MotionEvent.ACTION_CANCEL event handling for audio messages in chats.</li>
    <li>Added profile photo display in the conversation list, chat interface, detailed profile, and contacts.</li>
    <li>Added profile photo change in user profiles.</li>
    <li>Added Intent redirection to the offline push feature.</li>
    <li>Added random profile photos for one-to-one chats and group chats.</li>
    <li>Added prompts for granting and revoking the group admin role for a group member.</li>
    <li>Added prompts for muting and unmuting group members.</li>
    <li>Optimized the unread message count.</li>
    <li>Improved the latest conversation list loading speed after login.</li>
    <li>Added the log cleaning feature.</li>
    <li>Android: the com.tencent.imsdk.TIMGroupReceiveMessageOpt class is used in a unified manner.</li>
    <li>TUIKit/Demo: added tap feedback, allowing users to set and customize feedback in TUIKit.</li>
    <li>TUIKit/Demo: added support for sending custom messages.</li>
    <li>TUIKit/Demo: added C2C read receipts.</li>
    <li>TUIKit/Demo: added a red dot to unplayed voice messages.</li>
    <li>TUIKit/Demo: added a feature for viewing the large image by tapping the profile photo.</li>
    <li>TUIKit/Demo: adjusted the style of the small gray bar in group chats so that the member nickname becomes blue and tapping the nickname will redirect to the member's profile page.</li>
    <li>Optimized the logic for pinning a chat to the top to arrange chats in chronological order starting from the most recent.</li>
    <li>Optimized the logic for displaying nicknames in groups in the demo.</li>
    <li>Optimized the logic for displaying profile photos on the chat interface.</li>
    <li>Optimized the unread message count.</li>
    <li>Improved the latest conversation list loading speed after login.</li>
    <li>Improved the file message sending speed for users outside Chinese mainland.</li></ul></td>
<td>August 30, 2019</td>
<td>-</td>
</tr><tr>
<td>Renamed “Instant Messaging (IM)”</td>
<td>“Cloud Communication” is now “Instant Messaging (IM)”.</td>
<td>August 06, 2019</td>
<td>-</td>
</tr> </table>

## July 2019
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>SDK 4.4 improvements (Android, iOS, and Windows)</td>
<td><ul style="margin:0;">
    <li>Organized and merged some APIs.</li>
    <li>Added options to add friends in a one-way or two-way manner.</li>
    <li>Added the disableStorage API to disable all local storage.</li>
    <li>Added APIs to get the download URLs of file, video, and voice messages.</li>
    <li>Optimized the login module (repeated login/frequent login/frequent account switching/automatic connection/offline user being kicked off).</li>
    <li>Fixed the issue where it took a long time to deliver messages when the app went to the foreground after remaining in the background for a long time.</li>
    <li>Optimized the one-to-one chat unread count.</li></ul></td>
<td>July 16, 2019</td>
<td>-</td>
</tr> </table>

## June 2019
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>SDK 4.4 and new Demo release (Android, iOS, and Windows)</td>
<td><ul style="margin:0;">
    <li>Launched the TUIKit with a new mobile client UI design and product Demo.</li>
    <li>Improved Demo features such as contacts, group management, and relationship chain.</li>
    <li>Optimized the cache to mitigate UI lag.</li>
    <li>Improved the message sending efficiency.</li>
    <li>Added the JSON key for getting the unique ID of messages for cross-platform library messages.</li></ul></td>
<td>June 27, 2019</td>
<td>-</td>
</tr> </table>

## May 2019
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
            <td>SDK 4.3 improvements (Android, iOS, and Windows)</td>
<td><ul style="margin:0;">
    <li>Added querySelfProfile and queryUserProfile to the TIMFriendshipManager class (reading local data).</li>
    <li>Added the addTime field when getting a friend's profile.</li>
    <li>Added support for x86 and x86_64 architectures.</li>
    <li>Added support for custom field data reporting.</li>
    <li>Added messages that disappear after being viewed.</li>
    <li>Added use cases for recalling messages.</li>
    <li>Added the checkFriends API to verify friends.</li>
    <li>Added the queryGroupInfo API to get local data.</li>
    <li>Deprecated the getGroupDetailInfo and getGroupPublicInfo APIs and replaced them with the getGroupInfo API.</li>
    <li>Optimized the server connection strategy.</li>
    <li>Optimized the network reconnection strategy.</li>
    <li>Optimized the server overload strategy.</li>
    <li>Optimized heartbeat to reduce unnecessary outbound packets.</li>
    <li>Optimized connection requests during reconnection.</li>
    <li>Optimized the quality of first connections to different networks and access points outside Chinese mainland.</li>
    <li>Improved the network reconnection speed when iOS devices switch to Wi-Fi networks.</li>
    <li>Optimized group message synchronization.</li></ul></td>
<td>May 24, 2019</td>
<td>-</td>
</tr> </table>

## April 2019
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>SDK 4.3 release (Android, iOS, and Windows)</td>
<td><ul style="margin:0;">
    <li>Added relationship chain features such as blocklist, friend list, and friend request handling.</li>
    <li>Optimized issues related to unread counts.</li>
    <li>Optimized the message read status.</li>
    <li>Fixed disordered C2C messages sent by RESTful APIs.</li>
    <li>Fixed the occasional repeated fetching of roaming messages.</li>
    <li>Optimized the implementation issue when uniqueId is empty.</li>
    <li>Fixed the issue where TIMMessage failed to get user profiles through senderProfile.</li>
    <li>Fixed the issue with the read receipt callback and status.</li>
    <li>Fixed an issue with the synchronization of unread messages where the last message did not trigger a callback.</li>
    <li>Fixed the issue where group messages occasionally could not be received.</li>
    <li>Added support for IP connection and login information reporting.</li></ul></td>
<td>April 24, 2019</td>
<td>-</td>
</tr> </table>

## March 2019
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>SDK 4.2 release (Android, iOS, and Windows)</td>
<td><ul style="margin:0;">
    <li>iOS: TUIKit.framework supports bitcode 2.</li>
    <li>iOS: pod can directly integrate the TUIKit.framework.</li>
    <li>Windows: added the IM demo with the duilib library as a UI component.</li>
    <li>Windows: added the /source-charset:.65001 compilation option.</li>
    <li>Web: Web IM can play .amr recordings.</li>
    <li>Added the logic for adding, deleting, and querying friends.</li>
    <li>Fixed the compatibility issue with audio, file, and video messages between earlier and later versions.</li>
    <li>Optimized the audio playback logic for TUIKit.</li>
    <li>Fixed the message receiving error when an AVChatRoom had more than 100 members.</li>
    <li>Fixed ineffective group muting.</li>
    <li>Fixed the feature for modifying a user's role in a group.</li>
    <li>Fixed the issue with modifying group message receiving options.</li>
    <li>Fixed the issue with ineffective offline push toggle.</li>
    <li>Fixed the feature for modifying a user's role in a group.</li>
    <li>Fixed incorrect return results for group pending and processed requests.</li>
    <li>Fixed the issue where the client would crash when it went to the background.</li>
    <li>Fixed the issue where no messages were received after network reconnection.</li>
    <li>Fixed occasional message sorting errors.</li>
    <li>Fixed the issue where messages occasionally failed to be sent.</li>
    <li>Fixed the issue where clients did not receive relevant instructions after a group was deleted in the backend.</li></ul></td>
<td>March 2019</td>
<td>-</td>
</tr> </table>

## January 2019
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>SDK 4.0 release (Android, iOS, and Windows)</td>
<td>The new IM client SDK fixed issues with network connection, sending and receiving messages, and unread count, significantly improved the stability of important underlying modules such as network and message, and provides open source TUIKit to simplify the connection process for customers.</td>
<td>January 21, 2019</td>
<td>-</td>
</tr> </table>

## July 2017
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>Support for UGC short videos</td>
<td>Added support for UGC short video messages with video editing feature, providing better content and user experience.</td>
<td>July 2017</td>
<td>-</td>
</tr> </table>

## May 2017
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>SDK v3.0 release</td>
<td>More features, smaller size, and optimized code structure to improve customer integration efficiency and download experience.</td>
<td>May 2017</td>
<td>-</td>
</tr> </table>

## December 2016
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>Support for multi-instance force offline</td>
<td>Meets the needs for multi-instance force offline and for customer service scenario on web clients.</td>
<td>December 2016</td>
<td>-</td>
</tr> </table>

## August 2016
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>Support for broadcast messages</td>
<td>Broadcast messages can now be pushed to all members to improve message delivery efficiency and meet customers’ needs for message push.</td>
<td>August 2016</td>
<td>-</td>
</tr><tr>
<td>Support for multi-device login</td>
<td>Multi-device login is now supported to meet the need for using both mobile phone and PC, improving user experience.</td>
<td>August 2016</td>
<td>-</td>
</tr> </table>

## May 2016
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>Launch of audio-video chat rooms</td>
<td>Audio-video chat rooms with unlimited participants are now available for live streaming scenarios, providing features such as message frequency limit and custom messages.</td>
<td>May 2016</td>
<td>-</td>
</tr> </table>

## March 2016
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>Support for message push</td>
<td>Push notifications in Android and iOS are now supported to ensure message delivery and better user experience.</td>
<td>March 2016</td>
<td>-</td>
</tr> </table>

## December 2015
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>Support for short video messages</td>
<td>Short video messages are now supported, providing richer message content.</td>
<td>December 2015</td>
<td>-</td>
</tr> </table>

## August 2015
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>Support for web platform</td>   
<td>IM for web now supports custom emoji messages.</td>
<td>August 2015</td>
<td>-</td>
</tr> </table>

## July 2015
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>Support for Windows platform</td>
<td>IM for Windows now supports location and audio messages.</td>
<td>July 2015</td>
<td>-</td>
</tr> </table>

## May 2015
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>Launch of Instant Messaging IM (formerly Cloud Communication)</td>
<td>IM for Android and IM for iOS support multiple message types including text, image, and emoji.</td>
<td>May 2015</td>
<td>-</td>
</tr> </table>




## July 2021

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> 
<tr>
    <td> SDK 5.5.897 release (enhanced edition)</td>
    <td><ul style="margin:0">
	<li>Fixed occasional data reporting crashes.</li>
        <li>Removed the call of `getSimOperatorName()` for getting the carrier name.</li>
    </ul></td>
    <td> July 29, 2021 </td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.65 release (basic edition)</td>
    <td><ul style="margin:0">
        <li>Removed the call of `getSimOperatorName()` for getting the carrier name.</li>
    </ul></td>
    <td> July 29, 2021 </td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.5.892 release (enhanced edition)</td>
    <td><ul style="margin:0">
        <li> Added support for message search by multiple keywords in the logical relationship of AND or OR.</li>
    	<li> Added support for message search by sender account.</li>
    	<li> Added support for pulling historical messages of a certain time range.</li>
    	<li> Added support for pulling historical group messages by sequence.</li>
    	<li> Added notifications for message modifications by a third-party callback.</li>
    	<li> Added the API for getting the maximum number of group members allowed to the group profile.</li>
    	<li> Added the `orderKey` field for sorting conversation objects to facilitate sorting conversations without the last message at the app layer.</li>
    	<li> Optimized the audio-video group message receiving latency by making the backend complete account conversion in advance.</li>
    	<li> Upgraded the network connection scheduling protocol to reduce the network connection time outside the Chinese mainland.</li>
    	<li> Optimized the conversation list pulling logic.</li>
    	<li> Optimized the group member pulling logic and enabled local cache.</li>
    	<li> Fixed the issue where log callback was not triggered when the log level was lower than Debug.</li>
	<li> Fixed the issue where group member profiles obtained did not include friend remarks.</li>
    	<li> Fixed the issue where the obtained list of groups the user has joined contained groups to be approved by the group owner.</li>
    	<li> Fixed the stability issue reported online.</li>
    </ul></td>
    <td> July 14, 2021 </td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
</table>

## June 2021

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> 
<tr>
    <td> SDK 5.4.666 release (enhanced edition)</td>
    <td><ul style="margin:0">
        <li> Changed the name of lite edition SDK to enhanced edition SDK.</li>
    	<li> Added support for message, group, and friend search (available for the Flagship edition only).</li>
    	<li> Added a parameter to specify whether to update the last message of the conversation during message sending.</li>
    	<li> Added support for clearing the roaming messages of a conversation while retaining the conversation.</li>
    	<li> Added support for concurrent multi-device login on the same platform (available for the Flagship edition only).</li>
    	<li> Reduced the time for network connection and login.</li>
    	<li> Optimized the data reporting feature.</li>
    	<li> Optimized the offline push logic to support disabling offline push globally.</li>
    	<li> Optimized the offline push logic to allow setting the message classification field `classification` for vivo phone offline push.</li>
    	<li> Fixed the occasional incorrectness of the unread message count of one-to-one conversations.</li>
    	<li> Optimized the historical message pulling speed.</li>
    	<li> Added support for adding emojis and locations to multi-element messages.</li>
    	<li> Fixed the issue where, if an offline user changed the nickname of a group, the nickname of the corresponding conversation was not updated in a timely manner after the user logged in the next time.</li>
    	<li> Fixed the issue where the 20005 error code was occasionally reported when read messages of one-to-one conversations were reported.</li>
    </ul></td>
    <td> June 03, 2021</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
</table>

## May 2021

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> 
<tr>
    <td> SDK 5.3.435 release (lite edition)</td>
    <td><ul style="margin:0">
        <li>Added the API for deleting roaming messages in conversations.</li>
    	<li>Fixed the issue where some Android phones could not receive network status change notifications over persistent connections.</li>
    	<li>Optimized the logic for pulling user profiles to avoid requesting the backend every time when strangers request for user profiles.</li>
     	<li>Fixed the issue where group profiles and historical messages could not be obtained when the groups were deleted but conversations were retained.</li>
	<li>Fixed the issue where conversations were out of order when you got them via the API for getting conversation list.</li>
    	<li>Added the API for getting the total message unread count in conversations.</li>
    	<li>Fixed the issue where group conversations in Mute Notifications mode were filtered out when getting the total message unread count.</li>
    	<li>Fixed the occasional crashes caused by iOS HTTP requests.</li>
    </ul></td>
    <td>May 20, 2021</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.62 release (standard edition)</td>
    <td><ul style="margin:0">
        <li>Fixed known issues.</li>
    </ul></td>
    <td>May 20, 2021</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
</table>

## April 2021

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> 
<tr>
    <td> SDK 5.3.425 release (lite edition)</td>
    <td><ul style="margin:0">
        <li>Added support for pinning a conversion to the top.</li>
    	<li>Added support for setting the Mute Notifications option for one-to-one messages.</li>
    	<li>Added support for sending messages that are not counted as unread.</li>
     	<li>Added support for getting local conversation and message data when there is no network connection or your login fails.</li>
	<li>Added XCFramework (supporting Mac Catalyst) to the SDK for iOS.</li>
    	<li>Added the API for getting the total message unread count in conversations.</li>
    	<li>Added the `birthday` field to personal profiles.</li>
    	<li>Fixed the issue where, when group @ messages were recalled, the conversations of the @ target users still contained the group @ notifications.</li>
    	<li>Fixed the issue where, for some Android phones, the network would be disconnected and connected again after a successful initial network connection during persistent connections.</li>
    	<li>Fixed the issue where users could not set custom fields when creating a group in the SDK for iOS.</li>
    	<li>Fixed the issue where users with special accounts could not search for local messages via `findMessage`.</li>
    </ul></td>
    <td>April 19, 2021</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.2.212 release (lite edition)</td>
    <td><ul style="margin:0">
        <li>Fixed the issue where the SDK may be rejected by the App Store for using IDFA related keywords.</li>
    </ul></td>
    <td>April 06, 2021</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.60 release (standard edition)</td>
    <td><ul style="margin:0">
        <li>Fixed the issue where the SDK may be rejected by the App Store for using IDFA related keywords.</li>
    </ul></td>
    <td>April 06, 2021</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
</table>

## March 2021

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> 
<tr>
	<td> SDK 5.2.210 release (lite edition)</td>
	<td><ul style="margin:0">
	    <li>Added support for forwarding multiple messages as a combined single message.</li>
	    <li>Optimized the logic of persistent connections, improving the quality of connections outside Chinese mainland.</li>
	    <li>Specified login error codes in a detailed way to distinguish whether the network is normal during login.</li>
	    <li>Optimized the logic of COS upload, providing better experience of sending rich media messages.</li>
	    <li>Added the advanced API for getting historical messages.</li>
	    <li>Added the API for getting conversations in batches.</li>
		<li>Added the API for checking friend relationships in batches.</li>
		<li>For more information about updates, see <a href="https://intl.cloud.tencent.com/document/product/1047/34282">Update Log</a>.</li>
	</ul></td>
	<td>March 12, 2021</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
	<td> SDK 5.1.56 release (standard edition)</td>
	<td><ul style="margin:0">
	    <li>Fixed the issue of the Windows SDK where the client thread might block the SDK logic thread when a new message callback was triggered.</li>
	    <li>Replaced the log component of the Android SDK to improve stability.</li>
	    <li>Optimized the logic of persistent connections, improving the quality of connections outside Chinese mainland.</li>
	    <li>Optimized data reporting and specified error codes related to network timeout in a detailed way.</li>
	    <li>Fixed occasional failures of extracting logs in the iOS SDK.</li>
	    <li>Fixed several stability issues.</li>
	</ul></td>
	<td>March 03, 2021</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
</table>
## January 2021
<table>
<tr>
    <th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr>
<tr>
    <td> SDK 5.1.138 release (lite edition)</td>
    <td>
        <ul style="margin:0">
            <li>Optimized logging.</li>
	    <li>Optimized the policy of persistent connections, improving the quality of connections outside Chinese mainland.</li>
	    <li>Fixed the issue where sometimes the last message was incorrect when multiple C2C messages were sent or received in the same second.</li>
	    <li>Fixed the issue where sometimes there was be no callback for querying the conversation list.</li>
	    <li>Fixed the issue where sometimes the sequence number of a C2C message was incorrect.</li>
	    <li>Fixed the issue where sometimes a negative upload progress was displayed when a video greater than 24 MB was sent on the Android platform.</li>
	    <li>Fixed occasional crashes on the Android platform when messages were sent.</li>
        </ul>
    </td>
    <td>February 05, 2021</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.50 release (standard edition)</td>
    <td>
        <ul style="margin:0">
            	<li>V2 APIs added the `random` field for message objects.</li>
	    	<li>Added support for recalling the `lastMsg` message in a conversation.</li>
		<li>Fixed occasional exceptions in the status of the last message obtained via the `getMessage` API.</li>
		<li>Fixed the issue where messages were delayed when user profiles were frequently pulled after messages were received.</li>
		<li>Fixed the issue where deleting the account might cause the failure to pull the group member list.</li>
		<li>Fixed the issue where the message might not be found when `findMessage` was called after `insertLocalMessage`.</li>
		<li>Fixed the issue where a conversation update callback was triggered when a conversation was deleted.</li>
		<li>Fixed the issue of the Android version where the nicknames of historical group messages were not timely updated.</li>
		<li>Improved the database stability of the iOS version.</li>
		<li>For more information about updates, see <a href="https://intl.cloud.tencent.com/document/product/1047/34282">Update Log</a>.</li>
        </ul>
    </td>
    <td>February 05, 2021</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.137 release (lite edition)</td>
    <td>
        <ul style="margin:0">
            <li>Fixed the issue where sometimes there was no callback for the login API when a user logged in to the same account repeatedly on multiple iOS devices or Android devices.</li>
	    <li>Fixed occasional crashes when a low-end Android device tried to obtain the log path.</li>
        </ul>
    </td>
    <td>January 29, 2021</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.136 release (lite edition)</td>
    <td>
        <ul style="margin:0">
            <li>V2 APIs added the API for log callbacks.</li>
	    <li>Fixed the issue where the UserID of the @ target user in the group @ message was empty.</li>
	    <li>Fixed the issue where sometimes audio-video group messages could not be received.</li>
	    <li>Fixed the occasional issue of incorrect login status in the case of frequent network reconnections.</li>
	    <li>Fixed the issue where sometimes users failed to log in again after going offline and being kicked off.</li>
	    <li>Fixed occasional crashes during DNS resolution.</li>
        </ul>
    </td>
    <td>January 27, 2021</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.132 release (lite edition)</td>
    <td>
        <ul style="margin:0">
            <li>Added support for overload protection in the network module.</li>
	    <li>Fixed the issue where sometimes some sessions were lost when the standard edition was upgraded to the lite edition.</li>
	    <li>Fixed the issue where the `onUserSigExpired` callback could not be received after the login information expired.</li>
	    <li>Fixed the issue where a member received the `onMemberKicked` callback after being kicked out of a group and joining the group again.</li>
        </ul>
    </td>
    <td>January 22, 2021</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.131 release (lite edition)</td>
    <td>
        <ul style="margin:0">
            <li>Added the API for forwarding a single message.</li>
	    <li>Optimized the logic of receiving audio-video group messages. When an audio-video group receives a message, the sender's nickname and profile photo are no longer queried.</li>
	    <li>Fixed the issue where there was no conversation update notification when the last message in a conversation was deleted.</li>
	    <li>Fixed the issue where sometimes the unread messages count in C2C conversations was cleared when the C2C messages were synchronized after login.</li>
	    <li>Fixed the issue where the last message in a conversation was not updated when the conversation list was synchronized after a user went offline and then online.</li>
	    <li>Fixed the issue on the Android platform where the settings of the custom message field `description` and personal profile fields `level` and `role` did not take effect.</li>
	    <li>Fixed occasional crashes on the Android platform during deinitialization.</li>
        </ul>
    </td>
    <td>January 19, 2021</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.21 release (standard edition)</td>
    <td>
        <ul style="margin:0">
            <li>Improved internationalization support by eliminating the issue where there were Chinese characters in the English version.</li>
						<li>Fixed the issue on the Android platform where custom messages with the extended field `extension` failed to be sent.</li>
        </ul>
    </td>
    <td>January 15, 2021</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.129 release (lite edition)</td>
    <td>
        <ul style="margin:0">
            <li>Fixed the issue where a conversation update callback was triggered when a user tried to get the conversation list and there was no conversation update.</li>
            <li>Fixed the issue where the last message in a conversation was not cleared when a user tried to delete all the messages in the conversation.</li>
            <li>Fixed the issue on the iOS platform where the returned information was not `nil` when a non-signaling message was passed in using the `getSignallingInfo` method.</li>
            <li>Fixed occasional crashes on the Android platform caused by JNI local reference table exceeding the limit.</li>
        </ul>
    </td>
    <td>January 13, 2021</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.125 release (lite edition)</td>
    <td>
        <ul style="margin:0">
            <li>V2 APIs added the `random` field for message objects.</li>
            <li>V2 APIs added the `description` and `extension` fields for custom messages.</li>
            <li>V2 APIs added the `role` and `level` fields for user profile objects.</li>
            <li>Fixed the database compatibility issue in the upgrade from versions below 4.8.1 to the lite edition.</li>
            <li>Fixed the issue where sometimes users received the callbacks of messages sent by themselves.</li>
            <li>Fixed the issue where there was no callback when users tried to get the list of groups that they had joined when they hadn't joined any group.</li>
            <li>Fixed the issue where there was no conversation update callback when setting group message receiving options.</li>
            <li>Fixed the issue where sometimes there was no end callback for conversion synchronization.</li>
            <li>Fixed occasional crashes during conversion synchronization.</li>
        </ul>
    </td>
    <td>January 08, 2021</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.20 release (standard edition)</td>
    <td>
        <ul style="margin:0">
            <li>V2 custom messages added the `desc` and `ext` fields.</li>
            <li>V2 user profile APIs added the `role` and `level` fields.</li>
            <li>Optimized V2 APIs. Whether your login is successful or not, you can get the data of the local conversation list and local historical messages.</li>
            <li>V2 added the `getHistoryMessageList` API to support getting cloud or local messages and getting messages sent before or after a specific time.</li>
            <li>Optimized the issue in getting the profile photos of C2C messages.</li>
            <li>Optimized the security and renewal of rich media message file upload.</li>
            <li>Fixed the issue where the local paths of sent rich media messages were empty.</li>
            <li>Fixed the issue where when a local message was inserted into a group, the previous message was displayed as the `lastMessage` of the conversation after users logged out and logged back in.</li>
            <li>Fixed the issue where when a local message was inserted into a group, the previous message was displayed as the `lastMessage` of the conversation after users logged out and logged back in.</li>
            <li>For more information about updates, see <a href="https://intl.cloud.tencent.com/document/product/1047/34282">Update Log</a>.</li>
        </ul>
    </td>
    <td>January 08, 2021</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
</table>

## December 2020

<table>
<tr>
    <th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr>
<tr>
    <td> SDK 5.1.123 release (lite edition)</td>
    <td>
        <ul style="margin:0">
            <li> Fixed the issue where the Android edition cannot receive custom group system messages sent via the RESTful API.</li>
            <li> Optimized the method of generating the value of the `random` field for a message.</li>
            <li> Optimized log printing to facilitate troubleshooting.</li>
            <li> Fixed the issue of occasional crashes in the network module.</li>
        </ul>
    </td>
    <td>December 31, 2020</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.122 release (lite edition)</td>
    <td>
        <ul style="margin:0">
            <li> Fixed the issue where there might be no callbacks for setting conversion drafts.</li>
            <li> Fixed the issue where the message sender information was not completed when searching for messages via `findMessage`.</li>
            <li> Fixed the issue where it might fail to search for messages via `findMessage` after inserting local messages.</li>
            <li> Fixed the issue where conversation objects were not updated when setting group message receiving options.</li>
            <li> Fixed the issue where conversation change notifications were not sent when personal or group nicknames or profile photos were changed.</li>
            <li> Fixed the issue where the last message of a conversation was not updated when inserting local messages.</li>
            <li> Enabled the on-cloud control of personal profile update cycle.</li>
            <li> Fixed the issue of occasional crashes caused by improper dictionary or array operations on the iOS platform.</li>
            <li> Fixed the issue of occasional crashes when deleting messages on the Android platform.</li>
        </ul>
    </td>
    <td>December 25, 2020</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.121 release (lite edition)</td>
    <td>
        <ul style="margin:0">
            <li> Optimized the logic of pulling group profiles, so you don’t need to pull the group member information for audio-video groups.</li>
            <li> Improved log printing and added the device type field.</li>
            <li> Fixed the issue where the status of the last message in a C2C conversation was not updated when the conversation received a message recall notification.</li>
            <li> Fixed the issue where the delay of long polling messages in audio-video groups was too long.</li>
            <li> Fixed the issue where the message long polling module did not update messages and pull the key after a user logged in to the same account repeatedly and joined the same audio-video group.</li>
            <li> Fixed the issue of crashes during parsing on the signaling module of the receiver when a custom message field passed in a JSON array on the iOS platform.</li>
            <li>Fixed occasional crashes when setting conversation drafts on the Android platform.</li>
        </ul>
    </td>
    <td>December 18, 2020</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.118 release (lite edition)</td>
    <td>
        <ul style="margin:0">
            <li> Optimized the message deduplication logic and fixed the issue where repeated callbacks were triggered for the same message.</li>
            <li> Added an API for the local insertion of C2C messages.</li>
            <li> Fixed the issue where the unread group message count did not decrease when unread group messages were deleted or recalled.</li>
            <li> Fixed the issue where messages that failed to be sent could not be deleted.</li>
            <li> Fixed the issue where the deletion failure callback was triggered when a user attempted to delete a conversation for a group that the user had left or a group that had been deleted.</li>
            <li> Fixed the issue where the setting failure callback was triggered when a user attempted to enable reporting for read group messages for a group that the user had left or a group that had been deleted.</li>
            <li> Fixed the issue where setting a signature in personal profiles failed.</li>
            <li> Fixed the issue where adding a friend to a blocklist occasionally led to crashes.</li>
            <li> Fixed the issue where no message ID was returned when a message was sent.</li>
        </ul>
    </td>
    <td>December 11, 2020</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.115 release (lite edition)</td>
    <td>
        <ul style="margin:0">
            <li> Optimized the signaling timeout threshold and server time synchronization.</li>
            <li> Fixed occasional failures in establishing connections on a weak network.</li>
            <li> iOS: completed API header files.</li>
            <li> Android: fixed crashes by replacing Gson with JSON.</li>
        </ul>
    </td>
    <td>December 04, 2020</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.10 release (standard edition)</td>
    <td>
        <ul style="margin:0">
            <li> V2 APIs: added support for custom group fields and multi-element messages.</li>
            <li> V2 APIs: added an API for local insertion of C2C messages.</li>
            <li> Mitigated the issue of message loss for ordinary groups and audio-video groups.</li>
            <li> Fixed the issue where messages that failed to be sent could not be deleted.</li>
            <li> Fixed the C2C conversation issue where, if the first message was sent online, the read receipt was not received.</li>
            <li> Fixed the issue where, after a recalled message was returned through the API for pulling historical messages, the message status was incorrect.</li>
            <li> Fixed the failure to return all friend list information when ‘null’ was entered as the friend list name in the API request for obtaining friend list information on iOS.</li>
            <li> Fixed a stability issue.</li>
        </ul>
    </td>
    <td>December 04, 2020</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.111 release (lite edition)</td>
    <td>
        <ul style="margin:0">
            <li> Improved log printing.</li>
            <li> Fixed several stability issues.</li>
        </ul>
    </td>
    <td>December 01, 2020</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
</table>


## November 2020

<table>
<tr>
    <th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr>
<tr>
    <td> SDK 5.1.110 release (lite edition)</td>
    <td>
        <ul style="margin:0">
            <li> Supplemented all V2 APIs.</li>
            <li> Supplemented the conversation feature.</li>
            <li> Supplemented the relationship chain feature.</li>
            <li> Added the group @ feature.</li>
            <li> iOS now allows users to be online on both their iPhones and iPads at the same time.</li>
            <li> Added support for multi-element message sending.</li>
            <li> Supplemented custom fields in group profiles.</li>
            <li> Fixed several stability issues.</li>
        </ul>
    </td>
    <td>November 26, 2020</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.2 release (standard edition)</td>
    <td>
        <ul style="margin:0">
            <li> iOS now allows users to be online on both their iPhones and iPads at the same time.</li>
            <li> Mac added support for the ARM64 architecture.</li>
            <li> Fixed a stability issue in the Android edition.</li>
            <li> Substituted the standard TRTC dependency package.</li>
        </ul>
    </td>
    <td>November 12, 2020</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.1.1 release (standard edition)</td>
    <td>
        <ul style="margin:0">
            <li> Added an API to obtain the number of online users in an audio-video group (AVChatRoom).</li>
            <li> Added an API to query messages by unique ID.</li>
            <li> Added an API to obtain the server calibration timestamp.</li>
            <li> Optimized the login speed.</li>
            <li> Added support for group members to input <code>@All</code>.</li>
            <li> Added international support for TUIKit components.</li>
            <li> Added support for a small livestreaming window in group livestreaming.</li>
        </ul>
        For more information about updates, see <a href="https://intl.cloud.tencent.com/document/product/1047/34282">Update Log</a>.
    </td>
    <td>November 05, 2020</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
</table>


## October 2020

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>SDK 5.0.108 release (lite edition)</td>
<td>
    <li>Fixed a stability issue in the iOS edition.</li>
    <li>Fixed the occasional message callback failure issue for the Android edition.</li>
</td>
<td>October 23, 2020</td>
<td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a> </td>
</tr><tr>
<td> SDK 5.0.10 release (standard edition)</td>
<td><ul style="margin:0">
    <li> Optimized signaling APIs to support the setting of onlineUserOnly for online messages and offlinePushInfo for offline push messages.</li>
    <li> Optimized the async callback for the API used to obtain a single conversation.</li>
    <li> Added an API for obtaining group types for conversations to facilitate display filtering of the conversation list.</li>
    <li> Added group livestreaming features, such as co-anchoring, gifts, beauty filter, and voice changing.</li>
    <li> Added live rooms that support co-anchoring, PK, likes, gifts, beauty filter, on-screen comments, following friends, and other features.</li>
    <li> Optimized the recognition of audio and video signaling.</li>
</ul></td>
<td>October 15, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
</table>


## September 2020

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td> SDK 5.0.106 release (Android & iOS lite edition)</td>
<td>Fixed a known stability issue.</td>
<td>September 21, 2020</td>
<td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a> </td>
</tr><tr>
<td> SDK 5.0.6 release (standard edition)</td>
<td><ul style="margin:0">
    <li> Added the group @ feature.</li>
    <li>Added the deleteMessages API for iOS and Android, which will simultaneously delete local and roaming messages.</li>
    <li>When deleting a conversation, the deleteConversation API also deletes local and roaming messages.</li>
    <li>API 2.0 added APIs for setting and obtaining custom fields for user profiles, friend profiles, and group member profiles.</li></ul>
For more information about updates, see <a href="https://intl.cloud.tencent.com/document/product/1047/34282">Update Log</a>.</td>
<td>September 18, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr><tr>
<td> SDK 5.0.102 release (Android & iOS lite edition)</td>
<td><ul style="margin:0">
    <li>Released the Android & iOS lite edition SDK.</li>
    <li>Compared with the standard edition SDK, the lite edition SDK removed the friend and conversation capabilities and optimized some service logic to ensure higher execution efficiency and a smaller installation package size.</li>
</ul></td>
<td>September 04, 2020</td>
<td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download </td>
</tr>
</table>

## July 2020

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>SDK 4.9.1 release (Android, iOS, and Windows)</td>
<td><ul style="margin:0;">
    <li>Optimized login outside Chinese mainland.</li>
    <li>Fixed file upload failures in some regions outside Chinese mainland.</li>
    <li>Fixed file upload failures for accounts containing the @ symbol.</li>
    <li>Fixed occasional errors with C2C unread count.</li>
    <li>Fixed occasional exceptions in conversation showName display.</li>
    <li>Added an API for obtaining the download URL of file messages.</li>
    <li>iOS: fixed the issue where there was no callback when users attempted to obtain C2C messages without a network connection.</li>
    <li>Android: fixed occasional crashes of signaling parsing APIs.</li>
    <li>Android: fixed occasional crashes when obtaining offline push information in messages.</li>
    <li>Android: fixed the issue of no callback when API2.0 getFriendApplicationList carried no data, and fixed the issue of no callback when non-members were specified for getGroupMembersInfo.</li>
    <li>Windows: added detailed group information when users obtain the list of groups joined.</li>
    <li>Windows: fixed the failure to send small files.</li>
    <li>Windows: fixed error 6002 reported by logs.</li>
    <li>iOS Demo & Android Demo: added push of offline voice and video calls and enabled redirection to the call answering interface.</li>
    <li>iOS: fixed failure to delete or recall custom messages.</li>
    <li>iOS: changed the voice and video code swift -> oc to substantially reduce third-party dependent libraries.</li>
    <li>iOS: added support for TUIKit pod integration of two types of voice and video dependent libraries: LiteAV_TRTC and LiteAV_Professional.</li>
    <li>Android: optimized the offline push of the demo and upgraded the push SDK version for each vendor.</li>
</ul></td>
<td>July 24, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK download</a></td>
</tr> </table>


## June 2020

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>SDK 4.8.50 release (Android, iOS, and Windows)</td>
<td><ul style="margin:0;">
    <li>Fixed the API 2.0 issue where the onMemberEnter callback was not triggered when someone entered a audio-video group (AVChatRoom).</li>
    <li>Added the groupID parameter to the onGroupInfoChanged and onMemberInfoChanged callbacks of API 2.0.</li>
    <li>Fixed the issue where there was no conversation update callback after a C2C message was sent successfully.</li>
    <li>Fixed the issue where a user failed to receive messages after switching accounts and joining the same audio-video group (AVChatRoom).</li>
    <li>Fixed the issue of occasional incorrect callback sequence during unread message synchronization after login.</li>
    <li>Added signaling APIs.</li>
    <li>Added the custom group attribute API for audio-video groups (AVChatRoom).</li>
    <li>Fixed known crashes.</li>
    <li>Changed the default log storage location to /sdcard/Android/data/package name/files/log/tencent/imsdk to be compatible with Android Q versions.</li>
    <li>The Windows platform fixed group member role issues during group creation.</li>
    <li>TUIKit replaced API 2.0.</li>
    <li>Integrated TRTC to realize the voice and video call feature.</li>
    <li>iOS TUIKit added the deep-color mode.</li>
    <li>Added support for AndroidX.</li>
</ul></td>
<td>June 22, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK download</a></td>
</tr> </table>

## May 2020

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>SDK 4.8 release (Android, iOS, and Windows)</td>
<td><ul style="margin:0;">
    <li>iOS & Android launched all-new API 2.0.</li>
    <li>iOS and Android support IPv6.</li>
    <li>Audio-video groups (AVChatRoom) support dynamic updates of the group member list.</li>
    <li>Fixed xlog crashes.</li>
    <li>Fixed the failure of iOS to send big files.</li>
    <li>Fixed the exceptions that occurred when the sender’s friend remark was pulled from iOS messages.</li>
    <li>IM SDK supports AndroidX.</li>
    <li>Fixed the crashes of Android devices caused by network permission issues.</li>
</ul></td>
<td>May 15, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK download</a></td>
</tr> </table>


## March 2020

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>SDK 2.6 release (Mini Program and Web)</td>
<td><ul style="margin:0">
    <li>Web: added support for creating and sending video messages of up to 100 MB.</li>
    <li>Added the <code>nick</code> and <code>avatar</code> properties to Message to display the nickname and profile photo of the message sender in audio-video chat rooms (AVChatRoom). (updateMyProfile must be called in advance.)</li>
    <li>Web: when an account logs in on multiple instances, the C2C message recall notification can be synchronized across these instances.</li>
    <li>After updateGroupProfile is called to successfully modify custom group fields, group members can receive group prompts and obtain related content: Message.payload.newGroupProfile.groupCustomField.</li>
    <li>Deprecated the TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVED API, and replaced it with MESSAGE_RECEIVED.</li>
    <li>Fixed an occasional error that occurred when calling getGroupList.</li></ul></td>
<td>March 30, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK download</a></td>
</tr><tr>
<td>SDK 4.7 release (Android, iOS, and Windows)</td>
<td><ul style="margin:0;">
    <li>Optimized the local log size.</li>
    <li>Improved login speed.</li>
    <li>Fixed an issue with unread count synchronization across multiple devices.</li>
    <li>Added getFriendList to get single friends.</li>
    <li>You can now set the message title and content to display on the push notifications bar on iOS and Android devices respectively.</li>
</ul></td>
<td>March 23, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK download</a></td>
</tr> </table>

## February 2020

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>SDK 4.6 improvements (Android, iOS, and Windows)</td>
<td><ul style="margin:0;">
    <li>Increased the upper limit for file uploads to 100 MB.</li>
    <li>Optimized COS uploads.</li>
    <li>Improved the logic for processing pending requests for groups.</li></ul></td>
<td>February 28, 2020</td>
<td>-</td>
</tr><tr>
<td>SDK 2.5 release (Mini Program and Web)</td>
<td><ul style="margin:0;">
    <li>Added the network status change event TIM.EVENT.NET_STATE_CHANGE, which enables the access side to provide prompts and instructions.</li>
    <li>Added support for running in WeChat Mini Program plug-in environments.</li>
    <li>Reduced and optimized error codes.</li>
    <li>Fixed the issue where, after an audio-video chat room (AVChatRoom) was created in the console and a group owner was specified, messages sent by other group members would be repeated on the group owner side after the group owner joined the group.</li>
    <li>Fixed the issue where, when groups were frequently created and terminated in the console or through RESTful APIs, the SDK did not deliver the TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVED event.</li>
    <li>Fixed an occasional issue where getMessageList would fail to pull group message lists.</li></ul></td>
<td>February 28, 2020</td>
<td>-</td>
</tr> </table>

## January 2020

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>SDK 2.4 release (Mini Program and Web)</td>
<td><ul style="margin:0;">
    <li>Added the revokeMessage API to recall messages.</li>
    <li>Added the isRevoked property in Message, which identifies a recalled message when its value is true.</li>
    <li>Added TIM.EVENT.MESSAGE_REVOKED, which is the event notification for message recalls.</li>
    <li>Added force offline types of “force offline due to multi-device login” and “force offline due to UserSig expiration” in the force offline event notification TIM.EVENT.KICKED_OUT.</li>
    <li>Increased the file upload limit for createFileMessage from 20 MB to 100 MB.</li>
    <li>Group prompts msgMemberInfo and shutupTime will be deprecated. Use memberList and muteTime instead.</li>
    <li>Added the IM smart customer service entry in the console.</li>
    <li>Fixed the issue where calling the off API could not cancel listening events.</li>
    <li>Fixed the issue where the value and type of the `isRead` property in Message were incorrect.</li>
    <li>Fixed the issue where the error code and error message were incorrect when the video file in a sent video message exceeded the maximum size.</li>
    <li>Fixed an occasional issue where the field content was inaccurate after custom fields were updated.</li>
    <li>Fixed the issue where the JOIN_STATUS_ALREADY_IN_GROUP event occasionally occurred when a user logged in and joined an audio-video chat room.</li>
    <li>Fixed potential performance issues caused by core-js.</li></ul></td>
<td>January 03, 2020</td>
<td>-</td>
</tr> </table>

## December 2019
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>SDK 4.6 improvements (Android, iOS, and Windows)</td>
<td><ul style="margin:0;">
    <li>Improved the network connection quality to quickly detect changes in network quality.</li>
    <li>Optimized AVChatRoom message handling.</li>
    <li>Added the getSenderNickname API for messages.</li>
    <li>TUIKit/Demo: profile photos displayed in conversation lists can be set to have rounded corners.</li></ul></td>
<td>December 23, 2019</td>
<td>-</td>
</tr><tr>
<td>SDK 2.3 release (Mini Program and Web)</td>
<td><ul style="margin:0;">
    <li>createImageMessage and createFileMessage APIs added support for passing in File objects.</li>
    <li>Added createFaceMessage to create emoji messages.</li>
    <li>Optimized the message notification efficiency of TIM.TYPES.GRP_AVCHATROOM groups to greatly improve the user experience.</li>
    <li>Adjusted the actual error codes and error messages returned by the SDK when messages fail to be sent.</li>
    <li>Addressed the issue where, when logout was called, only the message channel of the current instance was logged out.</li>
    <li>When a callback function passed in by the access side is encapsulated for security purposes and the logic of the callback function is incorrect, errors can be captured and located quickly.</li>
    <li>The SDK provides Chinese error information when IM server-side error codes are received.</li>
    <li>Fixed the issue where messages were occasionally lost when the WeChat Mini Program went to the foreground after remaining in the background for a long time.</li>
    <li>Fixed the issue where sending a message triggered TIM.EVENT.CONVERSATION_LIST_UPDATED multiple times.</li>
    <li>Fixed the issue where the SDK reported errors when files, such as images, were uploaded and registerPlugin was not called or incorrect parameters were entered.</li>
    <li>Fixed the issue where long polling did not stop after a TIM.TYPES.GRP_AVCHATROOM group was deleted.</li>
    <li>Fixed the issue where, when "multi-instance" or "multi-client" login was enabled, other instances or clients failed to receive messages after a web instance was logged out.</li>
    <li>Fixed the issue where the SDK occasionally reported errors due to the structure of conversation lists that were pulled.</li></ul></td>
<td>December 13, 2019</td>
<td>-</td>
</tr> </table>

## November 2019
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>SDK 2.2 release (Mini Program and Web)</td>
<td><ul style="margin:0;">
    <li>Mini Programs support createVideoMessage for creating and sending video messages. Video messages can be synced across platforms (you need to update to the latest versions of the TUIKit and SDK).</li>
    <li>Added the getGroupMemberProfile API for querying group members’ profiles.</li>
    <li>Compatible with audio and file messages sent by Native IM v3.x.</li>
    <li>Added GeoPayload for receiving location messages.</li>
    <li>Fixed the issue where long polling of TIM.TYPES.GRP_AVCHATROOM groups continued after logout.</li>
    <li>Fixed the issue where the group contact cards in message instances of TIM.TYPES.GRP_AVCHATROOM groups did not have values.</li>
    <li>Fixed the issue where the Internet Explorer 10 browser would report errors.</li>
    <li>Fixed the issue where anonymous users could not join groups.</li></ul></td>
<td>November 21, 2019</td>
<td>-</td>
</tr><tr>
<td>SDK 4.6 release (Android, iOS, and Windows)</td>
<td><ul style="margin:0;">
    <li>Roaming message recalls are now supported.</li>
    <li>iOS/Mac: added OPPOChannelID settings to fix the issue where OPPO mobile phones running Android 8.0 or later failed to receive iOS push messages.</li>
    <li>iOS/Mac: optimized the annotations of objects returned by getGrouplist.</li>
    <li>The channelID for offline push of OPPO mobile phones (Android 8.0 or higher is required) can now be set in the console.</li>
    <li>TUIKit/Demo: added the video call feature.</li>
    <li>TUIKit/Demo: added 3x3 grid display of group profile photos and optimized the conversation list, contacts, and chat UI.</li></ul></td>
<td>November 13, 2019</td>
<td>-</td>
</tr><tr>
<td>Fixed pricing for message history storage</td>
<td>With fixed pricing, message history storage is easier and more cost-efficient to use.</td>
<td>November 04, 2019</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/34350">Pricing</a></td>
</tr> </table>

## October 2019
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>Launch of a new console</td>
<td>Officially launched a new edition of the IM console.</td>
<td>October 22, 2019</td>
<td><ul style="margin:0;">
    <li><a href="https://intl.cloud.tencent.com/document/product/1047/34577">Creating and Upgrading Applications</a></li>
    <li><a href="https://intl.cloud.tencent.com/document/product/1047/34540">Basic Configuration</a></li>
    <li><a href="https://intl.cloud.tencent.com/document/product/1047/34419">Feature Configuration</a></li>
    <li><a href="https://intl.cloud.tencent.com/document/product/1047/34578">Group Management</a></li>
    <li><a href="https://intl.cloud.tencent.com/document/product/1047/34520">Callback Configuration</a></li>
    <li><a href="https://intl.cloud.tencent.com/document/product/1047/34579">Statistics and Analysis</a></li>
    <li><a href="https://intl.cloud.tencent.com/document/product/1047/34580">Development Tools</a></li></ul></td>
</tr><tr>
<td>SDK 4.5 improvements (Android, iOS, and Windows)</td>
<td><ul style="margin:0;">
    <li>Added file format extension to the URL generated upon sending a file message.</li>
    <li>Added a notification callback after custom group fields are modified.</li>
    <li>Local user and group information can be obtained before login by calling the initStorage method.</li>
    <li>Android: optimized the return types of getElementCount.</li>
    <li>Windows: improved the network reconnection speeds of different platforms across platform libraries.</li>
    <li>Windows: added JVM configurations to cross-platform libraries to facilitate passing jvm from an Android environment.</li></ul></td>
<td>October 16, 2019</td>
<td>-</td>
</tr><tr>
<td>SDK 2.1 release (Mini Program and Web)</td>
<td><ul style="margin:0;">
    <li>Added support for receiving audio and video messages.</li>
    <li>Changed the maximum number of messages that can be pulled by a single call to the getMessageList API to 15.</li>
    <li>Deprecated TIM.TYPES.MSG_SOUND and replaced it with TIM.TYPES.MSG_AUDIO.</li>
    <li>Fixed the issue where the getMessageList API could not pull messages in deleted group chats.</li>
    <li>Fixed the issue where group system notifications did not show group names.</li>
    <li>Fixed the issue where a conversation created after receiving a new message did not have the profile of the message sender.</li></ul></td>
<td>October 16, 2019</td>
<td>-</td>
</tr> </table>

## September 2019
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>SDK 2.0 release (Mini Program and Web)</td>
<td>The new IM SDK for Mini Program and IM SDK for Web offer better module stability and overall connection experience, as well as visualized Demo for convenient and easy try-out by customers.</td>
<td>September 19, 2019</td>
<td>-</td>
</tr><tr>
<td>SDK 4.5 improvements (Android, iOS, and Windows)</td>
<td><ul style="margin:0;">
    <li>Android: added read receipts.</li>
    <li>Improved network connection quality.</li>
    <li>Optimized the logic for pulling custom group/group member fields.</li></ul></td>
<td>September 18, 2019</td>
<td>-</td>
</tr> </table>

## August 2019
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>SDK 4.5 release (Android, iOS, and Windows)</td>
<td><ul style="margin:0;">
    <li>Added MotionEvent.ACTION_CANCEL event handling for audio messages in chats.</li>
    <li>Added profile photo display in the conversation list, chat interface, detailed profile, and contacts.</li>
    <li>Added profile photo change in user profiles.</li>
    <li>Added Intent redirection to the offline push feature.</li>
    <li>Added random profile photos for one-to-one chats and group chats.</li>
    <li>Added prompts for granting and revoking the group admin role for a group member.</li>
    <li>Added prompts for muting and unmuting group members.</li>
    <li>Optimized the unread message count.</li>
    <li>Improved the latest conversation list loading speed after login.</li>
    <li>Added the log cleaning feature.</li>
    <li>Android: the com.tencent.imsdk.TIMGroupReceiveMessageOpt class is used in a unified manner.</li>
    <li>TUIKit/Demo: added tap feedback, allowing users to set and customize feedback in TUIKit.</li>
    <li>TUIKit/Demo: added support for sending custom messages.</li>
    <li>TUIKit/Demo: added C2C read receipts.</li>
    <li>TUIKit/Demo: added a red dot to unplayed voice messages.</li>
    <li>TUIKit/Demo: added a feature for viewing the large image by tapping the profile photo.</li>
    <li>TUIKit/Demo: adjusted the style of the small gray bar in group chats so that the member nickname becomes blue and tapping the nickname will redirect to the member's profile page.</li>
    <li>Optimized the logic for pinning a chat to the top to arrange chats in chronological order starting from the most recent.</li>
    <li>Optimized the logic for displaying nicknames in groups in the demo.</li>
    <li>Optimized the logic for displaying profile photos on the chat interface.</li>
    <li>Optimized the unread message count.</li>
    <li>Improved the latest conversation list loading speed after login.</li>
    <li>Improved the file message sending speed for users outside Chinese mainland.</li></ul></td>
<td>August 30, 2019</td>
<td>-</td>
</tr><tr>
<td>Renamed “Instant Messaging (IM)”</td>
<td>“Cloud Communication” is now “Instant Messaging (IM)”.</td>
<td>August 06, 2019</td>
<td>-</td>
</tr> </table>

## July 2019
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>SDK 4.4 improvements (Android, iOS, and Windows)</td>
<td><ul style="margin:0;">
    <li>Organized and merged some APIs.</li>
    <li>Added options to add friends in a one-way or two-way manner.</li>
    <li>Added the disableStorage API to disable all local storage.</li>
    <li>Added APIs to get the download URLs of file, video, and voice messages.</li>
    <li>Optimized the login module (repeated login/frequent login/frequent account switching/automatic connection/offline user being kicked off).</li>
    <li>Fixed the issue where it took a long time to deliver messages when the app went to the foreground after remaining in the background for a long time.</li>
    <li>Optimized the one-to-one chat unread count.</li></ul></td>
<td>July 16, 2019</td>
<td>-</td>
</tr> </table>

## June 2019
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>SDK 4.4 and new Demo release (Android, iOS, and Windows)</td>
<td><ul style="margin:0;">
    <li>Launched the TUIKit with a new mobile client UI design and product Demo.</li>
    <li>Improved Demo features such as contacts, group management, and relationship chain.</li>
    <li>Optimized the cache to mitigate UI lag.</li>
    <li>Improved the message sending efficiency.</li>
    <li>Added the JSON key for getting the unique ID of messages for cross-platform library messages.</li></ul></td>
<td>June 27, 2019</td>
<td>-</td>
</tr> </table>

## May 2019
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
            <td>SDK 4.3 improvements (Android, iOS, and Windows)</td>
<td><ul style="margin:0;">
    <li>Added querySelfProfile and queryUserProfile to the TIMFriendshipManager class (reading local data).</li>
    <li>Added the addTime field when getting a friend's profile.</li>
    <li>Added support for x86 and x86_64 architectures.</li>
    <li>Added support for custom field data reporting.</li>
    <li>Added messages that disappear after being viewed.</li>
    <li>Added use cases for recalling messages.</li>
    <li>Added the checkFriends API to verify friends.</li>
    <li>Added the queryGroupInfo API to get local data.</li>
    <li>Deprecated the getGroupDetailInfo and getGroupPublicInfo APIs and replaced them with the getGroupInfo API.</li>
    <li>Optimized the server connection strategy.</li>
    <li>Optimized the network reconnection strategy.</li>
    <li>Optimized the server overload strategy.</li>
    <li>Optimized heartbeat to reduce unnecessary outbound packets.</li>
    <li>Optimized connection requests during reconnection.</li>
    <li>Optimized the quality of first connections to different networks and access points outside Chinese mainland.</li>
    <li>Improved the network reconnection speed when iOS devices switch to Wi-Fi networks.</li>
    <li>Optimized group message synchronization.</li></ul></td>
<td>May 24, 2019</td>
<td>-</td>
</tr> </table>

## April 2019
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>SDK 4.3 release (Android, iOS, and Windows)</td>
<td><ul style="margin:0;">
    <li>Added relationship chain features such as blocklist, friend list, and friend request handling.</li>
    <li>Optimized issues related to unread counts.</li>
    <li>Optimized the message read status.</li>
    <li>Fixed disordered C2C messages sent by RESTful APIs.</li>
    <li>Fixed the occasional repeated fetching of roaming messages.</li>
    <li>Optimized the implementation issue when uniqueId is empty.</li>
    <li>Fixed the issue where TIMMessage failed to get user profiles through senderProfile.</li>
    <li>Fixed the issue with the read receipt callback and status.</li>
    <li>Fixed an issue with the synchronization of unread messages where the last message did not trigger a callback.</li>
    <li>Fixed the issue where group messages occasionally could not be received.</li>
    <li>Added support for IP connection and login information reporting.</li></ul></td>
<td>April 24, 2019</td>
<td>-</td>
</tr> </table>

## March 2019
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>SDK 4.2 release (Android, iOS, and Windows)</td>
<td><ul style="margin:0;">
    <li>iOS: TUIKit.framework supports bitcode 2.</li>
    <li>iOS: pod can directly integrate the TUIKit.framework.</li>
    <li>Windows: added the IM demo with the duilib library as a UI component.</li>
    <li>Windows: added the /source-charset:.65001 compilation option.</li>
    <li>Web: Web IM can play .amr recordings.</li>
    <li>Added the logic for adding, deleting, and querying friends.</li>
    <li>Fixed the compatibility issue with audio, file, and video messages between earlier and later versions.</li>
    <li>Optimized the audio playback logic for TUIKit.</li>
    <li>Fixed the message receiving error when an AVChatRoom had more than 100 members.</li>
    <li>Fixed ineffective group muting.</li>
    <li>Fixed the feature for modifying a user's role in a group.</li>
    <li>Fixed the issue with modifying group message receiving options.</li>
    <li>Fixed the issue with ineffective offline push toggle.</li>
    <li>Fixed the feature for modifying a user's role in a group.</li>
    <li>Fixed incorrect return results for group pending and processed requests.</li>
    <li>Fixed the issue where the client would crash when it went to the background.</li>
    <li>Fixed the issue where no messages were received after network reconnection.</li>
    <li>Fixed occasional message sorting errors.</li>
    <li>Fixed the issue where messages occasionally failed to be sent.</li>
    <li>Fixed the issue where clients did not receive relevant instructions after a group was deleted in the backend.</li></ul></td>
<td>March 2019</td>
<td>-</td>
</tr> </table>

## January 2019
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>SDK 4.0 release (Android, iOS, and Windows)</td>
<td>The new IM client SDK fixed issues with network connection, sending and receiving messages, and unread count, significantly improved the stability of important underlying modules such as network and message, and provides open source TUIKit to simplify the connection process for customers.</td>
<td>January 21, 2019</td>
<td>-</td>
</tr> </table>

## July 2017
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>Support for UGC short videos</td>
<td>Added support for UGC short video messages with video editing feature, providing better content and user experience.</td>
<td>July 2017</td>
<td>-</td>
</tr> </table>

## May 2017
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>SDK v3.0 release</td>
<td>More features, smaller size, and optimized code structure to improve customer integration efficiency and download experience.</td>
<td>May 2017</td>
<td>-</td>
</tr> </table>

## December 2016
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>Support for multi-instance force offline</td>
<td>Meets the needs for multi-instance force offline and for customer service scenario on web clients.</td>
<td>December 2016</td>
<td>-</td>
</tr> </table>

## August 2016
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>Support for broadcast messages</td>
<td>Broadcast messages can now be pushed to all members to improve message delivery efficiency and meet customers’ needs for message push.</td>
<td>August 2016</td>
<td>-</td>
</tr><tr>
<td>Support for multi-device login</td>
<td>Multi-device login is now supported to meet the need for using both mobile phone and PC, improving user experience.</td>
<td>August 2016</td>
<td>-</td>
</tr> </table>

## May 2016
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>Launch of audio-video chat rooms</td>
<td>Audio-video chat rooms with unlimited participants are now available for live streaming scenarios, providing features such as message frequency limit and custom messages.</td>
<td>May 2016</td>
<td>-</td>
</tr> </table>

## March 2016
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>Support for message push</td>
<td>Push notifications in Android and iOS are now supported to ensure message delivery and better user experience.</td>
<td>March 2016</td>
<td>-</td>
</tr> </table>

## December 2015
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>Support for short video messages</td>
<td>Short video messages are now supported, providing richer message content.</td>
<td>December 2015</td>
<td>-</td>
</tr> </table>

## August 2015
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>Support for web platform</td>   
<td>IM for web now supports custom emoji messages.</td>
<td>August 2015</td>
<td>-</td>
</tr> </table>

## July 2015
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>Support for Windows platform</td>
<td>IM for Windows now supports location and audio messages.</td>
<td>July 2015</td>
<td>-</td>
</tr> </table>

## May 2015
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> <tr>
<td>Launch of Instant Messaging IM (formerly Cloud Communication)</td>
<td>IM for Android and IM for iOS support multiple message types including text, image, and emoji.</td>
<td>May 2015</td>
<td>-</td>
</tr> </table>




