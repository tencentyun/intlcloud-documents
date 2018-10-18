CDH is a physical server equipped with a virtualized environment. Each model corresponds to the configuration of a different physical server, including the physical CPU model, number of CPU cores, memory size, local disk type, disk size and other hardware resources. You can choose the appropriate CDH model based on your business characteristics and size.

Currently, the following CDH models are supported:

| CDH configuration | Standard HS20 | Standard HS10 | High IO HI20 | High IO HI10 | MEM optimized HM20 | Compute HC20 |
| :-----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|
| Physical CPU model | Intel Xeon E5-2680 Broadwell (v4) | Intel Xeon CPU |Intel Xeon E5-2680 Broadwell (v4) | Intel Xeon CPU | Intel Xeon E5-2680 Broadwell (v4) | Intel Xeon(®) E5-2667v4 |
| Number of logic CPU cores | 56 | 48 | 56 | 48 |56 | 56 |
| Memory size (GB) | 224 | 96 | 224| 220 | 480 | 96 |
| Local disk type	 | Local HDD | Local HDD | Local SSD | Local SSD | Local HDD | Local SSD |
| Local Disk Size (GB) | 2452 | 2452 | 7052 | 7104 | 2452 | 1000 |

## Standard
The standard type is the balance of computing, memory and network resources that can meet application resource requirements in most scenarios.
### Standard HS20
Standard HS20 is the latest generation of standard CDH model. It uses Intel® Xeon® Broadwell processor which improves the performance of integer and floating point operations by 40% and DDR4 memory which improves the performance of random access by 30%. This model provides balanced computing, memory and network resources, making it a good choice for many applications.

#### Model Features
* 2.4 GHz Intel Xeon E5-2680 Broadwell (v4) processor, DDR4 memory 
* CPU performance is 20% higher than Series 1 (Standard HS10)
* A balance of computing, memory and network resources


### Standard HS10
Standard HS10 meets your needs of flexible choice of configuration at moderate prices and with flexible configuration options.
#### Model Features
* It offers flexible configuration options that range from low to high numbers of cores
* Intel Xeon CPU, DDR3 memory
* A balance of computing, memory and network resources

## High IO
High IO I2 instance is optimized to provide tens of thousands of low latency random I/O operations per second (IOPS) to applications, making it the best choice for high-IOPS scenarios.

### High IO HI20
High IO HI20 uses Intel Broadwell processor which improves the performance of integer and floating point operations by 40% and DDR4 memory which improves the performance of random access by 30%;
#### Model Features
* 2.4 GHz Intel Xeon E5-2680 Broadwell (v4) processor, DDR4 memory
* CPU performance is 20% higher than Series 1 (High IO I1)
* For SSD instance storage, a local SSD is used as system disk
>**High random IOPS**: In a typical scenario, the random read IOPS can be up to 75,000 (blocksize = 4 KB, iodepth = 32) and random write IOPS can be up to 10,000 (blocksize = 4 KB, iodepth = 32);
**High throughput**: In a typical scenario, random read throughput can be up to 250 MB/s (blocksize = 4 KB, iodepth = 32);
**Low latency**: In a typical scenario, the access latency can be down to sub-milliseconds (blocksize = 4 KB, iodepth =1).

#### Application Scenarios
High-performance database, NoSQL database (such as MongoDB), clustered database
I/O-intensive applications that require low latency, such as online transaction processing (OLTP) systems and ElasticSearch searches

### High IO HI10 
High IO HI10 is equipped with a high-performance local SSD that meets the needs for high disk reads and writes and low latency.
#### Model Features
* High random IOPS: In a typical scenario, the random read IOPS can be up to 40,000 (blocksize = 4 KB, iodepth = 32)
* High throughput: In a typical scenario, random read throughput can be up to 250 MB/s (blocksize = 4 KB, iodepth = 32);
* Low latency: The access latency can be down to sub-milliseconds

#### Application Scenarios
High-performance database, NoSQL database (such as MongoDB), clustered database
I/O-intensive applications that require low latency, such as online transaction processing (OLTP) systems and ElasticSearch searches

## MEM Optimized
The MEM optimized model features large memory, suitable for applications requiring a large number of memory operations, lookups and calculations such as high-performance databases and distributed memory caches.
### MEM Optimized HM20
MEM Optimized HM20 is designed to deliver fast performance for workloads that process large data sets in memory. It features large memory, making it the best choice for high-memory computing applications.

#### Model Features
* 2.4 GHz Intel Xeon® E5-2680v4 processor, DDR4 memory
* Processor to memory ratio is 1:8

#### Application Scenarios
- -Applications requiring a large number of memory operations, lookups and calculations such as high-performance databases and distributed memory caches. 
- Users with self-built Hadoop clusters or Redis databases for generic computation and other tasks

## Compute
The Compute model features a 3.2 GHz base clock rate and has the highest single-core computing performance. It is suitable for compute-intensive applications such as batch processing, high-performance computing and large-scale gaming servers.
### Compute HC20
Compute HC20 features the highest processor and cost performance, making it ideal for compute-intensive applications requiring high computing performance and high concurrent reads and writes.
#### Model Features
* 3.2 GHz Intel Xeon® E5-2667v4 processor (with a max turbo frequency of 3.6 GHz), DDR4 memory

#### Application Scenarios
Compute C2 is ideal for the following scenarios:
* Batch workloads
* High-traffic web servers, massively multiplayer online (MMO) gaming servers
* High-performance computing (HPC) and other compute-intensive applications.

For best performance, we recommend that you use the current generation of instance type when creating a new instance.
