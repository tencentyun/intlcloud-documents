
## 1. Overview
TencentDB for PostgreSQL has passed and meets the security requirements of the following certifications:
- ISO22301 Certification
- ISO27001 Certification
- ISO20000 Certification
- ISO9001 Certification
- Trusted Cloud Service Certification
- Cybersecurity Classified Protection Certification (Level 3)
- STAR Certification

Some features of TencentDB for PostgreSQL are designed based on the following standards:
- GBT 20273-2006 Information Security Technology - Security Techniques Requirement for Database Management System (Level 2 or Above)
- JRT 0072-2012 Testing and Evaluation Guide for Classified Protection of Information System of Financial Industry (Level 4)

## 2. TencentDB for PostgreSQL Service Security Protection
### 2.1 Overview
Management and technical security requirements of TencentDB for PostgreSQL comply with China's Cybersecurity Classified Protection (Level 3). Some of the product features meet the standards of Classified Protection of Information System of Financial Industry (Level 4).


### 2.2 Internal personnel and system authentication
To improve the security of database server system and ensure the security of various OPS activities, Tencent Cloud has implemented a series of security reinforcement measures, including but not limited to:
- Tencent Cloud carries out identification and authentication for users who log in to the operating system and database system and guarantees the uniqueness of usernames.
- Usernames and passwords must be configured as required. A password must contain at least 8 characters of 3 types and should be changed regularly.
- The login failure processing mechanism can be enabled to take actions such as ending session, limiting the number of unauthorized login attempts, and automatically exiting in case of login failures.
- Access to the system during remote management is under monitoring by Tencent Enterprise IT, and internal risk management and audit are provided, with all sensitive operations encrypted.
- Two-Factor authentication (dynamic token and password) is required for database server admins when they log in to the OPS system.

### 2.3 Internal personnel and system access control
For TencentDB management systems and admins, a discretionary access control scheme is implemented, including but not limited to:
- Internal OPS staff and systems are controlled based on Tencent Cloud security policies (audit requirements are met).
- The granularity of a subject is down to user level, and that of an object to database table level.
- Strict code management and access control are implemented.
- High-risk systems can only be accessed over Tencent private network (development network), which is physically isolated from the internet.


### 2.4 Internal security audit
A comprehensive security audit and risk management mechanism is provided: audit features include but are not limited to audit for database operations, management system operations, file operations, external device operations, unauthorized external connections, IP address changes, and services and processes. The audit range covers each operating system user and database user in the server, with crucial security-related system events audited, such as Tencent Cloud admin behaviors, exceptional system resource usage, and use of important system commands. Audit records contain information like event date, time, type, subject ID, object ID, and result, and can be stored for over a year in a location with a higher level of security in order to avoid unexpected deletion, modification, or overwriting.

- Management system operation audit: Tencent Cloud keeps detailed logs of all operations in both internal and external management systems for effective risk traceability.
- Routine risk assessment: Tencent Cloud security team performs security assessment on database OPS management on a regular basis.


### 2.5 Internal intrusion prevention
Tencent Cloud takes multi-dimensional approaches to intrusion prevention for database servers:
- The intrusion detection system can defend against intrusions into database servers.
- Vulnerability scanning is deployed, and system security inspection is performed periodically.
- The device security management system is deployed, and the patch distributing module is enabled to update systems with patches timely.
- The operating system is installed on a minimal installation basis, with only necessary components and applications installed and unwanted services disabled.
- Reinforcement is implemented on other security configurations based on system type.

### 2.6 Backup and restore
TencentDB provides data backup and restoration features by default. Full backup is performed at 1:00 AM every day and retained for 7 days (features such as automatic backup, custom backup retention period, and COS backup service will be available in the future). The xlog files will be automatically backed up when you perform operations and retained for 7 days. The backup files can be downloaded in **Backup Management** on the instance management page in the console. Full backup files are in the backup list, and xlog files required for incremental backup are in the xlog list. Data can be restored through full backup and xlog files. For more information, please see [Restoring PostgreSQL Data on CVMs](https://intl.cloud.tencent.com/document/product/409/11642).


### 2.7 Secure reuse of objects
For returned or replaced devices, Tencent Cloud will clear the residual information promptly, so that the storage capacity (memory and disk) where the previous user's sensitive information such as authentication information, files, directories, and database records is stored will be released in time or completely cleared before the devices are reassigned to other users.

### 2.8 Non-Repudiation
Tencent Cloud's internal OPS personnel are required to go through a two-factor authentication and non-repudiation process when logging in to the system. All the personnel involved have signed a NDA.

