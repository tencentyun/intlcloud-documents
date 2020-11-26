

TPNS provides two types of tags: custom tags and TPNS preset tags. Below is a tag use case:
![](https://main.qcloudimg.com/raw/315ed442cd0ccd711f0cdbbb116a17f1.jpg)
## Tag Setting Methods

### Binding custom tag

 Custom tag is a tag setting method where you can custom the device tag name.

#### Binding and unbinding custom tag

For more information, please see the API documentation for [Binding and Unbinding Tags](https://intl.cloud.tencent.com/document/product/1024/33766).

#### Unbinding all devices under specified custom tag

For more information, please see the API documentation for [Deleting All Devices Under Tag](https://intl.cloud.tencent.com/document/product/1024/33767).

### Binding preset tag
- Preset tags are tags maintained on the TPNS platform, i.e., tags automatically collected by the SDK when user devices are registered with or connected to the TPNS server. Currently, TPNS preset tags include app version, system version, district, active status, system language, SDK version, country/region, phone brand, and phone model.
- All devices are bound to the latest preset tags, which will automatically replace the corresponding legacy ones. For example, if the current app version of a device is 1.0.1, when the app is upgraded to 1.0.2, the device will be automatically unbound from the v1.0.1 tag and then bound to the v1.0.2 tag.

### Querying tags bound to device
 You can use the toolkit in the Tencent Cloud Console to query specific preset and custom tags by device token.
 See the figure below:
 ![](https://main.qcloudimg.com/raw/bea55142d1359075605e259a58b5e650.png)
## Custom Tag Use Cases and Keywords
Push by tag is suitable for scenarios where the number of devices bound to a tag is high (more than 10 generally) but the push frequency is low (below 10 pushes a day generally). For scenarios where the number of bound devices is small but the push frequency is high, you are recommended to use push by account, i.e., binding an account instead of a tag to multiple devices for push.

### Keywords

A colon ":" is the keyword for separating the `key` and `value` in a `key-value` pair for user tag binding; for example, if you assign the tag `level:3` to a device token, the TPNS backend will take `level` as the tag key and `3` as the tag value. The actual push will not be affected, where the tag `level:3` is still used for push. Storage based on `key-value` is mainly to facilitate subsequent overwriting of tags in the same category; for example, if the device token is bound to another tag such as `male` (i.e., the device has two tags: `male` and `level:3`), when the membership level of the device is upgraded to level 4 and you want to overwrite the tag `level:3` with `level:4` without affecting the `male` tag, you can directly call the key-value overwriting API to set the `level:4` tag for the device, and then the tags bound to the device token will become `male` and `level:4`.

## Tag Binding/Unbinding Scenarios

TPNS provides APIs for binding/unbinding a single tag to/from a single device, a single tag to/from multiple devices, multiple tags to/from a single device, and multiple tags to/from multiple devices.
### Single tag for single device 
#### Recommended scenarios
1. The device SDK API is called; for example, to automatically get the user subscription channel in the app, bind the channel tag to the device token, and vice versa.           
2. The RESTful API are called occasionally in scenarios such as integration testing.


##### Binding tag

```json
{
    "operator_type": 1,
    "platform": "android",
    "tag_list": ["tag"],
    "token_list": ["token"]
}
```

##### Unbinding tag
```json
{
    "operator_type": 2,
    "platform": "android",
    "tag_list": ["tag"],
    "token_list": ["token"]
}
```
#### Use limits
- A tag can contain up to 50 bytes.
- The API is called synchronously.

### Multiple tags for single device
#### Recommended scenarios
1. The device SDK API is called; for example, to automatically get user characteristics tags such as age, district, and gender in the app, bind them to the device token in batches, and vice versa.
2. The RESTful API is called; for example, to get a device's user subscription information tags such as marital status and hobbies (football, movies, etc,) through other internal channels, bind them to the device token in batches, and vice versa.

##### Binding tag
```json
{
    "operator_type": 3,
    "platform": "android",
    "tag_list": ["tag1","tag2"],
    "token_list": ["token"]
}

```
##### Unbinding tag
```json
{
    "operator_type": 4,
    "platform": "android",
    "tag_list": ["tag1","tag2"],
    "token_list": ["token"]
}
```
#### Use limits
- A tag can contain up to 50 bytes.
- Up to 500 tags can be included in one call.
- The API is called synchronously.

### Single tag for multiple devices
#### Recommended scenarios
1. Only the RESTful API can be called; for example, to add the "football" tag to all users who like football, this API can be called to bind tags in batches, and vice versa.
##### Binding tag
```json
{
    "operator_type": 7,
    "platform": "android",
    "tag_list": ["tag"],
    "token_list": ["token1","token2"]
}
```
##### Unbinding tag
```json
{
    "operator_type": 8,
    "platform": "android",
    "tag_list": ["tag"],
    "token_list": ["token1","token2"]
}
```
#### Use limits
- A tag can contain up to 50 bytes.
- Up to 500 device tokens can be included in one call.
- The API is called synchronously.

### Multiple tags for multiple devices
##### Recommended scenarios

1. Only the RESTful API can be called; for example, to add the "football" tag to all users who like football and the "basketball" tag to all users who like basketball, this API can be called to bind tags in batches, and vice versa.

##### Binding tag
```json
{
    "operator_type": 9,
    "platform": "android",
    "tag_token_list": [{"tag":"tag1","token":"token1"},{"tag":"tag2","token":"token2"}]
}
```
##### Unbinding tag
```json
{
    "operator_type": 10,
    "platform": "android",
    "tag_token_list": [{"tag":"tag1","token":"token1"},{"tag":"tag2","token":"token2"}]
}
```
#### Use limits
- A tag can contain up to 50 bytes.
- Up to 500 device tokens can be included in one call.
- The API is called synchronously.


## Tag Overwriting Scenarios

TPNS provides two tag overwriting methods, namely, general overwriting and overwriting by tag category (aka key-value (KV) overwriting), where a colon (":") is used to separate the `key` and `value` in a key-value pair.
### General overwriting
#### Recommended scenarios
1. The device SDK API is called. If all channel information subscribed by a device has expired, you need to unbind all the channel tags from the device. However, traversing all tags to unbind them one by one is very inconvenient. In this case, you can call this API to overwrite the tags in batches.
2. The RESTful API is called; for example, to set new tags for a device so that it will not be affected by legacy tags, this API can be called to overwrite them.

#### Tag overwriting method
```json
{
    "operator_type": 6,
    "platform": "android",
    "tag_list": ["test", "level:1",, "level:2"], 
    "token_list": ["token"]
}
```
#### Use limits
- A tag can contain up to 50 bytes.
- The API is called asynchronously. You are recommended to set the call interval to longer than 1 second.

### KV overwriting
#### Recommended scenarios
1. The device SDK API is called.
2. The RESTful API is called.
**Instructions:** a colon (":") is used for separation. The content before ":" is used as the tag category, while the content after ":" is used as the specific tag value. For example, `level:2` indicates that the device level is 2. Assume that the device level is upgraded to 3, then you need to delete the tag `level:2` before adding the tag `level:3`. If you know that the device has only the tag `level:2`, you can call the general overwriting API to overwrite it. However, a device usually has multiple tags. If the device has another tag `test` and you want to delete only the tag `level:2`, you need to manipulate all tags of the device or call the relevant TPNS API to find the corresponding legacy tag and delete it, which is very inconvenient. In this case, you can call this API to overwrite only tags with the key (category) of `level`.

#### Tag overwriting method
```json
{
    "operator_type": 6,
    "platform": "android",
    "tag_list": ["test:2", "level:3"], 
    "token_list": ["token"]
}
```
**API description:** only when all tags in the `tag_list` have a colon (":") can KV overwriting be performed properly; for example, if a token has tags `test` and `level:1`, after this API is called, the tag list of the token will include `test`, `test:2`, and `level:3`.

#### Use limits
- A tag can contain up to 50 bytes.
- Up to 500 tags can be included in one call.
- The API is called asynchronously. You are recommended to set the call interval to longer than 1 second.


## Tag Deletion Scenarios

 TPNS provides two tag deletion methods, namely, deleting all tags of a device and deleting specific tags of an app.

### Deleting all tags of a single device
#### Recommended scenarios
1. The device SDK API is called.
2. The RESTful API is called.

**Instructions:** you can use this API to delete all legacy tags of a device. This API is generally used to delete expired tags or set tags again after a faulty operation.

#### Tag deletion method
```json
{
    "operator_type": 5,
    "platform": "android", 
    "token_list": ["token"]
}
```
#### Use limits
- A tag can contain up to 50 bytes.
- The API is called asynchronously. You are recommended to set the call interval to longer than 1 second.

### Deleting specific tags of app

#### Recommended scenarios
1. Only the RESTful API can be called.
**Description:** you can use this API to delete specific tags of an app, i.e., removing them from the tag list of the app after unbinding them from bound devices. It is generally used to delete obsolete tags; for example, to delete testing tags added during test after the app is officially released, you can call this API.

#### Tag deletion method
```json
{
    "tag_list": ["tag1", "tag2"]
}
```
#### Use limits
- A tag can contain up to 50 bytes.
- Up to 500 tags can be included in one call.
- The API is called asynchronously. You are recommended to set the call interval to longer than 1 second.

## Push by Tag
Push by tag supports a single tag or multiple tags. For push by multiple tags, TPNS currently only supports tags in the same category (combined in the "AND" or "OR" relationship). Specifically, if you push messages by custom tags, only custom tags can be combined in "AND" or "OR" relationship; and if you push message by preset tags, only preset tags in the same category can be combined. For example, you can push a message to users in Guangdong and Hunan, but you cannot push a message to users in Guangdong who were active in the last three days.

### Push by tag in console

You can push a message by tag in the Tencent Cloud Console as shown below.

1. Select the tag type, e.g., custom tag or a category of preset tags.
![](https://main.qcloudimg.com/raw/b2e0e41398c907ebe8a57f2f848d59ba.png)
2. Select the tags for which you want to push a message after selecting the tag type.
After a tag is selected, the number of devices bound to it will be displayed.
![](https://main.qcloudimg.com/raw/fedb63301c89a7f4a8a7c3d0460a5837.png)

3. Select the "AND" or "OR" relationship for the selected tags as shown below:
Here, "Any" indicates the "OR" relationship, i.e., the message will be pushed to devices bound to any of the selected tags; "All" indicates the "AND" relationship, i.e., the message will be pushed to devices bound to all of the selected tags.
![](https://main.qcloudimg.com/raw/4fc45358b0177f1496ace6d9705ef494.png)


### Calling API for push by tag

For more information, please see the [Push API](https://intl.cloud.tencent.com/document/product/1024/33764) documentation.

## Applicable Scenarios for Push by Custom Tag

### KV tag overwriting (renewal notification)

You want to push a renewal notification in your app A to users whose membership will expire in three days. Assume that a device token is bound to tags `football` and `deadline:20200210`. If a user renews the membership for a month on February 9, 2020, you need to replace the tag `deadline:20200210` with `deadline:20200310`, i.e., the tag `deadline` can have only one value (the latest value). In this case, you can call the KV overwriting API to unbind the tag `deadline:20200210` and then bind the tag `deadline:20200310` without affecting other tags. When pushing a renewal notification (scheduled push is supported), set the tag to the current date plus three days; for example, if the current date is March 7, 2020, you can push the renewal notification to devices with the tag `deadline:20200310`.

### Binding tag for subscribed lecture and unbinding tag after lecture ends

Your app B provides many lectures given by influential people and you want to push a notification to inform users of an upcoming lecture to which they subscribe just before it begins. For example, if a user subscribes to the "COVID-19 Prevention" lecture, the title "COVID-19 Prevention" can be used as a tag to bind to the user device token. When the lecture is about to begin, you can select the `COVID-19 Prevention` tag to push a notification to inform the user of the lecture start. After the lecture ends, you can call the TPNS tag unbinding API to unbind the `COVID-19 Prevention` tag from the device token.


## FAQs

1. **Will be the API for querying bound devices by tag made publicly available?**
 This API is currently for internal use only and will not be made publicly available in the future for the sake of system stability. You can select a tag on the push page in the console to query its bound devices.

2. **Will be the API for querying bound tags by device token made publicly available?
This API is currently for internal use only and will not be made publicly available in the future for the sake of system stability. You can enter a token in the toolkit in the console to query its bound tags.
