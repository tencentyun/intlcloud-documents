### Feature Overview

A gateway device can connect and disconnect subdevices under it through the data communication with the cloud. This feature uses the same topics as those used in gateway subdevice topology management:
- Data upstream topic (for publishing): `$gateway/operation/${productid}/${devicename}`
- Data downstream topic (for subscribing): `$gateway/operation/result/${productid}/${devicename}`

### Proxied subdevice connection

The gateway device can connect the subdevice to the platform through the data upstream topic. After the request succeeds, the platform will return the connection information of the subdevice through the data downstream topic.

Data format of the proxied subdevice connection request:

```plaintext
{
  "type": "online",
  "payload": {
    "devices": [
      {
        "product_id": "CFCSQ5EAG7",
        "device_name": "onlinedev00"
      }
    ]
  }
}
```

Data format of the proxied subdevice connection response:

```plaintext
{
  "type": "online",
  "payload": {
    "devices": [
      {
        "product_id": "CFCSQ5EAG7",
        "device_name": "onlinedev00",
		"result":0
      }
    ]
  }
}
```

Request parameter description:

| Parameter | Type | Description |
| :-------------- | :----: | :----------------------------------------------- |
| type | String | Gateway message type. For proxied subdevice connection, the value is `online` |
| payload.devices | Array | List of subdevices to be connected |
| product_id | String | Subdevice product ID |
| device_name | String | Subdevice name |

Response parameter description:

| Parameter | Type | Description |
| :-------------- | :----: | :----------------------------------------------- |
| type | String | Gateway message type. For proxied subdevice connection, the value is `online` |
| payload.devices | Array | List of subdevices to be connected |
| product_id | String | Subdevice product ID |
| device_name | String | Subdevice name |
| result | Int | Subdevice connection result. For specific error codes, please see the table below |

### Proxied subdevice disconnection

The gateway device can disconnect the subdevice from the platform through the data upstream topic. After the request succeeds, the platform will return the disconnection success information of the subdevice through the data downstream topic.

Data format of the proxied subdevice disconnection request:

```plaintext
{
  "type": "offline",
  "payload": {
    "devices": [
      {
        "product_id": "CFCSQ5EAG7",
        "device_name": "offlinedev00"
      }
    ]
  }
}
```

Data format of the proxied subdevice disconnection response:

```plaintext
{
  "type": "offline",
  "payload": {
    "devices": [
      {
        "product_id": "CFCSQ5EAG7",
        "device_name": "offlinedev00",
		"result":-1
      }
    ]
  }
}
```

Request parameter description:

| Parameter | Type | Description |
| :-------------- | :----: | :------------------------------------------------ |
| type | String | Gateway message type. For proxied subdevice disconnection, the value is `offline` |
| payload.devices | Array | List of proxied subdevices to be disconnected |
| product_id | String | Subdevice product ID |
| device_name | String | Subdevice name |

Response parameter description:

| Parameter | Type | Description |
| :-------------- | :----: | :------------------------------------------------ |
| type | String | Gateway message type. For proxied subdevice disconnection, the value is `offline` |
| payload.devices | Array | List of proxied subdevices to be disconnected |
| product_id | String | Subdevice product ID |
| device_name | String | Subdevice name |
| result | Int | Subdevice disconnection result. For specific error codes, please see the table below |



### Error codes

| Error Code | Description |
| ------ | -------------------------------- |
| 0 | Success |
| -1 | The gateway device is not bound to the subdevice |
| -2 | System error. Subdevice connection or disconnection failed |
| 801 | Request parameter error |
| 802 | The device name is invalid, or the device does not exist |
| 810 | Unsupported subdevice |


