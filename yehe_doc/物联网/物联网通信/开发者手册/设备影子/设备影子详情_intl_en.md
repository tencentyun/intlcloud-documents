

A device shadow document is a file of status and configuration data cached by the server for a device, which is stored as JSON text and consists of the following parts:
![thing_shadow](https://mc.qcloudimg.com/static/img/f184e69d6f0190bd6125ad5d86e1eb61/image.png)

### state
 **reported**
This is the status reported by the device itself. The device can write data to this part of the document to report its new status, and the application can read this part to get the status of the device.
 
 **desired**
This is the desired status of the device. The application writes data to this part of the document through the HTTP RESTful API to update the device status. The device SDK syncs the shadow data to the device by registering relevant attributes and callback through the device shadow service.

### metadata
This is the metadata information of the device shadow, including the last updated time of each attribute in the `state` section.

### version
This is the version number of the device shadow document, which is increased each time the document is updated. The version number is maintained by Tencent Cloud on the backend, ensuring that the data of the device is consistent with that of the device shadow.

### timestamp
This is the last updated time of the device shadow document. Below is a sample document:
```
{
 "state": {
  "reported": {
   "attr_name1": "value1"
  },
  "desired": {
   "attr_name2": "value2"
  }
 },
 "metadata": {
  "reported": {
   "attr_name1": {
    "timestamp": 123456789
   }
  },
  "desired": {
   "attr_name2": {
    "timestamp": 123456789
   }
  }
 },
 "version": 1,
 "timestamp": 123456789
}
```

### Blank part

Below is a sample device shadow document that is blank:
```
{
	"state":{},
	"metadata":{},
	"version":0
}
```

Only when the device shadow document has the desired status will there be a `desired` part, and the `reported` part can be empty; for example:
```
{
 "state": {
  "desired": {
   "attr_name2": "value2"
  }
 },
 "metadata": {
  "desired": {
   "attr_name2": {
    "timestamp": 123456789
   }
  }
 },
 "version": 1,
 "timestamp": 123456789
}
```

After the device status is successfully updated, the latest status needs to be reported, and the `desired` part needs to be removed from the document. To remove this part, you need to set it to `null`; for example:

```
{
 "state": {
  "reported": {
   "attr_name1": "new_value1",
   "attr_name2": "new_value2"
  },
  "desired": null
 },
 "version": 1
}
```

### Array
The device shadow document supports arrays. Only an entire array but not an element in the array can be updated, and none of the elements can be null.


