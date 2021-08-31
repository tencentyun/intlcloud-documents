## Overview

Cloud Monitor Dashboard provides charts in table type. **Tables** allow you to easily view the monitoring data of each instance and sort them by maximum, minimum, and current values. This document describes how to create a table chart.


## Prerequisites

You have [created a metric](https://intl.cloud.tencent.com/document/product/248/38477).


## Directions

1. Log in to the Cloud Monitor console and go to the [Dashboard List](https://console.cloud.tencent.com/monitor/dashboard2/dashboards) page.
2. Click the dashboard for which to configure a chart to enter the dashboard management page.
3. Move the cursor to the chart for which to configure a table and select **...** > **Edit** to enter the chart editing page.

4. Click **Chart Type** in the chart configuration section on the right, select **Table** in the drop-down list, and configure as follows:
 - **Chart Elements**
	- **Serial No.:** indicates whether to display the serial number in the list.
	- **Precision:** indicates the number of decimal places to be retained for the maximum value, the minimum value, the average value, the sum, and the current value. 0: does no retain any decimals. 1: retains one decimal place.
	- **Displayed Quantity:** indicates the number of instances displayed in the list. Valid values: 10 items/page, 20 items/page, 30 items/page, 50 items/page, 100 items/page.
 - **Field Settings**
You can set the fields to be displayed in the table.
	- **Current:** indicates whether the table displays the current value.
	- **Maximum:** indicates whether the table displays the maximum value.
	- **Minimum:** indicates whether the table displays the minimum value.
	- **Average:** indicates whether the table displays the average value.
	- **Sum:** indicates whether the table displays the sum value.
  The bottom part of the field settings section displays the fields currently displayed in the table. You can select or deselect fields to display or hide them.
5. After completing the configuration, click **Save** in the top-right corner. **The configured table is as shown below:**

