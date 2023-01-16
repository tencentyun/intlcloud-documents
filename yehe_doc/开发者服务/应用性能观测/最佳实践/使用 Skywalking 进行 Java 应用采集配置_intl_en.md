This document describes how to configure Java application data collection with SkyWalking.

## Overview

When the number of access requests is high, reporting all trace data may greatly increase APM fees. In this case, data sampling is often used.
<dx-alert infotype="explain" title="">
In sampling, certain data is sampled from all the collected trace data for analysis, which reduces the span volume and trace storage fees.
</dx-alert>

## Prerequisites
You have [reported the data of the Java application over the SkyWalking protocol](https://www.tencentcloud.com/document/product/1166/51712https://cloud.tencent.com/document/product/1463/57870).

## Directions

1. Open the `agent/config/agent.config` file and find the `agent.sample_n_per_3_secs=${SW_AGENT_SAMPLE:-1}` configuration item.
![](https://qcloudimg.tencent-cloud.cn/raw/71f2f5691677913a07b36e20e499406a.png)
2. Modify the sample rate. **`agent.sample_n_per_3_secs` indicates the volume of trace data (TraceSegment) that can be collected every three seconds. If it is negative or `0`, all traces are collected, which is the default option.**

**Example:**

To collect 1,500 TraceSegments in three seconds, set as follows:
```
agent.sample_n_per_3_secs=${SW_AGENT_SAMPLE:1500}
```


