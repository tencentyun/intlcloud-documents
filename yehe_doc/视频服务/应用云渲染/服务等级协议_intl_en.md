In order to use the Tencent Cloud Cloud Application Rendering Service (the “Service”), you shall read and comply with this Tencent Cloud Cloud Application Rendering Service Level Agreement (this “Agreement”, or this “SLA”) and the Tencent Cloud Service Agreement. This Agreement contains, among others, the terms and definitions of the Service, Service Availability and Service Uptime Metrics, compensation plan and disclaimer of liabilities. Please carefully read and fully understand each and every provision hereof, and the provisions restricting or disclaiming certain liabilities, or otherwise related to your material rights and interests, are in bold font or underlined or otherwise brought to your special attention.
Please do not purchase the Service unless and until you have fully read, and completely understood and accepted all the terms hereof. By clicking “Agree”/ “Next”, or by purchasing or using the Service, or by otherwise accepting this Agreement, whether express or implied, you are deemed to have read, and agreed to be bound by, this Agreement. This Agreement shall then have legal effect on both you and Tencent Cloud, constituting a binding legal document on both parties. For the purposes of these Terms of Service, “Tencent Cloud” refers to the applicable Tencent entity as set forth in the Tencent Cloud Service Agreement.

## 1. Terms and Definitions

### 1.1 Cloud Application Rendering, CAR
Refers to the real-time rendering of your application, software, platform and any related contents deployed on the Cloud Application Rendering concurrency, where “concurrency” means a collection of a series of virtual computing resources, including CPU, bandwidth, disk, GPU, etc. The real-time rendering operation is completed on the server-side of Cloud Application Rendering concurrency, and Tencent Cloud will encode the rendered results into audio and video streams for transmission to the user's device through the network, and the device transmits the user's operation information to the cloud server and the application for real-time interaction.

### 1.2 CAR Concurrent Packet(s)
If you purchase n CAR Concurrent Packets, it means the Service will contain n cloud application rendering concurrency. The Service Availability (as defined below) is calculated by CAR Concurrent Packets.
### 1.3 Total Number of Minutes within Service Month(s)
Total Number of Minutes within Service Month(s) = the total number of days of the Service Month(s) × 24 (hours) × 60 (minutes).
### 1.4 Service Unavailability
When the Service is in a non-maintenance state, but the access to the Service with any IP address in both directions (outgoing/incoming) by UDP protocol fails, and such downtime lasts for more than one minute, the Service is deemed as unavailable (“Service Unavailability”) within such minute.
### 1.5 Service Downtime Calculated in Minutes
Service Downtime Calculated in Minutes = the time the Service Unavailability is fixed – the time the Service Unavailability starts.
The service downtime is calculated in minutes. If the service failure is back to normal within one minute, i.e., if the duration of Service Unavailability of the CAR Concurrent Packet does not exceed one minute, such duration is not counted as Service Downtime Calculated in Minutes. If the duration of Service Unavailability is longer than one minute but less than two minutes, Service Downtime Calculated in Minutes in such duration would be one minute. For example, if the service downtime lasts for one minute and one second, the Service Downtime Calculated in Minutes would be one minute.
### 1.6 Service Month(s)
Service Month(s) refers to the calendar month(s) within the term of the Service purchased by you. For example, if you purchase the Service for a term of three months starting from March 17, there will be four (4) Service Months (the first Service Month from March 17 to March 31, the second from April 1 to April 30, the third from May 1 to May 31, and the fourth from June 1 to June 16). The Service Availability will be calculated separately for each Service Month.
### 1.7 Monthly Service Fee
The Monthly Service Fee refers to the accumulated service fee you pay for the Service within a Service Month, excluding the portion that has been purchased but not consumed yet, and the fees deducted with vouchers, coupons, service fee reductions, etc.

## 2. Service Availability
### 2.1 Calculation of Service Availability
Service Availability = (Total Number of Minutes within a Service Month - Service Downtime Calculated in Minutes) / Total Number of Minutes within a Service Month × 100%.
### 2.2 Service Availability Standard
The Service Availability for the Service shall be no less than 99% (“Service Availability Standard”). If the Service fails to meet the Service Availability Standard (except under circumstances as set forth in the Disclaimer of Liabilities), you may claim compensation in accordance with Section 3 of this Agreement.

Assuming that a month contains 30 days, the Total Number of Minutes within such Service Month is 43,200 minutes (=30 days × 24 hours × 60 minutes), the available time shall be no less than 42,768 minutes (=30 days × 24 hours × 60 minutes × 99%), which means the Service Downtime Calculated in Minutes shall be less than 432 minutes (=43,200 – 42,768).

## 3. Compensation Plan
In respect of the Service, if the Service fails to meet the Service Availability Standard, you will be entitled to compensations in accordance with the following terms:
### 3.1 Standards of Compensation
(1) Compensations will be made in the form of voucher by Tencent Cloud, and you should use the voucher by abiding the voucher usage rules (including usage period, etc., subject to the voucher usage rules published on Tencent Cloud official website). Such voucher cannot be converted into cash, and no invoice will be issued with respect thereof. The voucher may only be used to purchase the Service by using your Tencent Cloud account, and you cannot use the voucher to purchase other services of Tencent Cloud, nor should you give the voucher to a third party for consideration or for free.

(2) If the Service Availability Standard is not met for any Service Month, the amount of compensation will be calculated for each such Service Month independently, and the aggregate amount shall be no more than the Monthly Service Fee you pay for the Service in the Service Month in which the Service Availability fails to meet the Service Availability Standard (the Monthly Service Fee referred to herein shall exclude the portion deducted by vouchers, coupons, service fee reduction or exemption, etc.). 
Service Availability in a Service Month	Value of Compensational Voucher
Less than 99% but is or higher than 97%	5% of the Monthly Service Fee
Less than 97% but is or higher than 95%	10% of the Monthly Service Fee
Less than 95%	20% of the Monthly Service Fee
### 3.2 Time Limit for Compensation Application
(1) If the Service Availability in a Service Month fails to meet the Service Availability standard, you may apply for compensation only through the Tencent Cloud ticket system under your relevant account after the fifth (5th) business day of the month immediately following such Service Month. Tencent Cloud will verify and ascertain your application upon receipt of such application. If there is any dispute over the calculation of the Service Availability for a Service Month, both parties agree that the back-end record of Tencent Cloud shall prevail.

(2) You shall apply for compensation no later than the sixtieth (60th) calendar day following the end of the applicable Service Month in which the Service Availability fails to meet the abovementioned standard. If you fail to make any application within such period, or make the application after such period, or make the application by any means other than that agreed herein, it shall be deemed that you have voluntarily waived your right to apply for such compensation and any other rights you may have against Tencent Cloud, in which case Tencent Cloud has the right to reject your application for compensation and not to make any compensation to you.

## 4. Disclaimer of Liabilities
If the Service is unavailable due to any of the following reasons, the corresponding Service Downtime shall not be counted towards Service Unavailability period, and is not eligible for compensation by Tencent Cloud, and Tencent Cloud will not be held liable to you:

4.1 Any attack on your application program by hackers.

4.2 Any loss or leak of data, passcode or password due to your improper maintenance and improper confidentiality measures.

4.3 Any negligence of you or any operation authorized by you.

4.4 Any network instability of your devices, including but not limited to network jitter, network disconnection, insufficient network signal.

4.5 Any compatibility issues of the applications deployed by you, including but not limited to hardware incompatibility, peripheral incompatibility, operating system incompatibility, GPU incompatibility.

4.6 Any Service Unavailability due to your own operation or maintenance of the applications deployed by you, including but not limited to application updates, maintenance.

4.7 Any Service Unavailability due to your failure to follow the Tencent Cloud product documentation or usage recommendations, including but not limited to the Service Unavailability caused by your refund/destruction operation of the Service in the console and by the usage operation of SDK and API interfaces.

4.8 Any error of the Service due to the applications or software installed by you, or other third-party software or configuration that are not directly operated by Tencent Cloud.

4.9 Any request to stop the service due to your or your applications’ violation of laws, regulations, policies and norms, including but not limited to the use of pirated, non-copyrighted, Trojan horse viruses, pornography and other acts.

4.10 Any Service Unavailability due to force majeure including but not limited to natural disasters such as earthquakes, floods, plague epidemics, etc., as well as social events such as war, unrest, government actions, telecommunications backbone line disruptions, hackers, network congestion, technical adjustments in telecommunications departments and government controls.

4.11 Any suspension or termination due to your violation of Tencent Cloud Service Agreement, including the suspension or termination of the Service due to the unpaid or overdue service fees, etc.

4.12 Any temporary service interruption arising from routine maintenance and upgrade to the Service by Tencent Cloud as described in the Tencent Cloud Service Agreement.

4.13 Any Service Unavailability due to any reason not attributable to Tencent Cloud.

4.14 Any other circumstances in which Tencent Cloud will be exempted or released from its liabilities for compensation or otherwise according to relevant laws, regulations, agreements or rules, or any relevant rules or guidelines published by Tencent Cloud separately.

## 5. Miscellaneous
5.1 The parties hereto acknowledge and agree that, for any losses incurred by you for the use of the Service due to any breach by Tencent Cloud, the aggregate liability of Tencent Cloud shall under no circumstance exceed the total service fees you have paid for the relevant Service which fails to meet the Service Availability Standard. If you have used the Service for more than 12 months, the total aggregate liability of Tencent Cloud shall not exceed the total service fees you have paid to Tencent Cloud for the Service which fails to meet the Service Availability Standard in the 12 months immediately preceding the date that event giving rise to the liability first occurred.

5.2 Tencent Cloud has the right to amend the terms of this Agreement as appropriate or necessary in light of changes in due course. You may review the most updated version of relevant Agreement terms on the Tencent Cloud official website. If you disagree with such revisions made by Tencent Cloud to this Agreement, you have the right to cease using the Service; by continuing to use the Service, you shall be deemed to have accepted this Agreement as amended.

5.3 As an ancillary agreement to the Tencent Cloud Service Agreement, this Agreement is of the same legal effect as the Tencent Cloud Service Agreement. In respect of any matter not agreed herein, you shall comply with relevant terms under the Tencent Cloud Service Agreement. In case of any conflict or discrepancy between this Agreement and the Tencent Cloud Service Agreement, this Agreement prevails to the extent of such conflict or discrepancy. (End)
