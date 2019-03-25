
1. Definition of Service
TencentDB for MongoDB is a high-performance distributed data storage service created by Tencent Cloud based on MongoDB, the world's most promising open source NoSQL database. It is fully compatible with MongoDB protocols, and applicable to non-relational database-oriented scenarios.
TencentDB for MongoDB also provides a high-performance, highly reliable, easy-to-use MongoDB cluster service. Each instance is at least a "1 master, 2 slaves" replica set or a sharding cluster that contains multiple replica sets, thus ensuring high availability of user data.

2. Data Persistence
During the period of service (the purchased usage period of a MongoDB instance), we guarantee a 99.9996% persistency for the data stored in the instances applied by users each month. That is, for each month, if a user stored 1m files in the instances, only 4 files are possibly lost.

3. Destroyable Data
Data needs to be destroyed when you actively deletes data or the service expires. After you deletes any data or before you discard or resell any device, Tencent Cloud completely deletes all your data by performing a low-level formatting on the disk. The deleted data cannot be recovered and the disk is demagnetized when it is due for scrap.

4. Right to Know
A. The location of an IDC where the data is stored. You can make an inquiry about this by submitting a ticket.
B. The number of data backups and the location of an IDC where the backup data is stored. You can make an inquiry about this by submitting a ticket.
C. Tencent Cloud will help you select the IDC that is most suitable for your network environment to store data. Cold backup will be dynamically allocated according to resource usage. By default, you don't need to choose the locations of the IDC and cold backup center. If you need to do so, you can make an inquiry about this by submitting a ticket.
D. IDCs shall comply with local laws and regulations and applicable laws and regulations of the PRC. (You can make an inquiry about this by submitting a ticket).
E. Any of your data is not disclosed to any third party, unless required by regulatory authorities for supervision and auditing purposes. Your behavior logs are used for data analysis for keeping track of database status, but not used to disclose any of your personal information to any third party.

5. Data Privacy
Tencent Cloud achieves network isolation by configuring firewall policy and using whitelist filtering mechanism, and ensures your data is not visible to any other users within the same resource pool by using permission control mechanism based on the user name and password for MongoDB instances.

6. Data Auditing
In accordance with the applicable laws and regulations and on condition of compliance with relevant process and availability of all necessary documents, Tencent Cloud may disclose information regarding databases, including operation logs of key components, operation records of OPS personnel and operation records of users, if required by regulatory authorities or if it is necessary to do so for other reasons such as collection of evidences during investigation into security incidents.

7. Service Availability
A. We guarantee a 99.95% business availability for TencentDB for MongoDB, which means the service should be available for users for at least 99.95% of the time, or 30(day)*24(hr)*60(min)*99.95%=43,178.4 minutes, and be unavailable for 43,200-43,178.4=21.6 minutes at most each month. The statistics of service unavailability is calculated based on a single user database instance.
B. The unavailability duration does not include daily maintenance duration of the system and unavailability duration caused by any user, third party or other force majeure.

8. Failure Recovery Capability
Tencent Cloud's professional team provides maintenance support on a 24/7 basis.

