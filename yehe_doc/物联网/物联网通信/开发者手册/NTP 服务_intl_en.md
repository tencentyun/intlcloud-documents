## Feature Overview

The NTP feature is mainly used to solve the problem with resource-constrained devices where they don't have the NTP service and thus have no accurate timestamps. The following two topics are required for this feature:
- Request topic (for publishing): `$sys/operation/${ProductId}/${DeviceName}`.
- Response topic (for subscribing): `$sys/operation/result/${ProductId}/${DeviceName}`.

## How It Works

The IoT Hub platform draws on the principles of the NTP protocol and uses the platform itself as an NTP server. After a device requests the platform, the platform will return the NTP time. After the device receives the response, it will calculate the current accurate time based on the request time and receipt time.

### Directions
1. The device sends a message in JSON format with the following content to `$sys/operation/${ProductId}/${DeviceName}` to request the platform for the NTP time and records the request time `deviceSendtime`:
```json
{
		 "type": "get",
		 "resource": [
		  "time"
		 ]
}
```
2. The platform returns the NTP time through `$sys/operation/result/${ProductId}/${DeviceName}` with a message in JSON format with the following content, and the device records the receipt time `deviceRecvtime`:
```
{
		 "type": "get",
		 "time": 1621562342,
		 "ntptime1": 1621562342773,
		 "ntptime2": 1621562342773
}
```
3. The accurate time is calculated through the NTP time (${ntptime1} + ${ntptime2}) received by the device, receipt time (${deviceRecvtime}), and request time (${deviceSendtime}) as follows:
**Accurate time =(${ntptime1} + ${ntptime2} + ${deviceRecvtime} - ${deviceSendtime}) / 2**

