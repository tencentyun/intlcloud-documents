

When you create an ECM instance, the instance type that you specified determines the server hardware configuration of the instance. Different instance types provide different computing, memory, and storage capabilities and are applicable to different use cases. You can flexibly select an appropriate instance type based on the service scale, computing power, storage space, and network connection method that you need. Currently, ECM supports two instance types: Standard S4 and Standard SN3ne.


## Glossary
#### Sent/Received Packets (PPS)
It is the maximum number of data packets that the instance can process per second for both sending and receiving, without differentiating between private and public network traffic. 

#### Number of queues
It is the number of sent/received packet queues supported by each virtual ENI (N queues indicates that N receiving queues and N sending queues can be simultaneously supported).

#### Private network bandwidth capability
It is the maximum data volume in bits that can be transferred by the instance per second over the private network.

## Instance Type
### Standard S4

Standard S4 instances are a new generation of standard instances. This type provides a balance of computing, memory, and network resources, and it is a good choice for many applications.

Standard S4 instances use the new-generation processor Xeon<sup>®</sup> Skylake and DDR4 memory, enable network optimization by default, and have packet sending/receiving capabilities of up to 2.4 million PPS over the private network, which can meet extremely high requirements for private network transfer. The instance network performance is subject to the specification. The higher the specification, the higher the performance, and the higher the maximum private network bandwidth.

You can purchase the following standard S4 instance configurations. Make sure that your selected instance specification meets the lowest requirements of your OS and applications for CPU and memory.


<table>
<thead>
<tr>
<th style="width: 21%;">Specification</th><th style="width: 8%;">vCPU</th><th style="width: 15%;">Memory (GB)</th>
<th style="width: 14%;">Sent/Received Packets (PPS)</th><th style="width: 13%;">Private Network Bandwidth (Gbps)</th><th style="width: 13%;">Number of Queues</th><th style="width: 16%;">Clock Rate (GHz)</th>
</tr>
</thead>
<tbody>
<tr><td>S4.LARGE8</td><td>4</td><td>8</td><td>300,000</td><td>1.5</td><td>2</td><td>2.5</td></tr>
<tr><td>S4.LARGE16</td><td>4</td><td>16</td><td>300,000</td><td>1.5</td><td>2</td><td>2.5</td></tr>
<tr><td>S4.LARGE32</td><td>4</td><td>32</td><td>300,000</td><td>1.5</td><td>2</td><td>2.5</td></tr>
<tr><td>S4.2XLARGE16</td><td>8</td><td>16</td><td>600,000</td><td>1.5</td><td>4</td><td>2.5</td></tr>
<tr><td>S4.2XLARGE32</td><td>8</td><td>32</td><td>600,000</td><td>1.5</td><td>4</td><td>2.5</td></tr>
<tr><td>S4.2XLARGE64</td><td>8</td><td>64</td><td>600,000</td><td>1.5</td><td>4</td><td>2.5</td></tr>
<tr><td>S4.4XLARGE32</td><td>16</td><td>32</td><td>1,210,000</td><td>3</td><td>8</td><td>2.5</td></tr>
<tr><td>S4.4XLARGE64</td><td>16</td><td>64</td><td>1,210,000</td><td>3</td><td>8</td><td>2.5</td></tr>
<tr><td>S4.6XLARGE48</td><td>24</td><td>48</td><td>1,800,000</td><td>4</td><td>12</td><td>2.5</td></tr>
<tr><td>S4.6XLARGE64</td><td>24</td><td>64</td><td>1,800,000</td><td>4</td><td>12</td><td>2.5</td></tr>
<tr><td>S4.8XLARGE64</td><td>32</td><td>64</td><td>2,400,000</td><td>5</td><td>16</td><td>2.5</td></tr>
</tbody></table>



### Standard SN3ne

Standard SN3ne instances are a relatively new generation of network optimized instances. This type provides a balance of computing, memory, and network resources, with outstanding network throughput, and it is a good choice for many applications.

You can purchase the following standard SN3ne instance configurations. Make sure that your selected instance specification meets the lowest requirements of your OS and applications for CPU and memory.

<table>
<thead>
<tr>
<th style="width: 21%;">Specification</th><th style="width: 8%;">vCPU</th><th style="width: 15%;">Memory (GB)</th>
<th style="width: 14%;">Sent/Received Packets (PPS)</th><th style="width: 13%;">Private Network Bandwidth (Gbps)</th><th style="width: 13%;">Number of Queues</th><th style="width: 16%;">Clock Rate (GHz)</th>
</tr>
</thead>
<tbody>
<tr><td>SN3ne.LARGE8</td><td>4</td><td>8</td><td>300,000</td><td>1.5</td><td>2</td><td>2.5</td></tr>
<tr><td>SN3ne.LARGE16</td><td>4</td><td>16</td><td>300,000</td><td>1.5</td><td>2</td><td>2.5</td></tr>
<tr><td>SN3ne.LARGE32</td><td>4</td><td>32</td><td>300,000</td><td>1.5</td><td>2</td><td>2.5</td></tr>
<tr><td>SN3ne.2XLARGE16</td><td>8</td><td>16</td><td>600,000</td><td>1.5</td><td>4</td><td>2.5</td></tr>
<tr><td>SN3ne.2XLARGE32</td><td>8</td><td>32</td><td>600,000</td><td>1.5</td><td>4</td><td>2.5</td></tr>
<tr><td>SN3ne.2XLARGE64</td><td>8</td><td>64</td><td>600,000</td><td>1.5</td><td>4</td><td>2.5</td></tr>
<tr><td>SN3ne.4XLARGE32</td><td>16</td><td>32</td><td>1,210,000</td><td>3</td><td>8</td><td>2.5</td></tr>
<tr><td>SN3ne.4XLARGE64</td><td>16</td><td>64</td><td>1,210,000</td><td>3</td><td>8</td><td>2.5</td></tr>
<tr><td>SN3ne.6XLARGE48</td><td>24</td><td>48</td><td>1,800,000</td><td>4</td><td>12</td><td>2.5</td></tr>
<tr><td>SN3ne.6XLARGE64</td><td>24</td><td>64</td><td>1,800,000</td><td>4</td><td>12</td><td>2.5</td></tr>
<tr><td>SN3ne.8XLARGE64</td><td>32</td><td>64</td><td>2,400,000</td><td>5</td><td>16</td><td>2.5</td></tr>
</tbody></table>

