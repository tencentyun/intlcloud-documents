## User Profile

### Obtaining your personal profile
This API is used to obtain your personal profile. For more information on the properties, see [Profile](https://web.sdk.qcloud.com/im/doc/zh-cn/Profile.html).

>! Custom profile fields are supported since SDK v2.3.2. Before using this API, upgrade your SDK to v2.3.2 or later.

**API name**

```js
tim.getMyProfile()
```

**Returned values**

This API returns a `Promise` object. The callback functions are as follows:
- The callback function parameter for `then` is [IMResponse](https://web.sdk.qcloud.com/im/doc/zh-cn/global.html#IMResponse). You can obtain your personal profile from `IMResponse.data`.
- The callback function parameter for `catch` is [IMError](https://web.sdk.qcloud.com/im/doc/zh-cn/global.html#IMError).

**Sample**

```js
let promise = tim.getMyProfile();
promise.then(function(imResponse) {
  console.log(imResponse.data); // Personal profile from the profile instance
}).catch(function(imError) {
  console.warn('getMyProfile error:', imError); // Information on the failure in obtaining the personal profile.
});
```



### Obtaining other users’ profiles
This API is used to obtain standard profile fields and [Custom Profile Fields](https://intl.cloud.tencent.com/document/product/1047/33520).

>!
>- Custom profile fields are supported since SDK v2.3.2. Before using this API, upgrade your SDK to v2.3.2 or later.
>- If you have not configured any custom profile fields or you have configured custom profile fields but have not set the values, this API will not return custom profile information.
>- You may pull profiles of up to 100 users to avoid failure caused by a large amount of data returned. If the length of an array passed in is greater than 100, only the first 100 users will be queried and the rest are discarded.

**API name**

```js
tim.getUserProfile(options)
```

**Request Parameters**

The `options` parameter is of the `Object` type. It contains the following property values:

| Name | Type | Description |
| :----------- | :-------------- | :------------------------- |
| `userIDList` | `Array<String>` | UserIDs. The value is of array type. |

**Returned values**

This API returns a `Promise` object. The callback functions are as follows:
- The callback function parameter for `then` is [IMResponse](https://web.sdk.qcloud.com/im/doc/zh-cn/global.html#IMResponse). You can obtain other users’ profiles from `IMResponse.data`.
- The callback function parameter for `catch` is [IMError](https://web.sdk.qcloud.com/im/doc/zh-cn/global.html#IMError).

**Sample**

```js
let promise = tim.getUserProfile({
  userIDList: ['user1', 'user2'] // Note: even if you retrieve only one user’s profile, the value must be of the array type, for example, userIDList: ['user1'].
});
promise.then(function(imResponse) {
  console.log(imResponse.data); // The array that stores other users’ profiles - [Profile]
}).catch(function(imError) {
  console.warn('getUserProfile error:', imError); // Information on the failure in obtaining other users’ profiles.
});
```



### Updating your personal profile

>! Custom profile fields are supported since SDK v2.3.2. Before using this API, upgrade your SDK to v2.3.2 or later.

**API name**

```js
tim.updateMyProfile(options)
```

**Request Parameters**

The `options` parameter is of the `Object` type. It contains the following property values:

| Name | Type | Description |
| :---------------- | :------- | :----------------------------------------------------------- |
| `nick` | `String` | Nickname. |
| `avatar` | `String` | URL of the avatar . |
| `gender` | `String` | Gender. Valid values:<li>TIM.TYPES.GENDER_UNKNOWN: unspecified<li>TIM.TYPES.GENDER_FEMALE: female</li><li>TIM.TYPES.GENDER_MALE: male</li> |
| `selfSignature` | `String` | Personal signature. |
| `allowType` | `String` | Specifies whether a friending request sent to the user must be verified.<li>TIM.TYPES.ALLOW_TYPE_ALLOW_ANY: the friending request is automatically accepted without verification. </li><li> TIM.TYPES.ALLOW_TYPE_NEED_CONFIRM: the friending request must be verified. </li><li>TIM.TYPES.ALLOW_TYPE_DENY_ANY: the friending request is rejected. </li> |
| `birthday` | `Number` | Birthday. It is recommended that the value is in the format of yyyymmdd, for example, 20000101. |
| `location` | `String` | Location. It is recommended that the app locally define a set of mappings between digits and location names, and the backend actually save four digits of the uint32_t type. <li>The first uint32_t indicates the country.</li><li>The second uint32_t indicates the province.</li><li>The third uint32_t indicates the city.</li><li>The fourth uint32_t indicates the county. |
| `language` | `Number` | Language. |
| `messageSettings` | `Number` | Message settings of the user. 0: receive messages. 1: do not receive messages. |
| `adminForbidType` | `String` | Specifies whether the admin forbids the user from friending other users. <li>TIM.TYPES.FORBID_TYPE_NONE: the friend can friend other users. This is the default value.</li><li>TIM.TYPES.FORBID_TYPE_SEND_OUT: the admin forbids the user from sending a friend request. </li> |
| `level` | `Number` | Level. It is recommended that you divide the values into categories to save level information of multiple roles. |
| `role` | `Number` | Role. It is recommended that you divide the values into categories to save information of multiple roles. |
| `profileCustomField` | `Array<Object>` | [Custom profile fields](https://intl.cloud.tencent.com/document/product/1047/33520). The value is a set of key-value pair. You can use this field based on your business needs. |

**Returned values**

This API returns a `Promise` object. The callback functions are as follows:
- The callback function parameter for `then` is [IMResponse](https://web.sdk.qcloud.com/im/doc/zh-cn/global.html#IMResponse). You can obtain other users’ new profiles from `IMResponse.data`.
- The callback function parameter for `catch` is [IMError](https://web.sdk.qcloud.com/im/doc/zh-cn/global.html#IMError).

**Sample**

```js
// Modify your personal standard profile.
let promise = tim.updateMyProfile({
  nick: 'My profile',
  avatar: 'http(s)://url/to/image.jpg',
  gender: TIM.TYPES.GENDER_MALE,
  selfSignature: 'My personal signature',
  allowType: TIM.TYPES.ALLOW_TYPE_ALLOW_ANY
});
promise.then(function(imResponse) {
  console.log(imResponse.data); // The profile is updated.
}).catch(function(imError) {
  console.warn('updateMyProfile error:', imError); // Information on the failure in updating the personal profile.
});
```

```js
// Modify my personal custom profile.
// Custom profile fields must be configured on the IM console in advance. For more information, see https://intl.cloud.tencent.com/document/product/1047/33520.
let promise = tim.updateMyProfile({
  // Ensure that you have applied for the custom profile field Tag_Profile_Custom_Test1 in the IM console by clicking the desired app card and choosing **Feature Configuration** > **User Custom Field**.
  // Note: even if only this one custom data field exists, the format of profileCustomField must be of array type.
  profileCustomField: [
    {
      key: 'Tag_Profile_Custom_Test1',
      value: 'My custom profile 1'
    }
  ]
});
promise.then(function(imResponse) {
  console.log(imResponse.data); // The profile is updated.
}).catch(function(imError) {
  console.warn('updateMyProfile error:', imError); // Information on the failure in updating the personal profile.
});
```

```js
// Modify my personal standard profile and custom profile.
let promise = tim.updateMyProfile({
  nick: 'My profile',
  // Ensure that you have applied for the custom profile fields Tag_Profile_Custom_Test1 and Tag_Profile_Custom_Test2 in the IM console by clicking the desired app card and choosing **Feature Configuration** > **User Custom Field**.
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
  console.log(imResponse.data); // The profile is updated.
}).catch(function(imError) {
  console.warn('updateMyProfile error:', imError); // Information on the failure in updating the personal profile.
});
```

## Blacklists

### Obtaining my blacklist

**API name**

```js
tim.getBlacklist()
```

**Request Parameters**

The `options` parameter is of the `Object` type. It contains the following property values:

**Returned values**

This API returns a `Promise` object. The callback functions are as follows:
- The callback function parameter for `then` is [IMResponse](https://web.sdk.qcloud.com/im/doc/zh-cn/global.html#IMResponse). You can obtain the blacklist from `IMResponse.data`.
- The callback function parameter for `catch` is [IMError](https://web.sdk.qcloud.com/im/doc/zh-cn/global.html#IMError).

**Sample**

```js
let promise = tim.getBlacklist();
promise.then(function(imResponse) {
  console.log(imResponse.data); // My blacklist. The value is an array that contains userIDs - [userID].
}).catch(function(imError) {
  console.warn('getBlacklist error:', imError); // Information on the failure in obtaining the blacklist.
});
```



### Adding a user to the blacklist

This API is used to add a user to the blacklist. By adding a user to the blacklist, you can block all the messages sent by the user. Therefore, this API can be used to block the messages of a specified user.

- If user A and user B are friends, the two-way friend relationship is terminated when either A or B is blacklisted by the other user.
- If user A and user B are in a blacklist relationship, neither user A nor user B can send a friend request to the other user.
- If both user A and user B have blacklisted each other, user A and user B cannot set up a chat session.
- If user A has blacklisted user A but user B has not blacklisted user A, user A can send a message to user B, but user B cannot send a message to user A.

**API name**

```js
tim.addToBlacklist(options)
```

**Request Parameters**

The `options` parameter is of the `Object` type. It contains the following property values:

| Name | Type | Description |
| :----------- | :-------------- | :----------------------------------------------------------- |
| `userIDList` | `Array<String>` | All the userIDs to be added to the blacklist. The number of userIDs in a single request cannot exceed 1,000. |

**Returned values**

This API returns a `Promise` object. The callback functions are as follows:
- The callback function parameter for `then` is [IMResponse](https://web.sdk.qcloud.com/im/doc/zh-cn/global.html#IMResponse). You can obtain the blacklist from `IMResponse.data`.
- The callback function parameter for `catch` is [IMError](https://web.sdk.qcloud.com/im/doc/zh-cn/global.html#IMError).

**Sample**

```js
let promise = tim.addToBlacklist({userIDList: ['user1', 'user2']}); // Note: even if you add only one userID to the blacklist, the value must be of array type, for example, userIDList: ['user1'].
promise.then(function(imResponse) {
  console.log(imResponse.data); // Information on the userIDs that are added to the blacklist. The value must be an array that contains userIDs - [userID].
}).catch(function(imError) {
  console.warn('addToBlacklist error:', imError); // Information on the failure in adding userIDs to the blacklist.
});
```



### Removing a user from the blacklist

This API is used to delete a user from the blacklist. After deleting the user from the blacklist, you can receive all the messages sent by the user.

**API name**

```js
tim.removeFromBlacklist(options)
```

**Request Parameters**

The `options` parameter is of the `Object` type. It contains the following property values:

| Name | Type | Description |
| :----------- | :-------------- | :----------------------------------------------------------- |
| `userIDList` | `Array<String>` | All the userIDs to be deleted from the blacklist. The number of userIDs in a single request cannot exceed 1000. |

**Returned values**

This API returns a `Promise` object. The callback functions are as follows:
- The callback function parameter for `then` is [IMResponse](https://web.sdk.qcloud.com/im/doc/zh-cn/global.html#IMResponse). You can obtain the userIDs that are deleted from the blacklist from `IMResponse.data`.
- The callback function parameter for `catch` is [IMError](https://web.sdk.qcloud.com/im/doc/zh-cn/global.html#IMError).

**Sample**

```js
let promise = tim.removeFromBlacklist({userIDList: ['user1', 'user2']}); // Note: even if you delete only one userID from the blacklist, the value must be of array type, for example, userIDList: ['user1'].
result.then(function(imResponse) {
  console.log(imResponse.data); // All userIDs that are deleted from the blacklist. The value is an array that contains the userIDs - [userID].
}).catch(function(imError) {
  console.warn('removeFromBlacklist error:', imError); // Information on the failure in deleting users from the blacklist.
});
```
