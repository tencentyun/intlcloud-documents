## Release 4

Release time: December 13, 2018 14:55:15

This release contains:

Improvement to existing documentation.

New APIs:

* [CreateTopicRule](https://cloud.tencent.com/document/api/634/31582)
* [DeleteTopicRule](https://cloud.tencent.com/document/api/634/31581)
* [DescribeDevice](https://cloud.tencent.com/document/api/634/31583)
* [DisableTopicRule](https://cloud.tencent.com/document/api/634/31580)
* [EnableTopicRule](https://cloud.tencent.com/document/api/634/31579)
* [ReplaceTopicRule](https://cloud.tencent.com/document/api/634/31578)

Modified APIs:

* [CreateDevice](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/634/19496)
	* New input parameters: LoraMoteType, Skey
	* New output parameters: LoraMoteType, LoraAppKey, LoraNwkKey
* [CreateProduct](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/634/19479)
	* New input parameters: Skey
* [DeleteDevice](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/634/19494)
	* New input parameters: Skey
* [DeleteProduct](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/634/19478)
	* New input parameters: Skey

New data structures:

* [TopicRulePayload](https://cloud.tencent.com/document/api/634/19497#TopicRulePayload)

Modified data structure:

* [ProductProperties](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/634/19497#ProductProperties)
	* New members: ModelId, ModelName

## Release 3

Release time: October 11, 2018 15:26:45

This release contains:

Improvement to existing documentation.

**Deleted APIs:**

* GetDeviceShadow

Modified data structure:

* [DeviceInfo](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/634/19497#DeviceInfo)
	* New members: LoraMoteType

## Release 2

Release time: September 27, 2018 17:06:25

This release contains:

Improvement to existing documentation.

Modified APIs:

* [CreateDevice](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/634/19496)
	* New input parameters: LoraDevEui
	* New output parameters: LoraDevEui
* [CreateProduct](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/634/19479)
	* New output parameters: ProductProperties
* [DescribeProducts](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/634/19477)
	* New input parameters: Filters

New data structures:

* [Filter](https://cloud.tencent.com/document/api/634/19497#Filter)

Modified data structure:

* [DeviceInfo](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/634/19497#DeviceInfo)
	* New members: LoraDevEui
* [ProductProperties](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/634/19497#ProductProperties)
	* New members: Platform, Appeui

## Release 1

Release time: August 30, 2018 16:03:13

This release contains:

Improvement to existing documentation.

New APIs:

* [CancelTask](https://cloud.tencent.com/document/api/634/19484)
* [CreateDevice](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/634/19496)
* [CreateMultiDevice](https://cloud.tencent.com/document/api/634/19495)
* [CreateProduct](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/634/19479)
* [CreateTask](https://cloud.tencent.com/document/api/634/19483)
* [DeleteDevice](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/634/19494)
* [DeleteProduct](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/634/19478)
* [DescribeDeviceShadow](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/634/19489)
* [DescribeDevices](https://cloud.tencent.com/document/api/634/19493)
* [DescribeMultiDevTask](https://cloud.tencent.com/document/api/634/19492)
* [DescribeMultiDevices](https://cloud.tencent.com/document/api/634/19491)
* [DescribeProducts](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/634/19477)
* [DescribeTask](https://cloud.tencent.com/document/api/634/19482)
* [DescribeTasks](https://cloud.tencent.com/document/api/634/19481)
* [GetDeviceShadow](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/634/19489)
* [PublishMessage](https://cloud.tencent.com/document/api/634/19486)
* [UpdateDeviceShadow](https://cloud.tencent.com/document/api/634/19488)

New data structures:

* [Attribute](https://cloud.tencent.com/document/api/634/19497#Attribute)
* [BatchPublishMessage](https://cloud.tencent.com/document/api/634/19497#BatchPublishMessage)
* [BatchUpdateShadow](https://cloud.tencent.com/document/api/634/19497#BatchUpdateShadow)
* [DeviceInfo](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/634/19497#DeviceInfo)
* [DeviceTag](https://cloud.tencent.com/document/api/634/19497#DeviceTag)
* [MultiDevicesInfo](https://cloud.tencent.com/document/api/634/19497#MultiDevicesInfo)
* [ProductInfo](https://cloud.tencent.com/document/api/634/19497#ProductInfo)
* [ProductMetadata](https://cloud.tencent.com/document/api/634/19497#ProductMetadata)
* [ProductProperties](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/634/19497#ProductProperties)
* [Task](https://cloud.tencent.com/document/api/634/19497#Task)
* [TaskInfo](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/634/19497#TaskInfo)

