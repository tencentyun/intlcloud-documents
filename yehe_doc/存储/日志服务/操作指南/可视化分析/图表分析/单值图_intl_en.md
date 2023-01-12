An individual value plot describes a single metric, typically a key metric of business value. It is suitable for collecting daily, weekly, or monthly metrics such as PV and UV.

## Chart Configuration

### General configuration



| Configuration Item | Description |
| -------- | -------------------------------------------------------- |
| Basic information | Chart Name: Set the display name of the table, which can be left empty.                                 |
| Standard configuration | Set the unit of all metric-type fields in the chart. For more information, see [Unit Configuration](https://intl.cloud.tencent.com/document/product/614/47788).     |


### Changes



| Configuration Item | Description |
| -------- | ------------------------------------------------------------ |
| Changes | After the changes feature is enabled, you can compare the data in a time period with the data in the same period X hours, days, months, or years ago. You can choose to compare absolute values or percentages. |


### Individual value plot configuration



| Configuration Item        | Description                                                         |
| ------ | ------------------------------------------------------------ |
| Individual value plot | Display: Control whether to display metric names on the individual value plot.<br />Value: If a metric has multiple statistical results, they need to be aggregated to one value or one of them needs to be selected for display on the individual value plot. By default, the latest non-null value will be used.<br />Metric: Set the target statistical metric, which is **Auto** by default, in which case the first metric field in the returned data will be selected.<br /> |

**Statistical method example:**
Three data entries are returned, and the latest non-null value will be selected by default, that is, the last value `383` will be displayed. If you set **Value** to **Sum**, the sum of the three data entries will be displayed.



### Threshold configuration



| Configuration Item | Description |
| -------- | ------------------------------------------------------------ |
| Threshold configuration | Threshold point: Set the threshold points. You can add multiple threshold intervals. You can click a threshold color to open the color picker to customize the color. |


