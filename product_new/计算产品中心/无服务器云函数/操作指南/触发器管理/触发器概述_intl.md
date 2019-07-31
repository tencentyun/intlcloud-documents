SCF is a typical event-triggered serverless runtime environment, whose core components are SCF functions and event sources. An event source is a Tencent Cloud service or user-defined code that publishes an event, an SCF function is the handler of the event, and a function trigger is a set that manages the correspondence between the function and the event source. For example, in the following scenarios:

* Image/video processing: Crops the image uploaded by a user into a appropriate size, stores the images in COS, creates thumbnails of each image, and displays them on the user page. In this scenario, you need to select COS as the event source, and publish the event (Event) to the SCF function when the file is created. The event data provides all the information about the bucket and the file.
* Data processing: Analyzes the data collected during the day (such as clickstreams) and generates a report at 00:00. In this scenario, you need to select a timer as the event source to publish an event to the SCF function at a specific time.
* Custom application: The first image is called in your application to handle the SCF function as a module of the application. In this scenario, you need to call the Invoke API in the application to publish an event.

These event sources can be any of the following:

* Internal event sources: These are pre-configured Tencent Cloud services that can be used with SCF. If you configure one of these event sources as function trigger, the function will be called automatically when an event occurs. The relationship between the event source and the function (i.e., the event source mapping) will be maintained on the event source side. For example, COS provides a [Put Bucket Notification API](https://cloud.tencent.com/document/product/436/8588). Using this API, you can bind the bucket event to the function.
* Custom applications: You can let custom applications publish events and call SCF functions.

## Sample 1. COS publishes an event and calls a function

You can configure the event source mapping for COS to determine what behaviors of COS trigger the SCF function (such as object PUT or DELETE). The COS event source mapping is stored in COS and uses the bucket notification feature to direct COS to call the function when an event of particular types occurs:

- A COS trigger is created.
- The user creates/deletes an object in the bucket.
- COS detects an object creation/deletion event.
- COS automatically calls a function. It will be determined which function should be called based on the event source mapping stored in the COS configuration. The bucket and object information will be passed to the function as event data.

## Sample 2: A timer publishes a time and calls a function
The event source mapping of the timer is saved in the SCF function configuration to determine when the function should be automatically triggered:

- A timer trigger is created.
- The timer automatically calls the function at the configured time.

## Sample 3: A custom application calls a function
If you need to call an SCF function in a custom application, you do not need to configure a function trigger or set up an event source mapping in this case. At this point, the event source uses the Invoke API.

- The custom application uses the Invoke API to call the function and pass in the event data.
- The function receives the triggering request and is executed.
- If a sync call is used, the function will return the result to the application.

>**Notes:**
In this example, since the custom application and the function are produced by the same user, the user credentials (APPID, SecretId, and SecretKey) can be specified.

## Considerations
1. The current trigger-related restrictions for a single function can be viewed in [Quota Limits](https://cloud.tencent.com/document/product/583/11637).
2. There are specific restrictions on event source mappings due to the limitations of different cloud services. For example, for a COS trigger, the same event (such as file upload) in the same COS bucket cannot trigger multiple different functions.
