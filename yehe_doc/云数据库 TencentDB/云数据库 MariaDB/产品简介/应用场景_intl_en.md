## Cloud-based Data Disaster Recovery (Remote Disaster Recovery)
Data is an important part of enterprise operations. Although the information technology brings convenience, it also reveals that electronic data and stored information are very vulnerable to damage or loss. Any incident, such as natural disaster, system failure, faulty operation, or virus, can cause complete interruption of business operations or even disastrous loss. Therefore, ensuring security and integrity of data, especially that in core databases, is a top priority of every enterprise.

Self-built data centers for off-site disaster recovery are usually expensive, as a great amount of hardware and software resources are required and continuous maintenance incurs high OPS expenses. Paying for incidents with small probability is certainly not in line with the principle of company operations.

TencentDB and Tencent Cloud's access products can be used to establish a data disaster recovery center directly in the cloud, which can sync data in the master IDC to the remote in-cloud backup center in real time over the secure private network. This scheme not only solves the problems of managing massive amounts of data, but also is highly cost-effective.
 

## Business System Cloudification
If your business system has not been migrated to cloud, you may encounter the following issues:
- Your business grows fast, but high costs will be incurred if you prepare servers every year based on the annual peak traffic.
- New business departments often need to launch new businesses quickly to ensure timeliness. If resource preparation and procurement are required every time, the launch efficiency will be affected.
- Almost every business system has experienced shortage of backend resources due to traffic surges.
- Many company leaders think that the IT department is a cost center and should focus on solving problems such as unstable systems or insufficient performance rather than promoting businesses.

- Backed by Tencent Cloud's many years of experience, TencentDB provides the following services and resources in face of the challenges above:
- Secure and open database solution.
- Highly available scheme that adopts strong sync replication and high availability (HA) architecture to implement high-performance disaster recovery.
- Auto scaling.

## Hybrid Cloud
TencentDB for MariaDB supports private cloud deployment in your own data center. Your business systems and data will be synced securely over Direct Connect (or VPN) to implement an easily scalable hybrid cloud architecture.

## Read/write Separation
By default, all slave TencentDB instances support read/write separation, i.e., read-only slave nodes.
- Read-only access can be implemented through SQL syntax or read-only account.
- If your configuration has multiple slaves, the load of read-only policy will be automatically distributed across the slaves.
- You can add more slaves by upgrading the specification.

## Development and Testing
You may need to maintain multiple testing environments for different software versions and even high amounts of resources for stress testing.

The traditional solution is to self-build servers and databases to this end. However, this will waste a lot of hardware resources as developers will not use testing resources all the time, causing the resources often to be idle. In contrast, with the auto scaling capability of CVM and TencentDB, you can effectively address the problems of insufficient or wasted testing resources.
