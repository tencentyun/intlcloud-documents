## Release 4

Release time: December 13, 2018 14:55:15

This release contains:

Improvement to existing documentation.

New APIs:

* [CreateTopicRule](/document/api/634/31582)
* [DeleteTopicRule](/document/api/634/31581)
* [DescribeDevice](/document/api/634/31583)
* [DisableTopicRule](/document/api/634/31580)
* [EnableTopicRule](/document/api/634/31579)
* [ReplaceTopicRule](/document/api/634/31578)

Modified APIs:

* [CreateDevice](/document/api/634/19496)
	* New input parameters: LoraMoteType, Skey
	* New output parameters: LoraMoteType, LoraAppKey, LoraNwkKey
* [CreateProduct](/document/api/634/19479)
	* New input parameters: Skey
* [DeleteDevice](/document/api/634/19494)
	* New input parameters: Skey
* [DeleteProduct](/document/api/634/19478)
	* New input parameters: Skey

New data structures:

* [TopicRulePayload](/document/api/634/19497#TopicRulePayload)

Modified data structure:

* [ProductProperties](/document/api/634/19497#ProductProperties)
	* New members: ModelId, ModelName

## Release 3

Release time: October 11, 2018 15:26:45

This release contains:

Improvement to existing documentation.

**Deleted APIs:**

* GetDeviceShadow

Modified data structure:

* [DeviceInfo](/document/api/634/19497#DeviceInfo)
	* New members: LoraMoteType

## Release 2

Release time: September 27, 2018 17:06:25

This release contains:

Improvement to existing documentation.

Modified APIs:

* [CreateDevice](/document/api/634/19496)
	* New input parameters: LoraDevEui
	* New output parameters: LoraDevEui
* [CreateProduct](/document/api/634/19479)
	* New output parameters: ProductProperties
* [DescribeProducts](/document/api/634/19477)
	* New input parameters: Filters

New data structures:

* [Filter](/document/api/634/19497#Filter)

Modified data structure:

* [DeviceInfo](/document/api/634/19497#DeviceInfo)
	* New members: LoraDevEui
* [ProductProperties](/document/api/634/19497#ProductProperties)
	* New members: Platform, Appeui

## Release 1

Release time: August 30, 2018 16:03:13

This release contains:

Improvement to existing documentation.

New APIs:

* [CancelTask](/document/api/634/19484)
* [CreateDevice](/document/api/634/19496)
* [CreateMultiDevice](/document/api/634/19495)
* [CreateProduct](/document/api/634/19479)
* [CreateTask](/document/api/634/19483)
* [DeleteDevice](/document/api/634/19494)
* [DeleteProduct](/document/api/634/19478)
* [DescribeDeviceShadow](/document/api/634/19489)
* [DescribeDevices](/document/api/634/19493)
* [DescribeMultiDevTask](/document/api/634/19492)
* [DescribeMultiDevices](/document/api/634/19491)
* [DescribeProducts](/document/api/634/19477)
* [DescribeTask](/document/api/634/19482)
* [DescribeTasks](/document/api/634/19481)
* [GetDeviceShadow](/document/api/634/19489)
* [PublishMessage](/document/api/634/19486)
* [UpdateDeviceShadow](/document/api/634/19488)

New data structures:

* [Attribute](/document/api/634/19497#Attribute)
* [BatchPublishMessage](/document/api/634/19497#BatchPublishMessage)
* [BatchUpdateShadow](/document/api/634/19497#BatchUpdateShadow)
* [DeviceInfo](/document/api/634/19497#DeviceInfo)
* [DeviceTag](/document/api/634/19497#DeviceTag)
* [MultiDevicesInfo](/document/api/634/19497#MultiDevicesInfo)
* [ProductInfo](/document/api/634/19497#ProductInfo)
* [ProductMetadata](/document/api/634/19497#ProductMetadata)
* [ProductProperties](/document/api/634/19497#ProductProperties)
* [Task](/document/api/634/19497#Task)
* [TaskInfo](/document/api/634/19497#TaskInfo)

