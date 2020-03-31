>The following statement is hereby made for this document.
>
>1. This document is intended to provide an overview of Tencent Cloud's security measures for TencentDB products and services, which are subject to change. If you have any mandatory requirement, you are recommended to enter into a service level agreement (SLA) with Tencent Cloud. Tencent Cloud makes no guarantees or warranties, express or implied, about the content of this document.
> 2. This document only involves "part of" the technical security features among the wide range of security features.
> 3. This document is not intended as a reference document for national or industry-specific information security standards or requirements.
> 4. This document has been adapted for readability. In the event of any ambiguity or inaccuracy, please refer to Item 1.
> 5. Tencent Cloud reserves the right to interpret this document.

## 1. Overview
TencentDB has passed and meets the security requirements of the following certifications:
- ISO22301 Certification
- ISO27001 Certification
- ISO20000 Certification
- ISO9001 Certification
- Trusted Cloud Service Certification
- Cybersecurity Classified Protection Certification (Level 3)
- STAR Certification

Some features of TencentDB are designed based on the following standards:

- GBT 20273-2006 Information Security Technology - Security Techniques Requirement for Database Management System (Level 2 or Above)
- JRT 0072-2012 Testing and Evaluation Guide for Classified Protection of Information System of Financial Industry (Level 4)

## 2. Tencent Cloud TencentDB Service Security Protection (OPS Security Description)
### 2.1. Overview
Management and technical security requirements of TencentDB comply with China's Cybersecurity Classified Protection (Level 3). Some of the product features meet the standards of Classified Protection of Information System of Financial Industry (Level 4).


### 2.2. Internal personnel and system authentication

To improve the security of database server system and ensure the security of various OPS activities, Tencent Cloud has implemented a series of security reinforcement measures, including but not limited to:
- Tencent Cloud carries out identification and authentication for users who log in to the operating system and database system, and guarantees the uniqueness of usernames.
- Usernames and passwords must be configured as required. A password must contain at least 8 characters of 3 types and should be changed regularly.
- The login failure processing mechanism can be enabled to take actions such as ending session, limiting the number of unauthorized login attempts, and automatically exiting in case of login failures.
- Access to the system during remote management is under monitoring by Tencent Enterprise IT, and internal risk management and audit are provided, with all sensitive operations encrypted.
- Two-factor authentication (dynamic token and password) is required for database server admins when they log in to the OPS system.

### 2.3. Internal personnel and system access control
For TencentDB management systems and admins, a discretionary access control scheme is implemented, including but not limited to:
- Internal OPS staff and systems are controlled based on Tencent Cloud security policies (audit requirements are met).
- The granularity of a subject is down to user level, and that of an object to database table level.
- Strict code management and access control are implemented.
- High-risk systems can only be accessed over Tencent private network (development network), which is physically isolated from the internet.


### 2.4. Internal security audit
A comprehensive security audit and risk management mechanism is provided: audit features include but are not limited to audit for database operations, management system operations, file operations, external device operations, unauthorized external connections, IP address changes, and services and processes. The audit range covers each operating system user and database user in the server, with crucial security-related system events audited, such as Tencent Cloud admin behaviors, exceptional system resource usage, and use of important system commands. Audit records contain information like event date, time, type, subject ID, object ID, and result, and can be stored for over a year in a location with a higher level of security in order to avoid unexpected deletion, modification, or overwriting.

- Database security audit: all operations on the database servers and databases will be audited by the database security audit system.
- Management system operation audit: Tencent Cloud keeps detailed logs of all operations in both internal and external management systems for effective risk traceability.
- Routine risk assessment: Tencent Cloud security team performs security assessment on database OPS management on a regular basis.


### 2.5. Internal intrusion prevention
Tencent Cloud takes multi-dimensional approaches to intrusion prevention for database servers:

- The intrusion detection system can defend against intrusions into database servers.
- Vulnerability scanning is deployed, and system security inspection is performed periodically.
- The device security management system is deployed, and the patch distributing module is enabled to update systems with patches timely.
- The operating system is installed on a minimal installation basis, with only necessary components and applications installed and unwanted services disabled.
- Reinforcement is implemented on other security configurations based on system type.

### 2.6. Backup and restore
TencentDB provides data backup and restore features by default. 

### 2.7. Secure reuse of objects
For returned or replaced devices, Tencent Cloud will clear the residual information promptly, so that the storage capacity (memory and disk) where the previous user's sensitive information such as authentication information, files, directories, and database records is stored will be released in time or completely cleared before the devices are reassigned to other users.

### 2.8. Non-repudiation
Tencent Cloud's internal OPS personnel are required to go through a two-factor authentication and non-repudiation process when logging in to the system. All the personnel involved have signed a NDA.


