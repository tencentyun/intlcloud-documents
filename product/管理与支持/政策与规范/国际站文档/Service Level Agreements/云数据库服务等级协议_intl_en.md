## 1.  General

(1) Tencent Cloud database service (the "**Service**") is the public cloud database service provided by Tencent Cloud based on relational database, distributed database, time series database, document database, etc. to meet different needs of various products including websites and applications. This agreement applies only to master - slave (master - backup) instances.

(2) This Tencent Cloud Database Service Level Agreement (SLA) is supplemental to the Tencent Cloud Service Agreement and the Tencent Cloud Privacy Policy.

(3) Tencent Cloud has the right to amend its terms of service at any time and will announce such amendment via a notice on its website, an email notice or a text message notice, without obtaining additional consent of you.

(4) Unless otherwise specifically stipulated herein, for the purpose of this agreement, a "month" equals to thirty (30) calendar days which shall commence on the date when the Service is activated.

## 2.  Service Guarantee Metrics

2.1  Service Availability

(1) Tencent Cloud guarantees that the availability of the Service will be no lower than 99.95%, which means that the available time of the Service in a month for your instances would be no less than 43,178.4 minutes (= 30 (day) × 24 (hour) × 60 (minute) × 99.95%), provided that the Service within a month may be unavailable for 21.6 minutes (= 43,200 minutes -- 43,178.4 minutes).

(2) The Service downtime due to any of the following reasons will not be counted into the Service downtime:

- any scheduled downtime due to any system maintenance with prior notice by Tencent Cloud, including system cutover, upgrade and malfunction simulation test.

- any malfunction or configuration adjustment of any network or equipment that is not Tencent Cloud facility.

- any Service unavailability attributable to any person other than Tencent Cloud, such as hacker attack or negligence of your third-party supplier.

- any slow or no responding of any cloud database instance under ultra-high performance pressure; or duration of log re-do or recovery practices.

- any loss or leak of data, passcode or password due to your improper maintenance or improper confidentiality measures.

- any mal-operation due to your negligence, or any operation authorized by you.

- any event of force majeure.

2.2  Data Deletion

Upon your request or prior to disposal or resale of a device, Tencent Cloud will perform low level formatting of disks to completely and irrecoverably delete all your data, and the disks will be demagnetized when they are discarded.

Upon destruction of a database, no data therein can be recovered.

2.3  Data Migration

Tencent Cloud will provide data in a standard database file format to enable you to save such data as a standard "sql" file by import/export tools, by means of which you may transfer such data into a cloud database or export such data onto your own server.

2.4  Data Confidentiality

Tencent Cloud adopts reasonable technical measures, including without limitation network isolation and access control, to ensure the isolation and invisibility of data and resources of different users.

2.5  Right to Know

(1) The location of data center where data is stored (users may query this by submitting a ticket).

(2) The number of data backups and the location of data center where the backup data is stored (users may query this by submitting a ticket).

(3) Tencent Cloud will assist you in choosing a data center with proper network conditions for data storage, and data backup will be allocated dynamically according to the utilization of resources. You, by default, is not required to choose a data center and a cold backup center. If you intend to choose a data center and/or a cold backup center, you may query this by submitting a ticket.

(4) The local laws and relevant laws of the People's Republic of China that a data center shall comply with.

(5) None of your data will be provided to any third party unless required by a government regulatory authority for regulation or audit purposes. The database instance behavior log will be used for data analysis of the database operation, but no user data will be presented externally.

2.6  Data Audit

Tencent Cloud may, in accordance with the current laws and regulations, and provided that the relevant procedural and formality requirements are fully compliant, disclose certain information, including without limitation operation log of key components, operation records of operation and maintenance personnel and operation records of users, for the purposes of cooperating with supervision and administration, evidence collection and investigations of governmental or regulatory authorities or otherwise.

2.7  Malfunction Recovery Capacity

Tencent Cloud database has failover capacity by default, which means that automatic failover will be triggered, without any action of a user, when any malfunction of a master server occurs, thus ensuring the continuity of the Service provided to you. You may submit a ticket or call customer service for support when necessary.

2.8  Due and Late Payments

With respect to database instances with payments to be settled on a pre-pay basis (annual or monthly plan), Tencent Cloud will provide you with a 7-day service period upon expiry of the term of the database, and will then terminate the Service upon expiry of such 7-day period. You should bear all cloud service fees (if any) incurred during such 7-day period, settle all your payments prior to the expiry of the 7-day period and complete the migration of all your data. Tencent Cloud database system will automatically delete all your data fourteen (14) days following such expiry or termination.

With respect to database instances with payments to be settled on a post-pay basis (pay-per-use), Tencent Cloud will provide you with a 2-hour service period when any payment of your account is overdue and will then terminate the Service upon expiry of such 2-hour period. You should bear all cloud service fees (if any) incurred during such 2-hour period and should timely top up your account to ensure the balance remains more than RMB0. Tencent Cloud database system will automatically delete all your data when the balance of your account remains less than RMB0 for twenty-four (24) hours.

## 3.  Service Compensation

3.1  Scope

If a user is not able to use Tencent Cloud database in a regular way or is completely unable to access the database due to any malfunction attributable to Tencent Cloud, the user has the right to require Tencent Cloud to compensate for such incident/malfunction. The application for such compensation must be submitted within three (3) months following the month for which the availability of the underlying Tencent Cloud database instance fails to meet the relevant standard, and any application submitted thereafter will not be accepted by Tencent Cloud.

3.2 Standards for Compensation

Duration of malfunction = the time when the malfunction is fixed-- the time when the malfunction starts. The duration of malfunction will be calculated in minutes. Where the duration of malfunction, or an unrounded portion thereof, is less than 1 minute, it will be rounded up to 1 minute. For example, if the duration of malfunction is 1 minute and 1 second, it will be calculated as 2 minutes.

One hundred times compensation for Tencent Cloud database malfunction:

(1) Pre-pay: the compensation will be made by extending the use period of the failed database, extended time = duration of malfunction × 100.

(2) Post-pay: the compensation will be made in the form of voucher, the amount of voucher = daily fee of the failed database / 24 / 60 × duration of malfunction × 100.
