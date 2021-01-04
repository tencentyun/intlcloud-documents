<span id="record_que1"></span>
### How is LVB recording billed?
LVB recording is billed by the peak number of concurrent recording channels in the current month, and the total number of recording channels in a statistical period is the concurrent channel peak. A single live stream recorded in one file format is counted as one recording channel. If you record in two formats (MP4 and HLS), they will be counted as two recording channels.

<span id="record_que2"></span>

### How is the LVB recording channel peak calculated?
When one live stream (one stream ID) is recorded in one file format, it will be counted as one LVB recording channel. The number of current recording channels is queried once every 5 minutes, and the maximum value of sample points in the current month will be used as the monthly recording channel peak for billing.
**Sample:**

<style>#ye{background:#ffe699;}#gr{background:#c6e0b4;}#br{background:#bdd7ee}</style>
<table id="rroad">
<tr><th rowspan=2 width="10%" style="text-align:center;">Stream ID</th>
<th rowspan=2 width="10%" style="text-align:center;">Recording <br>File Format</th>
<th colspan=7 width="50%" style="text-align:center;">Current Month (Day 01–30)</th>
</tr><tr>
<td style="text-align:center;">01</td><td style="text-align:center;">02</td><td style="text-align:center;">03</td>
<td style="text-align:center;">...</td>
<td style="text-align:center;">28</td><td style="text-align:center;">29</td><td style="text-align:center;">30</td>
</tr><tr>
<td rowspan=4 style="text-align:center;">A</td>
<td style="text-align:center;">HLS</td><td></td><td></td><td></td>
<td rowspan=13 style="text-align:center;">No recording</td>
<td id="ye"></td><td id="ye"></td>
<td></td>
</tr><tr>
<td style="text-align:center;">MP4</td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td>
</tr><tr>
<td style="text-align:center;">FLV</td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td></td>
</tr><tr>
<td style="text-align:center;">AAC</td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td>
</tr><tr>
<td rowspan=4 style="text-align:center;">B</td>
<td style="text-align:center;">HLS</td><td></td><td id="gr"></td><td id="gr"></td><td id="gr"></td><td></td><td></td>
</tr><tr>
<td style="text-align:center;">MP4</td><td id="gr"></td><td id="gr"></td><td></td><td id="gr"></td><td id="gr"></td><td></td>
</tr><tr>
<td style="text-align:center;">FLV</td><td></td><td id="gr"></td><td></td><td id="gr"></td><td></td><td id="gr"></td>
</tr><tr>
<td style="text-align:center;">AAC</td><td></td><td id="gr"></td><td></td><td id="gr"></td><td></td><td></td>
</tr><tr>
<td rowspan=4 style="text-align:center;">C</td>
<td style="text-align:center;">HLS</td><td id="br"></td><td></td><td id="br"></td><td id="br"></td><td></td><td></td>
</tr><tr>
<td style="text-align:center;">MP4</td><td></td><td></td><td id="br"></td><td id="br"></td><td id="br"></td><td id="br"></td>
</tr><tr>
<td style="text-align:center;">FLV</td><td></td><td></td><td></td><td id="br"></td><td></td><td></td>
</tr><tr>
<td style="text-align:center;">AAC</td><td></td><td></td><td></td><td></td><td></td><td id="br"></td>
</tr><tr>
<td colspan=2 style="text-align:center;">Recording channels</td>
<td style="text-align:center;">5</td><td style="text-align:center;">7</td><td style="text-align:center;">6</td><td style="text-align:center;">11</td><td style="text-align:center;">6</td><td style="text-align:center;">5</td>
</tr><tr>
<td colspan=2 style="text-align:center;">Recording channel peak</td><td colspan=7 style="text-align:center;">11</td>
</tr>
</table>

>? 
>- Yellow: recording task under stream ID **A**.
>- Green: recording task under stream ID **B**.
>- Blue: recording task under stream ID **C**.




<span id="record_que3"></span>
### Why is 10.5882 USD charged when I use LVB recording? 
If two live streams are recorded simultaneously or one live stream is recorded into two file formats, two recording channels will be generated. Recording is billed by the recording channel peak at a price of 5.2941 USD per channel per month, so if there are two channels in the month, then the fees will be 10.5882 USD. For more information, please see [LVB Recording Billing](https://intl.cloud.tencent.com/zh/document/product/267/2818#.E7.9B.B4.E6.92.AD.E5.BD.95.E5.88.B6).
We recommend you go to **Bill Details** > [Bill by Instance](https://console.cloud.tencent.com/expense/bill/summary)** in the Billing Center to check the billing details of LVB recording. You can click **Bill Details** in the "Operation" column to view the actual recording channel peak of the last month.

<span id="record_que4"></span>

### Why are fees still incurred when I don't use LVB recording for a long time?
We recommend you go to the [VOD console](https://console.cloud.tencent.com/vod/overview) to check whether there are recording files stored.
- If so, no more fees will be incurred after you delete the files.
- If not, please go to **Bill Details** > [Bill by Instance](https://console.cloud.tencent.com/expense/bill/summary)** in the Billing Center to check the billing details.




