## Feature Description

Users can set and get their nicknames, profile photos, and statuses as well as the profile information of non-friend users.

## User Profile Management

### Querying a user's own profile

**API**

<dx-codeblock>
:::  js

tim.getMyProfile();

:::
</dx-codeblock>

**Parameter**

None

**Returned value**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

let promise = tim.getMyProfile();
promise.then(function(imResponse) {
  console.log(imResponse.data); // Personal profile - profile instance
}).catch(function(imError) {
  console.warn('getMyProfile error:', imError); // Failed to obtain the user's profile
});

:::
</dx-codeblock>

### Querying the profile of another user

>!
>- If you haven't configured a custom profile field or have configured it without a value, this API will not return the custom profile content.
>- Up to 100 users can be pulled at a time, as a large data volume will cause a response failure. If the length of the array passed in exceeds 100, only the first 100 users will be queried, and the rest will be discarded.

**API**

<dx-codeblock>
:::  js

tim.getUserProfile(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name       | Type  | Description                               |
| ---------- | ----- | ----------------------------------------- |
| userIDList | Array | List of user accounts, which is an array. |

**Returned value**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

let promise = tim.getUserProfile({
  userIDList: ['user1', 'user2'] // Note: even if you retrieve the profile of only one user, the value must be of array type, for example, userIDList: ['user1'].
});
promise.then(function(imResponse) {
  console.log(imResponse.data); // Array that stores other users' profiles - [Profile]
}).catch(function(imError) {
  console.warn('getUserProfile error:', imError); // Failed to obtain the user's profile
});

:::
</dx-codeblock>

### Updating your personal profile

**API**

<dx-codeblock>
:::  js

tim.updateMyProfile(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name               | Type                | Description                                                  |
| ------------------ | ------------------- | ------------------------------------------------------------ |
| nick               | String \| undefined | Nickname                                                     |
| avatar             | String \| undefined | Profile photo URL                                            |
| gender             | String \| undefined | Gender. Valid values:<br/><li>TIM.TYPES.GENDER_UNKNOWN (not set)</li><li>TIM.TYPES.GENDER_FEMALE (female)</li><li>TIM.TYPES.GENDER_MALE (male)</li> |
| selfSignature      | String \| undefined | Status                                                       |
| allowType          | String \| undefined | When a friend request is received: Valid values<br/><li>TIM.TYPES.ALLOW_TYPE_ALLOW_ANY (no approval required)</li><li>TIM.TYPES.ALLOW_TYPE_NEED_CONFIRM (approval required)</li><li>TIM.TYPES.ALLOW_TYPE_DENY_ANY (reject)</li> |
| birthday           | Number \| undefined | Birth date, such as `20000101`.                              |
| location           | String \| undefined | Location. We recommend you define a mapping relationship between numbers and locations locally. Actually, the backend saves four numbers of the `uint32_t` type. Here, the first `uint32_t` indicates the country, the second the province, the third the city, and the fourth the district/county. |
| language           | Number \| undefined | Language                                                     |
| messageSettings    | Number \| undefined | Message settings. Valid values: 0 (receive messages), 1 (don't receive messages). |
| adminForbidType    | String \| undefined | Friending. Valid values:<br/><li>TIM.TYPES.FORBID_TYPE_NONE (allow, which is the default value)</li><li>TIM.TYPES.FORBID_TYPE_SEND_OUT (disallow)</li> |
| level              | Number \| undefined | Level. We recommend you split it to save the level information of multiple roles. |
| role               | Number \| undefined | Role. We recommend you split it to save the information of multiple roles. |
| profileCustomField | Array \| undefined  | Collection of custom profile key-value pairs, which can be used as needed. For more information, see https://cloud.tencent.com/document/product/269/1500#.E8.87.AA.E5.AE.9A.E4.B9.89.E8.B5.84.E6.96.99.E5.AD.97.E6.AE.B5. |

**Returned value**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

// Modify a user's profile
let promise = tim.updateMyProfile({
  nick: 'My nickname',
  avatar: 'http(s)://url/to/image.jpg',
  gender: TIM.TYPES.GENDER_MALE,
  selfSignature: 'My status',
  allowType: TIM.TYPES.ALLOW_TYPE_ALLOW_ANY
});
promise.then(function(imResponse) {
  console.log(imResponse.data); // Profile updated successfully
}).catch(function(imError) {
  console.warn('updateMyProfile error:', imError); // Failed to update the profile
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js

// Modify personal custom profile fields
// Custom profile fields must be configured in the IM console in advance. For more information, see https://cloud.tencent.com/document/product/269/1500#.E8.87.AA.E5.AE.9A.E4.B9.89.E8.B5.84.E6.96.99.E5.AD.97.E6.AE.B5.
let promise = tim.updateMyProfile({
  // Ensure that you have applied for the custom profile field Tag_Profile_Custom_Test1 in the IM console by clicking the desired app card and choosing Feature Configuration > User Custom Field.
  // Note: even if only this one custom data field exists, the format of profileCustomField must be of array type.
  profileCustomField: [
    {
      key: 'Tag_Profile_Custom_Test1',
      value: 'My custom profile 1'
    }
  ]
});
promise.then(function(imResponse) {
  console.log(imResponse.data); // Profile updated successfully
}).catch(function(imError) {
  console.warn('updateMyProfile error:', imError); // Failed to update the profile
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js

// Modify personal standard and custom profile fields
let promise = tim.updateMyProfile({
  nick: 'My nickname',
  // Ensure that you have applied for the custom profile fields Tag_Profile_Custom_Test1 and Tag_Profile_Custom_Test2 in the IM console by clicking the desired app card and selecting Feature Configuration > User Custom Field.
  profileCustomField: [
    {
      key: 'Tag_Profile_Custom_Test1',
      value: 'My custom profile 1'
    },
    {
      key: 'Tag_Profile_Custom_Test2',
      value: 'My custom profile 2'
    },
  ]
});
promise.then(function(imResponse) {
  console.log(imResponse.data); // Profile updated successfully
}).catch(function(imError) {
  console.warn('updateMyProfile error:', imError); // Failed to update the profile
});

:::
</dx-codeblock>