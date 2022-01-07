## Billing Mode
Instant Messaging (IM) is pay-as-you-go on a monthly billing cycle.
- Fees are billed by calendar month. Fees incurred within a calendar month will be deducted on the first to the third day of the next month.


## Basic Services
Three IM plans are available: Trial Edition, Pro Edition, and Flagship Edition. Applications will be assigned the free Trial Edition by default. You can select the plan that best suits your business needs. 
The following table compares the features of different editions:

| Feature | Trial Edition | Pro Edition | Flagship Edition |
| ----------------- |---------- |----------------- | ------------------- |
| Global coverage | Supported | Supported | Supported |
| Maximum users | 100 | Unlimited | Unlimited |
| Maximum friends for a single user | 20 | 3,000 | 3,000 |
| Maximum groups a single user can join | 50 | 500 | 1,000 |
| Maximum members per group (non–audio-video group) | 20 | 200 |  2,000 |
| Maximum non–audio-video groups (deleted groups do not count against the quota) | 100 | Unlimited | Unlimited |
| Maximum audio-video groups that can be created    | 10        | 50          | Unlimited             |
| Maximum net increase in group quantity per day | 10,000 | 10,000 | 10,000 |
| Free retention period of historical messages | 7 days | 7 days | 30 days |
| Quota of free daily active users (DAU) | 100/month | 10,000/month | 10,000/month |
| Free peak group count | 100,000/month | 100,000/month | 100,000/month |
| Pushing to all users | Not supported | Not supported |Supported |
| Concurrent logins on multiple devices on the same platform | Not supported | Not supported |Supported |
| Local message search (Android, iOS) | Not supported | Not supported |Supported |


- **Maximum audio-video groups that can be created**: indicates the total number of audio-video groups that can be created by all users in a single SDKAppID. Audio-video groups support only text, image, short audio, and custom messages. Services such as [Cloud Streaming Services](https://intl.cloud.tencent.com/document/product/267) and [Tencent Real-Time Communication](https://intl.cloud.tencent.com/document/product/647) need to be activated separately.
- **Maximum net increase in group quantity per day**: indicates the net total number of groups (of all types) that can be created by all users in a single SDKAppID in a calendar day. The maximum net increase in group quantity per day is 10,000, in which up to 5 online broadcasting chat rooms can be created. If you have reached the group creation threshold of the day but need to create more groups, you can delete the groups that are no longer needed and create new groups. For more information, see the [Group System](https://intl.cloud.tencent.com/document/product/1047/33529).
- **DAU**: indicates the number of unique users that log in to IM on a given day. A user that logs in repeatedly on the same day only counts as one DAU.
- **Peak group count**: indicates the total number of groups created and joined by all users under a single app (SDKAppID). Charges are billed according to the peak value in a calendar month.

## Value-added Services
Each value-added service has its own billing method. Value-added services are available only for Pro Edition and Ultimate Edition.

<table>
     <tr>
         <th nowrap="nowrap">Service</th>  
         <th>Description</th> 
     </tr>
	 <tr>   
	     <td nowrap="nowrap">Increasing the maximum number of audio-video groups (AvChatRoom) to unlimited</td>   
	     <td>Applies to all users in a single SDKAppID.</td>   
     </tr> 
	 <tr>   
	     <td>Increasing the maximum number of members in a single non–audio-video group</td>   
	     <td>Applies to all groups in a single SDKAppID. Different group types have different member limits. For more information, see <a href="https://intl.cloud.tencent.com/document/product/1047/33515">Group Features</a>.</td>   
     </tr> 
	 <tr>   
	     <td>Increasing the maximum number of groups a single user can join</td>   
	     <td>Applies to all users in a single SDKAppID.</td>   
     </tr> 
	 <tr>   
	     <td>Extending the retention period of historical messages</td>   
	     <td>Applies to a single SDKAppID.<br>While text, image, short audio, short video, and custom messages are supported by this service, different SDK versions allow you to extend the retention period for different message types. For more information, see <a href="https://intl.cloud.tencent.com/document/product/1047/33524">Message Storage</a>. You can extend the retention period to up to 360 days in the <a href="https://console.cloud.tencent.com/im">console</a>.</td>   
     </tr> 
	 <tr>   
	     <td>Audio-video group (AvChatRoom) on-screen comment bandwidth</td>   
	     <td>Applies to all audio-video groups in a single SDKAppID.</td>   
     </tr> 
</table>

## Relevant Documentation
- [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350)
- [Purchase Guide](https://intl.cloud.tencent.com/document/product/1047/34351)
