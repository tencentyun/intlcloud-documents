The exception diagnosis feature provides you with real-time performance monitoring, health checks, and failure diagnosis and optimization, so that you can intuitively know the real-time operation status of database instances, locate newly appeared performance exceptions in real time, and optimize the system based on the optimization suggestions. Exception diagnosis provides real-time and historical view modes.
This document describes how to use the exception diagnosis feature to diagnose and optimize real-time/historical exceptions in databases.

>Currently, exception diagnosis is supported only for TencentDB for MySQL (excluding the Basic Edition).

Log in to the [DBbrain Console](https://console.cloud.tencent.com/dbbrain/analysis), select **Diagnosis and Optimization** on the left sidebar, and select **Exception Diagnosis** at the top.
![](https://main.qcloudimg.com/raw/040ba89bd1915fd14e78507d33d12035.png)
## Real-Time/Historical Monitoring
The exception diagnosis page displays CPU, memory, and disk utilization as well as inbound/outbound traffic information. To view details on disk utilization, click **Details** in the top-right corner.
![](https://main.qcloudimg.com/raw/f492b6e9ea0232b6628b5d2513e8a27c.png)

## Real-Time/Historical Diagnosis
- The **Real-Time/Historical Diagnosis** column displays in real time the number of running threads, CPU utilization, and diagnosis events of the instance.
- The **Diagnosis Prompt** column displays the overview information of diagnosis event history, including health levels (healthy, notice, warning, severe, or fatal), start time, diagnosed items, and duration. DBbrain performs health checks on the instance once every ten minutes.



1. Click **View Details** or the recorded item under **Diagnosis Prompt** to access the diagnosis details page.
![](https://main.qcloudimg.com/raw/7a8826e6f9daaceeb9886bb5fd25d746.png)
2. Select the target time period to stretch the diagnosis view and view it at a finer granularity. After stretching the view, you can click **Reset** on the top-right corner to restore the original view.
 ![](https://main.qcloudimg.com/raw/befaedcb9588d0611e6d3ce00a3b7284.png)
3. You can click a graph curve in the view to check approximately 20 monitoring metrics spanning across the three major dimensions of resource, performance, and engine at a specific point in time. You can also click **Instance Monitoring** to access the monitoring page on the instance console and view metric details trends.
![](https://main.qcloudimg.com/raw/c7b994512c3c8f9a93a7a5993e1d2abc.png)
4. Click a diagnosis event in the view, and the event details will be displayed below.
 - Event Overview: includes diagnosed items, start and end times, risk level, duration, and overview.
 - Symptom: includes symptom snapshots and performance trends of the exception event (or health check event).
 - Intelligent Analysis: analyzes the root cause of the performance exception to help you locate the specific operation.
 - Expert Suggestion: optimization suggestions are provided, including but not limited to SQL optimization (index and rewrite), resource configuration optimization, and parameter fine-tuning.
![](https://main.qcloudimg.com/raw/a4ea4112eb5d5899b5d65089f51848da.png)

## Real-Time/Historical SQL
- "Real-Time/Historical SQL" displays the overall information and distribution of the number of requests made to the instance, including the trends of the total number of requests and the SELECT, REPLACE, INSERT, DELETE, and UPDATE statements.
- "Real-Time/Historical Slow SQL" displays the trends of slow SQL statements (slow logs) and CPU utilization. You can click **View Details** on the top-right corner to access the **Slow SQL Analysis** page and view analysis details.
![](https://main.qcloudimg.com/raw/ca4be1d10f5d19995327789752e42d59.png)
