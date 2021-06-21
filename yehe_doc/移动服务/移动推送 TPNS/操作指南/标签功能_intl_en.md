
Tag is a feature used in targeted push where you can call TPNS SDKs or server APIs to bind one or more tags to devices. After that, you can push messages based on the tags, which makes lean operations easier.

## Tag Push Scenarios

### User engagement and reactivation
Application operation often requires message reminders for new users, which is an important part of the new user experience design and improves the retention rate of new users. By selecting the `new devices` tag provided by TPNS during push, you can push messages to users registered on the specified date with speed and ease.
In addition, we also provide the `inactive users` tag, with which you can specify users who have not been active for N days as the push target and push messages to them for user reactivation, thus increasing the number of active application users.


### Event subscription notification

Your live streaming application will stream a football match at 18:00 on October 24, and the live stream will be available for reservation on October 20. You want to push a message about the upcoming start to users who subscribe to this program before the live stream starts.
If a user subscribes to this program, the title `10241800 Football` can be used as a tag to bind to the user device token. When the live stream is about to start, you can select the `Football` tag to push a notification to inform the user of the match start. After the match ends, you can call the TPNS tag unbinding API to unbind the `10241800 Football` tag from the device token.

### Renewal notification
You want to push a renewal notification in your application A to users whose membership will expire in three days. Assume that a device token is bound to tags `football` and `deadline:20200210`. If a user renews the membership for a month on February 9, 2020, you need to replace the tag `deadline:20200210` with `deadline:20200310`, i.e., the tag `deadline` can have only one value (the latest value). In this case, you can call the key-value overriding API to unbind the tag `deadline:20200210` and then bind the tag `deadline:20200310` without affecting other tags. When pushing a renewal notification (scheduled push is supported), set the tag to the current date plus three days; for example, if the current date is March 7, 2020, you can push the renewal notification to devices with the tag `deadline:20200310`.



## Tag Overview
TPNS provides two types of tags: custom tags and TPNS preset tags. Tag categories are as follows:

<table>
 <tr>
         <th>Tag Type</th>
            <th>Scenario</th>
						<th>tag_type Built in TPNS</th>
						  <th>Limit</th>
							 <th>Example</th>
 </tr>
         <tr><!--<td>1.1</td>-->
            <td>Custom tag</td>
            <td>Custom tag, such as meeting ID, class ID, and user hobbies (like basketball and digital products)</td>
						<td>xg_user_define</td>
						<td><li>Up to 10,000 custom tags are allowed (to increase the quota, <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a>).
<li>One device token can be bound to up to 100 custom tags (to increase the quota, <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a>).
<li>One custom tag can be bound to an unlimited number of device tokens.</td>
<td>love_basketball, love_shopping, male</td>
        </tr>
        <tr>
            <td  rowspan="12">Preset tag</td>
            <td>Application version</td>
						 <td>xg_auto_version</td>
            <td rowspan="9">Preset in TPNS, unlimited</td>
						<td>1.0.1, 1.0.2</td>
        </tr>
        <tr><!--<td>2.1</td>-->
            <td>Province</td>
						<td>xg_auto_province</td>
            <td>guangdong, hunan, shanghai</td>
        </tr>
        <tr><!--<td>3.1</td>-->
            <td>Active information</td>
						<td>xg_auto_active</td>
						 <td>20200521, 20200522</td>
        </tr>
				   <tr><!--<td>3.1</td>-->
            <td>TPNS SDK version</td>
						<td>xg_auto_sdkversion</td>
						 <td>1.1.5.4, 1.1.6.1</td>
        </tr>
				<tr><!--<td>4.1/td>-->
				  <td>System version</td>
					<td>xg_auto_systemversion</td>
					<td>10.0.0, 12.4.5</td>
				</tr><!--<td>4.1/td>-->
				  <td>System language</td>
					<td>xg_auto_systemlanguage</td>
				<td>zh, en, ja</td>
				</tr>
				<tr> <!--<td>5.1td>-->
				  <td>Country/Region</td>
					  <td>xg_auto_country</td>
					<td>CN, US (uppercase letters)</td>
				</tr>
				<tr><!--<td>5.1td>-->
				  <td>Phone brand</td>
					<td>xg_auto_devicebrand</td>
					 <td>xiaomi, huawei</td>
				</tr>
				<tr><!--<td>61td>-->
				  <td>Model</td>
					<td>xg_auto_deviceversion</td>
					<td>Samsung Note4, vivo Y75A</td>
				</tr>			
						<tr><!--<td>61td>-->
				  <td>Continuously active</td>
					<td>Does not support API call currently</td>
						<td>Devices active in the last N days. Value range: [1,30]. Format: string</td>
					<td>Devices active in the last "10" days</td>
				</tr>		
						<tr><!--<td>61td>-->
				  <td>Continuously inactive</td>
					<td>Does not support API call currently</td>
						<td>Devices inactive in the last N days. Value range: [1,30]. Format: string</td>
					<td>Devices inactive in the last "10" days</td>
				</tr>		
						<tr><!--<td>61td>-->
				  <td>Recently registered</td>
					<td>Does not support API call currently</td>
						<td><li>Devices recently registered. The tag value is [startDate,endDate] in the format of [YYYYmmdd,YYYYmmdd].
<li>The interval between `startDate` and `endDate` cannot exceed 30 days.
<li>`endDate` cannot be the current date.
<li>`startDate` cannot be more than 90 days ago.
<li>`startDate` and `endDate` can be the same.</td>
					<td>Devices registered within [20200901,20200910]</td>
				</tr>		
</table>

>?When you push by tag through API, you need to use the `tag_type` built in TPNS to set the tag type.

## Preparations
### Managing custom tags
 You can custom device tag names. Currently, TPNS allows you to set tags through RESTful APIs and device SDKs.

**Method 1. Set tags through RESTful APIs**
Bind and unbind a custom tag:
See [Tag Binding and Unbinding](https://intl.cloud.tencent.com/document/product/1024/33766).

**Method 2. Set tags through device SDKs**
For the iOS SDK, see [here](https://intl.cloud.tencent.com/document/product/1024/30727#tagging-feature).
For the Android SDK, see [Setting custom tag](https://intl.cloud.tencent.com/document/product/1024/30715#setting-custom-tag).

>?
>- One device can be bound to up to 100 tags (to increase the quota, [submit a ticket](https://console.cloud.tencent.com/workorder/category)).
>- One application can be bound to up to 10,000 tags (to increase the quota, [submit a ticket](https://console.cloud.tencent.com/workorder/category)).
>- One tag can contain up to 50 bytes.
>- One request can be used to bind or unbind up to 500 tags.

#### Custom tag use cases and keywords
Tag push is suitable for scenarios where more than 10 devices are bound to a tag and no more than 10 pushes are required per day. For other scenarios, account push (binding an account instead of a tag to multiple devices for push) is recommended.

**Keyword**
A colon (:) is the keyword for separating the key and value in a key-value pair for user tag binding. For example, if you assign the tag `level:3` to a device token, the TPNS backend will take `level` as the tag key and `3` as the tag value, while the original tag `level:3` is pushed. Storage based on key-value is mainly to facilitate subsequent overriding of tags of the same type.

#### Binding/Unbinding tags

TPNS provides APIs for binding/unbinding a single tag to/from a single device, a single tag to/from multiple devices, multiple tags to/from a single device, and multiple tags to/from multiple devices.

##### Binding/Unbinding a single tag to/from a single device
**Recommended scenarios**
1. Call the device SDK API, for example, to get a user's subscribed channel in the application and bind/unbind the channel tag to/from the device token.         
2. Call the RESTful API occasionally, for example, to perform integration testing.

**Tag binding method**

```json
{
    "operator_type": 1,

    "tag_list": ["tag"],
    "token_list": ["token"]
}
```

**Tag unbinding method**

```json
{
    "operator_type": 2,

    "tag_list": ["tag"],
    "token_list": ["token"]
}
```

**Use limits**
- A tag can contain up to 50 bytes.
- The API is called synchronously.

##### Binding/Unbinding multiple tags to/from a single device
**Recommended scenarios**
1. Call the device SDK API, for example, to get a user's characteristics tags such as age, province, and gender in the application and bind/unbind them to/from the device token in batches.
2. Call the RESTful API, for example, to get a device's user subscription information tags such as marital status and hobbies (football, movies, etc.) through other internal channels, bind/unbind them to/from the device token in batches.

**Tag binding method**
```json
{
    "operator_type": 3,

    "tag_list": ["tag1","tag2"],
    "token_list": ["token"]
}
```

**Tag unbinding method**

```json
{
    "operator_type": 4,

    "tag_list": ["tag1","tag2"],
    "token_list": ["token"]
}
```

**Use limits**
- A tag can contain up to 50 bytes.
- Up to 500 tags can be included in one call.
- The API is called synchronously.

##### Binding/Unbinding a single tag to/from multiple devices
**Recommended scenarios**
Call the RESTful API, for example, to bind/unbind the `football` tag to/from all users who like/dislike football in batches.

**Tag binding method**
```json
{
    "operator_type": 7,

    "tag_list": ["tag"],
    "token_list": ["token1","token2"]
}
```
**Tag unbinding method**
```json
{
    "operator_type": 8,

    "tag_list": ["tag"],
    "token_list": ["token1","token2"]
}
```

**Use limits**
- A tag can contain up to 50 bytes.
- Up to 500 device tokens can be included in one call.
- The API is called synchronously.

##### Binding/Unbinding multiple tags to/from multiple devices
**Recommended scenarios**
Call the RESTful API, for example, to bind/unbind the `football` and `basketball` tags to/from all users who like/dislike football and basketball in batches.

**Tag binding method**
```json
{
    "operator_type": 9,

    "tag_token_list": [{"tag":"tag1","token":"token1"},{"tag":"tag2","token":"token2"}]
}
```

**Tag unbinding method**
```json
{
    "operator_type": 10,

    "tag_token_list": [{"tag":"tag1","token":"token1"},{"tag":"tag2","token":"token2"}]
}
```
**Use limits**
- A tag can contain up to 50 bytes.
- Up to 500 device tokens can be included in one call.
- The API is called synchronously.


#### Tag overriding

TPNS provides two tag overriding methods: general overriding and overriding by tag category (key-value overriding). In key-value overriding, a colon (:) is used to separate the key and value in a key-value pair.

##### General overriding
**Recommended scenarios**
1. Call the device SDK API. For example, if all channel information subscribed by a device has expired, you need to unbind all the channel tags from the device. However, traversing all tags to unbind them one by one is inconvenient. In this case, you can call this API to override the tags.
2. Call the RESTful API. For example, to set new tags for a device so that it will not be affected by legacy tags, call this API to override them.

**Tag overriding method**
```json
{
    "operator_type": 6,

    "tag_list": ["test", "level:1",, "level:2"], 
    "token_list": ["token"]
}
```
**Use limits**
- A tag can contain up to 50 bytes.
- The API is called asynchronously. You are recommended to set the call interval to longer than 1 second.

##### Key-value overriding
**Recommended scenarios**
1. Call the device SDK API.
2. Call the RESTful API.

**Instructions:** a colon (:) is used for separating the key and value in a key-value pair. For example, `level:2` indicates that the device level is 2. Assume that the device level is upgraded to 3, then you need to delete the tag `level:2` before adding the tag `level:3`. If you know that the device has only the tag `level:2`, you can call the general overriding API to override it. However, a device usually has multiple tags. If the device has another tag `test` and you want to delete only the tag `level:2`, you need to manipulate all tags of the device or call the relevant TPNS API to find the corresponding legacy tag and delete it, which is inconvenient. In this case, you can call this API to override only tags with the key `level`.

**Tag overriding method**
```json
{
    "operator_type": 6,

    "tag_list": ["test:2", "level:3"], 
    "token_list": ["token"]
}
```
**API description:** key-value overriding can be performed properly only when all tags in the `tag_list` have a colon (:). For example, if a token has the tags `test` and `level:1`, after this API is called, the tag list of the token will include `test`, `test:2`, and `level:3`.
**Use limits**
- A tag can contain up to 50 bytes.
- Up to 500 tags can be included in one call.
- The API is called asynchronously. You are recommended to set the call interval to longer than 1 second.


#### Tag deletion scenarios

 TPNS provides two tag deletion methods: deleting all tags of a single device and deleting specific tags of an application.

###### Deleting all tags of a single device
**Recommended scenarios**
1. Call the device SDK API.
2. Call the RESTful API.

**Instructions:** you can use this API to delete all legacy tags of a device. This API is generally used to delete expired tags or set tags again after misoperations.

**Tag deletion method**
```json
{
    "operator_type": 5,

    "token_list": ["token"]
}
```
**Use limits**
- A tag can contain up to 50 bytes.
- The API is called asynchronously. You are recommended to set the call interval to longer than 1 second.

##### Deleting specific tags of an application
**Recommended scenarios**
Call the RESTful API.
**Instructions:** you can use this API to delete specific tags of an application, i.e., removing them from the tag list of the application after unbinding them from bound devices. This API is generally used to delete disused tags. For example, you can call this API to delete testing tags added during test after the application is officially released.
**Tag deletion method**
```json
{
    "tag_list": ["tag1", "tag2"]
}
```
**Use limits**
- A tag can contain up to 50 bytes.
- Up to 500 tags can be included in one call.
- The API is called asynchronously. You are recommended to set the call interval to longer than 1 second.


### Managing preset tags
- Preset tags are tags maintained on the TPNS platform, i.e., tags automatically collected by the SDK when user devices are registered with or connected to the TPNS server. Currently, TPNS preset tags include application version, system version, province, active information, system language, SDK version, country/region, phone brand, and phone model.
- All devices are bound to the latest preset tags, which will automatically replace the corresponding legacy ones. For example, if the current application version of a device is 1.0.1, when the application is upgraded to 1.0.2, the device will be automatically unbound from the `v1.0.1` tag and then bound to the `v1.0.2` tag.

### Querying tags bound to devices
 To query specific preset and custom tags by device token, go to the Tencent Cloud console and choose **Toolbox** > **Troubleshooting Tools**.
 See the figure below:
 ![](https://main.qcloudimg.com/raw/960e8eb3678ebe7457b5887966abed5f.png)

## Getting Started
Tag push supports a single tag or multiple tags. For push by multiple tags, TPNS currently supports only tags in the same category (combined in the "AND" or "OR" relationship). If you push messages by custom tags, only custom tags can be combined in the "AND" or "OR" relationship. If you push messages by preset tags, only preset tags in the same category can be combined. For example, you can push a message to users in Guangdong and Hunan, but you cannot push a message to users in Guangdong who were active in the last three days.

### Using the console
You can push a message by tag in the Tencent Cloud console as follows:
1. Select the tag type, e.g., custom tag or a category of preset tags.
![](https://main.qcloudimg.com/raw/62e856a901b5be9980f2c6102b0f020c.png)
2. Select the tags for which you want to push a message after selecting the tag type.
![](https://main.qcloudimg.com/raw/6dad332635c15202548a2aca25527b6a.png)
After a tag is selected, the number of devices bound to the selected tag will also be displayed. The tag combination in the figure above indicates to push a message to male users in Guangdong and Jiangsu who were active on 2020-04-23, 2020-04-22, or 2020-04-21. Then, click **Preview** to push the message to the corresponding target devices.



### Calling the push API for tag push

Set the `audience_type` (push target) in the push API request parameter to `tag` to enable tag push. For more information, see [Push API](https://intl.cloud.tencent.com/document/product/1024/33764).
API example: push a message to male users in Guangdong and Jiangsu who were active on 2020-04-23, 2020-04-22, or 2020-04-21.
```
{
    "audience_type": "tag",
    "tag_rules": [
        {
            "tag_items": [
                {
                    "tags": [
                        "guangdong",
                        "jiangsu"
                    ],
                    "is_not": false,
                    "tags_operator": "OR",
                    "items_operator": "OR",
                    "tag_type": "xg_auto_province"  
                },
                {
                    "tags": [
                        "20200421",
                        "20200422",
                        "20200423"
                    ],
                    "is_not": false,
                    "tags_operator": "OR",
                    "items_operator": "AND",
                    "tag_type": "xg_auto_active"
                }
            ],
            "operator": "OR",
            "is_not": false
        },
        {
            "tag_items": [
                {
                    "tags": [
                        "male"
                    ],
                    "is_not": false,
                    "tags_operator": "OR",
                    "items_operator": "OR",
                    "tag_type": "xg_user_define"
                }
            ],
            "operator": "AND",
            "is_not": false
        }
    ],
    "message_type": "notify",
    "message": {
    "title": "Test title",
    "content": "Test content",
    "android": {
		"ring": 1,
        "ring_raw": "ring",
        "vibrate": 1,
        "lights": 1,
        "clearable": 1,
        },
      "custom_content":"{\"key\":\"value\"}"
    }
}
}
```
## FAQs

1. **Will the API for querying bound devices by tag be made publicly available?**
 The API is currently for internal use only and will not be made publicly available in the future for the sake of system stability. You can select a tag on the push page in the console to query its bound devices.

2. **Will the API for querying bound tags by device token be made publicly available?**
The API is currently for internal use only and will not be made publicly available in the future for the sake of system stability. You can enter a token in the toolkit in the console to query its bound tags.
