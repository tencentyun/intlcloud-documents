A DC connection connects customer’s local IDC to Tencent Cloud. To create a connection, you need to first confirm the information and submit an application on the console, and then the carrier will start the engineering investigation and wiring. This process takes about 2-3 months; therefore, please plan ahead to guarantee the cloudification progress.

## Flowchart

The following flowchart describes how to create a connection.
![](https://main.qcloudimg.com/raw/f724d4b9b9dc505c6ed3e84826dd7101.png)

1. [Preparations](#preparatorywork): confirm the access points and collect requirements from Tencent Cloud and the carrier before creating a connection.
2. [Creating a connection](#Creatededicatedline): if your local IDC and Tencent Cloud access points are in different data centers, please apply for a connection in the Tencent Cloud console, and communicate your needs with the carrier. If your local IDC resides in the same data center as a Tencent Cloud access point, you only need the Tencent Cloud solution to start the connection construction.
3. Designing a solution: after receiving your application, Tencent Cloud will access resources, develop solutions, and confirm with you. The carrier also needs to prepare resources and develop solutions. Please contact the carrier for relevant fees.
4. [Constructing a connection](#Railwayconstruction): if your local IDC and Tencent Cloud access points are in different data centers, the carrier will perform the engineering investigation and wiring based on the solution. Meanwhile, you need to pay for the port in the Tencent Cloud console. Then Tencent Cloud will complete the access port configuration, and help the carrier connect the connection to Tencent Cloud. If your local IDC resides in the same data center as a Tencent Cloud access port, directly contact the Direct Connect representative for assistance.
>?Starting from February 1, 2021, all the new connections will be exempted from the initial installation fee.
> 
5. [Accepting a connection](#Specialacceptance): you need to check and test the links of the completed connection. Accept the connection that passes the test.

<span id="preparatorywork" ></span>
## Preparations
Determine the access point before creating a connection.
An access point is the location where you can access to Tencent Cloud connection’s network services. Nearby access is recommended. Generally, two or more access points are available in one Tencent Cloud region, implementing multi-connection disaster recovery. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to obtain the specific location of each access point. The following information helps you choose a proper access point:
- **Region**: a region is the physical location of an IDC. In Tencent Cloud, regions are fully isolated between each other, ensuring cross-region stability and fault tolerance. We recommend that you choose the region closest to your end users to minimize access latency and improve access speed.
- **Carrier**: the provider of connection resources.
- **Port type**: ports in 1, 10, and 100 gigabit are available.
>?To use a 100-gigabit port, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
- **Port**: choose a fiber optic port or electronic port as needed.
  - Fiber optic port: a physical port used to connect fiber optic cables. Three port types are available: 1, 10, and 100 gigabit, which are subdivided into 10 km gigabit single-mode fiber optic port (SFP-GE-LX-Sm1310, 10 KM), 80 km gigabit single-mode fiber optic port (SFP-GE-LH80-SM1550, 80 KM), 10 km 10-gigabit single-mode fiber optic port (SFP-XG-LX-SM1310, 10 KM), 80 km 10-gigabit single-mode fiber optic port (SFP-XG-LH80-SM1550, 80 KM) and 10 km 100-gigabit single-mode fiber optic port (QSFP-100G-LR4-WDM1300, 10 KM).
  - Electronic port: general ports (such as RJ45) in server and network for twisted pairs (ordinary cables). Tencent Cloud provides gigabit electrical ports (10/100/1000BASE-T), which are suitable for low bandwidth use cases.

<span id="Creatededicatedline" ></span>
## Creating a Connection
- If your local IDC and Tencent Cloud access points are in different data centers, apply for a connection in the Tencent Cloud console. For detailed directions, please see [Applying for Connection](https://intl.cloud.tencent.com/document/product/216/19244). 
- If your local IDC resides in the same data center as a Tencent Cloud access point, you only need to apply for a connection in the Tencent Cloud console. For detailed directions, please see [Applying for Connection](https://intl.cloud.tencent.com/document/product/216/19244).

<span id="Railwayconstruction" ></span>
## Constructing a Connection
- Local IDC and Tencent Cloud access point in different data centers
Both the carrier and Tencent Cloud are responsible for the connection construction as follows:
  - Responsibilities of the carrier
    After the engineering investigation, construction solution, and fees are finalized, the carrier can initiate the connection construction. In this process, fiber-to-the-building (FTTB) and in-house wiring rental fees may incur. For more information, consult your property operator or wiring provider.
    Perform the following steps to obtain the permission to enter the access point’s data center:
    1. Apply to the Direct Connect representative and provide the name, ID card and contact information of engineers who need to investigate the access point's data center.
    2. After the application is approved, the Direct Connect representative will help engineers access the data center within two business days.
 - Responsibilities of Tencent Cloud
   After you pay for the Tencent Cloud port in the console, Tencent Cloud will complete the access port configuration, and support the carrier for the connection to Tencent Cloud.
- Local IDC and Tencent Cloud access point in the same data center
 You only need to contact the Direct Connect representative for resource allocation and connection construction. During the construction, fiber-to-the-building and in-house wiring rental fees may incur. For more information, consult your property operator or wiring provider.

<span id="Specialacceptance" ></span>
## Checking and Accepting the Connection
You need to complete creating a Direct Connect instance before accepting the connection. For more information, please see [Connection Overview](https://intl.cloud.tencent.com/document/product/216/38524). Then test the connection for its performance, latency and reliability.
- Stress test: whether the Iperf3 can communicate with servers.
- Latency test: the latency between IDC and Tencent Cloud VPC.
- Reliability test: the packet loss during the communication between IDC and Tencent Cloud VPC. This test consists of two metrics: size 1500 and count 2000, size 5000 and count 2000.

