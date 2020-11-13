Connection is used to connect local IDC to Tencent Cloud. To create a connection, you need to first confirm the information and submit an application on the console, and then the carrier will start the engineering investigation and wiring. This process takes about 2-3 months, therefore, please plan ahead to guarantee the cloudification progress.

## Flowchart

The following flowchart describes how to create a connection:
![](https://main.qcloudimg.com/raw/f724d4b9b9dc505c6ed3e84826dd7101.png)
1. [Preparations](#preparatorywork): confirm the access points and collect the requirements with Tencent Cloud and carrier before creating a connection.
2. [Creating a connection](#Creatededicatedline): if your local IDC resides in a data center different from that of a Tencent Cloud access point, please apply to create the connection in the Tencent Cloud console, and confirm your demands with a carrier that meets the Direct Connect Audit Standard. If your local IDC is colocated with a Tencent Cloud access point, you only need the Tencent Cloud solution to start constructing the connection.
3. Solution design: after receiving your application, Tencent Cloud will access resources, develop solutions, and confirm the fees with you. The carrier also needs to prepare resources and develop solutions. Please contact the carrier for relevant fees.
4. [Constructing a connection](#Railwayconstruction): if your local IDC resides in a data center different from that of a Tencent Cloud access point, the carrier will perform the engineering investigation and wiring based on the solution. Meanwhile, you need to pay for the port in the Tencent Cloud console. Then Tencent Cloud will complete the access port configuration, and support the carrier for the connection to Tencent Cloud. If your local IDC resides in the same data center as a Tencent Cloud access port, directly contact the Direct Connect representative for assistance.
5. [Connection acceptance](#Specialacceptance): you need to check and test the links of the completed connection. Accept the connection that passes the test.
<span id="preparatorywork" ></span>
## Preparations
Confirm the access point before creating a connection.
An access point is the location where you can access to Tencent Cloud connection’s network services. Nearby access is recommended. Generally, two or more access points are available in one Tencent Cloud region, implementing multi-connection disaster recovery. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to obtain the specific location of each access point. The following information helps you choose an access point:
- **Region**: a region is the physical location of an IDC. In Tencent Cloud, different regions are fully isolated, ensuring maximum stability and fault tolerance among regions. We recommend that you choose the region closest to your users to minimize access latency and improve access speed.
- **Carrier**: a provider of connection resources, including China Mobile, China Unicom, China Telecom, and other carriers that meet the Direct Connect Audit Standard.
 >? According to the relevant national laws, regulations and the [Notice on Regulating the Internet Network Access Marketplace (MIIT [2017] No. 32)](http://www.scio.gov.cn/xwfbh/xwbfbh/wqfbh/35861/36970/xgzc36976/Document/1559330/1559330.htm), you should choose an eligible connection provider to complete the construction of the Direct Connect service.
  > Otherwise, you may be exposed to the administrative penalty and liability, and the line may be unavailable. In this case, Tencent Cloud assumes no responsibility.

- **Port type**: ports in 1, 10, and 100 gigabit are available.
>?To use a 100-gigabit port, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
- **Port**: choose a fiber optic port or electronic port as needed.
  - Fiber optic port: a physical port used to connect fiber optic cables. Three port types are available: 1, 10, and 100 gigabit, which are subdivided into 10 km gigabit single-mode fiber optic port (SFP-GE-LX-Sm1310, 10 KM), 80 km gigabit single-mode fiber optic port (SFP-GE-LH80-SM1550, 80 KM), 10 km 10-gigabit single-mode fiber optic port (SFP-XG-LX-SM1310, 10 KM), 80 km 10-gigabit single-mode fiber optic port (SFP-XG-LH80-SM1550, 80 KM) and 10 km 100-gigabit single-mode fiber optic port (QSFP-100G-LR4-WDM1300, 10 KM).
  - Electronic port: general ports (such as RJ45) in server and network for twisted pairs (ordinary cables). Tencent Cloud provides gigabit electrical ports including 10/100/1000BASE-T, which are suitable for low bandwidth use cases.
<span id="Creatededicatedline" ></span>
## Creating a Connection
- If your local IDC resides in a data center different from that of a Tencent Cloud access point, apply for a connection in the Tencent Cloud console. For detailed directions, please see [Applying for Connection](https://intl.cloud.tencent.com/document/product/216/19244). You also need to communicate your requirements with a carrier that meets the Direct Connect Audit Standard.
- If your local IDC is colocated with a Tencent Cloud access point, you only need to apply for connection in the Tencent Cloud console. For detailed directions, please see [Applying for Connection](https://intl.cloud.tencent.com/document/product/216/19244).
<span id="Railwayconstruction" ></span>
## Constructing a Connection
- Local IDC and Tencent Cloud access point in different data centers
The connection construction needs to be completed by the carrier and Tencent Cloud concurrently, as detailed below:
  - Carrier
    After the engineering investigation, construction solution, and fees are finalized, the carrier can initiate the connection construction. In this process, fiber-to-the-building (FTTB) and in-house wiring rental fees may incur. For more information, consult your property operator or wiring provider.
    Perform the following steps to obtain the access to the data center at the access point:
    1. Apply to the Direct Connect representative and provide the name, ID card and contact information of engineers who need to investigate the data center at the access point.
    2. After the application is approved, the Direct Connect representative will help engineers access the data center within two business day.
 - Tencent Cloud
   After you pay for the Tencent Cloud port in the console, Tencent Cloud will complete the access port configuration, and support the carrier for the connection to Tencent Cloud.
- Local IDC and Tencent Cloud access point in the same data center
 Directly contact the Direct Connect representative, and the resource allocation and connection construction will start. During the construction, fiber-to-the-building (FTTB) and in-house wiring rental fees may incur. For more information, consult your property operator or wiring provider.
<span id="Specialacceptance" ></span>
## Connection Acceptance
You need to complete creating a Direct Connect instance before accepting the connection. For more information, please see [Getting Started](https://intl.cloud.tencent.com/document/product/216/38524). Then test the connection for its performance, latency and reliability.
- Performance test: whether the Iperf3 can communicate with servers.
- Latency test: the latency between IDC and Tencent Cloud VPC
- Reliability test: the packet loss during the communication between IDC and Tencent Cloud VPC. This test consists of two metrics: size 1500 and count 2000, size 5000 and count 2000.

