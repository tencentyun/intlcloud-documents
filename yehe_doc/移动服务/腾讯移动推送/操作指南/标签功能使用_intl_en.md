
Tag is used in targeted push where you can call the TPNS SDK or server API to bind one or more tags to devices. After that, you can push messages based on the tags, which makes lean operations easier.

## Tag Push Use Cases

### User stickiness
In app operation, it is important to often send subscribed messages to new users and improve their retention rate. To do this, you only need to use the **New Equipment** tag provided by TPNS to push messages to users signed up on a specified date.
We also provide the **Offline Device** tag for message push to specified users who were inactive for N days to reduce customer attrition and improve user activity.

### Event subscription notification
Your live streaming application will stream a football match at 18:00 on October 24, and the live stream will be available for reservation on October 20. You want to push a message about the upcoming start to users who subscribe to this program before the live stream starts.
If a user subscribes to this program, the title `10241800 Football` can be used as a tag to bind to the user device token. When the live stream is about to start, you can select the `Football` tag to push a notification to inform the user of the match start. After the match ends, you can call the TPNS tag unbinding API to unbind the `10241800 Football` tag from the device token.

### Renewal notification
You want to push a renewal notification in your application A to users whose membership will expire in three days. Assume that a device token is bound to tags `football` and `deadline:20200210`. If a user renews the membership for a month on February 9, 2020, you need to replace the tag `deadline:20200210` with `deadline:20200310`, i.e., the tag `deadline` can have only one value (the latest value). In this case, you can call the KV overwriting API to unbind the tag `deadline:20200210` and then bind the tag `deadline:20200310` without affecting other tags. When pushing a renewal notification (scheduled push is supported), set the tag to the current date plus three days; for example, if the current date is March 7, 2020, you can push the renewal notification to devices with the tag `deadline:20200310`.


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
            <td>Custom tag, such as meeting ID, class ID, user hobbies (like basketball and digital products), etc.</td>
						<td>xg_user_define</td>
						  <td><li>Up to 10,000 custom tags are allowed (if you want to increase this limit, please submit a ticket)
<li>One device token can be bound to up to 100 custom tags (if you want to increase this limit, please submit a ticket)
<li>One custom tag can be bound to an unlimited number of device tokens</td>
<td> love_basketball, love_shopping, male, etc.</td>
        </tr>
        <tr>
            <td  rowspan="12">Preset tag</td>
            <td>Application version</td>
						 <td>xg_auto_version</td>
            <td rowspan="12">Preset in TPNS, unlimited</td>
						<td>1.0.1, 1.0.2, etc.</td>
        </tr>
        <tr><!--<td>2.1</td>-->
            <td>District</td>
						<td>xg_auto_province</td>
            <td>guangdong, hunan, shanghai, etc.</td>
        </tr>
        <tr><!--<td>3.1</td>-->
            <td>Active status information</td>
						<td>xg_auto_active</td>
						 <td>20200521, 20200522, etc.</td>
        </tr>
				   <tr><!--<td>3.1</td>-->
            <td>TPNS SDK version</td>
						<td>xg_auto_sdkversion</td>
						 <td>1.1.5.4, 1.1.5.4, 1.1.6.1, etc.</td>
        </tr>
				<tr><!--<td>4.1/td>-->
				  <td>System version</td>
					<td>xg_auto_systemversion</td>
					<td>10.0.0, 12.4.5, etc.</td>
				</tr><!--<td>4.1/td>-->
				  <td>System language</td>
					<td>xg_auto_systemlanguage</td>
				<td>zh, en, ja, etc.</td>
				</tr>
				<tr> <!--<td>5.1td>-->
				  <td>Country/Region</td>
					  <td>xg_auto_country</td>
					<td>CN, US, etc.</td>
				</tr>
				<tr><!--<td>5.1td>-->
				  <td>Phone brand</td>
					<td>xg_auto_devicebrand</td>
					 <td>xiaomi, huawei, etc.</td>
				</tr>
				<tr><!--<td>61td>-->
				  <td>Model</td>
					<td>xg_auto_deviceversion</td>
					<td>Samsung Note4, vivo Y75A, etc.</td>
				</tr>
						<tr><!--<td>61td>-->
				  <td>Online duration</td>
					<td>The API call is not supported</td>
					<td>Devices online in the last 10 days</td>
				</tr>		
						<tr><!--<td>61td>-->
				  <td>Offline duration</td>
					<td>The API call is not supported</td>
					<td>Devices offline in the last 10 days</td>
				</tr>		
						<tr><!--<td>61td>-->
				  <td>Recently registered</td>
					<td>The API call is not supported</td>
					<td>Devices registered between September 1 and September 10, 2020</td>
				</tr>							
</table>

>?When you push by tag through API, you need to use the `tag_type` built in TPNS to set the tag type.

## Preparations
### Managing custom tag
 Custom tag is a tag setting method where you can custom the device tag name. Currently, TPNS allows you to set tags through REST API and device SDK.

**Method 1. Set tags through REST API**
Bind and unbind a custom tag:
For more information on how to do so through API, please see [Binding Tag](https://intl.cloud.tencent.com/document/product/1024/33766)

**Method 2. Set tags through device SDK**
For more information on how to set tags through the SDK for iOS, please see [Setting Custom Tag](https://intl.cloud.tencent.com/document/product/1024/30727)
For more information on how to set tags through the SDK for Android, please see [Setting Custom Tag](https://intl.cloud.tencent.com/document/product/1024/30715)

#### Custom tag use cases and keywords
Tag push is suitable for scenarios where the number of devices bound to a tag is high (more than 10 generally) but the push frequency is low (below 10 pushes a day generally). For scenarios where the number of bound devices is small but the push frequency is high, you are recommended to use push by account, i.e., binding an account instead of a tag to multiple devices for push.

**Keyword**
A colon ":" is the keyword for separating the `key` and `value` in a `key-value` pair for user tag binding; for example, if you assign the tag `level:3` to a device token, the TPNS backend will take `level` as the tag key and `3` as the tag value. The actual push will not be affected, where the tag `level:3` is still used for push. Storage based on `key-value` is mainly to facilitate subsequent overwriting of tags in the same category; for example, if the device token is bound to another tag such as `male` (i.e., the device has two tags: `male` and `level:3`), when the membership level of the device is upgraded to level 4 and you want to overwrite the tag `level:3` with `level:4` without affecting the `male` tag, you can directly call the key-value overwriting API to set the `level:4` tag for the device, and then the tags bound to the device token will become `male` and `level:4`.

#### Binding/Unbinding tag

TPNS provides APIs for binding/unbinding a single tag to/from a single device, a single tag to/from multiple devices, multiple tags to/from a single device, and multiple tags to/from multiple devices.
##### Single tag for single device
**Recommended scenarios**
1. The device SDK API is called; for example, to automatically get the user subscription channel in the application, bind the channel tag to the device token, and vice versa.         
2. The RESTful API are called occasionally in scenarios such as integration testing.

**Binding tag**

```json
{
    "operator_type": 1,
    "platform": "android",
    "tag_list": ["tag"],
    "token_list": ["token"]
}
```

**Unbinding tag**

```json
{
    "operator_type": 2,
    "platform": "android",
    "tag_list": ["tag"],
    "token_list": ["token"]
}
```

**Use limits**
- A tag can contain up to 50 bytes.
- The API is called synchronously.

##### Multiple tags for single device
**Recommended scenarios**
1. The device SDK API is called; for example, to automatically get user characteristics tags such as age, district, and gender in the application, bind them to the device token in batches, and vice versa.
2. The RESTful API is called; for example, to get a device's user subscription information tags such as marital status and hobbies (football, movies, etc,) through other internal channels, bind them to the device token in batches, and vice versa.

**Binding tag**
```json
{
    "operator_type": 3,
    "platform": "android",
    "tag_list": ["tag1","tag2"],
    "token_list": ["token"]
}

```
**Unbinding tag**
```json
{
    "operator_type": 4,
    "platform": "android",
    "tag_list": ["tag1","tag2"],
    "token_list": ["token"]
}
```
**Use limits**
- A tag can contain up to 50 bytes.
- Up to 500 tags can be included in one call.
- The API is called synchronously.

##### Single tag for multiple devices
**Recommended scenarios**
Only the RESTful API can be called; for example, to add the "football" tag to all users who like football, this API can be called to bind tags in batches, and vice versa.

**Binding tag**
```json
{
    "operator_type": 7,
    "platform": "android",
    "tag_list": ["tag"],
    "token_list": ["token1","token2"]
}
```
**Unbinding tag**
```json
{
    "operator_type": 8,
    "platform": "android",
    "tag_list": ["tag"],
    "token_list": ["token1","token2"]
}
```
**Use limits**
- A tag can contain up to 50 bytes.
- Up to 500 device tokens can be included in one call.
- The API is called synchronously.

##### Multiple tags for multiple devices
**Recommended scenarios**
Only the RESTful API can be called; for example, to add the "football" tag to all users who like football and the "basketball" tag to all users who like basketball, this API can be called to bind tags in batches, and vice versa.

**Binding tag**
```json
{
    "operator_type": 9,
    "platform": "android",
    "tag_token_list": [{"tag":"tag1","token":"token1"},{"tag":"tag2","token":"token2"}]
}
```
**Unbinding tag**
```json
{
    "operator_type": 10,
    "platform": "android",
    "tag_token_list": [{"tag":"tag1","token":"token1"},{"tag":"tag2","token":"token2"}]
}
```
**Use limits**
- A tag can contain up to 50 bytes.
- Up to 500 device tokens can be included in one call.
- The API is called synchronously.


#### Tag overwriting

TPNS provides two tag overwriting methods, namely, general overwriting and overwriting by tag category (aka key-value (KV) overwriting), where a colon (":") is used to separate the `key` and `value` in a key-value pair.
##### General overwriting
**Recommended scenarios**
1. The device SDK API is called. If all channel information subscribed by a device has expired, you need to unbind all the channel tags from the device. However, traversing all tags to unbind them one by one is very inconvenient. In this case, you can call this API to overwrite the tags in batches.
2. The RESTful API is called; for example, to set new tags for a device so that it will not be affected by legacy tags, this API can be called to overwrite them.

**Tag overwriting method**
```json
{
    "operator_type": 6,
    "platform": "android",
    "tag_list": ["test", "level:1",, "level:2"], 
    "token_list": ["token"]
}
```
**Use limits**
- A tag can contain up to 50 bytes.
- The API is called asynchronously. You are recommended to set the call interval to longer than 1 second.

##### KV overwriting
**Recommended scenarios**
1. The device SDK API is called.
2. The RESTful API is called.

**Instructions:** a colon (":") is used for separation. The content before ":" is used as the tag category, while the content after ":" is used as the specific tag value. For example, `level:2` indicates that the device level is 2. Assume that the device level is upgraded to 3, then you need to delete the tag `level:2` before adding the tag `level:3`. If you know that the device has only the tag `level:2`, you can call the general overwriting API to overwrite it. However, a device usually has multiple tags. If the device has another tag `test` and you want to delete only the tag `level:2`, you need to manipulate all tags of the device or call the relevant TPNS API to find the corresponding legacy tag and delete it, which is very inconvenient. In this case, you can call this API to overwrite only tags with the key (category) of `level`.

**Tag overwriting method**
```json
{
    "operator_type": 6,
    "platform": "android",
    "tag_list": ["test:2", "level:3"], 
    "token_list": ["token"]
}
```
**API description:** only when all tags in the `tag_list` have a colon (":") can KV overwriting be performed properly; for example, if a token has tags `test` and `level:1`, after this API is called, the tag list of the token will include `test`, `test:2`, and `level:3`.
**Use limits**
- A tag can contain up to 50 bytes.
- Up to 500 tags can be included in one call.
- The API is called asynchronously. You are recommended to set the call interval to longer than 1 second.


#### Tag deletion scenarios

 TPNS provides two tag deletion methods, namely, deleting all tags of a device and deleting specific tags of an application.

##### Deleting all tags of a single device
**Recommended scenarios**
1. The device SDK API is called.
2. The RESTful API is called.

**Instructions:** you can use this API to delete all legacy tags of a device. This API is generally used to delete expired tags or set tags again after a faulty operation.

**Tag deletion method**
```json
{
    "operator_type": 5,
    "platform": "android", 
    "token_list": ["token"]
}
```
**Use limits**
- A tag can contain up to 50 bytes.
- The API is called asynchronously. You are recommended to set the call interval to longer than 1 second.

##### Deleting specific application tags
**Recommended scenarios**
1. Only the RESTful API can be called.
**Description:** you can use this API to delete specific tags of an application, i.e., removing them from the tag list of the application after unbinding them from bound devices. It is generally used to delete obsolete tags; for example, to delete testing tags added during test after the application is officially released, you can call this API.
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


### Managing preset tag
- Preset tags are tags maintained on the TPNS platform, i.e., tags automatically collected by the SDK when user devices are registered with or connected to the TPNS server. Currently, TPNS preset tags include application version, system version, district, active status, system language, SDK version, country/region, phone brand, and phone model.
- All devices are bound to the latest preset tags, which will automatically replace the corresponding legacy ones. For example, if the current application version of a device is 1.0.1, when the application is upgraded to 1.0.2, the device will be automatically unbound from the v1.0.1 tag and then bound to the v1.0.2 tag.

### Querying tags bound to device
 You can query specific preset and custom tags by device token on the **Toolkit > Troubleshooter** page in the Tencent Cloud Console.
 See below:
 ![](https://main.qcloudimg.com/raw/960e8eb3678ebe7457b5887966abed5f.png)

## Getting Started
Tag push supports a single tag or multiple tags. For push by multiple tags, TPNS currently only supports tags in the same category (combined in the "AND" or "OR" relationship). Specifically, if you push messages by custom tags, only custom tags can be combined in "AND" or "OR" relationship; and if you push message by preset tags, only preset tags in the same category can be combined. For example, you can push a message to users in Guangdong and Hunan, but you cannot push a message to users in Guangdong who were active in the last three days.

### Console
You can push a message by tag in the Tencent Cloud Console as shown below.
1. Select the tag type, e.g., custom tag or a category of preset tags.
![](https://main.qcloudimg.com/raw/62e856a901b5be9980f2c6102b0f020c.png)
2. Select the tags for which you want to push a message after selecting the tag type.
![](https://main.qcloudimg.com/raw/6dad332635c15202548a2aca25527b6a.png)
After a tag is selected, the number of devices bound to the selected tag will also be displayed. The tag combination in the figure above indicates to push a message to male users in Guangdong or Jiangsu who were active on April 23, 2020, April 22, 2020, or April 21, 2020. Then, click "Preview" to push the message to the corresponding target devices.



### Calling API for tag push

Set the `audience_type` (push target) in the Push API request parameter to `tag` to enable tag push. For more information, please see [Push API](https://intl.cloud.tencent.com/document/product/1024/33764).
API example: push a message to male users in Guangdong or Jiangsu who were active on April 23, 2020, April 22, 2020, or April 21, 2020.
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
    "title": "test title",
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

1. **Will be the API for querying bound devices by tag made publicly available?**
 This API is currently for internal use only and will not be made publicly available in the future for the sake of system stability. You can select a tag on the push page in the console to query its bound devices.

2. **Will be the API for querying bound tags by device token made publicly available?
This API is currently for internal use only and will not be made publicly available in the future for the sake of system stability. You can enter a token in the toolkit in the console to query its bound tags.
