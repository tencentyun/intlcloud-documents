Maintenance Task is designed to provide users with standardized CVM troubleshooting and authorized maintenance services.

To improve the running performance and stability of instances, and ensure the safe and efficient operation of the underlying platform, we regularly maintain and upgrade the underlying host and platform architecture without CVM shutdown. During the upgrade and maintenance, your CVM instances can operate stably without the need to interrupt the business applications.

Maintenance Task helps users learn and handle all kinds of issues of CVM instances in real time, prevent potential downtime risks in advance, improve maintenance efficiency and reduce maintenance costs. You can back up data of abnormal instances to ensure stable operation of your business. Also, you can configure preset authorization policies or use APIs as needed for automatic Ops of CVM failures and risks.

## Advantages

#### Free enablement

Maintenance Task is now fully available for free. After you create and use a CVM instance, you can go to [Task List](https://console.cloud.tencent.com/cvm/repair/list) to check all maintenance task records of your CVM instances.

#### Full coverage of exceptions and risks

All kinds of sudden exceptions (such as sudden abnormal downtime of underlying host, causing the CVM to abnormally restart), running risks (predict the risks of various software and hardware failures of the underlying host), disk exceptions/warnings (instance disk usage exceptions/ early warnings) and scheduled maintenance and upgrade tasks are covered.

#### Elastic configuration

Multiple preset authorization policies can be configured based on your own business scenarios and Ops requirements. Each policy can be associated with different instance families, and can be quickly bound through CVM tags.

#### Flexible authorization

Users can authorize for maintenance through the Maintenance Task console, preset authorization policies and APIs.

## Use Cases

#### Real-time awareness of instance exceptions and quick recovery

Users are notified with all kinds of CVM instance exceptions. Corresponding maintenance tasks are created. You can log in to the Maintenance Task console to check the recovery of the affected instances and avoid risks in time.

#### Real-time monitoring of risks on instances and avoid in advance

When the CVM instances are currently running normally, but the platform detects that there are software and hardware risks on the underlying host, or there are maintenance tasks planned by the platform for the CVM instances, users can receive relevant information in real time, make maintenance plans, and authorize for maintenance during low-peak business periods to avoid failures in advance and eliminate potential downtime risks.

#### Automatic Ops for CVM exceptions

Users can authorize for automatic Ops through preset authorization policies and APIs. When a new maintenance task or alarm event is triggered, the failure can be healed with automatic Ops to improve Ops efficiency.

## Use Limits

Maintenance Task is currently applicable to CVMs, CDHs and CPMs.
