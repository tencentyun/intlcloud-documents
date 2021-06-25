A DC connection connects customer’s local IDC to Tencent Cloud. To create a connection, you need to first confirm the information and submit an application on the console, and then the carrier will start the engineering investigation and wiring. This process takes about 2-3 months; therefore, please plan ahead to guarantee the cloudification progress.

## Flowchart
The following flowchart describes how to create a connection.
![](https://main.qcloudimg.com/raw/f724d4b9b9dc505c6ed3e84826dd7101.png)
1. [Preparations](#preparatorywork): confirm the access points and collect requirements from Tencent Cloud and the carrier before creating a connection.
2. [Creating a connection](#Creatededicatedline): if your local IDC and Tencent Cloud access points are in different data centers, please apply for a connection in the Tencent Cloud console, and communicate your needs with the carrier. If your local IDC resides in the same data center as a Tencent Cloud access point, you only need the Tencent Cloud solution to start the connection construction.
3. Designing a solution: after receiving your application, Tencent Cloud will access resources, develop solutions, and confirm with you. The carrier also needs to prepare resources and develop solutions. Please contact the carrier for relevant fees.
4. [Constructing a connection](#Railwayconstruction): if your local IDC and Tencent Cloud access points are in different data centers, the carrier will perform the engineering investigation and wiring based on the solution. Meanwhile, you need to pay for the port in the Tencent Cloud console. Then Tencent Cloud will complete the access port configuration, and help the carrier connect the connection to Tencent Cloud. If your local IDC resides in the same data center as a Tencent Cloud access port, directly contact the Direct Connect representative for assistance.
>?Starting from February 1, 2021, all the new connections will be exempted from the initial installation fee.
5. [Accepting a connection](#Specialacceptance): you need to check and test the links of the completed connection. Accept the connection that passes the test.

## Preparations[](id:preparatorywork)
Determine the access point before creating a connection.
An access point is the location where you can access to Tencent Cloud connection’s network services. Nearby access is recommended to ensure network quality and reduce connection costs. Generally, two or more access points are available in one Tencent Cloud region, implementing multi-connection disaster recovery. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to obtain the specific location of each access point. The following information helps you choose a proper access point:
- **Region**: a region is the physical location of an IDC. In Tencent Cloud, regions are fully isolated between each other, ensuring cross-region stability and fault tolerance. We recommend that you first check the distance from the access point to IDC and choose the region closest to your end users to minimize access latency and improve access speed.
- **Carrier**: the provider of connection resources.
 >? According to the relevant national laws, regulations and the [Notice on Regulating the Internet Network Access Marketplace (MIIT [2017] No. 32)](http://www.scio.gov.cn/xwfbh/xwbfbh/wqfbh/35861/36970/xgzc36976/Document/1559330/1559330.htm), you should choose an eligible connection provider to complete the construction of the Direct Connect service.
  > Using an illegal line may expose you to administrative penalty by the State regulatory authority and cause the line unavailability. In this case, Tencent Cloud accepts no responsibility.
- **Port**: choose a fiber optic port or electronic port as needed.
  - Fiber optic port: a physical port used to connect fiber optic cables. Tencent Cloud provides three port types: 1, 10, and 100 Gbps.
  - Electronic port: general ports (such as RJ45) in server and network for twisted pairs (ordinary cables). Tencent Cloud provides gigabit electronic ports (10/100/1000BASE-T), which are suitable for low bandwidth use cases.
>?To use a 100 Gbps port, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
<table>
  <tr>
	<th colspan="2">Port type</th>
	<th>Specifications</th>
	<tr>
	<td rowspan="5">Fiber optic port</td>
	<td rowspan="2">1 Gbps
	</td>
	<td colspan="2">SFP-GE-LX-Sm1310, 10KM</td>
	</tr>
	<tr>
	<td>SFP-GE-LH80-SM1550, 80KM</td>
	</tr>
		<tr>
	<td rowspan="2">10 Gbps
	</td>
	<td>SFP-XG-LX-SM1310, 10KM</td>
	</tr>
	<tr>
	<td>SFP-XG-LH80-SM1550, 80KM</td>
	</tr>
		<tr>
	<td>100 Gbps
	</td>
	<td >QSFP-100G-LR4-WDM1300, 10KM</td>
	</tr>
		<tr>
	<td colspan="2">Electronic port</td>
	<td >10/100/1000BASE-T</td>
	</tr>
	<tr>
</table>


## Creating a Connection[](id:Creatededicatedline)

| Use Case | Action|
|---------|---------|
| Local IDC and Tencent Cloud access point in different data centers| Apply for a connection in the Tencent Cloud console as instructed in [Applying for Connection](https://intl.cloud.tencent.com/document/product/216/19244), and communicate your requirements with the carrier.|
| Local IDC and Tencent Cloud access point in the same data center| Apply for a connection in the Tencent Cloud console. For detailed directions, please see [Applying for Connection](https://intl.cloud.tencent.com/document/product/216/19244).

## Constructing a Connection[](id:Railwayconstruction)
- Local IDC and Tencent Cloud access point in different data centers
  Both the carrier and Tencent Cloud are responsible for the connection construction as follows:
  - Responsibilities of the carrier
    ![](https://main.qcloudimg.com/raw/009c74aaf73486a93f8d26cfa52fed21.png)
   1. Perform the engineering investigation.
   2. Confirm the construction solution and relevant fees.
   3. Initiate the connection construction.
      
       >?During the construction, fiber-to-the-building (FTTB) and in-house wiring rental fees may incur. For more information, consult your property operator or wiring provider.
   4. Access the data center.
     1. Apply to the Direct Connect representative and provide the name, ID card and contact information of engineers who need to investigate the access point's data center.
     2. After the application is approved, the Direct Connect representative will help engineers access the data center within two business days.
 - Responsibilities of Tencent Cloud
   ![](	https://main.qcloudimg.com/raw/db1253e4dad83b283758af31e6de706d.png)
	 After you pay for the Tencent Cloud port in the console, Tencent Cloud will complete the access port configuration, and support the carrier for the connection to Tencent Cloud.
- Local IDC and Tencent Cloud access point in the same data center
 You only need to contact the Direct Connect representative for resource allocation and connection construction.
  
  >?During the construction, fiber-to-the-building and in-house wiring rental fees may incur. For more information, consult your property operator or wiring provider.

## Checking and Accepting the Connection[](id:Specialacceptance)
You need to complete creating a Direct Connect instance before accepting the connection. For more information, please see [Quick Start](https://intl.cloud.tencent.com/document/product/216/7557). Then test the connection for its performance, latency and reliability.
- Stress test: use the network test tool Iperf3 to check the interconnection between IDC and Tencent Cloud VPC.
- Latency test: use the network test tool Iperf3 to check latency between IDC and Tencent Cloud VPC.
- Reliability test: use the network test tool Iperf3 to check the packet loss during the communication between IDC and Tencent Cloud VPC.
   This test consists of two metrics: size 1500 and count 2000, size 5000 and count 2000.
	 >?The parameter `size` is the number of packets, and `count` is the sending times. For example, size 1500 and count 2000 means 1500 packets are sent 2000 times.
	 For more information about how to use the Iperf3 tool, see [iPerf 3 user documentation](https://iperf.fr/iperf-doc.php#3doc).
