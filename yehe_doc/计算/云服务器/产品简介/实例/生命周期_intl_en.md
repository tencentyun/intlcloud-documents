The lifecycle of a Tencent Cloud CVM instance refers to all statuses from the launch of the instance to its release. Properly managing the CVM instance in different statuses can ensure that applications running on the instance provide services economically and efficiently.

Instance Status

- **An instance has the following statuses:**
	<table>
	<tr><th>Status Name</th><th>Status Attributes</th><th>Description</th></tr>
	<tr><td>Creating</td><td>Intermediate status</td><td>The instance has been created but is not running yet.</td></tr>
	<tr><td>Running</td><td>Steady status</td><td>The instance is running normally, and you can run your services on this instance.</td></tr>
	<tr><td>Restarting</td><td>Intermediate status</td><td>A restart operation has been performed for the instance via the console or APIs, but the instance is not running yet. If this status lasts for a long time, there may be an exception.</td></tr>
	<tr><td>Reinstalling</td><td>Intermediate status</td><td>The instance's system has been reinstalled or its disk has been reconfigured via the console or APIs, but the instance is not running yet.</td></tr>
	<tr><td>Shutting Down</td><td>Intermediate status</td><td>A shutdown operation has been performed for the instance via the console or APIs, but the instance has not been shut down yet. If this status lasts for a long time, there may be an exception. We do not recommend forced shutdown.</td></tr>
	<tr><td>Shutdown</td><td>Steady status</td><td>The instance has been shut down normally and cannot provide external services. Some instance attributes can only be modified when the instance is in shutdown status.</td></tr>
	<tr><td>Terminating</td><td>Intermediate status</td><td>The instance has expired for 7 days or the user has performed the termination operation, but it has not completed yet.</td></tr>
	<tr><td>Reclaimed</td><td>Steady status</td><td>A pay-as-you-go instance has been manually terminated for less than 2 hours and put into the recycle bin. In this status, the instance does not provide external services.</td></tr>
	<tr><td>Released</td><td>Steady status</td><td>The release operation has been completed. The original instance no longer exists, cannot provide services, and its data is completely cleared.</td></tr>
</table>
- **Instance Status Transition:**
![](https://main.qcloudimg.com/raw/2de51f523cc5592c5daeecf179945cfe.jpg)

## Launching an instance
 - After an instance is launched, it goes to the "Creating" status. For an instance in this status, its hardware specifications will be configured according to the specified [instance type](https://intl.cloud.tencent.com/document/product/213/11518), and the system will launch the instance using the image specified at launch.
 - An instance goes to "Running" status after it is created. An instance in the running status can be connected to and accessed normally.

For more information about instance startup, see [Creating an Instance](https://intl.cloud.tencent.com/document/product/213/4855), [Logging In to a Windows Instance](https://intl.cloud.tencent.com/document/product/213/5435), and [Logging In to a Linux instance](https://intl.cloud.tencent.com/document/product/213/5436).

## Restarting an instance
We recommend you restart an instance via the Tencent Cloud Console or Tencent Cloud APIs instead of running the OS restart command in the instance.
 - After the restart operation is performed, the instance will enter the restarting status.
 - Restarting an instance is like restarting a computer. After restarted, the instance will retain its public IP address, private IP address and all data on its disk.
 - Depending on its configuration, restarting the instance normally takes dozens of seconds to several minutes.

For more information about how to restart an instance, see [Restarting Instances](https://intl.cloud.tencent.com/document/product/213/4928).

## Shutting down an instance
You can shut down the instance in the console or by using APIs.
 - Shutting down an instance is like shutting down a computer.
 - A shutdown instance no longer provides services, but the billing of the instance continues.
 - A shutdown instance is still visible in the console.
 - You need to shutdown an instance for some operations, such as adjusting hardware configurations and resetting the password.
 - The shutdown operation does not change the CVM's public IP, private IP, or any data on its disks.
 
For more information about shutting down an instance, see [Shutting Down Instances](https://intl.cloud.tencent.com/document/product/213/4929).

## Terminating and releasing an instance
If you no longer need an instance, you can terminate and release it in the console or by using APIs.

- Manual termination: Pay-as-you-go instances are released after being moved to the recycle bin for two hours.
- Auto termination due to expiry or overdue payment: Pay-as-you-go instances will be automatically terminated when the account balance drops below 0 for 2 hours and 15 days. Billing will continue for the first 2 hours, then the instance will shut down and no longer be billed. The overdue pay-as-you-go instance will not enter the recycle bin and can be viewed on the instance list. You can continue to use the instance if you renew it within the specified time.

When an instance is terminated, its system disk and data disks specified at purchase will be released. However, cloud disks attached to the instance will not be affected.
For more information on terminating an instance, see [Terminating Instances](https://intl.cloud.tencent.com/document/product/213/4930).
