

ECM provides various instance types with different computing, memory, and storage capabilities. For now, ECM supports Standard S5, Standard S4 and Standard SN3ne.


## Specification Items
#### PPS
The maximum number of data packets that the instance can process per second for both sending and receiving, without differentiating private or public network traffic. 

#### Queues
The maximum number of queues for packet sending and receiving respectively supported by each ENI. For example, if the number is 2, it means two packet sending queues and two package receiving queues. 

#### Private network bandwidth
It is the maximum data volume in bits that can be transferred by the instance per second over the private network.

## Instance Types

#### Standard S5
Standard S5 is the latest generation of standard instances. 

It supports up to 25 Gbps of private network bandwidth to meet your high demand of private network transfer. 

<table>
<thead>
<tr>
<th style="width: 21%;">Item</th><th style="width: 8%;">vCPU</th><th style="width: 15%;">Memory (GB)</th>
<th style="width: 14%;">PPS (In + Out)</th><th>Connections</th><th style="width: 13%;">Queues</th><th style="width: 13%;">Private network bandwidth (In + Out in Gbps)</th><th style="width: 16%;">Clock rate (GHz)</th>
</tr>
</thead>
<tbody>
<tr><td>S5.LARGE8</td><td>4</td><td>8</td><td>500K</td><td>250K</td><td>2</td><td>4</td><td>2.5</td></tr>
<tr><td>S5.LARGE16</td><td>4</td><td>16</td><td>500K</td><td>250K</td><td>2</td><td>4</td><td>2.5</td></tr>
<tr><td>S5.2XLARGE16</td><td>8</td><td>16</td><td>800K</td><td>250K</td><td>4</td><td>4</td><td>2.5</td></tr>
<tr><td>S5.2XLARGE32</td><td>8</td><td>32</td><td>800K</td><td>250K</td><td>4</td><td>4</td><td>2.5</td></tr>
<tr><td>S5.4XLARGE32</td><td>16</td><td>32</td><td>1.5M</td><td>300K</td><td>8</td><td>8</td><td>2.5</td></tr>
<tr><td>S5.4XLARGE64</td><td>16</td><td>64</td><td>1.5M</td><td>300K</td><td>8</td><td>8</td><td>2.5</td></tr>
<tr><td>S5.6XLARGE48</td><td>24</td><td>38</td><td>2M</td><td>400K</td><td>12</td><td>10</td><td>2.5</td></tr>
<tr><td>S5.8XLARGE64</td><td>32</td><td>64</td><td>2.5M</td><td>600K</td><td>16</td><td>15</td><td>2.5</td></tr>
<tr>
<tr><td>S5.8XLARGE128</td><td>32</td><td>128</td><td>2.5M</td><td>600K</td><td>16</td><td>15</td><td>2.5</td></tr>
<tr><td>S5.16XLARGE128</td><td>64</td><td>128</td><td>5M</td><td>1.2M</td><td>16</td><td>25</td><td>2.5</td></tr>
</tbody></table>


### Standard S4

Standard S4 instances use Xeon<sup>®</sup> Skylake and DDR4 memory. It provides up to 2.4M pps over the private network. 


<table>
<thead>
<tr>
<th style="width: 21%;">Item</th><th style="width: 8%;">vCPU</th><th style="width: 15%;">Memory (GB)</th>
<th style="width: 14%;">PPS (In + Out)</th><th>Connections</th><th style="width: 13%;">Queues</th><th style="width: 13%;">Private network bandwidth (In + Out in Gbps)</th><th style="width: 16%;">Clock rate (GHz)</th>
</tr>
</thead>
<tbody>
<tr><td>S4.LARGE8</td><td>4</td><td>8</td><td>300K</td><td>1.5</td><td>2</td><td>2.5</td></tr>
<tr><td>S4.LARGE16</td><td>4</td><td>16</td><td>300K</td><td>1.5</td><td>2</td><td>2.5</td></tr>
<tr><td>S4.LARGE32</td><td>4</td><td>32</td><td>300K</td><td>1.5</td><td>2</td><td>2.5</td></tr>
<tr><td>S4.2XLARGE16</td><td>8</td><td>16</td><td>600K</td><td>1.5</td><td>4</td><td>2.5</td></tr>
<tr><td>S4.2XLARGE32</td><td>8</td><td>32</td><td>600K</td><td>1.5</td><td>4</td><td>2.5</td></tr>
<tr><td>S4.2XLARGE64</td><td>8</td><td>64</td><td>600K</td><td>1.5</td><td>4</td><td>2.5</td></tr>
<tr><td>S4.4XLARGE32</td><td>16</td><td>32</td><td>1.21M</td><td>3</td><td>8</td><td>2.5</td></tr>
<tr><td>S4.4XLARGE64</td><td>16</td><td>64</td><td>1.21M</td><td>3</td><td>8</td><td>2.5</td></tr>
<tr><td>S4.6XLARGE48</td><td>24</td><td>48</td><td>1.8M</td><td>4</td><td>12</td><td>2.5</td></tr>
<tr><td>S4.6XLARGE64</td><td>24</td><td>64</td><td>1.8M</td><td>4</td><td>12</td><td>2.5</td></tr>
<tr><td>S4.8XLARGE64</td><td>32</td><td>64</td><td>2.4M</td><td>5</td><td>16</td><td>2.5</td></tr>
</tbody></table>



### Standard SN3ne

<table>
<thead>
<tr>
<th style="width: 21%;">Item</th><th style="width: 8%;">vCPU</th><th style="width: 15%;">Memory (GB)</th>
<th style="width: 14%;">PPS (In + Out)</th><th>Connections</th><th style="width: 13%;">Queues</th><th style="width: 13%;">Private network bandwidth (In + Out in Gbps)</th><th style="width: 16%;">Clock rate (GHz)</th>
</tr>
</thead>
<tbody>
<tr><td>SN3ne.LARGE8</td><td>4</td><td>8</td><td>300K</td><td>1.5</td><td>2</td><td>2.5</td></tr>
<tr><td>SN3ne.LARGE16</td><td>4</td><td>16</td><td>300K</td><td>1.5</td><td>2</td><td>2.5</td></tr>
<tr><td>SN3ne.LARGE32</td><td>4</td><td>32</td><td>300K</td><td>1.5</td><td>2</td><td>2.5</td></tr>
<tr><td>SN3ne.2XLARGE16</td><td>8</td><td>16</td><td>600K</td><td>1.5</td><td>4</td><td>2.5</td></tr>
<tr><td>SN3ne.2XLARGE32</td><td>8</td><td>32</td><td>600K</td><td>1.5</td><td>4</td><td>2.5</td></tr>
<tr><td>SN3ne.2XLARGE64</td><td>8</td><td>64</td><td>600K</td><td>1.5</td><td>4</td><td>2.5</td></tr>
<tr><td>SN3ne.4XLARGE32</td><td>16</td><td>32</td><td>1.21M</td><td>3</td><td>8</td><td>2.5</td></tr>
<tr><td>SN3ne.4XLARGE64</td><td>16</td><td>64</td><td>1.21M</td><td>3</td><td>8</td><td>2.5</td></tr>
<tr><td>SN3ne.6XLARGE48</td><td>24</td><td>48</td><td>1.8M</td><td>4</td><td>12</td><td>2.5</td></tr>
<tr><td>SN3ne.6XLARGE64</td><td>24</td><td>64</td><td>1.8M</td><td>4</td><td>12</td><td>2.5</td></tr>
<tr><td>SN3ne.8XLARGE64</td><td>32</td><td>64</td><td>2.4M</td><td>5</td><td>16</td><td>2.5</td></tr>
</tbody></table>
