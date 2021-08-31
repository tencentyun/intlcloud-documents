This document describes the use cases of and the operations directions for dashboards.

## Use Cases

**Dashboard**: is applicable to percentage metrics such as the CPU utilization, memory usage, and disk utilization.

**Dashboard configuration effects:**
![](https://main.qcloudimg.com/raw/18bfc12b92695a6f62835a53e77ea7c7.png)

## Directions

1. Log in to the Cloud Monitor console and click **Dashboard** > **[Default Dashboard](https://console.cloud.tencent.com/monitor/dashboard2/default)** on the left sidebar.
2. Click **![](https://main.qcloudimg.com/raw/09d4ca5824542316bf485350e4d5f62f.png)** > **Create Chart** to go to the chart editing page.
3. In the chart configuration module, select dashboard as the chart type.
4. Configure the dashboard information.

#### Chart elements

- **Statistical mode**: indicates the metric statistical mode, which can be the current value, the minimum value, the maximum value, the average value, and the sum.
- **Unit**: indicates whether to display the unit of the statistical value. For more information on the meanings of different units, see [List of Units](https://intl.cloud.tencent.com/document/product/248/38478#step1).
- **Precision**: indicates the number of decimal places to be retained for the metric statistical value. 0: do not retain decimals. 1: retain one decimal place.

#### Threshold

- **Threshold**: indicates the thresholds for colors. Format: <Numerical value>,<Numerical value>. For example, if you enter "50,80" in this field, it means that the displayed color of the metric will be green when the metric value is less than 50, orange if the metric value is equal to or greater than 50 but less than 80, and red if the metric value is equal to or greater than 80.
- **Color**: indicates the color sequence. For example, set the "Threshold” field to "50,80".
  #### Non-reverse cases:
	- If the metric value is less than 50, display <font color="#78bd6d">green</font>.
	- If the metric value is equal to or greater than 50 but less than 80, display <font color="#ff7f47">orange</font>.
	- If the metric value is equal to or greater than 80, display <font color="#f54e4e">red</font>.

 #### Reverse cases:
	- If the metric value is less than 50, display <font color="#f54e4e">red</font>.
	- If the metric value is equal to or greater than 50 but less than 80, display <font color="#ff7f47">orange</font>.
	- If the metric value is equal to or greater than 80, display <font color="#78bd6d">green</font>.
		![](https://main.qcloudimg.com/raw/507aff74e6af82b156abeb830f60ea19.png)
- **Min, Max**: indicates the minimum and maximum values displayed on the dashboard.
- **Show Threshold**: indicates whether to display the threshold for each color on the dashboard.

