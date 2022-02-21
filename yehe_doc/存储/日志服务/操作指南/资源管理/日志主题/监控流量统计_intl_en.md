### Traffic

| Metric                   | Meaning                                       | Unit | Dimension       |
| ---------- | ---------------------------- | ---------------------------------------------- | ---- | 
| Write traffic                | Traffic incurred during log upload                        | MB   | Log topic ID |
| Index traffic                | Traffic incurred after the index feature is enabled                         | MB   | Log topic ID |
| Private network read traffic | Private network read traffic incurred when a log is downloaded, consumed, or shipped via a private network | MB   | Log topic ID |
| Public network read traffic | Public network read traffic incurred when a log is downloaded, consumed, or shipped via a public network | MB   | Log topic ID |
| Read traffic                 | Total private and public network read traffic                             | MB   | Log topic ID |

### Storage capacity

| Metric             | Meaning                     | Unit | Dimension       |
| ---------- | ---------------------- | ---------------------------- | ---- | 
| Log storage capacity   | Storage capacity occupied by log data | MB   | Log topic ID |
| Index storage capacity | Storage capacity occupied by index data | MB   | Log topic ID |
| Storage Capacity       | Total storage capacity occupied by log and index data   | MB   | Log topic ID |

### Service request quantity

| Metric       | Meaning                                                     | Unit  | Dimension       |
| ---------- | ---------------- | ------------------------------------------------------------ | ----- |
| Service requests | Number of requests that users use LogListener, API, or SDK to call CLS APIs, including read and write requests such as upload and download, creation and deletion, and search and analysis | COUNT | Log topic ID |


>? The preceding monitoring metrics are reported to Cloud Monitor. For the corresponding detailed metrics and parameters, please see the CLS monitoring metrics.
>



