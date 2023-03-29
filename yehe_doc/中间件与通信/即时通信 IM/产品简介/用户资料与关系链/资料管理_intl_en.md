## Profile System Overview
Instant Messaging (IM) provides a complete set of profile solutions through its user profile hosting capacity. IM's profile hosting service enables your users to easily set and pull profiles.
- IM can store profile information, ensuring that your data has remote disaster recovery, cross-region deployment, and auto scaling capabilities. In this way, you are completely free from complex processing flows, such as server downtime, multi-copy primary-secondary replication, and capacity scaling.
- IM provides the business processing flows commonly used in the industry, with which you do not have to worry about user profile business logic.
- IM provides professional operation processes and teams, ensuring 99.99% service quality annually and helping you offer services known for their stability.
- IM provides easy-to-use service APIs and easy-to-access guidelines, with premium services throughout the whole process.

By using IM's profile hosting service, you will be able to:
- Store, read, and write standard profile fields.
- Store, read, and write custom profile fields.

## Profile Fields
A profile is a set of data that describes user properties. IM's profile system supports standard and custom profile fields. Profile fields have the following characteristics:
- Profile fields are expressed in key-value format.
- Key is in string format, and its name can only contain uppercase and lowercase letters, numbers, and underscores.
- Value has the following types:
   a. An integer of uint32_t type (not supported for custom fields)
   b. An integer of uint64_t type (not supported for custom fields)
   c. A string of string type (the length of the string cannot exceed 500 bytes.)
   d. A buffer of bytes type (the length of the buffer cannot exceed 500 bytes.)

- You can configure the read and write permissions for each key. The read and write permissions of profile fields are as follows:

<table style="display:table;width:100%">
		<tbody>
			<tr>
			<th style="width:20%;">Permission Name</th>
				<th style="width:30%;">Permission Type</th>
				<th>Notes</th>
			</tr>
			<tr>
				<td>Read permission</td>
				<td>
					Readable by app<br>
					Readable by app admin<br>
				</td>
				<td>You can select one or more types of read permission.</td>
			</tr>
			<tr>
				<td>Write permission</td>
				<td>
					Writable by app<br>
					Writable by app admin<br>
				</td>
				<td>You can select one or more types of write permission.</td>
			</tr>
		</tbody>
	</table>

## Standard Profile Fields

Currently, IM supports the following standard profile fields:

<table style="display:table;width:100%">
		<tbody>
			<tr>
			<th style="width:15%;">Field Name</th>
				<th style="width:5%;">Type</th>
				<th style="width:10%;">Description</th>
				<th style="width:19%;">Push Notification upon Update</th>
				<th>Notes</th>
			</tr>
			<tr>
				<td>Tag_Profile_IM_Nick</td>
				<td>string</td>
				<td>Nickname</td>
				<td>Yes</td>
				<td>The maximum length is 500 bytes.</td>
			</tr>
			<tr>
				<td>Tag_Profile_IM_Gender</td>
				<td>string</td>
				<td>Gender</td>
				<td>Yes</td>
				<td>
					Gender_Type_Unknown: the gender is not set<br>
					Gender_Type_Female: female<br>
					Gender_Type_Male: male<br>
				</td>
			</tr>
			<tr>
				<td>Tag_Profile_IM_BirthDay</td>
				<td>uint32</td>
				<td>Date of birth</td>
				<td>Yes</td>
				<td>Recommended format: 20190419</td>
			</tr>
			<tr>
				<td>Tag_Profile_IM_Location</td>
				<td>string</td>
				<td>Location</td>
				<td>Yes</td>
				<td>
					The maximum length is 16 bytes. Recommended usage:<br>
					The app locally defines a set of number-location mappings.<br>
					The backend stores four uint32_t numbers.<br>
					The first uint32_t denotes the country or region.<br>
					The second uint32_t denotes the state or province.<br>
					The third uint32_t denotes the city.<br>
					The fourth uint32_t denotes the district or county.<br>
				</td>
			</tr>
			<tr>
				<td>Tag_Profile_IM_SelfSignature</td>
				<td>string</td>
				<td>Personal signature</td>
				<td>Yes</td>
				<td>The maximum length is 500 bytes.</td>
			</tr>
			<tr>
				<td>Tag_Profile_IM_AllowType</td>
				<td>string</td>
				<td>Approval method for new friend requests</td>
				<td>Yes</td>
				<td>
					AllowType_Type_NeedConfirm: manually accept new friend requests.<br>
					AllowType_Type_AllowAny: automatically accept all new friend requests.<br>
					AllowType_Type_DenyAny: reject all new friend requests.<br>
				</td>
			</tr>
			<tr>
				<td>Tag_Profile_IM_Language</td>
				<td>uint32</td>
				<td>Language</td>
				<td>Yes</td>
				<td> The application locally defines the number-language mapping and needs to locally convert the number corresponding to the language into text.</td>
			</tr>
			<tr>
				<td>Tag_Profile_IM_Image</td>
				<td>string</td>
				<td>URL of the profile photo</td>
				<td>Yes</td>
				<td>The maximum length is 500 bytes.</td>
			</tr>
			<tr>
				<td>Tag_Profile_IM_AdminForbidType</td>
				<td>string</td>
				<td>Admin forbids tagging new friend requests</td>
				<td>Yes</td>
				<td>
					AdminForbid_Type_None: the default value, and sending new friend requests is allowed.<br>
					AdminForbid_Type_SendOut: sending new friend requests is forbidden.<br>
				</td>
			</tr>
			<tr>
				<td>Tag_Profile_IM_Level</td>
				<td>uint32</td>
				<td>Level</td>
				<td>Yes</td>
				<td>Generally, a piece of UINT-8 data stores the information of one level.<br>You can divide the level to store the level information of multiple roles.</td>
			</tr>
			<tr>
				<td>Tag_Profile_IM_Role</td>
				<td>uint32</td>
				<td>Role</td>
				<td>Yes</td>
				<td>Generally, a piece of UINT-8 data stores the information of one role.<br>You can divide the role to store the information of multiple roles.</td>
			</tr>
		</tbody>
	</table>

## Custom Profile Fields
Custom profile fields are the user data set by each app according to its own business needs. By using custom profile fields, an app can add additional data to user profiles and perform read and write operations through existing APIs.

### Applying for custom profile fields
To apply for custom profile fields, log in to the [IM console](https://console.cloud.tencent.com/im) and select **Application Configuration** > **Feature Configuration**. After your application is submitted, the custom profile fields will take effect in five minutes.
When applying for custom profile fields, you need to submit the following information for each field:
- The name of the custom profile field (Key). For more information, see [Naming Rules for Custom Profile Fields](#.E8.87.AA.E5.AE.9A.E4.B9.89.E8.B5.84.E6.96.99.E5.AD.97.E6.AE.B5.E7.9A.84.E5.91.BD.E5.90.8D.E8.A7.84.E8.8C.83).
- The type of the custom profile field (Value). For more information, see [Profile Fields](#.E8.B5.84.E6.96.99.E5.AD.97.E6.AE.B5).
- Read and write permissions of the custom profile field. For more information, see [Profile Fields](#.E8.B5.84.E6.96.99.E5.AD.97.E6.AE.B5).

### Naming rules for custom profile fields
The rules for naming custom profile fields are as follows:
- The name of the custom profile field contains the prefix and keyword parts.
- The prefix of the custom profile field is Tag_Profile_Custom.
- Keyword: the keyword must be a string of letters with a length no more than 8 bytes. We recommend you use an English word or its abbreviation as the keyword.
- Example: if the custom field to be applied for by an app has the keyword **Test**, then the name of the custom profile field is: Tag_Profile_Custom_Test.


