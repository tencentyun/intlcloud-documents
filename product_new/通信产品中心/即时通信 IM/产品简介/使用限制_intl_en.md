
## Limits on the API Calling Frequency

### Group system

<table>
        <tr>
            <th style="width:20%;">API</th>
            <th style="width:20%;">Backend Call Limit</th>
            <th style="width:60%;">Notes</th>
        </tr>
         <tr>
            <td>
                Create a group
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>
                The daily net increase cap is 10,000 per app. To increase the limit, <a href="https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=40&source=0&data_title=%E4%BA%91%E9%80%9A%E4%BF%A1%20%20IM&step=1">submit a ticket</a> to apply. A single app can have up to 100 million groups, but you need to pay fees when the number exceeds 100,000. For more information on pricing, see <a href="https://intl.cloud.tencent.com/document/product/1047/34350">Pricing</a>.
            </td>
        </tr>
        <tr>
            <td>
                Add a group member
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>
                A maximum of 100 members can be added at a time. A single user can join up to 1,000 groups. For more information, see <a href="https://intl.cloud.tencent.com/document/product/1047/34350">Pricing</a>.
            </td>
        </tr>
        <tr>
            <td>
                Delete a group member
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>
                Supports deleting up to 500 members in one request.
            </td>
        </tr>
        <tr>
            <td>
                Modify a group member’s profile
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>-</td>
        </tr>
        <tr>
            <td>
                Obtain groups that a user has joined
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>
                If a user has joined more than 5,000 groups, only the first 5,000 groups will be pulled.
            </td>
        </tr>
        <tr>
            <td>
                Query a user’s role in the group
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>
                Supports querying up to 500 accounts in one request.
            </td>
        </tr>
        <tr>
            <td>
                Batch muting
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>
                Supports muting up to 500 accounts in one request.
            </td>
        </tr>
        <tr>
            <td>
                Batch unmuting
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>
                Supports unmuting up to 500 accounts in one request.
            </td>
        </tr>
        <tr>
            <td>
                Send a common message
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>
                The default sending frequency of a single group is limited to 40 messages per second, and the length of a single message is limited to 9,000 bytes. Note: if two messages sent within 5 minutes from the same sender have the same random value (the value of the Random parameter), the later message will be discarded as a duplicate message.
            </td>
        </tr>
        <tr>
            <td>
                Send a system notification
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>-</td>
        </tr>
        <tr>
            <td>
                Import group messages
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>
                A maximum of 20 messages can be imported at a time. Messages must be imported in ascending order by timestamp. The timestamps of imported messages must be earlier than the current time and later than the group creation time. Otherwise, the import fails.
            </td>
        </tr>
        <tr>
            <td>
                Import group members
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>
                Supports importing up to 500 members in one request. AVChatRoom and BChatRoom groups do not support importing members.
            </td>
        </tr>
        <tr>
            <td>
                Pull roaming group messages
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>
                AVChatRoom and BChatRoom groups do not support roaming messages. Groups of other types support roaming messages for the last 7 days by default.
            </td>
        </tr>
        <tr>
            <td>
                Obtain all groups in the app
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>-</td>
        </tr>
        <tr>
            <td>
                Obtain the group profile
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>-</td>
        </tr>
        <tr>
            <td>
                Obtain a group member’s details
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>-</td>
        </tr>
        <tr>
            <td>
                Modify the basic information of a group
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>-</td>
        </tr>
        <tr>
            <td>
                Dismiss a group
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>-</td>
        </tr>
        <tr>
            <td>
                Obtain the list of muted group members
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>-</td>
        </tr>
        <tr>
            <td>
                Transfer a group
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>-</td>
        </tr>
        <tr>
            <td>
                Import the basic information of a group
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>-</td>
        </tr>
        <tr>
            <td>
                Set the unread count for group members
             </td>
            <td>
                100 requests/sec per app
            </td>
            <td>-</td>
        </tr>
        <tr>
            <td>
                Delete messages sent by a specified user
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>-</td>
        </tr>
        <tr>
            <td>
                Set global muting
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>-</td>
        </tr>
        <tr>
            <td>
                Query global muting
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>-</td>
        </tr>
        <tr>
            <td>
                Query custom dirty words for an app
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>-</td>
        </tr>
        <tr>
            <td>
                Add custom dirty words for an app
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>
                The total number of custom dirty words cannot exceed 5,000.
            </td>
        </tr>
        <tr>
            <td>
                Delete custom dirty words for an app
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>-</td>
        </tr>
			</tbody>
</table>


### Profile system

<table>
        <tr>
            <th style="width:20%;">API</th>
            <th style="width:20%;">Backend Call Limit</th>
            <th style="width:60%;">Notes</th>
        </tr>
				        <tr>
            <td>
                Set the profile
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>
                Profiles support standard fields and custom fields. The keywords of custom fields must consist of alphabetic characters with a length no greater than 8 bytes. The length of the value of a custom field cannot exceed 500 bytes.
            </td>
        </tr>
        <tr>
            <td>
                Pull the profile
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>-</td>
        </tr>
</table>

### Relationship chain system


<table>
        <tr>
            <th style="width:20%;">API</th>
            <th style="width:20%;">Backend Call Limit</th>
            <th style="width:60%;">Notes</th>
        </tr>
				<tr>
            <td>
                Pull recent contacts
            </td>
            <td>-</td>
            <td>
                Currently, up to 100 recent contacts can be saved for an ordinary user.
            </td>
        </tr>
        <tr>
            <td>
                ### Add a friend
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>
                A single user can have up to 3,000 friends, 32 friend groups, and 100 pending friend requests. The length of a friend group name cannot exceed 30 bytes, while that of friend remarks cannot exceed 96 bytes.
            </td>
        </tr>
        <tr>
            <td>
                Blacklist a user
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>
                Currently, a single user can blacklist up to 1,000 users.
            </td>
        </tr>
        <tr>
            <td>
                Import friends
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>
                Batch import supports importing up to 1,000 friends at a time.
            </td>
        </tr>
        <tr>
            <td>
                Delete a friend
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>-</td>
        </tr>
        <tr>
            <td>
                Delete all friends
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>-</td>
        </tr>
        <tr>
            <td>
                Verify friends
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>-</td>
        </tr>
        <tr>
            <td>
                Pull friends
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>-</td>
        </tr>
        <tr>
            <td>
                Remove a user from the blacklist
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>-</td>
        </tr>
        <tr>
            <td>
                Pull the blacklist
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>-</td>
        </tr>
        <tr>
            <td>
                Verify the blacklist
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>-</td>
        </tr>
</table>

### One-to-one chat message system

<table>
        <tr>
            <th style="width:20%;">API</th>
            <th style="width:20%;">Backend Call Limit</th>
            <th style="width:60%;">Notes</th>
        </tr>
				        <tr>
            <td>
                Send a one-to-one chat message
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>
                We recommend that the sending frequency between accounts not exceed 10 messages per second. When this limit is exceeded, all online messages are delivered. For offline messages, only 10 messages are stored per second, and additional messages will be discarded. The length of a single message cannot exceed 9,000 bytes.
            </td>
        </tr>
        <tr>
            <td>
                Batch send one-to-one chat messages
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>
                Supports sending messages to up to 500 users at a time. The length of a single message cannot exceed 9,000 bytes.
            </td>
        </tr>
        <tr>
            <td>
                Import one-to-one chat messages
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>-</td>
        </tr>
</table>


### Account system

<table>
        <tr>
            <th style="width:20%;">API</th>
            <th style="width:20%;">Backend Call Limit</th>
            <th style="width:60%;">Notes</th>
        </tr>
				        <tr>
            <td>
                Obtain a user’s online state
            </td>
            <td>
                100 requests/sec per app
            </td>
            <td>
                Supports querying the state of up to 500 users.
            </td>
        </tr>
        <tr>
            <td>
                UserSig expiration API
            </td>
            <td>
                1,000 requests/sec per app
            </td>
            <td>-</td>
        </tr>
        <tr>
            <td>
                Import a single account
            </td>
            <td>
                1,000 requests/sec per app
            </td>
            <td>
                The length of a username cannot exceed 32 bytes.
            </td>
        </tr>
        <tr>
            <td>
                Batch import accounts
            </td>
            <td>
                10 requests/sec per app
            </td>
            <td>
                Supports importing up to 100 usernames at a time. The length of a username cannot exceed 32 bytes.
            </td>
        </tr>
</table>

### Others

<table>
        <tr>
            <th style="width:20%;">API</th>
            <th>Backend Call Limit</th>
        </tr>
        <tr>
            <td>
                RESTful APIs
            </td>
            <td>
                <li>Verify accounts, delete an account, and obtain all groups in an app: 100 requests/sec</li><li>Other APIs: 200 requests/sec</li>
            </td>
        </tr>
</table>


## Limits on Features

<table>
        <tr>
            <th style="width:20%;">Feature</th>
            <th style="width:20%;">Limitation Type</th>
            <th style="width:60%;">Description</th>
        </tr>
        <tr>
            <td>
                Message content
            </td>
            <td>
                Content length
            </td>
            <td>
                For one-to-one messages and group messages, the length of a single message cannot exceed 8,000 bytes. Messages longer than 8,000 bytes will be discarded by the system.
            </td>
        </tr>
        <tr>
            <td>
                Sending a file
            </td>
            <td>
                File size
            </td>
            <td>
                For file messages, the size of a single file cannot exceed 28 MB for SDKs and 20 MB for WebSDKs.
            </td>
        </tr>
        <tr>
            <td>
                System message
            </td>
            <td>
                Quantity and retention period
            </td>
            <td>
                A maximum of 100 messages are retained for up to 7 days.
            </td>
        </tr>
        <tr>
            <td>
                Multi-device login
            </td>
            <td>
                Online mode
            </td>
            <td>
                Currently, four login modes are supported: single-client login (Windows, web, and Android or iOS single-client login), dual-client login (concurrent Windows, Android or iOS single-client login, and web single-client login is allowed), triple-client login (concurrent Android or iOS single-client login, Windows single-client login, and web single-client login is allowed), multi-client login (concurrent Windows, web, and Android or iOS single-client login, or any combination of them is allowed.) You can change the mode in the IM <a href="https://console.cloud.tencent.com/im">console</a>.
            </td>
        </tr>
        <tr>
            <td>
                UserID
            </td>
            <td>
                Naming restriction
            </td>
            <td>
                The length of a user account name cannot exceed 32 bytes. The name only supports letters and numbers, but does not support special characters.
            </td>
        </tr>
        <tr>
            <td>
                UserSig
            </td>
            <td>
                Validity period
            </td>
            <td>
                This is used as the user password. Signatures generated by the default API of the IM backend SDK are valid for 180 days.
            </td>
        </tr>
        <tr>
            <td>
                One-to-one chat/Group chat message
            </td>
            <td>
                Message roaming period
            </td>
            <td>
                Currently, message roaming is only available to Private, Public, and ChatRoom groups, with messages retained for 7 days by default. If you need a longer retention period, change the message roaming period in the IM <a href="https://console.cloud.tencent.com/im">console</a>. Increasing the message roaming period is a value-added service. For more information on pricing, see <a href="https://intl.cloud.tencent.com/document/product/1047/34350">Pricing</a>.
            </td>
        </tr>
        <tr>
            <td>
                Group profile
            </td>
            <td>
                Profile content restriction
            </td>
            <td>
                The length of a group name cannot exceed 30 bytes, that of a group introduction cannot exceed 240 bytes, that of a group announcement cannot exceed 300 bytes, that of a group profile photo URL cannot exceed 100 bytes, and that of a group contact card cannot exceed 50 bytes.
            </td>
        </tr>
        <tr>
            <td>
                Group member
            </td>
            <td>
                Number of members
            </td>
            <td>
                Maximum number of group members: Private: 200, Public: 2,000, ChatRoom: 10,000, AVChatRoom and BChatRoom: no limit.
            </td>
        </tr>
        <tr>
            <td>
                Custom group ID
            </td>
            <td>
                ID naming restriction
            </td>
            <td>
                Custom group IDs must be composed of ASCII characters (0x20-0x7e) and cannot exceed 48 bytes in length. In addition, they cannot begin with @TGS# to avoid confusion with default group IDs assigned by IM.
            </td>
        </tr>
        <tr>
            <td>
                Custom fields of a group
            </td>
            <td>
                Field restriction
            </td>
            <td>
                A group supports up to 20 custom fields. The Key field is of the String type with a maximum length of 16 bytes. The group name can only contain uppercase and lowercase letters, numbers, and underscores. The Value field is a user-defined buffer and can be binary. The maximum length of Value for groups is 512 bytes.
            </td>
        </tr>
        <tr>
            <td>
                Custom fields of group members
            </td>
            <td>
                Field restriction
            </td>
            <td>
                A group member supports up to 5 custom fields. The Key field is of the String type with a maximum length of 16 bytes. Its name can only contain uppercase and lowercase letters, numbers, and underscores. The Value field is a user-defined buffer and can be binary. The maximum length of Value for group members is 64 bytes.
            </td>
        </tr>
</table>
