## July 2020

<table>
     <tr>
         <th width="20%">Update</th>  
         <th width="50%">Description</th>  
         <th width=10%>Release Date</th>  
          <th width="15%">Related Documents</th>  
     </tr> 
	 <tr>      
         <td>SDK 4.9.1 release (Android, iOS and Windows)</td>   
         <td><ul style="margin:0;">
		 <li>Optimized login outside China.</li>
                 <li>Fixed file upload failures in some regions outside China.</li>
		 <li>Fixed file upload failures for accounts containing the @ symbol.</li>
		 <li>Fixed occasional errors with C2C unread count.</li>
		 <li>Fixed occasional exceptions in conversation showName display.</li>
		 <li>Added an API for obtaining the download URL of file messages.</li>
		 <li>iOS fixed the issue where there was no callback when users attempted to obtain C2C messages while no network connection is available.</li>
		 <li>Android fixed occasional crashes of signal parsing APIs.</li>
		 <li>Android fixed occasional crashes when obtaining offline push information.</li>
		 <li>Android fixed the issue where there was no callback when API2.0 getFriendApplicationList carried no data, and fixed the issue where there was no callback when non-members were specified for getGroupMembersInfo.</li>
		 <li>Windows added detailed group information when users obtain the list of groups joined.</li>
		 <li>Windows fixed the failure to send small files.</li>
		 <li>Windows fixed error 6002 reported by logs.</li>
		 <li>iOS Demo & Android Demo added push for offline voice and video calls and enabled redirection to the call answering interface.</li>
		 <li>iOS fixed the failure to delete or recall custom messages.</li>
		 <li>iOS changed the voice and video code swift -> oc to substantially reduce third-party dependent libraries.</li>
		 <li>iOS supports TUIKit pod integration of two types of voice and video dependent libraries: LiteAV_TRTC and LiteAV_Professional.</li>
		 <li>Android optimized the offline push of the demo and upgraded the push SDK version for each vendor.</li>
</ul></td>   
	     <td>2020-07-24</td>   
	     <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>   
     </tr> 
</table>


## June 2020

<table>
     <tr>
         <th width="20%">Update</th>  
         <th width="50%">Description</th>  
         <th width=10%>Release Date</th>  
          <th width="15%">Related Documents</th>  
     </tr> 
	 <tr>      
         <td>SDK 4.8.50 release (Android, iOS and Windows)</td>   
         <td><ul style="margin:0;"><li>Fixed the API 2.0 issue where the onMemberEnter callback was not triggered when someone entered a livestreaming group (AVChatRoom).</li>
<li>Added the groupID parameter to the onGroupInfoChanged and onMemberInfoChanged callbacks of API 2.0.</li>
		 <li>Fixed the issue where there was no conversation update callback after a C2C message was sent successfully.</li>
		 <li>Fixed the issue where a user failed to receive messages after switching accounts and joining the same livestreaming group (AVChatRoom).</li>
		 <li>Fixed the occasional issue of incorrect callback sequence during unread message synchronization after login.</li>
		 <li>Adding signaling APIs.</li>
		 <li>Added the custom group attribute API for livestreaming groups (AVChatRoom).</li>
		 <li>Fixed known crashes.</li>
		 <li>Changed the default log storage location to /sdcard/Android/data/package name/files/log/tencent/imsdk to be compatible with Android Q versions.</li>
		 <li>The Windows platform fixed group member role issues during group creation.</li>
		 <li>TUIKit replaced API 2.0.</li>
		 <li>Integrated TRTC to implement the voice and video call feature.</li>
		 <li>iOS TUIKit added the deep-color mode.</li>
		 <li>Supports AndroidX.</li>
</ul></td>   
	     <td>2020-06-22</td>   
	     <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>   
     </tr> 
</table>

## May 2020

<table>
     <tr>
         <th width="20%">Update</th>  
         <th width="50%">Description</th>  
         <th width=10%>Release Date</th>  
          <th width="15%">Related Documents</th>  
     </tr> 
	 <tr>      
         <td>SDK 4.8 release (Android, iOS and Windows)</td>   
         <td><ul style="margin:0;"><li>iOS & Android launched all-new API 2.0.</li>
<li>iOS and Android support IPv6.</li>
		 <li>Livestreaming groups (AVChatRoom) support dynamic updates of the group member list.</li>
		 <li>Fixed xlog crashes.</li>
		 <li>Fixed the failure of iOS to send big files.</li>
		 <li>Fixed the exceptions that occurred when the sender’s friend remark was pulled from iOS messages.</li>
		 <li>IM SDK supports AndroidX.</li>
		 <li>Fixed the Android device crashes caused by network permission issues.</li>
</ul></td>   
	     <td>2020-05-15</td>   
	     <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>   
     </tr> 
</table>


## March 2020

<table>
     <tr>
         <th width="20%">Update</th>  
         <th width="50%">Description</th>  
         <th width=10%>Release Date</th>  
          <th width="15%">Related Documents</th>  
     </tr> 
	 <tr>      
         <td>SDK 2.6 release (Mini Program and Web)</td>   
         <td><ul style="margin:0;"><li>Web: you can now create and send video messages of up to 100 MB.</li><li>Added the <code>nick</code> and <code>avatar</code> properties to Message to display the nickname and profile photo of the message sender in audio-video chat room (AVChatRoom). updateMyProfile must be called in advance.</li><li>When multiple instances are logged in on Web devices, C2C message recall notifications can be synced on all instances.</li><li>When modifying group custom fields by calling updateGroupProfile succeeds, group members will receive group tips and related content Message.payload.newGroupProfile.groupCustomField.</li><li>Deprecated TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVED and replaced it with MESSAGE_RECEIVED.</li><li>Fixed an occasional error with calling getGroupList.</li></ul></td>   
	     <td>2020-03-30</td>   
	     <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>   
     </tr> 
	 <tr>      
         <td>SDK 4.7 release (Android, iOS and Windows)</td>   
         <td><ul style="margin:0;"><li>Reduced local log size.</li>
<li>Improved login speed.</li>
<li>Fixed an issue with unread count synchronization across multiple devices.</li>
<li>Added getFriendList to get single friends.</li>
<li>You can now set the message title and content to display on the push notifications bar on iOS and Android devices respectively.</li>
</ul></td>   
	     <td>2020-03-23</td>   
	     <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>   
     </tr> 
</table>

## February 2020

<table>
     <tr>
         <th width="20%">Update</th>  
         <th width="50%">Description</th>  
         <th width=10%>Release Date</th>  
          <th width="15%">Related Documents</th>  
     </tr>
	 <tr>      
         <td>SDK 4.6 improvements (Android, iOS and Windows)</td>   
         <td><ul style="margin:0;"><li>Increased the file upload limit to 100 MB.</li><li>Improved COS upload.</li><li>Improved the logic for processing group pending requests.</li></ul></td>   
	     <td>2020-02-28</td>   
	     <td>-</td>   
     </tr> 
	 <tr>      
         <td>SDK 2.5 release (Mini Program and Web)</td>   
         <td><ul style="margin:0;"><li>Added network change event TIM.EVENT.NET_STATE_CHANGE which enables the access side to provide prompts and instructions.</li><li>Added support for running in WeChat Mini Program plugin environment.</li><li>Reduced and optimized error codes.</li><li>Fixed an issue where group member messages would repeat on the group owner side after an audio-video chat room (AVChatRoom) was created from the console and the group owner was specified and entered the group.</li><li>Fixed an issue where the SDK did not distribute TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVED events after groups were frequently created or terminated from the console or via RESTful API.</li><li>Fixed an occasional issue where getMessageList would fail to pull group message lists.</li></ul></td>   
	     <td>2020-02-28</td>   
	     <td>-</td>   
     </tr> 
</table>

## January 2020

<table>
     <tr>
         <th width="20%">Update</th>  
         <th width="50%">Description</th>  
         <th width=10%>Release Date</th>  
          <th width="15%">Related Documents</th>  
     </tr>
	 <tr>      
         <td>SDK 2.4 release (Mini Program and Web)</td>   
         <td><ul style="margin:0;"><li>Added the revokeMessage API to recall messages.</li><li>Added the isRevoked property in Message, which identifies a recalled message when its value is true.</li><li>Added TIM.EVENT.MESSAGE_REVOKED, which is the event notification for message recalls.</li><li>Added force offline types of “force offline due to multi-device login” and “force offline due to UserSig expiration” in force offline event notification TIM.EVENT.KICKED_OUT.</li><li>Increased file upload limit for createFileMessage from 20 MB to 100 MB.</li><li>msgMemberInfo and shutupTime of group tips will be deprecated soon. Please use memberList and muteTime instead.</li><li>Added entry to IM smart customer service in the console.</li><li>Fixed an issue where calling the off API could not cancel listening events.</li><li>Fixed inaccurate value and type of the isRead property of Message.</li><li>Fixed an issue where incorrect error code and error message were returned when the video size exceeded the limit in a video message.</li><li>Fixed an occasional issue where field content was inaccurate after custom fields were updated.</li><li>Fixed an occasional issue where JOIN_STATUS_ALREADY_IN_GROUP was seen when a logged in user joined an audio-video chat room.</li><li>Fixed a potential performance issue caused by core-js.</li></ul></td>   
	     <td>2020-01-03</td>   
	     <td>-</td>   
     </tr> 
</table>

## December 2019
<table>
     <tr>
         <th width="20%">Update</th>  
         <th width="50%">Description</th>  
         <th width=10%>Release Date</th>  
          <th width="15%">Related Documents</th>  
     </tr>
	 <tr>      
         <td>Launch of standard billing plan (Flagship Edition)</td>   
         <td>Standard billing plan (Flagship Edition) is now available with features such as “unlimited audio-video chat rooms”, “30-day message history storage”, and “maximum of 2,000 group members”. This is a one-time purchase to get more features.</td>   
	     <td>2019-12-26</td>   
	     <td><ul style="margin:0;"><li><a href="https://intl.cloud.tencent.com/document/product/1047/34349">Billing Overview</a></li><li><a href="https://intl.cloud.tencent.com/document/product/1047/34350">Price Specification</a></li><li><a href="https://cloud.tencent.com/document/product/269/32458">Purchase Guide</a></li><li><a href="https://intl.cloud.tencent.com/document/product/1047/34577">Create and upgrade applications</a></li></ul></td>   
     </tr> 
	 <tr>      
         <td>SDK 4.6 improvements (Android, iOS and Windows)</td>   
         <td><ul style="margin:0;"><li>Improved network connection quality to quickly detect changes in network quality.</li><li>Better handling of AVChatRoom messages.</li><li>Added getSenderNickname in Message to return sender nicknames synchronously.</li><li>TUIKit/Demo: conversation list profile photos can now be set with rounded corners.</li></ul></td>  
	     <td>2019-12-23</td>   
	     <td>-</td>   
     </tr> 
	 <tr>      
         <td>SDK 2.3 release (Mini Program and Web)</td>   
         <td><ul style="margin:0;"><li>createImageMessage and createFileMessage now support passing File objects.</li><li>Added createFaceMessage to create emoji messages.</li><li>Improved the message delivery efficiency of TIM.TYPES.GRP_AVCHATROOM groups to significantly enhance user experience.</li><li>Adjusted the situation where the SDK returns the actual error codes and error messages when messages fail to be sent.</li><li>Adjusted the situation where calling logout only logs out the message channel of the current instance.</li><li>The callback functions passed in by the access side are encapsulated for security purposes. If there is something wrong with the logic of callback functions, errors can be captured and located quickly.</li><li>The SDK outputs an error messages in Chinese when encountering IM server side error codes.</li><li>Fixed an occasional issue where messages were lost when the app went to the foreground after staying in the background for a long time in the WeChat Mini Program environment.</li><li>Fixed an issue where sending a message triggered multiple TIM.EVENT.CONVERSATION_LIST_UPDATED.</li><li>Fixed an issue where the SDK would report an error while uploading a file (for example, an image) in the event that registerPlugin was not called or the wrong argument was passed.</li><li>Fixed an issue where long polling would not stop after TIM.TYPES.GRP_AVCHATROOM groups were disbanded.</li><li>Fixed an issue where, when “multi-instance” or “multi-device” login was enabled, other instances or devices failed to receive messages after a web instance was logged out.</li><li>Fixed an occasional error that was reported by the SDK due to problem with the structure of the conversation list pulled.</li></ul></td>  
	     <td>2019-12-13</td>   
	     <td>-</td>   
     </tr> 
</table>

## November 2019
<table>
     <tr>
         <th width="20%">Update</th>  
         <th width="50%">Description</th>  
         <th width=10%>Release Date</th>  
          <th width="15%">Related Documents</th>  
     </tr>
	 <tr>      
         <td>SDK 2.2 release (Mini Program and Web)</td>   
         <td><ul style="margin:0;"><li>Mini Program now supports createVideoMessage to create and send video messages. Video messages are supported across platforms. Please update to the latest TUIKit and SDK.</li><li>Added getGroupMemberProfile to query group member profiles.</li><li>Compatible with audio and file messages sent by Native IM v3.x.</li><li>Added support for receiving location messages GeoPayload.</li><li>Fixed an issue where long polling of TIM.TYPES.GRP_AVCHATROOM groups continued after logout.</li><li>Fixed an issue where the group contact cards in message instances of TIM.TYPES.GRP_AVCHATROOM groups did not have values.</li><li>Fixed an issue where the IE 10 browser would report errors.</li><li>Fixed an issue where anonymous users could not join groups.</li></ul></td>   
	     <td>2019-11-21</td>   
	     <td>-</td>   
     </tr> 
	 <tr>      
         <td>SDK 4.6 release (Android, iOS and Windows)</td>   
         <td><ul style="margin:0;"><li>Roaming message recalls is now supported.</li><li>iOS/Mac: added OPPOChannelID to resolve an issue where OPPO mobile phones running Android 8.0 or higher could not receive iOS push notifications.</li><li>iOS/Mac: optimized the annotations of objects returned by getGrouplist.</li><li>The channleID for push notifications of OPPO mobile phones (Android 8.0 or higher is required) can now be set in the console.</li><li>TUIKit/Demo: video calls are now supported.</li><li>TUIKit/Demo: group profile photos can now be displayed as a 3X3 grid consisting of group members’ profile photos; optimized conversation list, contacts, and chat screen UI.</li></ul></td>   
	     <td>2019-11-13</td>   
	     <td>-</td>   
     </tr> 
	 <tr>      
         <td>Fixed pricing for message history storage</td>   
         <td>With fixed pricing, message history storage is easier and more cost-efficient to use.</td>   
	     <td>2019-11-04</td>   
	     <td><a href="https://intl.cloud.tencent.com/document/product/1047/34350">Price Specification</a></td>   
     </tr> 
</table>

## October 2019
<table>
     <tr>
         <th width="20%">Update</th>  
         <th width="50%">Description</th>  
         <th width=10%>Release Date</th>  
          <th width="15%">Related Documents</th>  
     </tr>
	 <tr>      
         <td>Launch of new console</td>   
         <td>-</td>   
	     <td>2019-10-22</td>   
	     <td><ul style="margin:0;"><li><a href="https://intl.cloud.tencent.com/document/product/1047/34577">Create and upgrade applications</a></li><li><a href="https://intl.cloud.tencent.com/document/product/1047/34540">Basic Configuration</a></li><li><a href="https://intl.cloud.tencent.com/document/product/1047/34419">Feature Configuration</a></li><li><a href="https://intl.cloud.tencent.com/document/product/1047/34578">Group Management</a></li><li><a href="https://intl.cloud.tencent.com/document/product/1047/34520">Callback Configuration</a></li><li><a href="https://intl.cloud.tencent.com/document/product/1047/34579">Statistics and Analysis</a></li><li><a href="https://intl.cloud.tencent.com/document/product/1047/34580">Development Aids</a></li></ul></td>   
     </tr> 
	 <tr>      
         <td>SDK 4.5 improvements (Android, iOS and Windows)</td>   
         <td><ul style="margin:0;"><li>Added file format extension to the URL generated upon sending a file message.</li><li>Added notification callback after custom group fields are modified.</li><li>Local user and group information can be obtained before login by calling the initStorage method.</li><li>Android: optimized the return types of getElementCount.</li><li>Windows: improved the network reconnection speed of different platforms across platform libraries.</li><li>Windows: added JVM configuration across platform libraries to make passing JVM from Android environment easier.</li></ul></td>   
	     <td>2019-10-16</td>   
	     <td>-</td>   
     </tr> 
	 <tr>      
         <td>SDK 2.1 release (Mini Program and Web)</td>   
         <td><ul style="margin:0;"><li>Added support for receiving audio and video messages.</li><li>The getMessageList API can now pull up to 15 messages at a time.</li><li>Deprecated TIM.TYPES.MSG_SOUND and replaced it with TIM.TYPES.MSG_AUDIO.</li><li>Fixed an issue where getMessageList could not pull messages in deleted group chats.</li><li>Fixed an issue where group system notifications did not show group name.</li><li>Fixed an issue where conversations created through receiving new messages did not have profiles.</li></ul></td>   
	     <td>2019-10-16</td>   
	     <td>-</td>   
     </tr> 
</table>

## September 2019
<table>
     <tr>
         <th width="20%">Update</th>  
         <th width="50%">Description</th>  
         <th width=10%>Release Date</th>  
          <th width="15%">Related Documents</th>  
     </tr>
	 <tr>      
         <td>SDK 2.0 release (Mini Program and Web)</td>   
         <td>The new IM SDK for Mini Program and IM SDK for Web offer better module stability and overall connection experience, as well as visualized Demo for convenient and easy try-out by customers.</td>   
	     <td>2019-09-19</td>   
	     <td>-</td>   
     </tr> 
	 <tr>      
         <td>SDK 4.5 improvements (Android, iOS and Windows)</td>   
         <td><ul style="margin:0;"><li>Android: added read receipts.</li><li>Improved network connection quality.</li><li>Optimized logic for pulling custom group/group member fields.</li></ul></td>   
	     <td>2019-09-18</td>   
	     <td>-</td>   
     </tr> 
</table>

## August 2019
<table>
     <tr>
         <th width="20%">Update</th>  
         <th width="50%">Description</th>  
         <th width=10%>Release Date</th>  
          <th width="15%">Related Documents</th>  
     </tr>
	 <tr>      
         <td>SDK 4.5 release (Android, iOS and Windows)</td>   
         <td><ul style="margin:0;"><li>Added MotionEvent.ACTION_CANCEL event handling for audio messages in chats.</li><li>Profile photos can now be displayed in the conversation list, chat interface, detailed profile, and contacts.</li><li>Profile photos in user profiles can now be changed.</li><li>Added Intent redirection to offline push functions.</li><li>Random profile photos are now supported in one-to-one chats and group chats.</li><li>Added group tips for granting and revoking group admin role to a group member.</li><li>Added group tips for muting and unmuting group members.</li><li>Optimized unread count.</li><li>Improved conversation list loading speed after login.</li><li>Added the feature of cleaning logs.</li><li>Android: unified the use of the com.tencent.imsdk.TIMGroupReceiveMessageOpt class.</li><li>TUIKit/Demo: added tap feedback to all interfaces, allowing developers to set up and customize feedback in TUIKit.</li><li>TUIKit/Demo: added support for sending custom messages.</li><li>TUIKit/Demo: added C2C read receipts.</li><li>TUIKit/Demo: red dot is displayed on audio messages that have not been played.</li><li>TUIKit/Demo: you can now view large image by tapping on profile photo.</li><li>TUIKit/Demo: modified the style of the small gray bar in group chats so that the member nickname becomes blue and tapping the nickname will direct user to the member’s profile page.</li><li>Optimized logic for pinning a chat to the top and chats are arranged in chronological order starting from the most recent one.</li><li>Optimized the logic for displaying nicknames in a group in Demo.</li><li>Optimized the logic for displaying profile photos on the chat interface.</li><li>Improved unread count.</li><li>Improved conversation list loading speed after login.</li><li>Improved delivery speed of file messages from overseas users.</li></ul></td>   
	     <td>2019-08-30</td>   
	     <td>-</td>   
     </tr> 
	 <tr>      
         <td>Renamed “Instant Messaging (IM)”</td>   
         <td>“Cloud Communication” is now “Instant Messaging (IM)”.</td>   
	     <td>2019-08-06</td>   
	     <td>-</td>   
     </tr> 
</table>

## July 2019
<table>
     <tr>
         <th width="20%">Update</th>  
         <th width="50%">Description</th>  
         <th width=10%>Release Date</th>  
          <th width="15%">Related Documents</th>  
     </tr>
	 <tr>      
         <td>SDK 4.4 improvements (Android, iOS and Windows)</td>   
         <td><ul style="margin:0;"><li>Organized and merged some APIs.</li><li>Added options to add friends in one-way or two-way manner.</li><li>Added disableStorage to disable all local storage.</li><li>Added API to get the download URLs of file, video, and audio messages.</li><li>Improved the login module (repeated login/frequent login/frequent account switching/auto connection/offline user being kicked out).</li><li>Fixed an issue with the excessive time needed to deliver messages when the app went to foreground after staying in background for a long time.</li><li>Optimized unread count for one-to-one chats.</li></ul></td>   
	     <td>2019-07-16</td>   
	     <td>-</td>   
     </tr> 
</table>

## June 2019
<table>
     <tr>
         <th width="20%">Update</th>  
         <th width="50%">Description</th>  
         <th width=10%>Release Date</th>  
          <th width="15%">Related Documents</th>  
     </tr>
	 <tr>      
         <td>SDK 4.4 and new Demo release (Android, iOS and Windows)</td>   
         <td><ul style="margin:0;"><li>The TUIKit with new mobile client UI design and product Demo are now available.</li><li>Improved Demo features such as contacts, group management, and relationship chain.</li><li>Optimized cache to mitigate UI lag.</li><li>Improved message delivery efficiency.</li><li>Added JSON key that gets the unique ID of a message to cross-platform library messages.</li></ul></td>   
	     <td>2019-06-27</td>   
	     <td>-</td>   
     </tr> 
</table>

## May 2019
<table>
     <tr>
         <th width="20%">Update</th>  
         <th width="50%">Description</th>  
         <th width=10%>Release Date</th>  
          <th width="15%">Related Documents</th>  
     </tr>
	 <tr>      
					 <td>SDK 4.3 improvements (Android, iOS and Windows)</td>   
         <td><ul style="margin:0;"><li>Added querySelfProfile and queryUserProfile to the TIMFriendshipManager class to read local data.</li><li>Added the addTime field to getting friend’s profile.</li><li>Added support for x86 and x86_64 architectures.</li><li>Custom field data reporting is now supported.</li><li>Messages that disappear after being viewed are now supported.</li><li> Added use case for recalling messages.</li><li>Added checkFriends to verify friends.</li><li>Added queryGroupInfo to get local data.</li><li>Deprecated getGroupDetailInfo and getGroupPublicInfo in favor of a unified getGroupInfo API.</li><li>Optimized server connection strategy.</li><li>Optimized strategy for reconnection after network disconnection.</li><li>Optimized server overload strategy.</li><li>Optimized heartbeat to reduce unnecessary outbound packets.</li><li>Optimized connection requests during reconnection.</li><li>Optimized the quality of first connections to different networks and overseas access points.</li><li>Improved network reconnection speed when iOS devices switch Wi-Fi networks.</li><li>Optimized group message synchronization.</li></ul></td>   
	     <td>2019-05-24</td>   
	     <td>-</td>   
     </tr> 
</table>

## April 2019
<table>
     <tr>
         <th width="20%">Update</th>  
         <th width="50%">Description</th>  
         <th width=10%>Release Date</th>  
          <th width="15%">Related Documents</th>  
     </tr>
	 <tr>      
         <td>SDK 4.3 release (Android, iOS and Windows)</td>   
         <td><ul style="margin:0;"><li>Added relationship chain features such as blocklist, friend list, and friend request handling.</li><li>Optimized issues related to unread counts.</li><li>Optimized message read status.</li><li>Fixed disorder of C2C messages sent by RESTful API.</li><li>Fixed an occasional issue with repeated messages while fetching roaming messages.</li><li>Optimized empty implementation issue with uniqueId.</li><li>Resolved an issue where TIMMessage failed to get user profiles through senderProfile.</li><li>Fixed issue with read receipt callback and status.</li><li>Fixed issue with the synchronization of unread messages where the last message did not call back.</li><li>Fixed an occasional issue where group messages could not be received.</li><li>Reporting IP connections and login information statistics is now supported.</li></ul></td>   
	     <td>2019-04-24</td>   
	     <td>-</td>   
     </tr> 
</table>

## March 2019
<table>
     <tr>
         <th width="20%">Update</th>  
         <th width="50%">Description</th>  
         <th width=10%>Release Date</th>  
          <th width="15%">Related Documents</th>  
     </tr>
	 <tr>      
         <td>SDK 4.2 release (Android, iOS and Windows)</td>   
         <td><ul style="margin:0;"><li>iOS: TUIKit.framework now supports bitcode 2.</li><li>iOS: pod can now directly integrate with TUIKit.framework.</li><li>Windows: added IM Demo with duilib library as a UI component.</li><li>Windows: added the /source-charset:.65001 compilation option.</li><li>Web: the newly added WEBIM now supports playback of .amr recordings.</li><li>Added logic for adding, deleting, and searching friends.</li><li>Fixed a compatibility issue with audio, file, and video messages between new and older versions.</li><li>Optimized audio playback logic for TUIkit.</li><li>Fixed message receiving error when an AVChatRoom had more than 100 members.</li><li>Fixed ineffective muting in groups.</li><li>Fixed the feature for modifying a user’s role in a group.</li><li>Fixed issue with modifying group message receiving options.</li><li>Fixed ineffective offline push toggle.</li><li>Fixed the feature for modifying a user’s role in a group.</li><li>Fixed an issue where incorrect values were returned when groups retrieved pending and processed requests.</li><li>Fixed a client crash when going to the background.</li><li>Fixed an issue where no messages were received after network reconnection.</li><li>Fixed an occasional error with message sorting.</li><li>Fixed an occasional issue where messages failed to send.</li><li>Fixed an issue where clients did not receive relevant instructions after a group was disbanded by the backend.</li></ul></td>   
	     <td>2019-03</td>   
	     <td>-</td>   
     </tr> 
</table>

## January 2019
<table>
     <tr>
         <th width="20%">Update</th>  
         <th width="50%">Description</th>  
         <th width=10%>Release Date</th>  
          <th width="15%">Related Documents</th>  
     </tr>
	 <tr>      
         <td>SDK 4.0 release (Android, iOS and Windows)</td>   
         <td>The new IM client SDK fixed issues with network connection, sending and receiving messages, and unread count, significantly improved the stability of important underlying modules such as network and message, and provides open source TUIKit to simplify the connection process for customers.</td>   
	     <td>2019-01-21</td>   
	     <td>-</td>   
     </tr> 
</table>

## July 2017
<table>
     <tr>
         <th width="20%">Update</th>  
         <th width="50%">Description</th>  
         <th width=10%>Release Date</th>  
          <th width="15%">Related Documents</th>  
     </tr>
	 <tr>      
         <td>Support for UGC short videos</td>   
         <td>Added support for UGC short video messages with video editing feature, providing better content and user experience.</td>   
	     <td>2017-07</td>   
	     <td>-</td>   
     </tr> 
</table>

## May 2017
<table>
     <tr>
         <th width="20%">Update</th>  
         <th width="50%">Description</th>  
         <th width=10%>Release Date</th>  
          <th width="15%">Related Documents</th>  
     </tr>
	 <tr>      
         <td>SDK 3.0 release</td>   
         <td>More features, smaller size, and optimized code structure to improve customer integration efficiency and download experience.</td>   
	     <td>2017-05</td>   
	     <td>-</td>   
     </tr> 
</table>

## December 2016
<table>
     <tr>
         <th width="20%">Update</th>  
         <th width="50%">Description</th>  
         <th width=10%>Release Date</th>  
          <th width="15%">Related Documents</th>  
     </tr>
	 <tr>      
         <td>Support for multi-instance force offline</td>   
         <td>Meets the needs for multi-instance force offline and for customer service scenario on Web clients.</td>   
	     <td>2016-12</td>   
	     <td>-</td>   
     </tr> 
</table>

## August 2016
<table>
     <tr>
         <th width="20%">Update</th>  
         <th width="50%">Description</th>  
         <th width=10%>Release Date</th>  
          <th width="15%">Related Documents</th>  
     </tr>
	 <tr>      
         <td>Support for broadcast messages</td>   
         <td>Broadcast messages can now be pushed to all members to improve message delivery efficiency and meet customers’ needs for message push.</td>   
	     <td>2016-08</td>   
	     <td>-</td>   
     </tr> 
	 <tr>      
         <td>Support for multi-device login</td>   
         <td>Multi-device login is now supported to meet the need for using both mobile phone and PC, improving user experience.</td>   
	     <td>2016-08</td>   
	     <td>-</td>   
     </tr> 
</table>

## May 2016
<table>
     <tr>
         <th width="20%">Update</th>  
         <th width="50%">Description</th>  
         <th width=10%>Release Date</th>  
          <th width="15%">Related Documents</th>  
     </tr>
	 <tr>      
         <td>Launch of live streaming chat rooms</td>   
         <td>Live streaming chat rooms with unlimited participants are now available for live streaming scenarios, providing features such as message frequency limit and custom messages.</td>   
	     <td>2016-05</td>   
	     <td>-</td>   
     </tr> 
</table>

## March 2016
<table>
     <tr>
         <th width="20%">Update</th>  
         <th width="50%">Description</th>  
         <th width=10%>Release Date</th>  
          <th width="15%">Related Documents</th>  
     </tr>
	 <tr>      
         <td>Support for message push</td>   
         <td>Push notifications in Android and iOS are now supported to ensure message delivery and better user experience.</td>   
	     <td>2016-03</td>   
	     <td>-</td>   
     </tr> 
</table>

## December 2015
<table>
     <tr>
         <th width="20%">Update</th>  
         <th width="50%">Description</th>  
         <th width=10%>Release Date</th>  
          <th width="15%">Related Documents</th>  
     </tr>
	 <tr>      
         <td>Support for short video messages</td>   
         <td>Short video messages are now supported, providing richer message content.</td>   
	     <td>2015-12</td>   
	     <td>-</td>   
     </tr> 
</table>

## August 2015
<table>
     <tr>
         <th width="20%">Update</th>  
         <th width="50%">Description</th>  
         <th width=10%>Release Date</th>  
          <th width="15%">Related Documents</th>  
     </tr>
	 <tr>      
         <td>Support for Web platform</td>   
         <td>IM for Web now supports custom emoji messages.</td>   
	     <td>2015-08</td>   
	     <td>-</td>   
     </tr> 
</table>

## July 2015
<table>
     <tr>
         <th width="20%">Update</th>  
         <th width="50%">Description</th>  
         <th width=10%>Release Date</th>  
          <th width="15%">Related Documents</th>  
     </tr>
	 <tr>      
         <td>Support for Windows platform</td>   
         <td>IM for Windows now supports location and audio messages.</td>   
	     <td>2015-07</td>   
	     <td>-</td>   
     </tr> 
</table>

## May 2015
<table>
     <tr>
         <th width="20%">Update</th>  
         <th width="50%">Description</th>  
         <th width=10%>Release Date</th>  
          <th width="15%">Related Documents</th>  
     </tr>
	 <tr>      
         <td>Launch of Instant Messaging IM (formerly Cloud Communication)</td>   
         <td>IM for Android and IM for iOS support multiple message types including text, image, and emoji.</td>   
	     <td>2015-05</td>   
	     <td>-</td>   
     </tr> 
</table>
