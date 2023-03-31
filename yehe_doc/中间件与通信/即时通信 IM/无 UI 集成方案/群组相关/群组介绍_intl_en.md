## Group Overview

The IM SDK on the new version comes with upgraded group types, including work groups (Work), public groups (Public), meeting groups (Meeting), communities, and audio-video groups (AVChatRoom).

The groups on the earlier SDK version and the new SDK version are as compared below:

| Groups on the Earlier Version | Groups on the New Version       | Group Feature                                                |
| ----------------------------- | ------------------------------- | ------------------------------------------------------------ |
| Public                        | Public<br>Public group          | It allows the group owner to designate group admins. To join the group, a user needs to search for the group ID and send a request for approval by the group owner or admin. |
| Private                       | Work<br>Work group              | A work group allows users to join after being invited by a friend who is a member of the group, without acceptance by the user or approval by the group owner required. |
| ChatRoom                      | Meeting<br>Meeting group        | A meeting group allows users to join and leave freely and view message history from before they joined the group. This group type is suitable for scenarios where Tencent Real-Time Communication (TRTC) is used, for example, audio and video conferences and online education. |
| AVChatRoom                    | AVChatRoom<br>Audio-video group | An audio-video group allows users to join and leave freely. It supports an unlimited number of group members and doesn't store message history. This group type can be used with live streaming products to support on-screen comment chat scenarios. |
| -                             | Community<br>Community          | <li>A community allows users to join and leave freely. It is a new powerful tool for entertainment collaboration and is suitable for chat scenarios with a super large number of community members, such as finding like-minded people, gaming social networking, fan marketing, and organization management.</li><li>Within the same community, a high number of members can be divided into different groups and topics to separate messages for hierarchical communication, yet they can also share the same set of friend relationships. |

> ? The community feature is supported only by the SDK of the Enhanced edition on v5.8.1668 or later and the SDK for web on v2.17.0 or later. You need to [purchase the Ultimate edition](https://www.tencentcloud.com/document/product/1047/34577#.E5.8D.87.E7.BA.A7.E5.BA.94.E7.94.A8), go to the **[console](https://console.cloud.tencent.com/im)**, select **Feature Configuration** > **Group configuration** > **Group feature configuration**, and enable **Community**.

By default, message history pull is not enabled for work groups (Work) and public groups (Public). To use this feature, log in to the [IM console](https://console.cloud.tencent.com/im) and modify the configuration as follows:
![get_message_before_joining](https://qcloudimg.tencent-cloud.cn/raw/1d778fa8875fea11a38a3477028439aa.png)


The features and limits of each group type are as described below:

<table>
<tr>
<th width="20%">Feature</th>
<th width="16%">Work Group (Work)</th>
<th width="16%">Public Group (Public)</th>
<th width="16%">Meeting Group (Meeting)</th>
<th width="16%">Community Group (Community)</th>
<th>Audio-Video Group (AVChatRoom)</th>
</tr>


<tr>
<td>Available member roles</td>
<td>Group owner and common member</td>
<td>Group owner, group admin, and common member</td>
<td>Group owner, group admin, and common member</td>
<td>Group owner, group admin, and common member</td>
<td>Group owner and common member</td>
</tr>
<tr>
<td>Requesting to join a group</td>
<td>Not supported</td>
<td>Supported with group owner or admin approval required</td>
<td>Supported with no approval required</td>
<td>Supported with no approval required</td>
<td>Supported with no approval required</td>
</tr>
<tr>
<td>Joining group via invitation by a member</td>
<td>Supported</td>
<td>Not supported</td>
<td>Not supported</td>
<td>Supported</td>
<td>Not supported</td>
</tr>
<tr>
<td>Group owner leaving group</td>
<td>Supported</td>
<td>Not supported</td>
<td>Not supported</td>
<td>Not supported</td>
<td>Not supported</td>
</tr>
<tr>
<td>Who can modify group profile</td>
<td>Any group member</td>
<td>Group owner and admin</td>
<td>Group owner and admin</td>
<td>Group owner and admin</td>
<td>Group owner</td>
</tr>
<tr>
<td>Who can kick group members out of group</td>
<td>Group owner</td>
<td colspan="3">Group owner and admin. Group admin can only remove common group members.</td>
<td>Group members cannot be removed. The same effect can be achieved by muting members.</td>
</tr>
<tr>
<td>Who can mute members</td>
<td>Muting members is not supported</td>
<td colspan="3">Group owner and admin.
	Group admin can only mute common group members.</td>
<td>Group owner</td>
</tr>
<tr>
<td>Unread count</td>
<td>Supported</td>
<td>Supported</td>
<td>Not supported</td>
<td>Supported</td>
<td>Not supported</td>
</tr>
<tr>
<td>Viewing message history earlier than user's entry time</td>
<td>Not supported</td>
<td>Not supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Not supported</td>
</tr>
<tr>
<td>Retaining message history in the cloud</td>
<td colspan="4"><ul style="margin:0;padding-left:10px" ><li>Free Edition: Seven days</li><li>Pro Edition: Seven days by default, which can be increased to up to 360 days via <a href="https://intl.cloud.tencent.com/document/product/1047/34350">value-added service</a> </li><li>Ultimate Edition: 30 days by default, which can be increased to up to 360 days via <a href="https://intl.cloud.tencent.com/document/product/1047/34350">value-added service</a> </li></ul></td>
<td>Not supported</td>
</tr>
<tr>
<td>Number of groups</td>
<td colspan="3"><ul style="margin:0;padding-left:10px"><li>Free Edition: Up to 100 existing groups, and deleted groups do not count against the quota.</li><li>Pro Edition or Ultimate Edition: Unlimited</li></ul></td>
<td><ul style="margin:0;padding-left:10px"><li>Free Edition and Pro Edition: Not supported</li><li>Ultimate Edition: 100,000</li></ul></td>
<td><ul style="margin:0;padding-left:10px"><li>Free Edition: Up to ten existing groups, and disbanded groups do not count against the quota.</li><li>Pro Edition: Up to 50 existing groups, and disbanded groups do not count against the quota.<br>You can upgrade to unlimited number of audio-video groups by purchasing the <a href="https://intl.cloud.tencent.com/document/product/1047/34350">value-added service</a>.</li><li>Ultimate Edition: Unlimited</li></ul></td>
</tr>
<tr>
<td>Number of group members</td>
<td colspan="3"><ul style="margin:0;padding-left:10px"><li>Free Edition: 20 per group</li><li>Pro Edition: 200 per group by default, which can be increased to up to 2,000 per group via <a href="https://intl.cloud.tencent.com/document/product/1047/34350">value-added service</a> </li><li>Ultimate Edition: 2,000 per group, which can be increased to up to 6,000 per group via <a href="https://intl.cloud.tencent.com/document/product/1047/34350">value-added service</a> </li></ul></td>
<td>100,000</td>
<td>Unlimited number of group members</td>
</tr>
</table>

> ? In the `SDKAppID` of the Pro or Ultimate edition, the maximum net increase in group count per day is 10,000 for all group types. Free peak group count is 100,000 per month, and you will need to <a href="https://intl.cloud.tencent.com/document/product/1047/34350">pay for usage not covered by the free tier</a>.
