### Feature Overview

A gateway device can bind and unbind subdevices under it through data communication with the cloud. To implement this feature, the following two topics will be used:
- Data upstream topic (for publishing): `$gateway/operation/${productid}/${devicename}`
- Data downstream topic (for subscribing): `$gateway/operation/result/${productid}/${devicename}`

### Binding device

The gateway device can request to add its topological relationship with the subdevice through the data upstream topic so as to bind the subdevice. After the request succeeds, the platform will return the binding information of the subdevice through the data downstream topic.

Data format of the subdevice binding request:

<dx-codeblock>
:::  plaintext
{
  "type": "bind",
  "payload": {
    "devices": [
      {
        "product_id": "CFCS****G7",
        "device_name": "****ev",
        "signature": "signature",
        "random": 121213,
        "timestamp": 1589786839,
        "signmethod": "hmacsha256",
        "authtype": "psk"
      }
    ]
  }
}
:::
</dx-codeblock>

Request parameter description:

| Parameter | Type | Description |
| :-------------- | :----: | :----------------------------------------- |
| type | String | Gateway message type. For subdevice binding, the value is `bind` |
| payload.devices | Array | List of subdevices to be bound |
| product_id | String | Subdevice product ID |
| device_name | String | Subdevice name |
| signature | String | Signature string for subdevice binding. Signature algorithm: <br>1. Concatenate the product ID, device name, random number, and timestamp into the string to sign: `text=${product_id}${device_name};${random};${expiration_time}` <br>2. Use the PSK of the device or the SHA1 digest of the certificate to sign: `sign = hmac_sha1(device_secret, text)`
| random| Int | Random number |
|timestamp|Int| Timestamp in seconds |
|signmethod|String| Signature algorithm. `hmacsha1` and `hmacsha256` are supported |
|authtype |String| Signature type. <li>psk: uses device PSK to sign <li>certificate: uses device public key certificate to sign |


Data format of the subdevice binding response:

<dx-codeblock>
:::  plaintext
{
  "type": "bind",
  "payload": {
    "devices": [
      {
        "product_id": "CFCS****G7",
        "device_name": "****ev",
        "result": -1
      }
    ]
  }
}
:::
</dx-codeblock>

Response parameter description:

| Parameter | Type | Description |
| :-------------- | :----: | :----------------------------------------- |
| type | String | Gateway message type. For subdevice binding, the value is `bind` |
| payload.devices | Array | List of subdevices to be bound |
| product_id | String | Subdevice product ID |
| device_name | String | Subdevice name |
| result | Int | Subdevice binding result. For specific error codes, please see the table below |

### Unbinding device

The gateway device can request to unbind its topological relationship with the subdevice through the data upstream topic. After the request succeeds, the platform will return the unbinding information of the subdevice through the data downstream topic.

Data format of the subdevice unbinding request:
<dx-codeblock>
:::  plaintext
{
  "type": "unbind",
  "payload": {
    "devices": [
      {
        "product_id": "CFCS****G7",
        "device_name": "****ev"
      }
    ]
  }
}
:::
</dx-codeblock>

Request parameter description:

| Parameter | Type | Description |
| :-------------- | :----: | :------------------------------------------- |
| type | String | Gateway message type. For subdevice unbinding, the value is `unbind` |
| payload.devices | Array | List of subdevices to be unbound |
| product_id | String | Subdevice product ID |
| device_name | String | Subdevice name |

Data format of the subdevice unbinding response:
<dx-codeblock>
:::  plaintext
{
  "type": "bind",
  "payload": {
    "devices": [
      {
        "product_id": "CFCS****G7",
        "device_name": "****ev",
        "result": -1
      }
    ]
  }
}
:::
</dx-codeblock>

Response parameter description:

| Parameter | Type | Description |
| :-------------- | :----: | :------------------------------------------- |
| type | String | Gateway message type. For subdevice unbinding, the value is `unbind` |
| payload.devices | Array | List of subdevices to be unbound |
| product_id | String | Subdevice product ID |
| device_name | String | Subdevice name |
| result | Int | Subdevice binding result. For more information, please see [Error codes](#test) |


### Querying topological relationship

The gateway device can upstream a request to query the topological relationship of the subdevice through this topic.
Data upstream topic: `$gateway/operation/${productid}/${devicename}`
Data downstream topic: `$gateway/operation/result/${productid}/${devicename}`

Data format of the subdevice topological relationship query request:
<dx-codeblock>
:::  plaintext
{
    "type": "describe_sub_devices"
}
:::
</dx-codeblock>


Request parameter description:

| Parameter | Type | Description |
| :--- | :----: | :--------------------------------------------------------- |
| type | String | Gateway message type. For subdevice query, the value is `describe_sub_devices` |

Data format of the subdevice topological relationship query response:

<dx-codeblock>
:::  plaintext
{
  "type": "describe_sub_devices",
  "payload": {
    "devices": [
      {
        "product_id": "XKFA****LX",
        "device_name": "2OGDy7Ws8mG****YUe"
      },
      {
        "product_id": "XKFA****LX",
        "device_name": "5gcEHg3Yuvm****2p8"
      },
      {
        "product_id": "XKFA****LX",
        "device_name": "hmIjq0gEFcf****F5X"
      },
      {
        "product_id": "XKFA****LX",
        "device_name": "x9pVpmdRmET****mkM"
      },
      {
        "product_id": "XKFA****LX",
        "device_name": "zmHv6o6n4G3****Bgh"
      }
    ]
  }
}
:::
</dx-codeblock>


Response parameter description:

| Parameter | Type | Description |
| :-------------- | :----: | :--------------------------------------------------------- |
| type | String | Gateway message type. For subdevice query, the value is `describe_sub_devices` |
| payload.devices | Array | List of subdevices bound to the gateway |
| product_id | String | Subdevice product ID |
| device_name | String | Subdevice name |



### Changing topological relationship

The gateway device can subscribe to the topological relationship changes of the subdevice on the platform through this topic.
Data downstream topic: `$gateway/operation/result/${productid}/${devicename}`

When the subdevice is bound or unbound, the gateway will receive the change in the topological relationship of the subdevice. The data format is as follows:

<dx-codeblock>
:::  plaintext
{
  "type": "change",
  "payload": {
  "status": 0,  // 0: unbound, 1: bound
  "devices": [
      {
        "product_id": "CFCS****G7",
        "device_name": "****ev",
      }
    ]
  }
}
:::
</dx-codeblock>

Request parameter description:

| Parameter | Type | Description |
| :-------------- | :----: | :--------------------------------------------- |
| type | String | Gateway message type. For topological relationship change, the value is `change` |
| status | Int | Topological relationship change status. <li>0: unbound<li>1: bound |
| payload.devices | Array | List of subdevices bound to the gateway |
| product_id | String | Subdevice product ID |
| device_name | String | Subdevice name |

Data format of the gateway response:

<dx-codeblock>
:::  plaintext
{
  "type": "change",
  "result": 0
}
:::
</dx-codeblock>

Response parameter description:

| Parameter | Type | Description |
| :----- | :----: | :--------------------------------------------- |
| type | String | Gateway message type. For topological relationship change, the value is `change` |
| result | Int | Gateway response processing result |

### [Error codes](id:test)

| Error Code | Description |
| ------ | -------------------------------- |
| 0 | Success |
| -1 | The gateway device is not bound to the subdevice |
| -2 | System error. Subdevice connection or disconnection failed |
| 801 | Request parameter error |
| 802 | The device name is invalid, or the device does not exist |
| 803 | Signature verification failed |
| 804 | The signature algorithm is not supported |
| 805 | The signature request has expired |
| 806 | This device has already been bound |
| 807 | Non-general devices cannot be bound |
| 808 | Forbidden operation |
| 809 | Duplicate binding |
| 810 | Unsupported subdevice |



