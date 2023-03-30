## Billing Overview
IM is billed on a monthly billing cycle:
- Fees are billed by calendar month. Fees incurred in a calendar month will be deducted within the first 3 days of the next month.


## Basic Services
The basic service fee covers two parts: the **resource plan** fee and **resource usage exceeding the quota in a plan** fee.
- Resource plan: IM offers the Free, Pro, and Ultimate editions. The edition for a created application defaults to the Free edition (free). You can choose a plan based on your needs. For resource plan comparison, see [Comparison of billing plans](#tc).
- Fees for out-of-plan resource usage: The fees charged for DAU count and peak group count that exceed the free quota of the Pro or Ultimate edition plan.


<dx-alert infotype="explain" title="Notes:">
- The feature of pushing to all users is available only to users with Ultimate edition accounts. You can apply for this feature as instructed in [Configuration Change Ticket](https://www.tencentcloud.com/document/product/1047/44322). The feature will be enabled **48 hours** after your application is approved.
- The community feature is available in native SDK 5.8.1668 (enhanced) or later and web SDK 2.17.0 or later and only to users with Ultimate edition accounts (it will be unavailable after you change to the Pro edition). You can apply for this feature as instructed in [Configuration Change Ticket](https://www.tencentcloud.com/document/product/1047/44322). You can create up to 100,000 communities.
- The feature of read receipts for group messages is available in native SDK 6.1.2155 or later and only to Ultimate edition users. It is applicable to work groups (Work), public groups (Public), and meeting groups (Meeting) that support up to 200 members per group.
</dx-alert>

[](id:tc)
The following table compares the features of different plans:

| Feature | Free | Pro | Ultimate|
| ----------------- |---------- |----------------- | ------------------- |
| Global coverage | Supported | Supported | Supported |
| Maximum users | 100 | Unlimited | Unlimited |
| Maximum friends for a single user | 20 | 3,000 | 3,000 |
| Maximum groups a single user can join | 50 | 500 | 1,000 |
| Maximum members per group (non–audio-video group) | 20 | 200 |  2,000 |
| Maximum non–audio-video groups (excluding disbanded ones) | 100 | Unlimited | Unlimited |
| Maximum audio-video groups that can be created    | 10        | 50          | Unlimited             |
| Maximum net increase in group quantity per day | 10,000 | 10,000 | 10,000 |
| Free retention period of historical messages | 7 days | 7 days | 30 days |
| Quota of free daily active users (DAU) | 100/month | 10,000/month | 10,000/month |
| Free peak group count | 100,000/month | 100,000/month | 100,000/month |
| [Pushing to all users](https://intl.cloud.tencent.com/document/product/1047/37165) | Not supported | Not supported |Supported|
| Concurrent logins on multiple devices on the same platform | Not supported | Not supported |Supported |
| Local message search (Android and iOS) | Not supported | Not supported |Supported |
| Message history for new members in audio-video groups | Not supported | Not supported |Supported |
| [Community](https://intl.cloud.tencent.com/document/product/1047/33529)   | Not supported | Not supported |Supported|
| Read receipts for group messages  | Not supported | Not supported | Supported |
|Targeted group messages | Not supported | Not supported| Supported|
| List of online audio-video group members | Not supported | Not supported | Supported |
| Broadcast messaging of audio-video group   | Not supported | Not supported| Supported |
| User status      | Not supported | Not supported | Supported |
| Conversation mark  | Not supported | Not supported | Supported |
| Conversation group | Not supported | Not supported | Supported |
|Audio-video group member banning | Not supported |Not supported | Supported  |



- **Maximum audio-video groups that can be created**: The total number of audio-video groups that can be created by all users under an application (SDKAppID). Audio-video groups support only text, image, short audio, and custom messages. Services such as [Cloud Streaming Services](https://intl.cloud.tencent.com/document/product/267) and [Tencent Real-Time Communication](https://intl.cloud.tencent.com/document/product/647) need to be activated separately.
- **Maximum net increase in group quantity per day**: The net total number of groups (of all types) that can be created by all users under an application (SDKAppID) in a calendar day. Its value is 10,000, and up to 5 online broadcasting chat rooms can be created. If the quantity of groups created reaches the threshold of the day, but you need to create more groups, delete the groups that are no longer needed. For more information, see [Groups](https://intl.cloud.tencent.com/document/product/1047/33529).
- **DAU**: The number of unique users that log in to IM on a given day. A user that logs in repeatedly on the same day only counts as one DAU.
- **Peak group count**: indicates the total number of groups created and joined by all users under an application (SDKAppID). Charges are billed according to the peak value in a calendar month.
- **Community**: A community allows users to join and leave freely. It is suitable for chat scenarios with a super large number of community members, such as knowledge sharing and game discussion. For more information, see [Groups](https://intl.cloud.tencent.com/document/product/1047/33529).


## Value-Added Services
Each value-added service is subject to a separate billing method. Value-added services are available only in Pro and Ultimate editions.

> ! The free edition of the audio/video call feature (a value-added service) is available under the Free edition plan.

<table>
     <tr>
         <th nowrap="nowrap">Billable Item</th>  
         <th>Description</th> 
     </tr>
	 <tr>   
	     <td nowrap="nowrap">Setting the number of audio-video groups (AvChatRoom) to unlimited</td>   
	     <td>Applies to all users under an application (SDKAppID).</td>   
     </tr> 
	 <tr>   
	     <td>Increasing the maximum members per non-audio-video group</td>   
	     <td>Applies to all groups under an application (SDKAppID). Different group types have different member limits. For more information, see <a href="https://www.tencentcloud.com/zh/document/product/1047/33515#.E7.BE.A4.E7.BB.84.E5.8A.9F.E8.83.BD">Group Features</a>.</td>   
     </tr> 
	 <tr>   
	     <td>Increasing the maximum number of groups a single user can join</td>   
	     <td>Applies to all users under an application (SDKAppID).</td>   
     </tr> 
	 <tr>   
	     <td>Extending the retention period of historical messages</td>   
	     <td>Applies to a single application (SDKAppID).<br>While this service supports extending the retention periods of text, image, short audio, short video, file, and custom messages, specific message types supported vary by SDK version. For more information, see <a href="https://intl.cloud.tencent.com/document/product/1047/33524">Message Storage</a>. You can extend the retention period to up to 360 days in the <a href="https://console.cloud.tencent.com/im">console</a>.</td>  
   </tr> 
	 <tr>
	 <td>Audio/video call feature</td>
	 <td><li><b>It is currently in beta, with a 60-day free edition provided. </b></li><li>It applies to an individual application (SDKAppID) and supports status display, multi-client login, and cutting in a group call. The <b>free edition</b> of the audio/video call feature provides all feature items. For more details, see <a href="">Audio/video call feature details</a>.</li></td>
	 </tr>
</table>


Audio/video call feature details:

| Feature                  | Free Edition            |
| :---------------------- | :---------------- |
| Audio/video call          | Supported              |
| Complete chat UI         | Supported              |
| Call status display        | Supported              |
| Calling notification        | Supported             |
| Floating window for call   | Supported              |
| Custom calling ringtone          | Supported              |
| Call launching/answering/rejecting/hanging up | Supported              |
| Group call                | Supported              |
| Launching/Cutting in a group call   | Supported              |
| Switch from video call to audio call    | Supported              |
| AI-based noise reduction                | Supported              |
| Outdoor calls optimization         | Supported              |
| Platform                | iOS, Android, Web |

<dx-alert infotype="explain" title="Notes:">

- A value-added service applies to the application (SDKAppID) bound only. To upgrade the services for multiple applications (SDKAppID), handle them one by one.
- Increasing the maximum members per group:
   - Different group types have different member limits. For more information, see [Group Features](https://www.tencentcloud.com/zh/document/product/1047/33515#.E7.BE.A4.E7.BB.84.E5.8A.9F.E8.83.BD).
   - After you purchase the [Increasing the max members per group](https://www.tencentcloud.com/document/product/1047/34577) service or upgrade your plan, call [RESTful API](https://intl.cloud.tencent.com/document/product/1047/34962) to update the group member limits before adjusting the member limits of existing non-audio-video groups.
- Extending the retention period of historical messages: The service supports extending the retention period of text, image, short audio, short video, file and custom messages, but specific message types supported vary by SDK version. For more information, see [Message Storage](https://intl.cloud.tencent.com/document/product/1047/33524). Since this service requires additional resources, fees will be charged by month from the month the service is activated. We recommend you activate the service at a proper time.
- **Audio/video call feature**:
  - **The Audio/video call feature is currently in beta, with a 60-day free edition provided**.
  - It is implemented based on IM and TRTC services. Therefore, the TRTC service will be activated and applications created for you by default if you enable this feature.
  - Its free edition **only grants you the right to use the free edition free of charge. Your calls launched via this feature will be charged as stated in [Billing of TRTC Basic Services](https://www.tencentcloud.com/zh/document/product/647/42734), and relevant IM services will be charged as stated in [Billing Overview](https://www.tencentcloud.com/zh/document/product/1047/34349) of IM**.
    </dx-alert>


## References
- [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350)
- [Purchase Guide](https://intl.cloud.tencent.com/document/product/1047/34351)