During product use, some operations may not be instantly completed. The result polling feature allows you to periodically check if an operation is completed. For example, after an instance is activated, it may not immediately enter the `RUNNING` state. In this case, you can use polling to check its status until it enters the `RUNNING` state.

## Directions
- Run the following command to initiate a polling program that checks the instance status at a specific interval. The program runs until the instance enters the `RUNNING` state or until the polling times out.
```bash
tccli cvm DescribeInstancesStatus --region ap-hongkong --waiter "{'expr':'InstanceStatusSet[0].InstanceState','to':'RUNNING'}"
```
- You can specify a timeout period and an interval for polling. Run the following command to set the timeout period to 180s and the interval to 5s.
```bash
tccli cvm DescribeInstancesStatus --region ap-hongkong --waiter "{'expr':'InstanceStatusSet[0].InstanceState','to':'RUNNING','timeout':180,'interval':5}"
```
- You can set the values of optional subparameters in the configuration file. Add the following configuration to the `default.configure` file to specify a timeout period of 180s and an interval of 5s.
```
"waiter": {
		"interval": 5,
		"timeout": 180
	},
```

## Parameter description
 - **--region**: Set this parameter to the region where your instance is located.
 - **--waiter**: Parameters after `waiter` must be in JSON format and enclosed in double quotation marks. The table below lists the required and optional parameters:
 <table>
 <tr>
 <th>Parameter</th> <th>Required</th> <th>Description</th>
 </tr>
 <tr>
	<td>expr</td>
	<td>Yes</td>
	<td>The field that you want to query. Use <a href="http://jmespath.org/">JMESPath</a> to query the value of the specified field.</td>
 </tr>
 <tr>
	<td>to</td>
	<td>Yes</td>
	<td>The target value of the field that you want to query.</td>
 </tr>
 <tr>
	<td>timeout</td>
	<td>No</td>
	<td>The timeout period for polling in seconds.</td>
 </tr>
 <tr>
	<td>interval</td>
	<td>No</td>
	<td>The polling interval in seconds.</td>
 </tr>
 </table>
