## User Profiles

### Obtaining my personal profile
This API is used for obtaining personal profiles. For more details, see [Profile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Profile.html).

**API name**

```js
tim.getMyProfile()
```

**Returned value**

This API returns `Promise` objects:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). Personal profiles can be obtained from `IMResponse.data`.
- The callback function parameter for `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.getMyProfile();
promise.then(function(imResponse) {
  console.log(imResponse.data); // Personal profile - Profile instance
}).catch(function(imError) {
  console.warn('getMyProfile error:', imError); // Information about failures to obtain the personal profile
});
```



### Obtaining other users’ profiles
This API obtains the standard profile and [custom profile](https://cloud.tencent.com/document/product/269/1500#.E8.87.AA.E5.AE.9A.E4.B9.89.E8.B5.84.E6.96.99.E5.AD.97.E6.AE.B5) at the same time.

> If you have not configured custom profile fields or have configured custom profile fields but have not set their values, this API does not return custom profile information.

**API name**

```js
tim.getUserProfile(options)
```

**Request parameters**

The `options` parameter is of the `Object` type. The attribute values that it contains are shown in the following table:

| Name | Type | Description |
| :----------- | :-------------- | :------------------------- |
| `userIDList` | `Array<String>` | User account list of the array type |

**Returned value**

This API returns `Promise` objects:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). The user profile array can be obtained from `IMResponse.data`.
- The callback function parameter for `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.getUserProfile({
  userIDList: ['user1', 'user2'] // Note: even if you want to fetch one user’s profile, the list format still must be an array, for example, userIDList: ['user1'].
});
promise.then(function(imResponse) {
  console.log(imResponse.data); // Array that stores user profiles - [Profile]
}).catch(function(imError) {
  console.warn('getUserProfile error:', imError); // Information about failure to obtain other users’ profiles
});
```



### Updating personal profiles

**API name**

```js
tim.updateMyProfile(options)
```

**Request parameters**

The `options` parameter is of the `Object` type. The attribute values that it contains are shown in the following table:

| Name | Type | Description |
| :---------------- | :------- | :----------------------------------------------------------- |
| `nick` | `String` | Nickname |
| `avatar` | `String` | Profile photo address |
| `gender` | `String` | Gender <li>TIM.TYPES.GENDER_UNKNOWN: no gender <li>TIM.TYPES.GENDER_FEMALE: female </li><li>TIM.TYPES.GENDER_MALE: male</li> |
| `selfSignature` | `String` | Personal signature |
| `allowType` | `String` | Indicates whether the user requires approval for friend requests.<li>TIM.TYPES.ALLOW_TYPE_ALLOW_ANY: the user allows others to directly add him/her as a friend. </li><li>TIM.TYPES.ALLOW_TYPE_NEED_CONFIRM: approval is required. </li><li>TIM.TYPES.ALLOW_TYPE_DENY_ANY: friend requests are rejected.</li> |
| `birthday` | `Number` | Birthday, whose recommended format is similar to: 20000101 |
| `location` | `String` | Location. Recommended usage: the app locally defines a set of mappings between numbers and location names, and the backend actually stores four numbers of the uint32_t type. <li>The first uint32_t number indicates the country.</li><li>The second uint32_t number indicates the province or state.</li><li>The third uint32_t number indicates the city.</li><li>The fourth uint32_t number indicates the county. |
| `language` | `Number` | Language |
| `messageSettings` | `Number` | Message setting. 0: receive messages. 1: do not receive messages. |
| `adminForbidType` | `String` | Indicates whether the admin forbids friend requests. <li>TIM.TYPES.FORBID_TYPE_NONE: friend requests are allowed. This is the default value.</li><li>TIM.TYPES.FORBID_TYPE_SEND_OUT: the user is forbidden to initiate friend requests.</li> |
| `level` | `Number` | Level. We recommend that you use tiered levels to store the level information of multiple roles. |
| `role` | `Number` | Role. We recommend that you use tiered roles to store the information of multiple roles. |
| `profileCustomField` | `Array<Object>` | A collection of [custom profile](https://cloud.tencent.com/document/product/269/1500#.E8.87.AA.E5.AE.9A.E4.B9.89.E8.B5.84.E6.96.99.E5.AD.97.E6.AE.B5) key-value pairs. You can use it based on your business needs. |

**Returned value**

This API returns `Promise` objects:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). Users’ new profiles can be obtained from `IMResponse.data`.
- The callback function parameter for `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
// Modify my personal standard profile
let promise = tim.updateMyProfile({
  nick: 'My nickname',
  avatar: 'http(s)://url/to/image.jpg',
  gender: TIM.TYPES.GENDER_MALE,
  selfSignature: 'My personal signature',
  allowType: TIM.TYPES.ALLOW_TYPE_ALLOW_ANY
});
promise.then(function(imResponse) {
  console.log(imResponse.data); // Updated the profile successfully
}).catch(function(imError) {
  console.warn('updateMyProfile error:', imError); // Information about failures to update the profile
});
```

```js
// Modify my personal custom profile
// Custom profile fields need to be configured in the console in advance. For details, visit: https://cloud.tencent.com/document/product/269/1500#.E8.87.AA.E5.AE.9A.E4.B9.89.E8.B5.84.E6.96.99.E5.AD.97.E6.AE.B5.
let promise = tim.updateMyProfile({
  // You must have already applied for the custom profile field Tag_Profile_Custom_Test1 in the IM console by navigating to **App Configuration** > **Feature Configuration**.
  // Note: even if there is only one custom data field, the format of profileCustomField still must be an array.
  profileCustomField: [
    {
      key: 'Tag_Profile_Custom_Test1',
      value: 'My custom profile 1'
    }
  ]
});
promise.then(function(imResponse) {
  console.log(imResponse.data); // Updated the profile successfully
}).catch(function(imError) {
  console.warn('updateMyProfile error:', imError); // Information about failures to update the profile
});
```

```js
// Modify my personal standard profile and custom profile
let promise = tim.updateMyProfile({
  nick: 'My nickname',
  // You must have already applied for the custom profile fields Tag_Profile_Custom_Test1 and Tag_Profile_Custom_Test2 in the IM console by navigating to **App Configuration** > **Feature Configuration**.
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
  console.log(imResponse.data); // Updated the profile successfully
}).catch(function(imError) {
  console.warn('updateMyProfile error:', imError); // Information about failures to update the profile
});
```

## Blacklist

### Obtaining my blacklist

**API name**

```js
tim.getBlacklist()
```

**Request parameters**

The `options` parameter is of the `Object` type. The attribute values that it contains are as follows:

**Returned value**

This API returns `Promise` objects:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). The blacklist can be obtained from `IMResponse.data`.
- The callback function parameter for `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.getBlacklist();
promise.then(function(imResponse) {
  console.log(imResponse.data); // My blacklist, which is an array of users’ userIDs - [userID]
}).catch(function(imError) {
  console.warn('getBlacklist error:', imError); // Information about failures to obtain the blacklist
});
```



### Adding users to the blacklist

This API is used for adding users to the blacklist. By adding users to the blacklist, you can block all messages sent by these users. Therefore, this API can block the messages of specified users.

- If user A and user B are friends, the two-way friend relationship is terminated when either user A or B is added to the blacklist of the other.
- If a blacklist relationship exists between user A and user B, conversations cannot be initiated between them.
- If a blacklist relationship exists between user A and user B, neither user can initiate a friend request to the other.

**API name**

```js
tim.addToBlacklist(options)
```

**Request parameters**

The `options` parameter is of the `Object` type. The attribute values that it contains are as follows:

| Name | Type | Description |
| :----------- | :-------------- | :----------------------------------------------------------- |
| `userIDList` | `Array<String>` | List of userIDs to be added to the blacklist. The number of userIDs in a single request cannot exceed 1,000. |

**Returned value**

This API returns `Promise` objects:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). The blacklist can be obtained from `IMResponse.data`.
- The callback function parameter for `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.addToBlacklist({userIDList: ['user1', 'user2']}); // Note: even if you add one account to the blacklist, the format of the user list still must be an array, for example: userIDList: ['user1'].
promise.then(function(imResponse) {
  console.log(imResponse.data); // Information about accounts successfully added to the blacklist, which is an array of users’ userIDs - [userID]
}).catch(function(imError) {
  console.warn('addToBlacklist error:', imError); // Information about failures to add users to the blacklist
});
```



### Removing users from the blacklist

This API is used for removing users from the blacklist. After removing a user from the blacklist, you can receive all messages sent by the user.

**API name**

```js
tim.removeFromBlacklist(options)
```

**Request parameters**

The `options` parameter is of the `Object` type. The attribute values that it contains are shown in the following table:

| Name | Type | Description |
| :----------- | :-------------- | :----------------------------------------------------------- |
| `userIDList` | `Array<String>` | List of userIDs to be removed from the blacklist. The number of userIDs in a single request cannot exceed 1,000. |

**Returned value**

This API returns `Promise` objects:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). The list of accounts successfully removed from the blacklist can be obtained from `IMResponse.data`.
- The callback function parameter for `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.removeFromBlacklist({userIDList: ['user1', 'user2']}); // Note: even if you remove one account from the blacklist, the format of the user list still must be an array, for example: userIDList: ['user1'].
result.then(function(imResponse) {
  console.log(imResponse.data); // List of accounts successfully removed from the blacklist, which is an array of users’ userIDs - [userID]
}).catch(function(imError) {
  console.warn('removeFromBlacklist error:', imError); // Information about failures to remove users from the blacklist
});
```
