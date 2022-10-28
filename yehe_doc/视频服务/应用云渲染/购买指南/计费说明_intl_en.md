CAR is billed by application rendering **concurrency**. A concurrency represents the collection of virtual computing resources, including CPU, bandwidth, disk, and GPU, required for one user to render your application content. **Each concurrency supports access by only one user at a time**; that is, if 100 concurrencies are purchased, 100 users can access the cloud rendering environment at the same time, and excessive users need to queue up to wait for a concurrency to become available.

## CAR concurrency scales

| Concurrency Scale | CPU        | Memory      | GPU         | Video Memory    | Bandwidth    | Minimum quantity for sale |
| ---------------------- | ---------------------- | ---------------------- | ---------------------- | ---------------------- | ---------------------- |---------------------- |
| S - For rendering small applications    | 4-core vCPU or above  | 8 GB or above  | 2 TF SP/30T INT or above   | 4 GB or above  | Up to 8 Mbps | 1 concurrency (1 concurrent user) |
| M - For rendering medium-sized applications    | 4-core vCPU or above  | 16 GB or above | 4 TF SP/30T INT or above   | 6 GB or above  | Up to 8 Mbps |1 concurrency (1 concurrent user) |
| L - For rendering large applications    | 10-core vCPU or above  | 32 GB or above | 8.1 TF SP/30T INT or above   | 12 GB or above  | Up to 8 Mbps |1 concurrency (1 concurrent user) |


>? The main metrics for the GPU performance are floating-point operations capabilities.
>- TF indicates floating-point operations per second (FLOPS).
>- SP indicates single-precision floating-point operations.
>- DP indicates double-precision floating-point operations.
>- INT8 indicates INT8 integer operations.

## Pricing for CAR concurrency
<table>
<thead>
<tr>
<th>Billing Mode</th>
<th>Billable Item</th>
<th>Billing Cycle</th>
<th>Singapore (USD/Concurrent User/Cycle)</th>
<th>Tokyo (USD/Concurrent User/Cycle)</th>
<th>Seoul (USD/Concurrent User/Cycle)</th>
</tr>
</thead>
<tbody><tr>
<td rowspan=3>Prepaid - Monthly subscription</td>
<td>S - For rendering small applications</td>
<td rowspan=3>Monthly</td>
<td>398</td>
<td>374</td>
<td>460</td>
</tr>
<tr>
<td>M - For rendering medium-sized applications</td>
<td>612</td>
<td>588</td>
<td>661</td>
</tr>
<tr>
<td>L - For rendering large applications</td>
<td>1041</td>
<td>1016</td>
<td>1064</td>
</tr>
<tr>
<td rowspan=3>Prepaid - Daily subscription</td>
<td>S - For rendering small applications</td>
<td rowspan=3>Daily</td>
<td>40</td>
<td>38</td>
<td>46</td>
</tr>
<tr>
<td>M - For rendering medium-sized applications</td>
<td>62</td>
<td>59</td>
<td>67</td>
</tr>
<tr>
<td>L - For rendering large applications</td>
<td>105</td>
<td>102</td>
<td>107</td>
</tr>
</tbody></table>

>?Currently, concurrency packs in North America and Europe are in beta testing. To try them out, please contact us.
