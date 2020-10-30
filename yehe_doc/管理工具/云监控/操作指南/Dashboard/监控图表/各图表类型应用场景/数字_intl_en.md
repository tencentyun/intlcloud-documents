This document describes the use cases and the operations directions of numerical charts.

## Use Cases

**Numerical chart**: is applicable to metric values within a period of time. Examples include TCP links, public network outbound packets, and private network inbound packets.

**Configuration effects of numerical charts:**
![](https://main.qcloudimg.com/raw/bb2b9328854f43f41c1745c6f2205533.png)

## Directions

1. Log in to the Cloud Monitor console and click [Default Dashboard](https://console.cloud.tencent.com/monitor/dashboard2/default).
2. Click **<img src="https://main.qcloudimg.com/raw/09d4ca5824542316bf485350e4d5f62f.png" width="3%"></img>** > **Create a Chart**.
3. In the chart configuration module, select “Numerical” as the chart type.
4. Configure the numerical chart information.


#### Chart elements

- **Statistical Mode**: indicates the metric statistical mode, which can be the current value, the minimum value, the maximum value, the average value, or the sum.
- **Unit**: indicates whether to display the unit of the statistical value. For more information on the meanings of different units, see [List of Units](https://intl.cloud.tencent.com/document/product/248/38478#step1).
- **Hide Curve**: indicates whether to hide curves.
- **Precision**: indicates the number of decimal places to be retained for the metric statistical value. 0: do not retain decimals. 1: retain one decimal place.

#### Threshold

- **Threshold**: indicates the threshold for colors. Format: `<Numerical value>,<Numerical value>`. For example, if you enter `50,80`, it means that the displayed color of the metric will be green if the metric value is less than 50, orange if the metric value is equal to or greater than 50 but less than 80, and red if the metric value is equal to or greater than 80.
- **Color**: indicates the color sequence. For example, set the "Threshold" field to `50,80`.
  **Non-reverse cases:**
	- If the metric value is less than 50, display <font color="#78bd6d">green</font>.
	- If the metric value is equal to or greater than 50 but less than 80, display <font color="#ff7f47">orange</font>.
	- If the metric value is equal to or greater than 80, display <font color="#f54e4e">red</font>.

 **Reverse cases:**
	- If the metric value is less than 50, display <font color="#f54e4e">red</font>.
	- If the metric value is equal to or greater than 50 but less than 80, display <font color="#ff7f47">orange</font>.
	- If the metric value is equal to or greater than 80, display <font color="#78bd6d">green</font>.
