
## Overview
TKE provides users with an out-of-the-box event dashboard and can automatically configure analysis dashboards of event overview and exception events aggregation search for the clusters with the feature of **Event Storage** enabled. With user-defined filter items, and built-in CLS event global search, uses can comprehensively observe, find, analyze, and locate problems in the TKE console.


## Feature Description

Three dashboards are configured in the **Event Search**, namely **Event Overview**, **Exception Events Aggregation Search**, and **Global Search**. Please follow the steps below to go to the **Event Search** page and use the corresponding features:
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. Enable **Event Storage**. For more information, see [Event Storage](https://intl.cloud.tencent.com/document/product/457/30686).
3. Click **Cluster Ops** > **Event Search** in the left sidebar to go to the **Event Search** page.


### Event overview

On the "Event Overview" page, you can filter events based on dimensions such as time, namespace, level, reason, resource type, resource object, etc., view summary statistics of core events, and display data comparison within a period, for example, dashboards of the total number and distribution of events, node exceptions, Pod OOM, important event trends, and top exception event lists.
You can customize the filter items as needed (up to 10 filter items can be set)

You can modify the custom fields of the filter item 

You can view more statistics in this page, as shown below:
- Total number of events, level distribution, exception event reason and object distribution 
- The summary of various common events 
- Event trend and top exception event list 


### Exception events aggregation search
On the **Exception Events Aggregation Search** page, you can set filter conditions to view the type and object distribution trends of various exception events in a certain period of time. You can also search the exception events in the list below the trend diagrams to quickly locate the problems 

### Global search
Global search dashboard, with built-in CLS search analysis page, is convenient for users to quickly search all events in the TKE console 
