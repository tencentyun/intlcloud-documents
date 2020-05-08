The lifecycle of a Cloud Virtual Machine (CVM) instance refers to the process of the instance from its launch to release. Proper management of CVM instances from launch to release ensures that applications running on these instances can provide services in an efficient and economic manner.

## Instance States

- **A CVM instance has the following states:**
	<table>
	<tr><th>State</th><th>Attribute</th><th>Description</th></tr>
	<tr><td>Creating</td><td>Intermediate state</td><td>It is a state prior to Running after the instance is created.</td></tr>
	<tr><td>Running</td><td>Steady state</td><td>This state indicates that the instance is running normally, and you can run your services on this instance.</td></tr>
	<tr><td>Restarting</td><td>Intermediate state</td><td>It is a state prior to Running after a restart operation is executed in the console or through an API. If the instance remains in Restarting state for a long time, an exception may have occurred.</td></tr>
	<tr><td>Resetting</td><td>Intermediate state</td><td>It is a state prior to Running after the system is reinstalled or the disk is reset through the console or an API.</td></tr>
	<tr><td>Shutting Down</td><td>Intermediate state</td><td>It is a state prior to Shut Down after a shutdown operation is executed in the console or through an API. If the instance remains in Shutting Down state for a long time, an exception may have occurred. However, forcible shutdown is not recommended.</td></tr>
	<tr><td>Shut Down</td><td>Steady state</td><td>This state indicates that the instance is shut down correctly. An instance in Shut Down state cannot provide external services. Some instance attributes can be modified only when the instance is in Shut Down state.</td></tr>
	<tr><td>Terminating</td><td>Intermediate state</td><td>It is the state when the instance has expired for 7 days or when the user manually terminates the instance, but the termination is not completed yet.</td></tr>
	<tr><td>Reclaimed</td><td>Steady state</td><td>It is the state when a pay-as-you-go instance has been manually terminated for less than 2 hours and moved into the recycle bin. In this state, the instance does not provide external services.</td></tr>
	<tr><td>Released</td><td>Steady state</td><td>This state indicates that the release operation is completed. In this state, the instance no longer exists and cannot provide services, and instance data is completely deleted.</td></tr>
</table>

- **Instance state transition**
![](https://main.qcloudimg.com/raw/1c018b2724bf142b1f3e90b97002d7a0.png)

## Instance Launch
 - After you perform the instance launch  operation, the instance enters the Creating state. In this state, hardware specifications are configured based on the specified [instance specifications](https://intl.cloud.tencent.com/document/product/213/11518). The system starts the instance by using the image specified during startup.
 - The instance enters the Running state after it is created. An instance in the Running state can be accessed normally.

For more information on instance launch, see [Creating an Instance](https://intl.cloud.tencent.com/document/product/213/4855), [Logging In to a Windows Instance](https://intl.cloud.tencent.com/document/product/213/5435), and [Logging In to a Linux Instance](https://intl.cloud.tencent.com/document/product/213/5436).

## Instance Restart
We recommend that you relaunch an instance in the Tencent Cloud Console or through Tencent Cloud APIs, instead of running the OS restart command in the instance.
 - After you perform the restart operation, the instance enters the Restarting state.
 - Restarting an instance is equivalent to restarting a computer. After the restart, the instance retains its public IP address, private IP address, and all data on the disk.
 - Normally, it takes dozens of seconds to several minutes to restart the instance, depending on the instance configuration.

For information on how to restart an instance, see [Restarting an Instance](https://intl.cloud.tencent.com/document/product/213/4928).

## Instance Shutdown
You can use the console or APIs to shut down an instance.
 - Shutting down an instance is equivalent to shutting down a computer.
 - The shut-down instance no longer provides external services, but billing continues.
 - The shut-down instance is still visible in the console.
 - Being in Shutdown state is a prerequisite for some configuration operations, such as adjusting hardware configurations and resetting passwords.
 - The shutdown operation does not change the public or private IP address of the CVM instance, or any data on its disk.
 
For information on the shutdown of an instance, see [Shutting Down an Instance](https://intl.cloud.tencent.com/document/product/213/4929).

## Instance Termination and Release
You can terminate and release an CVM instance in the console or through Tencent Cloud APIs if you no longer need it.

- Manual termination: you can manually terminate a pay-as-you-go instance that is not in arrears. A pay-as-you-go instance is released after it is kept in the recycle bin for up to 2 hours.
- Automatic termination upon expiration or in arrears: if the account balance of a pay-as-you-go instance remains below 0 for 26 hours, the instance will be automatically released. (Within these 26 hours, billing continues for the first 2 hours, and the instance is shut down and billing stops for the remaining 24 hours. If the account is in arrears, the pay-as-you-go instance is not moved to the recycle bin, but you can view this instance in the instance list.) If you pay the renewal fee within the specified period, you can continue to use the instance.

When an instance is terminated, the system disks and data disks designated for the instance when you purchase the instance are also released. However, cloud disks mounted to the instance are not affected.
For information on the termination of an instance, see [Terminating or Returning an Instance](https://intl.cloud.tencent.com/document/product/213/4930).
