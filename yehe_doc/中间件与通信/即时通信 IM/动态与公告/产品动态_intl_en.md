## January 2023
<table>
<tr><th width="20%">Update</th>  <th width="44%">Description</th><th width="15%">Release Date</th><th width="21%">Document</th>
</tr> 
<tr>
    <td> SDK 7.0.3754 release (enhanced edition)</td>
    <td><ul style="margin:0">
    <li> Supported mentioning (@) group members in all types of messages. </li>
    <li> Supported getting the total message unread count by conversation filter. </li>
    <li> Supported the meta counter for common groups and audio-video groups. </li>
    <li> Supported text message translation. </li> 
    <li> Supported custom attributes for community groups. </li>     
    <li> Supported setting the Huawei category and Mi channel ID for offline push. </li>
    <li> For more information about updates, see <a href="https://intl.cloud.tencent.com/document/product/1047/34282">Native</a>.</li>    
        </ul></td>
    <td> 2023-01-06 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">Native SDK download</a> </td>
</tr> 
<tr>
    <td>Launched the cloud moderation feature</td>
    <td>The cloud moderation feature is to check the text, image, audio, and video content generated in one-to-one chat, group chat, and profile scenarios on the server. You can configure different moderation policies for different content in different scenarios and intercept the identified unsafe content.</td>
    <td> 2023-01-04 </td>
    <td> </a></td>
</tr> 
</table>

## December 2022
<table>
<tr><th width="20%">Update</th>  <th width="44%">Description</th><th width="15%">Release Date</th><th width="21%">Document</th>
</tr> 
<tr>
    <td> Launched the local moderation feature</td>
    <td>The local moderation feature is local text moderation on clients. It intercepts or replaces sensitive words in texts locally on clients to achieve sensitive word filtering. You can use this feature to intercept or replace sensitive words that are generated during operations such as sending a text message and modifying a nickname/remark/group notification and are not expected to be sent.</td>
    <td> 2022-12-07 </td>
    <td></td>
</tr> 
</table>

## November 2022
<table>
<tr><th width="20%">Update</th>  <th width="44%">Description</th><th width="15%">Release Date</th><th width="21%">Document</th>
</tr>
    <tr>
    <td>SDK 6.9.3557 release (enhanced edition)</td>
    <td><ul style="margin:0">
    <li> Fixed the occasional crash when getting the `V2TIMOfflinePushInfo` content from messages for Android. </li>
    <li> Fixed the occasional crash of the Pro SDK enhanced edition for Android. </li>
    <li> Refined the JSON data content returned by the C API `TIMConvGetConvList`. </li>
    <li> Released a new minimalist theme, more in line with the styles of international apps. </li>    
        </ul></td>
    <td> 2022-11-29 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">Native SDK download</a> </td>
</tr>
    <tr>
    <td>SDK 6.8.3374 release (enhanced edition)</td>
    <td><ul style="margin:0">
    <li> Supported local text moderation on clients. </li>
    <li> Released the Swift SDK. </li>
    <li> Supported the group attribute feature for non-audio-video groups. </li>
    <li> Optimized the logic for updating the number of members in a non-audio-video groups when someone entered the group. </li>     
    <li> Fixed the failure to deliver a notification when a custom friend field is set independently. </li>
    <li> For more information about updates, see <a href="https://intl.cloud.tencent.com/document/product/1047/34282">Native</a>.</li>    
        </ul></td>
    <td> 2022-11-14 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">Native SDK download</a> </td>
</tr> 
</table>

## September 2022
<table>
<tr><th width="20%">Update</th>  <th width="44%">Description</th><th width="15%">Release Date</th><th width="21%">Document</th>
</tr> 
<tr>
    <td>SDK 6.7.3184 release (enhanced edition)</td>
    <td><ul style="margin:0">
    <li> Supported messages extension. </li>
    <li> Supported signaling messages modification.</li>
    <li> Supported VoIP for iOS offline push.</li>
    <li> Supported Honor phones for Android offline push.</li> 
    <li> Added backup domain name to the access layer. </li>     
    <li> Fixed the problem that the login and logout callbacks could not be executed under special network environment.</li>
    <li> For more information about updates, see <a href="https://intl.cloud.tencent.com/document/product/1047/34282">Native</a></li>    
        </ul></td>
    <td> September 29, 2022</td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">Native SDK download</a> </td>
</tr> 
</table>

## August 2022
<table>
<tr><th width="20%">Update</th>  <th width="44%">Description</th><th width="15%">Release Date</th><th width="21%">Document</th>
</tr> 
<tr>
    <td>SDK 6.6.3002 release (enhanced edition)</td>
    <td><ul style="margin:0">
    <li> Supported marking a member of an audio-video group. </li>
    <li> Supported removing a member from an audio-video group.</li>
    <li> Fixed the occasional crash of the topic update callback for Android.</li>
    <li> Fixed incorrect enumerated values of the notifications for group join option changes.</li> 
    <li> Fixed the issue where no callback for `onTopicInfoChanged` was received after custom topic fields were set. </li>     
    <li> Fixed the issue for Android where the network IP was requested repeatedly.</li>
    <li> For more information about updates, see <a href="https://intl.cloud.tencent.com/document/product/1047/34282">Native</a></li>    
        </ul></td>
    <td> August 18, 2022</td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">Native SDK download</a> </td>
</tr> 
<tr>
    <td> SDK 2.22.0 release (Mini Program and Web)</td>
<td data-sheets-value="" ><li>Supported packaging the uni-app into the native app for offline push. For details, see <a  target="_blank" href="https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#registerPlugin">registerPlugin</a><br>
<li>Supported getting the list of online members of an audio-video group. For details, see <a  target="_blank" href="https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#getGroupMemberList">getGroupMemberList </a> (Ultimate edition required).<br>
<li>Supported blocking a member of an audio-video group. For details, see <a  target="_blank" href="https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#deleteGroupMember">deleteGroupMember</a> (Ultimate edition required).<br>
Added <a  target="_blank" href="https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#setConversationCustomData"><li>setConversationCustomData </a>for setting custom conversation fields.<li> For more information about updates, see <a href="https://intl.cloud.tencent.com/document/product/1047/34281">Web, Mini Program, and Uni-App</a></td></td>
    <td> August 18, 2022</td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996#web">Web SDK download</a></td>
</tr>
<tr>
    <td> SDK 2.21.1 release (Mini Program and Web)</td>
    <td>
<li>Fixed the possible message duplication caused by <a href="https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#resendMessage">resendMessage.</a></li>
<li> For more information about updates, see <a href="https://intl.cloud.tencent.com/document/product/1047/34281">Web, Mini Program, and Uni-App.</a></td>
    <td>August 3, 2022</td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996#web">Web SDK download</a></td>
</tr>
</table>

## July 2022
<table>
<tr><th width="20%">Update</th>  <th width="44%">Description</th><th width="15%">Release Date</th><th width="21%">Document</th>
</tr> 
<tr>
    <td>SDK 6.5.2816 release (enhanced edition)</td>
    <td><ul style="margin:0">
    <li> Optimized the split zone selection policy for India.</li>
    <li> Optimized the callback for the upload/download progress of a rich media message.</li>
    <li> Optimized the compliance required for obtaining the device process information at an Android client.</li>
    <li> Fixed the crash that occurred when several topics were created one after another.</li> 
    <li> Fixed the occasional crash occurred in the Windows based packet sending.</li>     
    <li> Fixed the crash that occurred in the Android v7a architecture when a friend in the blocked list is added again.</li>
    <li> For more information about updates, see <a href="https://intl.cloud.tencent.com/document/product/1047/34282">Native</a></li>    
        </ul></td>
    <td>July 29, 2022</td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">Native SDK download</a> </td>
</tr> 
<tr>
    <td> SDK 2.21.0 release (Mini Program and Web)</td>
    <td>
<li>Added <a href="https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#setSelfStatus">setSelfStatus</a> for setting a custom self status.</li>
<li>Added <a href="https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#getUserStatus">getUserStatus</a> for querying the user status.</li>
<li>Added <a href="https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#getUserStatus">getUserStatus</a> for subscribing the user status.</li>
<li>Added <a href="https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#unsubscribeUserStatus">unsubscribeUserStatus</a> for unsubscribing the user status.</li>
<li>Added a feature of <a href="https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#setMessageRemindType">setMessageRemindType</a>: Sync the settings of group and topic message muting across clients and instances.</li>
<li> For more information about updates, see <a href="https://intl.cloud.tencent.com/document/product/1047/34281">Web, Mini Program, and Uni-App.</a></td>
    <td>July 28, 2022</td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996#web">Web SDK download</a></td>
</tr>
<tr>
    <td>SDK 6.5.2803 release (enhanced edition)</td>
    <td><ul style="margin:0">
	<li> Supported <a href="https://intl.cloud.tencent.com/document/product/1047/48853">Conversation Tag</a>.
	<li> Supported <a href="https://intl.cloud.tencent.com/document/product/1047/48854">Conversation Grouping</a>.
	<li> Supported custom conversation fields.</li>
	<li> Added the advanced API <a href="https://cloud.tencent.com/document/product/269/75366#.E8.8E.B7.E5.8F.96.E4.BC.9A.E8.AF.9D.E5.88.97.E8.A1.A8.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3"> for getting the conversation list.</a>    
	<li> Supported receiving broadcast messages of an audio-video group.</li> 
	<li> Supported delivering the notifications for group join option changes.</li>     
	<li> Supported synchronizing changes of the group message receiving option across clients.</li>
	<li> For more information about updates, see <a href="https://intl.cloud.tencent.com/document/product/1047/34282">Native</a>.</li>    
    </ul></td>
    <td>July 15, 2022</td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">Native SDK download</a> </td>
</tr>
</table>


## June 2022
<table>
<tr><th width="20%">Update</th>  <th width="44%">Description</th><th width="15%">Release Date</th><th width="21%">Document</th>
</tr> 
<tr>
    <td>SDK 6.3.2619 release (enhanced edition)</td>
    <td><ul style="margin:0">
	<li>Fixed the occasional crashes when the topic list was obtained.</li>
	<li>Fixed the exception in getting the conversation list after a topic was deleted.</li>
    </ul></td>
    <td> 2022-06-29 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">Native SDK download</a> </td>
</tr>
<tr>
    <td>SDK 2.20.1 release (web)</td>
    <td><li>Aligned with the native SDK experience, where only group records are deleted and group conversations are not deleted after users leave or are kicked out of a non-audio-video group or the group is deleted.</li><li>Made <a href="https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteMessage">deleteMessage</a> unable to delete group system notifications; if a deletion attempt is made, an error message will be reported.</li><li>Supported HTTP for rich media messages of the on-premises deployment.</li><li>Fixed the issue where `lastMessage` of the one-to-one conversation was abnormally updated.</li></td>
    <td> 2022-06-27 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996#web">Web SDK download</a></td>
</tr>
<tr>
    <td>SDK 6.3.2609 release (enhanced edition)</td>
    <td><ul style="margin:0">
	<li>Added the online status and custom status.</li>
	<li>Supported pulling the list of up to 1,000 members of an audio-video group.</li>
	<li>Supported @ all in a topic.</li>
	<li>Fixed the cross-platform SQL execution error.</li> 
	<li>Added community topic APIs for the cross-platform SDK.</li>
	<li> For more information about updates, see <a href="https://intl.cloud.tencent.com/document/product/1047/34282">Native</a>.</li>
    </ul></td>
    <td> 2022-06-16 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">Native SDK download</a> </td>
</tr>
<tr>
    <td> SDK 2.20.0 release (web)</td>
    <td><ul style="margin:0">
<li>Added <a href="https://web.sdk.qcloud.com/im/doc/en/SDK.html#modifyMessage">modifyMessage</a> to support message modification.
<li>Added <a href="https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageListHopping">getMessageListHopping</a> to pull the conversation message list by specified sequence or time range.
<li>Supported read receipts for one or more one-to-one messages (supported only by the Ultimate edition).
<li>Added the `isPeerRead` field for `lastMessage` of one-to-one conversation to indicate whether a message was read by the receiver.<li>For more information on updates, see <a href="https://intl.cloud.tencent.com/document/product/1047/34281">Web, Mini Program, and uni-app</a>.</li>
    </ul></td>
    <td> 2022-06-09 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996#web">Web SDK download</a></td>
</tr>
</table>


## May 2022
<table>
<tr><th width="20%">Update</th>  <th width="44%">Description</th><th width="15%">Release Date</th><th width="21%">Document</th>
</tr> 
<tr>
    <td> SDK 2.19.0 release (web)</td>
    <td><ul style="margin:0">
<li>Supported topic creation in a <a href="https://intl.cloud.tencent.com/document/product/1047/33529">community</a> for stronger interactions.</li>
<li>Added <a href="https://web.sdk.qcloud.com/im/doc/en/SDK.html#getJoinedCommunityList">getJoinedCommunityList</a> to get the list of topic-enabled communities.</li>
<li>Added <a href="https://web.sdk.qcloud.com/im/doc/en/SDK.html#createTopicInCommunity">createTopicInCommunity</a> to create a topic.</li>
<li>Added <a href="https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteTopicFromCommunity">deleteTopicFromCommunity</a> to delete a topic.</li>
<li>Added <a href="https://web.sdk.qcloud.com/im/doc/en/SDK.html#updateTopicProfile">updateTopicProfile</a> to set the topic profile.</li>
<li>Added <a href="https://web.sdk.qcloud.com/im/doc/en/SDK.html#getTopicList">getTopicList</a> to get the topic list.</li>
<li>Added <a href="https://web.sdk.qcloud.com/im/doc/zh-cn/Topic.html">Topic</a>, which indicates the topic object of a community and is used to describe topic attributes such as name, notice, introduction, and unread count.</li>
<li>Added the <a href="https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.TOPIC_CREATED">TIM.EVENT.TOPIC_CREATED</a> event, which will be triggered when a topic is created.</li>
<li>Added the <a href="https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.TOPIC_DELETED">TIM.EVENT.TOPIC_DELETED</a> event, which will be triggered when a topic is deleted.</li>
<li>Added the <a href="https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.TOPIC_UPDATED">TIM.EVENT.TOPIC_UPDATED</a> event, which will be triggered when the topic profile is updated.</li></li>
    </ul></td>
    <td> 2022-05-07 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996#web">Web SDK download</a></td>
</tr>
</table>

## April 2022
<table>
<tr><th width="20%">Update</th>  <th width="44%">Description</th><th width="15%">Release Date</th><th width="21%">Document</th>
</tr> 
<tr>
    <td>SDK 6.2.2363 release (enhanced edition)</td>
    <td><ul style="margin:0">
	<li>Added the community topic feature.</li>
	<li>Added the message editing API.</li>
	<li>Supported read receipts for one-to-one messages.</li>
	<li>Optimized the network quality of Tencent Cloud International customers.</li> 
	<li>Fixed the issue where a read message was displayed as unread after the application was uninstalled and reinstalled.</li>
	<li> For more information about updates, see <a href="https://intl.cloud.tencent.com/document/product/1047/34282">Native</a>.</li>
    </ul></td>
    <td> 2022-04-29 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">Native SDK download</a> </td>
</tr>
<tr>
    <td>SDK 2.18.2 release (Mini Program and Web)</td>
    <td><ul style="margin:0">
<li>Optimized the audio-video group user experience.</li><li>Fixed the issue where the statistics in certain use cases were inaccurate.</li><li>Fixed the issue where the result returned by the <a href="https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMessageReadMemberList">getGroupMessageReadMemberList</a> API was inaccurate.<li>For more information on updates, see <a href="https://intl.cloud.tencent.com/document/product/1047/34281">Web</a>.</li>
    </ul></td>
    <td> 2022-04-22 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996#web">Web SDK download</a></td>
</tr>
<td>Flutter SDK 3.9.3</td>
<td><ul style="margin:0">
  <li>Fixed the issue where the `boolValue` of a group muting tip was lost.
    <ul>
      <li>Added the `key(string)-boolValue(bool)` format in addition to the existing `key(string)-value(string)` in the callback for group information modification.</li>
    </ul>
  </li>
  <li>Fixed the issue where the `nameCard` field of a conversation was not parsed by the instance.
  <li>Added APIs for group message read receipts.
    <ul>
      <li>Added <a href="https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_message_manager/V2TIMMessageManager/sendMessageReadReceipts.html">sendMessageReadReceptes</a> to send a read receipt for a group message.</li>
      <li>Added <a href="https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_message_manager/V2TIMMessageManager/getMessageReadReceipts.html">getMessageReadReceptes</a> to get the read receipt for a sent message.</li>
      <li>Added <a href="https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_message_manager/V2TIMMessageManager/getGroupMessageReadMemberList.html">getgroupMessageReadMemeberList</a> to get the list of group members who have or have not read a sent group message.</li>
    </ul>
  </li>
  <li>Improved the Flutter for web.
</ul>
</td>
<td>2022-04-20</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">Framework SDK download</a></td>
<tr>
    <td> SDK 2.18.0 release (Mini Program and Web)</td>
    <td><ul style="margin:0">
<li>Added <a href="https://web.sdk.qcloud.com/im/doc/en/SDK.html#sendMessageReadReceipt">sendMessageReadReceipt</a> to send a read receipt for a group message.</li>
<li>Added <a href="https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageReadReceiptList">getMessageReadReceiptList</a> to pull the list of read receipts for a group message.</li>
<li>Added <a href="https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMessageReadMemberList">getGroupMessageReadMemberList</a> to pull the list of group members who have or have not read a group message.</li>
<li>Added <a href="https://web.sdk.qcloud.com/im/doc/en/SDK.html#findMessage">findMessage</a> to query local messages in a conversation by `messageID`.
Aligned with the native IM experience of the conversation unread count change after a message is recalled.</li><li>For more information on updates, see <a href="https://intl.cloud.tencent.com/document/product/1047/34281"> Web </a>.</li>
    </ul></td>
    <td> 2022-04-08 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996#web">Web SDK download</a></td>
</tr>



<tr>
    <td>SDK 6.1.2166 release (enhanced edition)</td>
    <td><ul style="margin:0">
	<li> Fixed the issue where no data was returned when two or more userIDs were entered for `senderUserIDList` to search for local messages.</li>
	<li> Fixed the issue where the SDK for Android called back only one message when a user recalled multiple messages with the RESTful API.</li>
	<li> Fixed occasional crashes in quickly clearing unread messages for Windows.</li>
	<li> Released the International edition demo.</li>
	<li> Switched the demo's offline push back to vendor channels.</li>
	<li> Switched the demo's login with mobile number to the aPaaS service.</li>
	<li> Fixed the failure of audio/video call sync across multiple clients.</li>
    </ul></td>
    <td> April 2, 2022</td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">Native SDK download</a> </td>
</tr>
</table>



## March 2022
<table>
<tr><th width="20%">Update</th>  <th width="44%">Description</th><th width="15%">Release Date</th><th width="21%">Document</th>
</tr> 
<tr>
<td>Flutter SDK 3.9.1</td>
<td><ul style="margin:0;">
<li>Upgraded the underlying library to v6.1.2155.
</ul></td>
<td>March 24, 2022</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">Framework SDK download</a></td>
</tr>
<tr>
<td>Flutter SDK 3.9.0</td>
<td><ul style="margin:0;">
<li>Modified GroupListener.
</ul></td>
<td>March 22, 2022</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">Framework SDK download</a></td>
</tr>
<tr>
<td>Flutter SDK 3.8.9</td>
<td><ul style="margin:0;">
<li>Fixed the registration result listening issue.
</ul></td>
<td>March 18, 2022</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">Framework SDK download</a></td>
</tr>
<tr>
<td>Flutter SDK 3.8.4</td>
<td><ul style="margin:0;">
<li>Updated APIs.
</ul></td>
<td>March 14, 2022</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">Framework SDK download</a></td>
</tr>
<tr>
    <td>SDK 6.1.2155 release (enhanced edition)</td>
    <td><ul style="margin:0">
        <li> Added support for read receipts for group messages (<a href="https://intl.cloud.tencent.com/document/product/1047/36360#.E7.BE.A4.E6.B6.88.E6.81.AF.E5.B7.B2.E8.AF.BB.E5.9B.9E.E6.89.A7">iOS documentation</a>, <a href="https://intl.cloud.tencent.com/document/product/1047/36359#.E7.BE.A4.E6.B6.88.E6.81.AF.E5.B7.B2.E8.AF.BB.E5.9B.9E.E6.89.A7">Android documentation</a>). </li>
	<li> Added support for setting offline push alert sound for Android.</li>
	<li> Added the API for setting network proxy for mobile SDKs.</li>
	<li> Supplemented offline push APIs for the C/C++ platform.</li>
	<li> Added support for automatically synchronizing signaling messages in a group after login.</li>
	<li> Fixed the issue where a user cannot get complete custom fields after receiving a notification on custom field changes.</li>
	<li> Fixed the notification muting status return error that occasionally occurred when the conversation list was pulled under a weak network.</li>
	<li> For more information about updates, see <a href="https://intl.cloud.tencent.com/document/product/1047/34282">Update Log (Native)</a>.</li>
    </ul></td>
    <td> March 18, 2022</td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">Native SDK download</a> </td>
</tr>
<tr>
<td>Flutter SDK 3.8.4</td>
<td><ul style="margin:0;">
<li>Updated APIs.
</ul></td>
<td>March 14, 2022</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">Framework SDK download</a></td>
</tr>
<tr>
    <td> SDK 2.17.0 release (Mini Program and Web)</td>
    <td><ul style="margin:0">
       <li>Added support for <a href="https://intl.cloud.tencent.com/document/product/1047/33529">community groups</a>.</li>
<li>Recent contacts' `Conversation.lastMessage` supports group notifications. </li>
<li>`Message.payload.memberList` supports getting the nickname, profile photo, and other information of group members who joined or left a group.</li>
<li>Images in WEBP format can be sent.</li><li> For more information about updates, see <a href="https://intl.cloud.tencent.com/document/product/1047/34281">Update Logs (Web & Mini Programs).</a></li>
    </ul></td>
    <td>March 2, 2022 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996#web">Web SDK download</a></td>
</tr>
</tr> 
<tr>
<td>Flutter SDK 3.8.3 </td>
<td><ul style="margin:0;">
<li>Switched the token encoding format based on the environment.
</ul></td>
<td>March 1, 2022</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">Framework SDK download</a></td>
</tr>
</table>

## February 2022
<table>
<tr><th width="20%">Update</th>  <th width="44%">Description</th><th width="15%">Release Date</th><th width="21%">Document</th>
</tr>
<tr>
<td>Flutter SDK 3.8.2</td>
<td><ul style="margin:0;">
<li>Updated group member parameter constraints.
</ul></td>
<td>February 21, 2022</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">Framework SDK download</a></td>
</tr>
<tr>
<td>Flutter SDK 3.8.0</td>
<td><ul style="margin:0;">
<li>Upgraded the underlying API dependencies.
</ul></td>
<td>February 17, 2022</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">Framework SDK download</a></td>
</tr>
<tr>
<td>Flutter SDK 3.7.8</td>
<td><ul style="margin:0;">
<li>Fixed the exception caused by force unwrapping.
</ul></td>
<td>February 15, 2022</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">Framework SDK download</a></td>
</tr>
<tr>
    <td>SDK 2.16.3 release (Mini Program and Web)</td>
    <td><ul style="margin:0">
        <li>Fixed login failures that occurred when Windows WeChat accessed mini programs and uni-app packaged Android apps (some devices).
    </ul></td>
    <td>February 11, 2022</td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996#web">Web SDK download</a></td>
</tr>
</tr> 
<tr>
    <td>SDK 2.16.2 release (Mini Program and Web)</td>
    <td><ul style="margin:0">
        <li>Added support for sending file messages after uni-app packages native apps.</li>
        <li>Added support for the international website in India.</li>
				        <li>Fixed some emoji rendering issues.</li>
    </ul></td>
    <td>February 10, 2022</td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996#web">Web SDK download</a></td>
</tr>
<tr>
<td>Flutter SDK 3.7.7</td>
<td><ul style="margin:0;">
<li>Fixed the Swift code warning.                        </li><li>Rewrote Swift's force unwrapping code.                          </li><li>Added the `id` field to the `message` instance returned by the `sendMessage` API.  </li>
</ul></td>
<td>February 10, 2022</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">Framework SDK download</a></td>
</tr>
<tr>
    <td> SDK 6.0.1992 release (enhanced edition)</td>
    <td><ul style="margin:0">
        <li> Fixed occasional crashes when sending two consecutive messages to a deleted or nonexistent group.</li>
    </ul></td>
    <td> February 9, 2022</td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">Native SDK download</a> </td>
</tr>
</table>

## January 2022
<table>
<tr><th width="20%">Update</th>  <th width="44%">Description</th><th width="15%">Release Date</th><th width="21%">Document</th>
</tr> 
<tr>
    <td> TUIKit 6.0.1992 release (enhanced edition)</td>
    <td><ul style="margin:0">
        <li> Added the theme setting capability.</li>
    	<li> Added the language setting capability.</li>
	<li> Added the group profile card feature of group management.</li>
	<li> Added the file message feature of animation upload/download.</li>
        <li> Added the redirection entry "Received xx new messages" when browsing the message history.</li>
	<li> Added the redirection entry "Back to the latest" when browsing the message history.</li>
	<li> Added the entry for one-click redirection to group @ messages.</li>
	<li> Optimized the display style of the last message in the conversation list.</li>
    <li> Added the selected state for text messages.</li>
	<li> Optimized the A2 and D2 error descriptions.</li>
	<li> Added iOS 15 system UI adaptation.</li>
    </ul></td>
    <td>January 25, 2022</td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">Native SDK download</a> </td>
</tr>
<tr>
<td>Flutter SDK 3.7.5</td>
<td><ul style="margin:0;">
<li>Upgraded the underlying library to v6.0.1975.
<li>Supported the TPNS token for offline push configuration.
</ul></td>
<td>2022-01-23</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">Framework SDK download</a></td>
</tr>
<tr>
    <td> SDK 6.0.1975 release (enhanced edition)</td>
    <td><ul style="margin:0">
        <li> Released SDK version for all-platform C++ APIs.</li>
    	<li> Added the feature of integrating the TPNS channel for offline push.</li>
	<li> Added change notification for custom fields of personal profile.</li>
	<li> Fixed the issue where the returned content was occasionally empty when a user attempted to obtain friend remarks.</li>
        <li> Optimized network type log printing.</li>
	<li> Supplemented the message priority fields of the message object for iOS.</li>
	<li> Fixed the issue where the message object returned for callback of inserting local messages was incomplete in the C interface version.</li>
	<li> Switched the offline push for the open source demo of the official TUIKit to the TPNS channel.</li>
    </ul></td>
    <td>January 14, 2022</td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">Native SDK download</a> </td>
</tr>

<tr>
<td>SDK 2.16.1 release (Mini Program and Web)</td>
<td><ul style="margin:0;">
<li>Added support for Alipay Mini Program to send .image images.                                                                                </li>
<li>Added the feature of deleting historical messages while deleting conversations (<a href="https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#deleteConversation">deleteConversation</a>).   </li>
<li>Fixed the error caused by the downstream file message 'fileName' being an empty string.                                                                          </li>
<li>Fixed the issue caused by the group attribute API call sequence.                                                                                          </li>
<li>Fixed the `__wxConfig is not defined` issue occurred when uni-app packaged apps to Baidu Mini Program and other platforms.                                               </li>
</ul></td>
<td>January 14, 2022</td>
<td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996#web">Web SDK download</a></td>
</tr>
<tr>
<td>Unity SDK 1.6.4 </td>
<td><ul style="margin:0;">
<li>SDK supports package manager import.
<li>Added the feature of adding dependencies after iOS compilation.
</ul></td>
<td>January 13, 2022</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">Framework SDK download</a></td>
</tr>
<tr>
<td>Flutter SDK 3.7.1</td>
<td><ul style="margin:0;">
<li>Added the feature of returning the message creation ID for a message sending progress event.
<li>Optimized the callback by reminding the business side that the callback error is caught in SDK and needs to be modified.
</ul></td>
<td>January 12, 2022</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">Framework SDK download</a></td>
</tr>
<tr>
<td>Flutter SDK 3.7.0</td>
<td><ul style="margin:0;">
<li>Optimized the unpacking of cloudCustomData.
</ul></td>
<td>2022-01-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">Framework SDK download</a></td>
</tr>

<tr>
<td>Flutter SDK 3.6.9</td>
<td><ul style="margin:0;">
<li>Optimized the message reply parameters.
</ul></td>
<td>2022-01-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">Framework SDK download</a></td>
</tr>
<tr>
<td>Flutter SDK 3.6.8</td>
<td><ul style="margin:0;">
<li>Optimized the message reply API.
</ul></td>
<td>2022-01-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">Framework SDK download</a></td>
</tr>
<tr>
<td>SDK 2.16.0 release (Mini Program and Web)</td>
<td><ul style="margin:0;">
<li>Added <a href="https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#setMessageRemindType">setMessageRemindType</a> for setting the **Mute Notifications** mode for C2C conversations.             </li>
<li>Added <a href="https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#setAllMessageRead">setAllMessageRead</a> for quickly marking unread messages of all conversations as read.                      </li>
<li>Added <a href="https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#sendMessage">sendMessage</a> for excluding sent messages from the conversation's unread message count and not updating the conversation's `lastMessage`.   </li>
<li>Added the feature that allows new members of an audio-video group to view historical messages before joining the group (the users must activate the Flagship Edition package to use the feature).                                                                                                 </li>
<li>Update: SDK uses the <a href="https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Strict_mode">strict mode</a>.                                      </li>
<li>Update: the conversations with deleted accounts are filtered out for the conversation list.                                                                                                                 </li>
<li>Update: optimized the update timing of 'nick' and 'avatar' for roaming messages.                                                                                                       </li>
<li> For more information about updates, see <a href="https://intl.cloud.tencent.com/document/product/1047/34281">Update Log (Native)</a>.</li>
</ul></td>
<td>2022-01-05</td>
<td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996#web">Web SDK download</a></td>
</tr>
<tr>
<td>Flutter SDK 3.6.7</td>
<td><ul style="margin:0;">
<li>Upgraded the compilation environment for iOS from 8.0 to 9.0.
</ul></td>
<td>2022-01-05</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">Framework SDK download</a></td>
</tr>
</table>


## December 2021
<table>
<tr><th width="20%">Update</th>  <th width="44%">Description</th><th width="15%">Release Date</th><th width="21%">Document</th>
</tr> 
<tr>
    <td> SDK 5.9.1886 release (enhanced edition)</td>
    <td><ul style="margin:0">
        <li> Fixed the issue of incomplete unread messages in the callback after a user logged in and synchronized C2C unread messages.</li>
    	<li> Fixed the issue of incomplete returned messages after a user pulled local messages.</li>
	<li> Fixed HTTPS request errors on the Linux platform.</li>
	<li> Fixed the issue where no result was returned for querying the custom fields of friends in the C API version.</li>
        <li> Optimized the error code descriptions for the network layer.</li>
	<li> TUIKit: image and video messages can be scrolled horizontally for viewing.</li>
	<li> TUIKit: recalled messages can be edited again.</li>
	<li> For more information about updates, see <a href="https://intl.cloud.tencent.com/document/product/1047/34282">Update Log (Native)</a>.</li>
    </ul></td>
    <td>December 31, 2021</td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">Native SDK download</a> </td>
</tr>
<tr>
<td>Flutter SDK 3.6.6</td>
<td><ul style="margin:0;">
<li>Added the message reply API.
<li>Fixed the issue for web where the release mode triggered an error.
</ul></td>
<td>2021-12-30</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">Framework SDK download</a></td>
</tr>
<tr>
<td>Unity SDK 1.6.0</td>
<td><li>Switched the underlying cross-platform C API.</li><li>Supports the Windows, macOS, Android, and iOS platforms with unified APIs.</li><li>Note that v1.6.0 is incompatible with earlier versions.</li></td>
<td>2021-12-21</td>
<td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">Native SDK download</a> </td>
</tr> 
<tr>
    <td> SDK 5.9.1872 release (enhanced edition)</td>
    <td><ul style="margin:0">
        <li> Added the feature of sending targeted group messages.</li>
    	<li> Added authentication for COS file download.</li>
	<li> Added AES support for the encrypted tunnels of persistent connections.</li>
	<li> Added support for avoiding access point silos for the connection logic.</li>
        <li> Added support for configuring the concurrent COS file uploads and downloads in the backend.</li>
	<li> For more information about updates, see <a href="https://intl.cloud.tencent.com/document/product/1047/34282">Update Log (Native)</a>.</li>
    </ul></td>
    <td>December 20, 2021</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">Framework SDK download</a></td>
</tr>
<tr>
<td>Flutter SDK 3.6.5</td>
<td><ul style="margin:0;">
<li>Fixed Java syntax errors.
</ul></td>
<td>2021-12-17</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">Framework SDK download</a></td>
</tr>
<tr>
<td>Flutter SDK 3.6.4</td>
<td><ul style="margin:0;">
<li>Fixed the issue where there was no return for Android async registration events.
<li>Fixed the issue where an error was reported when basic listening events were removed.
<li>Added the UUID of a message being sent in its progress event.
</ul></td>
<td>2021-12-17</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">Framework SDK download</a></td>
</tr>

<tr>
    <td> SDK 5.8.1696 release (enhanced edition)</td>
    <td><ul style="margin:0">
        <li> Fixed the failure to quickly clearing the unread message count of conversations including disbanded or left group conversations.</li>
    	<li> TUIKit: added the message reply feature.</li>
	<li> TUIKit: changed the default skin and optimized the UI logic.</li>
	<li> iOS: fixed the occasional failure to load resource files.</li>
    </ul></td>
    <td> December 10, 2021</td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">Native SDK download</a> </td>
</tr>
<tr>
<td>Flutter SDK 3.6.3</td>
<td><ul style="margin:0;">
<li>Optimized the `addFriend` API: changed `addType` from int to FriendTypeEnum.
<li>Optimized the `acceptFriendApplication` API: changed `acceptType` from int to FriendResponseTypeEnum.
<li>Optimized the `getHistoryMessageList` API: changed `type` from int to HistoryMsgGetTypeEnum.
	<li> For more information about updates, see <a href="https://intl.cloud.tencent.com/document/product/1047/45915">Update Log (Native)</a>.</li>
</ul></td>
<td>December 9, 2021</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">Framework SDK download</a></td>
</tr>
<tr>
<td>Flutter SDK 3.6.2</td>
<td><ul style="margin:0;">
<li>Fixed the issue where no UUID was passed in for removing an advanced message.
</ul></td>
<td>2021-12-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">Framework SDK download</a></td>
</tr>
<tr>
<td>Flutter SDK 3.6.1</td>
<td><ul style="margin:0;">
<li>Fixed the issue where file progress events got lost.
</ul></td>
<td>2021-12-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">Framework SDK download</a></td>
</tr>
<tr>
<td>Flutter SDK 3.6.0</td>
<td><ul style="margin:0;">
<li>Added support for multiple listener registrations and callbacks in modules.
<li>Added the `markAllMessageAsRead` API for marking all messages as read.
<li>Added the feature of parsing combined messages.
<li>Upgraded the Native SDK to v5.8.1668.
</ul></td>
<td>2021-12-01</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">Framework SDK download</a></td>
</tr>

</table>


## November 2021
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th>
</tr> 
<tr>
    <td> SDK 5.8.1672 release (enhanced edition)</td>
    <td><ul style="margin:0">
        <li> Optimized the device information getting logic to meet compliance requirements.</li>
    	<li> Fixed the crashes in quickly clearing the unread message count under certain conditions.</li>
    </ul></td>
    <td> 2021-11-30 </td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
<tr>
    <td> SDK 5.8.1668 release (enhanced edition)</td>
    <td><ul style="margin:0">
        <li> Added the feature of quickly clearing the total unread message count of all conversations.</li>
    	<li> Added support for community groups (Community) which support up to 100,000 members per group. Users must activate the Flagship Edition package before they can use the feature.</li>
    	<li> Added the feature of displaying the 20 historical messages before a user joins an audio-video group (AVChatRoom). Users must activate the Flagship Edition package before they can use the feature.</li>
    	<li> Added the feature of automatically excluding conversions whose message receiving option is "Receive but not notify" or "Not receive" when getting the total unread message count of all conversations.</li>
    	<li> Added support for Chinese SM algorithms for encrypted tunnels of persistent connections.</li>
    	<li> Fixed the issue where, when historical messages were pulled, the end tag was incorrectly determined occasionally.</li>
    	<li> Fixed the issue where, when the SDK was upgraded from the Basic Edition to Enhanced Edition in overriding mode, audio-video groups that users previously joined had unread message count.</li>
    	<li> Fixed the failure to setting auto read reporting for accounts in special formats.</li>
    	<li> Fixed the occasional error of connecting to incorrect servers during frequent network reconnections in private environments.</li>
	<li> For more information about updates, see <a href="https://intl.cloud.tencent.com/document/product/1047/34282">Update Log (Native)</a>.</li>
    </ul></td>
    <td> 2021-11-19 </td>
    <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>
</tr>
</table>

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




