## Remote Disaster Recovery for TencentDB Instances
DTS is capable of disaster recovery sync for TencentDB disaster recovery instances based on Direct Connect over Tencent Cloud's private network. This disaster recovery architecture enables mutual redundancy between data centers in different regions, so that when a data center fails or is out of service due to force majeure, the service can be quickly switched to another data center.
By optimizing database replication, DTS greatly reduces sync delay between master/slave databases and minimizes the risk of data loss caused by such delay in the event of disasters.
![](https://main.qcloudimg.com/raw/2566ca976edb875fdb007d9ac8073bc8.png)

## Migrating Data to the Cloud
To migrate your data to Tencent Cloud, it only takes a few steps in DTS to set up data migration with no complicated configuration required. The migration process will not interrupt the service provided by your source database, thereby minimizing the impact of cloudification on your business.
![][img2]

## Disaster Recovery for Local IDC
DTS supports data sync between your local IDC as business center and Tencent Cloud as disaster recovery center. This feature, together with out-of-the-box Tencent Cloud services, enables you to implement disaster recovery for your local IDC easily without having to invest a lot in infrastructure.
![][img3]

## Data Archiving and Storage
The data subscription feature of DTS can help you push incrementally updated data in your TencentDB instance to an archive database or data warehouse in real time through data streams.
![][img4]


[img2]: //mc.qcloudimg.com/static/img/bbe90cec1fc0882e05c441ac38089295/image.png
[img3]: //mc.qcloudimg.com/static/img/7459283867e3acbcb4bff4e5b8481d31/DTS-scenarios3.png
[img4]: //mc.qcloudimg.com/static/img/6bc58a2088159ccb0264765a4f2e922e/DTS-scenarios4.png
