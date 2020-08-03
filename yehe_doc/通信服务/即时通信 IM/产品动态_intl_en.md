## May 2020

<table>
     <tr>
         <th width="20%">Update</th> 
         <th width="50%">Description</th> 
         <th width="15%">Release Date</th> 
          <th width="15%">Related Documents</th> 
     </tr>
<tr>     
         <td>SDK 4.8 release (Android, iOS, and Windows)</td>  
         <td><ul style="margin:0;"><li>Released API 2.0 for iOS and Android clients.</li>
<li>Supported IPv6 addresses for iOS and Android clients.</li>
<li>Supported the dynamic update of the group member list in audio-video chat rooms (AVChatRoom).</li>
<li>Fixed xlog crashes.</li>
<li>Fixed the issue where the iOS client failed to send large files.</li>
<li>Fixed the issue where the friend remarks in the sender information of the get iOS messages is abnormal.</li>
<li>The IM SDK supports AndroidX.</li>
<li>Fixed Android device crashes due to the network permission issues.</li>
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
         <th width="15%">Release Date</th> 
          <th width="15%">Related Documents</th> 
     </tr>
<tr>     
         <td>SDK 2.6 release (Mini Program and Web)</td>  
         <td><ul style="margin:0;"><li>You can create and send video messages of up to 100 MB on the web client.</li><li>Added the <code>nick</code> and <code>avatar</code> properties to Message to display the nickname and profile photo of the message sender in an audio-video chat room (AVChatRoom). To set the nickname and profile photo of the message sender, you must call updateMyProfile in advance.</li><li>When an account logs in on multiple instances, namely, multiple webpages or web browsers, the C2C message cancellation notification can be synchronized between these webpages or web browsers.</li><li>When group custom fields are modified by calling updateGroupProfile, group members will receive group prompts and related content Message.payload.newGroupProfile.groupCustomField.</li><li>Deprecated TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVED and replaced it with MESSAGE_RECEIVED.</li><li>Fixed the issue where errors were reported occasionally when getGroupList was called.</li></ul></td>  
     <td>2020-03-30</td>  
     <td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDK Download</a></td>  
     </tr>
<tr>     
         <td>SDK 4.7 release (Android, iOS, and Windows)</td>  
         <td><ul style="margin:0;"><li>Reduced the local log size.</li>
<li>Improved the login speed.</li>
<li>Fixed the issue with unread count synchronization across multiple devices.</li>
<li>Added getFriendList to get single friends.</li>
<li>You can set the message title and content to display on the offline push notifications bar on iOS and Android devices, respectively.</li>
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
         <th width="15%">Release Date</th> 
          <th width="15%">Related Documents</th> 
     </tr>
<tr>     
         <td>SDK 4.6 improvements (Android, iOS, and Windows)</td>  
         <td><ul style="margin:0;"><li>Increased the file upload limit to 100 MB.</li><li>Optimized COS uploads.</li><li>Optimized the logic for processing group pending requests.</li></ul></td>  
     <td>2020-02-28</td>  
     <td>-</td>  
     </tr>
<tr>     
         <td>SDK 2.5 release (Mini Program and Web)</td>  
         <td><ul style="margin:0;"><li>Added network status change event TIM.EVENT.NET_STATE_CHANGE. The access side can provide prompts and instructions based on the event.</li><li>Running in WeChat Mini Program plug-in environments is supported.</li><li>Reduced and optimized error codes.</li><li>Fixed the issue where messages sent by other group members were repeated on the group owner side after an audio-video chat room (AVChatRoom) was created in the console and a group owner was specified and joined the group.</li><li>Fixed the issue where the SDK did not distribute TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVED events when groups were created and terminated in the console or using a RESTful API frequently.</li><li>Fixed the issue where getMessageList occasionally failed to get the group message list.</li></ul></td>  
     <td>2020-02-28</td>  
     <td>-</td>  
     </tr>
</table>

## January 2020

<table>
     <tr>
         <th width="20%">Update</th> 
         <th width="50%">Description</th> 
         <th width="15%">Release Date</th> 
          <th width="15%">Related Documents</th> 
     </tr>
<tr>     
         <td>SDK 2.4 release (Mini Program and Web)</td>  
         <td><ul style="margin:0;"><li>Added the revokeMessage API to recall messages.</li><li>Added the isRevoked property in Message, which identifies a recalled message when its value is true.</li><li>Added TIM.EVENT.MESSAGE_REVOKED to notify message recalls.</li><li>Added the force offline types "force offline due to multi-device login" and "force offline due to UserSig expiration" in the force offline event notification TIM.EVENT.KICKED_OUT.</li><li>Increased the file upload limit for createFileMessage from 20 MB to 100 MB.</li><li>msgMemberInfo and shutupTime of group prompts will be deprecated soon. Use memberList and muteTime instead.</li><li>Added an entry to IM smart customer service in the console.</li><li>Fixed the issue where calling the off API could not cancel listening events.</li><li>Fixed the inaccurate value and type of the isRead property in Message.</li><li>Fixed the issue where incorrect error codes and error messages were returned when the size of a video message exceeded the limit.</li><li>Fixed the issue where the content of updated custom fields was occasionally inaccurate.</li><li>Fixed the issue where JOIN_STATUS_ALREADY_IN_GROUP was seen occasionally when a logged in user joined an audio-video chat room.</li><li>Fixed potential performance issues caused by core-js.</li></ul></td>  
     <td>2020-01-03</td>  
     <td>-</td>  
     </tr>
</table>

## December 2019
<table>
     <tr>
         <th width="20%">Update</th> 
         <th width="50%">Description</th> 
         <th width="15%">Release Date</th> 
          <th width="15%">Related Documents</th> 
     </tr>
<tr>     
         <td>Launch of the standard billing plan (Flagship Edition)</td>  
         <td>The standard billing plan (Flagship Edition) is available with features such as "unlimited audio-video chat rooms", "30-day message history storage", and "up to 2,000 group members". This is a one-time purchase of additional features.</td>  
     <td>2019-12-26</td>  
     <td><ul style="margin:0;"><li><a href="https://intl.cloud.tencent.com/document/product/1047/34349">Billing Overview</a></li><li><a href="https://intl.cloud.tencent.com/document/product/1047/34350">Pricing</a></li><li><a href="https://intl.cloud.tencent.com/document/product/1047/34577">Creating and Upgrading Applications</a></li></ul></td>  
     </tr>
<tr>     
         <td>SDK 4.6 improvements (Android, iOS, and Windows)</td>  
         <td><ul style="margin:0;"><li>Improved the network connection quality to quickly detect network quality changes.</li><li>Optimized audio-video chat room (AVChatRoom) message processing.</li><li>Added getSenderNickname in Message to return the sender's nickname synchronously.</li><li>TUIKit/Demo: supported round corners for conversation list profile photos.</li></ul></td> 
     <td>2019-12-23</td>  
     <td>-</td>  
     </tr>
<tr>     
         <td>SDK 2.3 release (Mini Program and Web)</td>  
         <td><ul style="margin:0;"><li>createImageMessage and createFileMessage support passing File objects.</li><li>Added createFaceMessage to create emoji messages.</li><li>Improved the message delivery efficiency of TIM.TYPES.GRP_AVCHATROOM groups to significantly improve the user experience.</li><li>Adjusted the actual error codes and error messages returned by the SDK when messages failed to be sent.</li><li>Adjusted the situation where calling logout only logs out the message channel of the current instance.</li><li>The callback functions passed in by the access side are encapsulated for security purposes. If there is something wrong with the logic of callback functions, errors can be captured and located quickly.</li><li>The SDK generates an error message in Chinese when encountering IM server side error codes.</li><li>Fixed the issue in the WeChat Mini Program environment where messages were lost occasionally when the app went to the foreground after staying in the background for a long time.</li><li>Fixed the issue where sending a message triggered multiple TIM.EVENT.CONVERSATION_LIST_UPDATED events.</li><li>Fixed the issue where the SDK reported an error when a file (such as an image) was uploaded when registerPlugin was not called or an incorrect parameter was passed.</li><li>Fixed the issue where long polling did not stop after TIM.TYPES.GRP_AVCHATROOM groups were disbanded.</li><li>Fixed the issue where other instances or clients failed to receive messages after a web instance was logged out when "multi-instance" or "multi-client" login was enabled.</li><li>Fixed the issue where the SDK reported an error occasionally due to the structure of the conversation list pulled.</li></ul></td> 
     <td>2019-12-13</td>  
     <td>-</td>  
     </tr>
</table>

## November 2019
<table>
     <tr>
         <th width="20%">Update</th> 
         <th width="50%">Description</th> 
         <th width="15%">Release Date</th> 
          <th width="15%">Related Documents</th> 
     </tr>
<tr>     
         <td>SDK 2.2 release (Mini Program and Web)</td>  
         <td><ul style="margin:0;"><li>Mini Program supports createVideoMessage to create and send video messages. Video messages are supported across platforms. Please update to the latest TUIKit and SDK.</li><li>Added getGroupMemberProfile to query group members' profiles.</li><li>Compatible with audio and file messages sent by Native IM v3.x.</li><li>Supported receiving GeoPayload location messages.</li><li>Fixed the issue where long polling of TIM.TYPES.GRP_AVCHATROOM groups continued after logout.</li><li>Fixed the issue where group contact cards in message instances of TIM.TYPES.GRP_AVCHATROOM groups did not have values.</li><li>Fixed the issue where errors were reported when IE 10 was used.</li><li>Fixed the issue where anonymous users could not join groups.</li></ul></td>  
     <td>2019-11-21</td>  
     <td>-</td>  
     </tr>
<tr>     
         <td>SDK 4.6 release (Android, iOS, and Windows)</td>  
         <td><ul style="margin:0;"><li>Roaming messages can be recalled.</li><li>iOS/Mac: added OPPOChannelID to fix the issue where OPPO mobile phones running Android 8.0 or later could not receive iOS push notifications.</li><li>iOS/Mac: optimized the annotations of objects returned by getGrouplist.</li><li>channleID for push notifications of OPPO mobile phones (Android 8.0 or later) can be set in the console.</li><li>TUIKit/Demo: video calls are supported.</li><li>TUIKit/Demo: group profile photos can be displayed as a 3X3 grid consisting of group members' profile photos. Optimized conversation list, contact, and chat UIs.</li></ul></td>  
     <td>2019-11-13</td>  
     <td>-</td>  
     </tr>
<tr>     
         <td>Fixed pricing for message history storage</td>  
         <td>With fixed pricing, message history storage is easier and more cost-effective to use.</td>  
     <td>2019-11-04</td>  
     <td><a href="https://intl.cloud.tencent.com/document/product/1047/34350">Price Specification</a></td>  
     </tr>
</table>

## October 2019
<table>
     <tr>
         <th width="20%">Update</th> 
         <th width="50%">Description</th> 
         <th width="15%">Release Date</th> 
          <th width="15%">Related Documents</th> 
     </tr>
<tr>     
         <td>Launch of the new console</td>  
         <td>-</td>  
     <td>2019-10-22</td>  
     <td><ul style="margin:0;"><li><a href="https://intl.cloud.tencent.com/document/product/1047/34577">Creating and Upgrading Applications</a></li><li><a href="https://intl.cloud.tencent.com/document/product/1047/34540">Basic Configuration</a></li><li><a href="https://intl.cloud.tencent.com/document/product/1047/34419">Feature Configuration</a></li><li><a href="https://intl.cloud.tencent.com/document/product/1047/34578">Group Management</a></li><li><a href="https://intl.cloud.tencent.com/document/product/1047/34520">Callback Configuration</a></li><li><a href="https://intl.cloud.tencent.com/document/product/1047/34579">Statistics and Analysis</a></li><li><a href="https://intl.cloud.tencent.com/document/product/1047/34580">Auxiliary Development Tools</a></li></ul></td>  
     </tr>
<tr>     
         <td>SDK 4.5 improvements (Android, iOS, and Windows)</td>  
         <td><ul style="margin:0;"><li>Added file format extensions to the URLs generated upon sending a file message.</li><li>Added a notification callback after custom group fields are modified.</li><li>Local user and group information can be obtained before login by calling the initStorage method.</li><li>Android: optimized the getElementCount return types.</li><li>Windows: improved the network reconnection speed of different platforms across platform libraries.</li><li>Windows: added JVM configurations across platform libraries to make passing JVM from Android environments easier.</li></ul></td>  
     <td>2019-10-16</td>  
     <td>-</td>  
     </tr>
<tr>     
         <td>SDK 2.1 release (Mini Program and Web)</td>  
         <td><ul style="margin:0;"><li>Supported receiving audio and video messages.</li><li>The getMessageList API can pull up to 15 messages at a time.</li><li>Deprecated TIM.TYPES.MSG_SOUND and replaced it with TIM.TYPES.MSG_AUDIO.</li><li>Fixed the issue where getMessageList could not get messages in deleted group chats.</li><li>Fixed the issue where group notifications did not show the group name.</li><li>Fixed the issue where the conversion did not have the profile of the message sender when a conversation was created after receiving a new message.</li></ul></td>  
     <td>2019-10-16</td>  
     <td>-</td>  
     </tr>
</table>

## September 2019
<table>
     <tr>
         <th width="20%">Update</th> 
         <th width="50%">Description</th> 
         <th width="15%">Release Date</th> 
          <th width="15%">Related Documents</th> 
     </tr>
<tr>     
         <td>SDK 2.0 release (Mini Program and Web)</td>  
         <td>The new IM SDK for Mini Programs and web offers better module stability and overall connection experience, as well as a visual demo that allows customers to easily try out the features.</td>  
     <td>2019-09-19</td>  
     <td>-</td>  
     </tr>
<tr>     
         <td>SDK 4.5 improvements (Android, iOS, and Windows)</td>  
         <td><ul style="margin:0;"><li>Android: added read receipts.</li><li>Improved the network connection quality.</li><li>Optimized the logic for getting custom group/group member fields.</li></ul></td>  
     <td>2019-09-18</td>  
     <td>-</td>  
     </tr>
</table>

## August 2019
<table>
     <tr>
         <th width="20%">Update</th> 
         <th width="50%">Description</th> 
         <th width="15%">Release Date</th> 
          <th width="15%">Related Documents</th> 
     </tr>
<tr>     
         <td>SDK 4.5 release (Android, iOS, and Windows)</td>  
         <td><ul style="margin:0;"><li>Added the MotionEvent.ACTION_CANCEL event handling for audio messages in chats.</li><li>Profile photos can be displayed in the conversation list, chat interface, detailed profile, and contacts.</li><li>Profile photos in user profiles can be changed.</li><li>Added Intent redirection to offline push features.</li><li>Random profile photos are supported in one-to-one chats and group chats.</li><li>Added group prompts for granting and revoking the group admin role for a group member.</li><li>Added group prompts for muting and unmuting group members.</li><li>Optimized the unread count.</li><li>Improved the conversation list loading speed after login.</li><li>Added a feature for cleaning logs.</li><li>Android: unified the use of the com.tencent.imsdk.TIMGroupReceiveMessageOpt class.</li><li>TUIKit/Demo: added tap feedback to all interfaces, allowing developers to set up and customize feedback in TUIKit.</li><li>TUIKit/Demo: supported sending custom messages.</li><li>TUIKit/Demo: added C2C read receipts.</li><li>TUIKit/Demo: a red dot is displayed on audio messages that have not been played.</li><li>TUIKit/Demo: you can view a large image by tapping on the profile photo.</li><li>TUIKit/Demo: modified the style of the small gray bar in group chats so that the member nickname becomes blue and tapping the nickname will direct a user to the member's profile page.</li><li>Optimized the logic for pinning a chat to the top of the list. Chats are arranged in chronological order starting from the most recent one.</li><li>Optimized the logic for displaying nicknames in a group in the demo.</li><li>Optimized the logic for displaying profile photos on the chat interface.</li><li>Optimized the unread count.</li><li>Improved the conversation list loading speed after login.</li><li>Improved the speed of file sending by users outside China.</li></ul></td>  
     <td>2019-08-30</td>  
     <td>-</td>  
     </tr>
<tr>     
         <td>Renamed "Instant Messaging (IM)"</td>  
         <td>"Cloud Communication" is renamed "Instant Messaging (IM)".</td>  
     <td>2019-08-06</td>  
     <td>-</td>  
     </tr>
</table>

## July 2019
<table>
     <tr>
         <th width="20%">Update</th> 
         <th width="50%">Description</th> 
         <th width="15%">Release Date</th> 
          <th width="15%">Related Documents</th> 
     </tr>
<tr>     
         <td>SDK 4.4 improvements (Android, iOS, and Windows)</td>  
         <td><ul style="margin:0;"><li>Organized and merged some APIs.</li><li>Added options to add friends in one-way and two-way manners.</li><li>Added disableStorage to disable all local storage.</li><li>Added an API to get the download URLs of file, video, and audio messages.</li><li>Optimized the login module (repeated login/frequent login/frequent account switching/auto connection/offline user kicked out).</li><li>Fixed the issue it took too long to deliver messages when the app went to the foreground after staying in the background for a long time.</li><li>Optimized the unread count for one-to-one chats.</li></ul></td>  
     <td>2019-07-16</td>  
     <td>-</td>  
     </tr>
</table>

## June 2019
<table>
     <tr>
         <th width="20%">Update</th> 
         <th width="50%">Description</th> 
         <th width="15%">Release Date</th> 
          <th width="15%">Related Documents</th> 
     </tr>
<tr>     
         <td>SDK 4.4 and new Demo release (Android, iOS, and Windows)</td>  
         <td><ul style="margin:0;"><li>The TUIKit with a new mobile client UI design and product Demo are available.</li><li>Optimized demo features such as contacts, group management, and relationship chain.</li><li>Optimized the cache to mitigate UI lag.</li><li>Improved the message delivery efficiency.</li><li>Added the JSON key used to get the unique ID of messages across platform libraries.</li></ul></td>  
     <td>2019-06-27</td>  
     <td>-</td>  
     </tr>
</table>

## May 2019
<table>
     <tr>
         <th width="20%">Update</th> 
         <th width="50%">Description</th> 
         <th width="15%">Release Date</th> 
          <th width="15%">Related Documents</th> 
     </tr>
<tr>     
<td>SDK 4.3 improvements (Android, iOS, and Windows)</td>  
         <td><ul style="margin:0;"><li>Added querySelfProfile and queryUserProfile to the TIMFriendshipManager class to read local data.</li><li>Added the addTime field for getting a friend's profile.</li><li>Supported x86 and x86_64 architectures.</li><li>Supported custom field data reporting.</li><li>Supported messages that disappear after being viewed.</li><li>Added use case for recalling messages.</li><li>Added checkFriends to verify friends.</li><li>Added queryGroupInfo to get local data.</li><li>Deprecated getGroupDetailInfo and getGroupPublicInfo in favor of a unified getGroupInfo API.</li><li>Optimized the server connection strategy.</li><li>Optimized the strategy for reconnection after network disconnection.</li><li>Optimized the server overload strategy.</li><li>Optimized the heartbeat feature to reduce unnecessary outbound packets.</li><li>Optimized connection requests during reconnection.</li><li>Optimized the quality of first connections to different networks and access points outside China.</li><li>Improved the network reconnection speed when iOS devices switch Wi-Fi networks.</li><li>Optimized group message synchronization.</li></ul></td>  
     <td>2019-05-24</td>  
     <td>-</td>  
     </tr>
</table>

## April 2019
<table>
     <tr>
         <th width="20%">Update</th> 
         <th width="50%">Description</th> 
         <th width="15%">Release Date</th> 
          <th width="15%">Related Documents</th> 
     </tr>
<tr>     
         <td>SDK 4.3 release (Android, iOS, and Windows)</td>  
         <td><ul style="margin:0;"><li>Added relationship chain features such as blocklist, friend list, and friend request handling.</li><li>Optimized issues related to unread counts.</li><li>Fixed the message read issue.</li><li>Fixed disordered C2C messages sent by a RESTful API.</li><li>Fixed the issue where fetched roaming messages were occasionally repeated.</li><li>Optimized the empty implementation issue with uniqueId.</li><li>Fixed the issue where TIMMessage failed to get user profiles through senderProfile.</li><li>Fixed the issue with read receipt callbacks and statuses.</li><li>Fixed the issue where the last message did not trigger a callback when unread messages were synchronized.</li><li>Fixed the issue where group messages occasionally could not be received.</li><li>Supported reporting IP connections and login information statistics.</li></ul></td>  
     <td>2019-04-24</td>  
     <td>-</td>  
     </tr>
</table>

## March 2019
<table>
     <tr>
         <th width="20%">Update</th> 
         <th width="50%">Description</th> 
         <th width="15%">Release Date</th> 
          <th width="15%">Related Documents</th> 
     </tr>
<tr>     
         <td>SDK 4.2 release (Android, iOS, and Windows)</td>  
         <td><ul style="margin:0;"><li>iOS: TUIKit.framework supports bitcode 2.</li><li>iOS: pods can be directly integrated with TUIKit.framework.</li><li>Windows: added an IM demo with the duilib library as a UI component.</li><li>Windows: added the /source-charset:.65001 compilation option.</li><li>Web: the newly added WEBIM supports playback of .amr recordings.</li><li>Added logic for adding, deleting, and searching for friends.</li><li>Fixed the compatibility issues with audio, file, and video messages between earlier and later versions.</li><li>Optimized the audio playback logic for TUIkit.</li><li>Fixed the message receiving error when an audio-video chat room (AVChatRoom) had more than 100 members.</li><li>Fixed ineffective muting in groups.</li><li>Optimized the feature for modifying a user's role in a group.</li><li>Fixed the issue with modifying group message receiving options.</li><li>Fixed the ineffective offline push switch issue.</li><li>Optimized the feature for modifying a user's role in a group.</li><li>Fixed the issue where incorrect values were returned when groups received pending and processed requests.</li><li>Fixed the issue where the client crashed when going to the background.</li><li>Fixed the issue where no messages were received after network reconnection.</li><li>Fixed the issue where message sorting was occasionally incorrect.</li><li>Fixed the issue where messages occasionally failed to be sent.</li><li>Fixed the issue where clients did not receive relevant instructions after a group was disbanded in the backend.</li></ul></td>  
     <td>2019-03</td>  
     <td>-</td>  
     </tr>
</table>

## January 2019
<table>
     <tr>
         <th width="20%">Update</th> 
         <th width="50%">Description</th> 
         <th width="15%">Release Date</th> 
          <th width="15%">Related Documents</th> 
     </tr>
<tr>     
         <td>SDK 4.0 release (Android, iOS, and Windows)</td>  
         <td>The new IM client SDK fixed issues with network connection, sending and receiving messages, and unread counts, significantly improved the stability of important underlying modules such as the network and message modules, and provided open-source TUIKit to simplify the connection process for customers.</td>  
     <td>2019-01-21</td>  
     <td>-</td>  
     </tr>
</table>

## July 2017
<table>
     <tr>
         <th width="20%">Update</th> 
         <th width="50%">Description</th> 
         <th width="15%">Release Date</th> 
          <th width="15%">Related Documents</th> 
     </tr>
<tr>     
         <td>Support for UGC short videos</td>  
         <td>Supported UGC short video messages with the video editing feature, providing better content and a better user experience.</td>  
     <td>2017-07</td>  
     <td>-</td>  
     </tr>
</table>

## May 2017
<table>
     <tr>
         <th width="20%">Update</th> 
         <th width="50%">Description</th> 
         <th width="15%">Release Date</th> 
          <th width="15%">Related Documents</th> 
     </tr>
<tr>     
         <td>SDK 3.0 release</td>  
         <td>Added more features, reduced the size, and optimized the code structure to improve the customer integration efficiency and download experience.</td>  
     <td>2017-05</td>  
     <td>-</td>  
     </tr>
</table>

## December 2016
<table>
     <tr>
         <th width="20%">Update</th> 
         <th width="50%">Description</th> 
         <th width="15%">Release Date</th> 
          <th width="15%">Related Documents</th> 
     </tr>
<tr>     
         <td>Support for multi-instance force offline</td>  
         <td>Met the needs for multi-instance force offline and customer service on web clients.</td>  
     <td>2016-12</td>  
     <td>-</td>  
     </tr>
</table>

## August 2016
<table>
     <tr>
         <th width="20%">Update</th> 
         <th width="50%">Description</th> 
         <th width="15%">Release Date</th> 
          <th width="15%">Related Documents</th> 
     </tr>
<tr>     
         <td>Support for broadcast messages</td>  
         <td>Broadcast messages can be pushed to all members to improve the message delivery efficiency and meet customers' needs for message push.</td>  
     <td>2016-08</td>  
     <td>-</td>  
     </tr>
<tr>     
         <td>Support for multi-device login</td>  
         <td>Multi-device login is supported to meet the needs of users who use both a mobile phone and PC and improve the user experience.</td>  
     <td>2016-08</td>  
     <td>-</td>  
     </tr>
</table>

## May 2016
<table>
     <tr>
         <th width="20%">Update</th> 
         <th width="50%">Description</th> 
         <th width="15%">Release Date</th> 
          <th width="15%">Related Documents</th> 
     </tr>
<tr>     
         <td>Launch of broadcasting chat rooms</td>  
         <td>Broadcasting chat rooms with unlimited participants are available for live streaming scenarios, with support for features such as message frequency limits and custom messages.</td>  
     <td>2016-05</td>  
     <td>-</td>  
     </tr>
</table>

## March 2016
<table>
     <tr>
         <th width="20%">Update</th> 
         <th width="50%">Description</th> 
         <th width="15%">Release Date</th> 
          <th width="15%">Related Documents</th> 
     </tr>
<tr>     
         <td>Support for message push</td>  
         <td>Offline push notifications in Android and iOS are supported to ensure message delivery and a better user experience.</td>  
     <td>2016-03</td>  
     <td>-</td>  
     </tr>
</table>

## December 2015
<table>
     <tr>
         <th width="20%">Update</th> 
         <th width="50%">Description</th> 
         <th width="15%">Release Date</th> 
          <th width="15%">Related Documents</th> 
     </tr>
<tr>     
         <td>Support for short video messages</td>  
         <td>Short video messages are supported, providing richer message content.</td>  
     <td>2015-12</td>  
     <td>-</td>  
     </tr>
</table>

## August 2015
<table>
     <tr>
         <th width="20%">Update</th> 
         <th width="50%">Description</th> 
         <th width="15%">Release Date</th> 
          <th width="15%">Related Documents</th> 
     </tr>
<tr>     
         <td>Support for Web platform</td>  
         <td>IM for web supports custom emoji messages.</td>  
     <td>2015-08</td>  
     <td>-</td>  
     </tr>
</table>

## July 2015
<table>
     <tr>
         <th width="20%">Update</th> 
         <th width="50%">Description</th> 
         <th width="15%">Release Date</th> 
          <th width="15%">Related Documents</th> 
     </tr>
<tr>     
         <td>Support for Windows platform</td>  
         <td>IM for Windows supports location and audio messages.</td>  
     <td>2015-07</td>  
     <td>-</td>  
     </tr>
</table>

## May 2015
<table>
     <tr>
         <th width="20%">Update</th> 
         <th width="50%">Description</th> 
         <th width="15%">Release Date</th> 
          <th width="15%">Related Documents</th> 
     </tr>
<tr>     
         <td>Launch of IM (formerly Cloud Communication)</td>  
         <td>IM for Android and IM for iOS support multiple message types, including text, image, and emoji.</td>  
     <td>2015-05</td>  
     <td>-</td>  
     </tr>
</table>
