[//]: # (chinagitpath:XXXXX)

A device shadow document is a file of state and configuration data cached by the server for the device. It is stored as JSON text and consists of the following parts:
![thing_shadow](https://mc.qcloudimg.com/static/img/f184e69d6f0190bd6125ad5d86e1eb61/image.png)

### state
 - **reported**
This is the state reported by the device itself. The device can write data to this part of the document to report its new state. The application can read this part of the document to get the state of the device.
 - **desired**
This is the desired state of the device. The application writes data to this part of the document via the HTTP RESTful API to update the device state. The device-side SDK syncs the shadow data to the device by registering relevant property and callback through the device shadow service.

### metadata
This is the metadata information of the device shadow, including the last update time of each property in the "state" part.

### version
This is the version number of the device shadow document, which is incremented each time the device shadow document is updated. The version number is maintained by Tencent Cloud backend, ensuring that the data of the device is consistent with that of the device shadow.

### timestamp
This is the last update time of the device shadow document.

Sample device shadow document:

```
{
	"state":{
		"reported":{
			"attr_name1":"value1",
		},
		"desired":{
			"attr_name2":"value2",
		}
	},
	"metadata":{
		"reported":{
			"attr_name1":{
				"timestamp":123456789
			},	
		},
		"desired":{
			"attr_name2":{
				"timestamp":123456789
			},		
		}
	},
	"version":1,
	"timestamp":123456789
}
```

### Blank part

If the device shadow document is empty, the device shadow document obtained at this time is:

```
{
	"state":{},
	"metadata":{},
	"version":0
}
```

Only when the device shadow document has the desired state, there will be a "desired" part, and the "reported" part can be empty, for example:

```
{
	"state":{
		"desired":{
			"attr_name2":"value2",
		}
	},
	"metadata":{
		"desired":{
			"attr_name2":{
				"timestamp":123456789
			},		
		}
	},
	"version":1,
	"timestamp":123456789
}
```

After the device state is successfully updated, the latest state needs to be reported and the "desired" part removed from the document. To remove the "desired" part, it needs to be set to null, for example:

```
{
	"state":{
		"reported":{
			"attr_name1":"new_value1",
			"attr_name2":"new_value2",
		},
		"desired":null
	},
	"version":1
}
```

### Array

The device shadow document supports arrays. Only an entire array but not an element of the array can be updated, and none of the array elements ***can be null***.

