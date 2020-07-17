## Namespace

Namespace=QCE/TXMR_SPARK

## Monitoring Metrics

#### Spark - SparkJobHistory 

| Parameter | Metric Name | Description | Unit | Dimension |
| ----------------------- | ---------------- | ------------------------------------- | ---- | ------------------------------------------------------------ |
| SparkShGcUtilGcCountYgc | GC count_YGC       | Young GC count                         | -   | host4sparksparkjobhistoryserver<br>id4sparksparkjobhistoryserver |
| SparkShGcUtilGcCountFgc | GC count_FGC       | Full GC count                          | -   | host4sparksparkjobhistoryserver<br/>id4sparksparkjobhistoryserver |
| SparkShGcUtilGcTimeFgct | GC time_FGCT      | Full GC time                      | s    | host4sparksparkjobhistoryserver<br/>id4sparksparkjobhistoryserver |
| SparkShGcUtilGcTimeGct  | GC time_GCT       | Garbage collection time                      | s    | host4sparksparkjobhistoryserver<br/>id4sparksparkjobhistoryserver |
| SparkShGcUtilGcTimeYgct | GC time_YGCT      | Young GC time                     | s    | host4sparksparkjobhistoryserver<br/>id4sparksparkjobhistoryserver |
| SparkShGcUtilMemoryS0   | Memory space percentage_S0  | Percentage of used Survivor 0 memory             | %    | host4sparksparkjobhistoryserver<br/>id4sparksparkjobhistoryserver |
| SparkShGcUtilMemoryE    | Memory space percentage_E   | Percentage of used Eden memory                   | %    | host4sparksparkjobhistoryserver<br/>id4sparksparkjobhistoryserver |
| SparkShGcUtilMemoryCcs  | Memory space percentage_CCS | Percentage of memory used by compressed class space | %    | host4sparksparkjobhistoryserver<br/>id4sparksparkjobhistoryserver |
| SparkShGcUtilMemoryS1   | Memory space percentage_S1  | Percentage of used Survivor 1 memory             | %    | host4sparksparkjobhistoryserver<br/>id4sparksparkjobhistoryserver |
| SparkShGcUtilMemoryO    | Memory space percentage_O   | Percentage of used Old memory                    | %    | host4sparksparkjobhistoryserver<br/>id4sparksparkjobhistoryserver |
| SparkShGcUtilMemoryM    | Memory space percentage_M   | Percentage of used Metaspace memory              | %    | host4sparksparkjobhistoryserver<br/>id4sparksparkjobhistoryserver |

## Overview of Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| :----------------------------- | :------------------------------ | :--------------------------- | :------------------------------------------------------- |
| Instances.N.Dimensions.0.Name  | id4sparksparkjob<br/>historyserver   | Dimension name of EMR instance ID       | String-type dimension name, such as id4sparksparkjobhistoryserver  |
| Instances.N.Dimensions.0.Value | id4sparksparkjob<br/>historyserver   | Specific EMR instance ID              | Specific EMR instance ID, such as emr-mm8bs222                |
| Instances.N.Dimensions.1.Name  | host4sparksparkjob<br/>historyserver | Dimension name of node IP in EMR instance | String-type dimension name, such as host4sparksparkjobhistoryserver |
| Instances.N.Dimensions.1.Value | host4sparksparkjob<br/>historyserver | Specific node IP in EMR instance        | Specific node IP, such as 1.1.1.1                          |

## Input Parameter Description

To query the monitoring data of EMR (Spark), use the following input parameters:
&Namespace=QCE/TXMR_SPARK
&Instances.N.Dimensions.0.Name=id4sparksparkjobhistoryserver
&Instances.N.Dimensions.0.Value=Specific EMR instance ID
&Instances.N.Dimensions.1.Name=host4sparksparkjobhistoryserver
&Instances.N.Dimensions.1.Value=Specific node IP in EMR instance 
