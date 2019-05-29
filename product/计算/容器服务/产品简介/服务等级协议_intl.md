## 1.Terms and Definitions

### 1.1 Tencent Kubernetes Engine

Tencent Kubernetes Engine (“TKE”)means the Kubernetes cluster management services provided by Tencent Cloud to you (“Client”) via Tencent Cloud platform, including without limitation cluster management, node management and image storage management. For details, please refer to the Service purchased by you and the content of Service provided by Tencent Cloud. You may create and manage Kubernetes cluster by using the Service and deploy your container business in the cluster.

### 1.2	Service Month(s)

Service Month(s) means the calendar month(s) within the term of the Service purchased by you. For example, if you purchase the Service for a term of three months starting from March 17, there will be four (4) Service Months (the first Service Month from March 17 to March 31, the second from April 1 to April 30, the third from May 1 to May 31, and the fourth from June 1 to June 16). The availability of the Service will be calculated independently for each Service Month.

### 1.3 Service Downtime Calculated in Minutes within a Service Month

When all the attempted operation made by you within one minute via cluster management API or management penal page of the Service fail, such one minute shall count towards the Service downtime of the Service Month. When the attempted operations made by you within one minute via cluster management API or management penal page of the Service succeed in full or in part, such one minute shall not count towards the Service downtime of the Service Month, and the Service within such one minutes shall be deemed available. The sum of the unavailable minutes during a Service Month shall be the Service downtime calculated in minutes for such Service Month. 

### 1.4 Total Time of a Service Period Calculated in Minutes 

Total Time of a Service Period Calculated in Minutes = The number of days of the Service Month × 24 (hours) × 60 (minutes).

### 1.5 Directly Related Tencent Cloud Products

When using container function of the Service, Tencent Cloud products such as CVM, CLB, CBS, CFS and CLS, may be involved. The Directly Related Tencent Cloud Products means that if business abnormity is caused by TKE components, only costs for directly affected products, rather than indirectly affected products, shall be compensated, including without limitation the following:

1.	 If load balance creation is abnormal due to abnormal TKE load balance components, only relevant load balance costs will be compensated. The backend cloud server costs shall be excluded.
2.	If block storage is abnormal due to abnormal TKE block storage components, only relevant block storage costs will be compensated. The backend cloud server costs shall be excluded.
3.	If cluster node is abnormal due to abnormal TKE node management components, only relevant abnormal node costs will be compensated. The CLB, CBS and other costs shall be excluded.


## 2. Service Availability

### 2.1 Calculation of Service Availability

Service Availability = 1 - (Service Downtime Calculated in Minutes within a Service Month , Total Time of a Service Month Calculated in Minutes) × 100%

### 2.2 Standards of Service Availability

The Service Availability of the Service provided by Tencent Cloud will be no less than 99.95%. You are entitled to the compensation as set forth in Section 3 below if the Service Availability fails to meet the aforementioned standard, other than in any circumstance as provided for in the release of liabilities provisions below. 

**TKE service provide Standards of Service Availability for following product features:**

1.	Cluster Management: adding, deleting, modifying and checking clusters, opening or closing API server of cluster access of public network and private network.
2.	Node Management: adding, deleting, modifying and checking nodes (for product anomaly due to Tencent Cloud Virtual Machine, please refer to Tencent Cloud Virtual Machine Service Level Agreement).
3.	Network Storage Plugin Management: including Kubernetes components expanded from TKE, such as Elastic Network Interface, VPC, CLB, CBS (For product anomaly due to Tencent Cloud Elastic Network Interface, VPC, CLB, CBS, please refer to the service level agreement for the corresponding product).
4.	Image Storage Management: adding, deleting, modifying and checking image storage.


## 3. Compensation Plan

### 3.1 Scope of Compensation

Tencent Cloud TKE provides compensation for affected product features including without limitation the following:

1.	Cloud Virtual Machine anomaly due to TKE node management components.
2.	Anomaly in creating or using load balance due to TKE load balance components.
3.	Anomaly in creating or using block storage due to TKE block storage components.
4.	Anomaly in creating or using document storage due to TKE document storage components.
5.	Anomaly in creation or use due to TKE network management components (Gloabal Router, VPC-CNI).


> Note:The following features are beyond the scope of compensation for Standards of Service Availability of TKE.
>1.	Effect caused open source software Kubernetes, Docker and operating system kernel and other open source portions.
>2.	Effect caused by relevant Tencent Cloud products per se, e.g., failure for TKE to create CLB due to CLB interface anomaly, anomaly for TKE to create resources because the quota has been reached or the resources are sold out.

3.	Kubernetes plugins made available to the community as open source software’s by TKE.


### 3.2 Standards of Compensation

In respect of this Service, if the Service Availability fails to meet the abovementioned standard, you will be entitled to compensations in accordance with the following terms:

1.	For TKE service, Tencent Cloud only compensates for issues caused by Directly Related Tencent Cloud Products, e.g., only relevant costs of load balance will be compensated for anomaly in creating load balance components due to the TKE load balance components.

2.	Compensations will be made in the form of coupon by Tencent Cloud, and you should follow the rules for using the coupon (including the valid term; for details, please refer to the rules of coupons published on Tencent Cloud’s official website). You cannot redeem such coupon for cash or request to issue an invoice for such coupon. Such coupon can only be used to purchase the Service by using your Tencent Cloud account. You cannot use the coupon to purchase other services of Tencent Cloud, nor should you give the coupon to a third party for consideration or for free.

3.	If the Service Availability for a Service Month fails to meet the standard, the amount of compensation will be calculated for such month independently, **and the aggregate amount shall be no more than the applicable monthly service fee paid by you for such month** (the monthly service fee referred herein shall exclude the portion deducted by a coupon or promotional voucher, due to discounted service fee or otherwise deducted). 

| Service Availability for a Service Month| Value of Compensation Coupon |
|---------|---------|
|≥ 99.0% and < 99.95% | 10% of the monthly service fee for Directly Related Tencent Cloud Products |
| ≥ 98.0% and < 99.0% | 20% of the monthly service fee for Directly Related Tencent Cloud Products |
| < 98.0% | 50% of the monthly service fee for Directly Related Tencent Cloud Products |

### 3.3 Time Limit for Compensation Application

(1)	If the Service Availability for a Service Month fails to meet the abovementioned Service Availability standard, you may apply for compensation through (and only through) the support ticket system under your relevant account after the fifth (5th) business day of the month immediately following such Service Month. Tencent Cloud will verify and ascertain your application upon receipt of such application. If there is any dispute over the calculation of the Service Availability for a Service Month, both parties agree that the back-end record of Tencent Cloud will prevail.

(2)	You should apply for such compensation no later than sixty (60) calendar days following the expiry of the applicable Service Month in which the Service Availability fails to meet the standard. If you fail to make any application within such period, or make the application after such period, or make the application by any means other than that agreed herein, it shall be deemed that you have voluntarily waived your right to apply for such compensation and any other rights you may have against Tencent Cloud, in which case Tencent Cloud has the right to reject your application for compensation and not to make any compensation to you.

## 4. Release of Liabilities

**If the Service is unavailable due to any of the following reasons, the corresponding Service downtime shall not be counted towards Service unavailability period, and is not eligible for compensation by Tencent Cloud, and Tencent Cloud will not be held liable to you:**

1.	any system maintenance with prior notice by Tencent Cloud to you, including system cutover, maintenance, upgrade and failure simulation test;
2.	any failure or configuration adjustment of network or equipment that is not Tencent Cloud facility;
3.	any attack on your application interface or data, or any other misconduct;
4.	any loss or leak of data, pin or password due to your improper maintenance or improper confidentiality measures;
5.	any negligence in authorization or mal-operation by you, or any of your equipment, or third-party software or device; 
6.	any failure of you to abide by documentation or suggestions for using Tencent Cloud products;
7.	any Service unavailability or failure of the Service to meet the availability standard not attributable to Tencent Cloud.
8.	any other circumstances in which Tencent Cloud will be exempted or released from its liabilities (for compensation or otherwise) according to relevant laws, regulations, agreements or rules, or any rules or guidelines published by Tencent Cloud separately.


**Before using the TKE service, you should read carefully the relevant service description, technical specification and operation guide, etc. in official documentation of Tencent Cloud, and fully understand the relevant content and potential consequences. You understand and agree that, your use of TKE service is based on your sole independent and prudent judgement, and you shall be responsible for your own judgement or actions, including without limitation:**

1. You should decide on your own the compatibility between the Service and the operation system, database and other software and hardware you choose;
2. TKE service does not guarantee the availability of operating system and kernel defects caused by the community;
3. You shall be responsible for your own operations (e.g., health check configuration, resource limitation configuration, container image configuration, code writing and business logic setting);
4. If you use other non-free-of-charge Tencent Cloud products while using TKE service, you shall pay for such products in accordance with the corresponding pricing arrangement and observe corresponding service terms;
5. TKE service only includes relevant technical structure and components for container service, including without limitation TKE API Server, ETCD, CLB, CBS and other Kubernetes Controller components of Tencent Cloud IAAS. TKE service is only responsible for the availability of its own components. For other Tencent Cloud products such as CVM, CLB and CBS, please refer to relevant service level agreements. You shall be solely responsible for your upstream application (business). In addition, it may cause adverse effect such as downtime if you upgrade operation system on your own. Please consider the risk and operate with caution.


## 5. Miscellaneous

1.	The parties hereto acknowledge and agree that, for any losses incurred by you during the course of using the Service due to any breach by Tencent Cloud, the aggregate compensation amount payable by Tencent Cloud shall under no circumstance exceed the total service fees you have paid for the relevant Service which is not performed.

2.	Tencent Cloud has the right to amend the terms of this Agreement and notify you as appropriate or necessary in light of changes in due course. If you disagree with such revisions made by Tencent Cloud to this Agreement, you have the right to cease using the Service; by continuing to use the Service, you shall be deemed to have accepted the Agreement as amended.

3.	As an ancillary agreement to the Tencent Cloud Service Agreement, this Agreement is of the same legal effect as the Tencent Cloud Service Agreement. In respect of any matter not agreed herein, you shall comply with relevant terms under the Tencent Cloud Service Agreement. In case of any conflict or discrepancy between this Agreement and the Tencent Cloud Service Agreement, this Agreement prevails to the extent of such conflict or discrepancy. (End of Document)
