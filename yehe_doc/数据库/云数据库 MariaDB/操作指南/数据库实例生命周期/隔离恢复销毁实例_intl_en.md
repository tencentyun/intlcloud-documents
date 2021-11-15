>Currently, only database instances assigned in a dedicated cluster support active isolation and termination.

Isolation, termination, and recovery are necessary operations in managing instances. You should note that these operations may affect the business system stability and data reliability; therefore, please perform them with caution. To avoid faulty operations, all instances support isolation before termination, and only isolated instances (no matter whether they contain data) can be terminated.

## Isolating an Instance
Once isolated, an instance cannot be used or accessed; however, it is not terminated or deleted. You can terminate or recover it. After isolation, resource capacity will not be released, and the most basic data replicas will be retained.
>
>- After an instance is isolated, its IP will be released, and you may not get back the original IP after the instance is recovered.
>- After an instance is isolated, you cannot upgrade it, modify its parameters, create or modify an account for it, roll it back, add sets to it, or rename it.
>- If you do not actively terminate an isolated instance, it will not be automatically terminated.

## Recovering an Instance
Instance recovery is to recover an isolated instance to its normal running status. The recovery may take several minutes to complete. In addition, the recovered instance may have a new IP rather than the original IP before isolation.

## Terminating an Instance
All isolated instances can be terminated. Terminating an instance will permanently delete all its data; therefore, please do so with caution.

To prevent you from deleting data by mistake and causing irreversible risks due to data loss, the termination operation on instances applied for in a dedicated cluster will be delayed for 24 hours by default. In other words, after an instance is deleted, release of its capacity in the dedicated cluster will happen after 24 hours. If you need to release the capacity as soon as possible or recover the instance before it is completely terminated, please [submit a ticket](https://console.cloud.tencent.com/workorder/category)
for assistance.
