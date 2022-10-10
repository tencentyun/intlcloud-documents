**In order to use the Tencent Cloud Managed Service for Grafana (the “Service”), you shall read and comply with this Tencent Cloud Managed Service for Grafana Service Level Agreement (this “Agreement”) and** **the** [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248). This Agreement contains, among others, the terms and definitions of the Service, Service Availability and Service Availability Standard, Compensation Plan and Disclaimer of Liabilities. Please carefully read and fully understand each and every provision hereof, and the provisions restricting or disclaiming certain liabilities, or otherwise related to your material rights and interests, are in bold font or underlined or otherwise brought to your special attention.

Please do not purchase or use the Service unless and until you have fully read, and completely understood and accepted all the terms hereof. By clicking “Agree”/ “Next”, or by purchasing or using the Service, or by otherwise accepting this Agreement, whether express or implied, you are deemed to have read, and agreed to be bound by, this Agreement. This Agreement shall then have legal effect on both you and Tencent Cloud, constituting a binding legal document on both parties. For the purposes of these Terms of Service, “Tencent Cloud” refers to the applicable Tencent entity as set forth in the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248).

## 1. Terms and Definitions

**1.1 Tencent Cloud Managed Service for Grafana (TCMG)**

Refers to a managed service developed by Tencent Cloud in collaboration with Grafana Lab, based on a popular open-source visualization project, Grafana. TCMG provides secure, operation-and-maintenance-free Grafana capabilities and built-in Tencent Cloud plug-ins for various data sources, such as Managed Service for Prometheus, Container Service, Logging Service, Graphite and InfluxDB, to achieve unified visualization of data. The specific services are subject to the services you have purchased and the service content provided by Tencent Cloud.

**1.2 A Single Instance**

Refers to a Grafana instance whose unit number is 1. The Service Availability (as defined below) shall be calculated based on a Single Instance.

**1.3 Total Number of Minutes within Service Month(s) for a Single Instance**

Total Number of Minutes within Service Month(s) for a Single Instance = the total number of days in Service Month(s) for a Single Instance × 24 (hours) × 60 (minutes).

**1.4 Service Unavailability for a Single Instance**

Grafana’s failure to display visualized data properly for reasons attributable to Tencent Cloud shall be deemed as Service Unavailability for a Single Instance.

**1.5 Service Downtime Calculated in Minutes for a Single Instance**

Service Downtime Calculated in Minutes for a Single Instance = the time when Service Unavailability for a Single Instance is fixed - the time when Service Unavailability for a Single Instance starts. 

Service Downtime refers to the time period from the start of a service failure to the time the services are back to normal, including system maintenance time without prior notice. If the duration of a service failure lasts for more than 5 minutes, such duration would be counted as Service Downtime Calculated in Minutes. If the duration of a service failure lasts for less than 5 minutes (i.e., the duration of Service Unavailability for a Single Instance does not exceed 5 minutes), such duration wouldn’t be counted as Service Downtime Calculated in Minutes.

**1.6 Service Month(s)**

Service Month(s) refers to the calendar month(s) within the term of the Service purchased by you. For example, if you purchase the Service for a term of three months starting from March 17, there will be four (4) Service Months (the first Service Month from March 17 to March 31, the second from April 1 to April 30, the third from May 1 to May 31, and the fourth from June 1 to June 16). The Service Availability will be calculated separately for each Service Month.

**1.7 Monthly Service Fee**

The Monthly Service Fee refers to the accumulated cash service fee you pay for a Single Instance within a Service Month, excluding the portion that has been purchased but not consumed yet, and the fees deducted by vouchers, coupons, service fee reduction or exemption, etc.

## 2. Service Availability

**2.1 Calculation of Service Availability**

Service Availability = (Total Number of Minutes within a Service Month for a Single Instance - Service Downtime Calculated in Minutes for a Single Instance) / Total Number of Minutes within a Service Month for a Single Instance × 100%.

**2.2 Service Availability Standard**

The Service Availability for the Service **shall be no less than 99.95%** (“Service Availability Standard”). If the Service fails to meet the Service Availability Standard (except under circumstances as set forth in the Article 4 (Disclaimer of Liabilities)), you may claim compensation in accordance with Article 3 of this Agreement (Compensation Plan).

Assuming that Total Number of Minutes within a Service Month for a Single Instance is 43,200 minutes (=30 × 24 × 60), Service Downtime Calculated in Minutes for a Single Instance shall be less than 21.6 minutes (=43,200 – 43,200 × 99.95%).

## 3. Compensation Plan

In respect of the Service, if the Service fails to meet the Service Availability Standard, you will be entitled to compensations in accordance with the following terms:

**3.1 Standards of Compensation**

(1) Compensations will be made **in the form of voucher** by Tencent Cloud, and after receiving the voucher, you should use the voucher by abiding the voucher usage rules (including usage period, etc., subject to the voucher usage rules published on Tencent Cloud official website). Such voucher cannot be converted into cash, and no invoice will be issued with respect thereof. The voucher may only be used to purchase the Service by using your Tencent Cloud account, and you cannot use the voucher to purchase other services of Tencent Cloud, nor should you give the voucher to a third party for consideration or for free.

(2) If the Service fails to meet the Service Availability Standard in any Service Month, the amount of compensation shall be calculated for such Service Month independently, and **the aggregate amount shall be no more than the Monthly Service Fee you pay for the Service in the Service Month in which the Service fails to meet the Service Availability Standard** (the Monthly Service Fee refers to the actual amount you pay in cash, excluding the portion deducted by vouchers, coupons, service fee reduction or exemption, etc.). 

| **Service   Availability in a Service Month** | **Value of Compensational Voucher** |
| --------------------------------------------- | ----------------------------------- |
| Less  than 99.95% but is or higher than 99%   | 10%  of the Monthly Service Fee     |
| Less  than 99% but is or higher than 95%      | 25%  of the Monthly Service Fee     |
| Less  than 95%                                | 100%  of the Monthly Service Fee    |

**3.2 Time Limit for Compensation Application**

(1) If the Service Availability in a Service Month fails to meet the Service Availability Standard, you may **apply for compensation only through the Tencent Cloud ticket system under your relevant account** after the fifth (5th) business day of the month immediately following such Service Month. Tencent Cloud will verify and ascertain your application upon receipt of such application. If there is any dispute over the calculation of the Service Availability for a Service Month, **both parties agree that the back-end record of Tencent Cloud shall prevail**.

(2) **You shall apply for compensation no later than the sixtieth (60th) calendar day following the end of the Service Month in which the Service fails to meet the Service Availability Standard.** If you fail to make any application within such period, or make the application after such period, or make the application by any means other than that agreed herein, it shall be deemed that you have voluntarily waived your right to apply for such compensation and any other rights you may have against Tencent Cloud, in which case Tencent Cloud has the right to reject your application for compensation and not to make any compensation to you.

## 3. Disclaimer of Liabilities

**If the service is unavailable due to any of the following reasons, the corresponding Service Downtime shall not be counted towards Service Unavailability period, and is not eligible for compensation by Tencent Cloud, and Tencent Cloud will not be held liable to you****:**

4.1 Any system maintenance with prior notice by Tencent Cloud, including system cutover, maintenance, upgrade and malfunction simulation test and other planned downtime.

4.2 Any failure or configuration adjustment of any network or equipment that is not a Tencent Cloud facility.

4.3 Any Service Unavailability caused by a third party other than Tencent Cloud, such as any Service Unavailability due to an attack by hackers or negligence of your third-party supplier.

4.4 Any loss or leakage of data, passcode or password due to your improper maintenance or confidentiality.

4.5 Any maloperation due to your negligence or any operation authorized by you, such as user-initiated reconstruction.

4.6 Any failure of you to abide by documentation or suggestions for using Tencent Cloud products.

4.7 The Service is unavailable or fails to meet the Service Availability Standard due to any reason not attributable to Tencent Cloud.

4.8 Any other circumstances in which Tencent Cloud will be exempted or released from its liabilities for compensation or otherwise according to applicable laws, regulations, agreements or rules, or rules or guidelines published by Tencent Cloud separately.

4.9 Any event of force majeure or accidents.

## 5. Miscellaneous

**5.1 The parties hereto acknowledge and agree that, for any losses incurred by you for the use of the Service due to any breach by Tencent Cloud, the aggregate liability of Tencent Cloud shall under no circumstance exceed the total service fees you have paid for the relevant Service which fails to meet the Service Availability Standard. If you have used the Service for more than 12 months, the total aggregate liability of Tencent Cloud shall not exceed the total service fees you have paid to Tencent Cloud for the Service which fails to meet the Service Availability Standard in the 12 months immediately preceding the date that event giving rise to the liability first occurred.**

5.2 Tencent Cloud has the right to amend the terms of this Agreement as appropriate or necessary in light of changes in due course. You may review the most updated version of relevant Agreement terms on the Tencent Cloud official website. If you disagree with such revisions made by Tencent Cloud to this Agreement, you have the right to cease using the Service; by continuing to use the Service, you shall be deemed to have accepted this Agreement as amended.

5.3 As an ancillary agreement to the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248), this Agreement is of the same legal effect as the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248). In respect of any matter not agreed herein, you shall comply with relevant terms under the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248). In case of any conflict or discrepancy between this Agreement and the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248), this Agreement prevails to the extent of such conflict or discrepancy. (End)

 