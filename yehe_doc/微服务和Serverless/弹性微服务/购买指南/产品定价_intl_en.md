
## Billable Items and Unit Prices
See below for the pricing details of TEM service:

<table>
    <tr>
        <th>Category</th><th>Item</th><th>Unit price</th>
    </tr>
    <tr>
        <td>Environment</td><td>Environment</td><td>0.00024876 USD/environment/minute</td>
    </tr>
    <tr>
        <td rowspan="2">Application</td><td>CPU</td><td> 0.00031344 USD/core/minute</td>
    </tr>
    <tr>
        <td>MEM</td><td> 0.0001195 USD/GiB/minute</td>
    </tr>
</table>

## Billing Example
See below for the billing example.

- An environment is created on August 1, 2022 at 10:00:10, and then terminated on August 1, 2022 at 10:29:40.
- An application is deployed in the environment on August 1, 2022 at 10:15:20, with five 1C2GiB instances created. All the instances are stopped on August 1, 2022 at 10:24:59.
- There are no other TEM resources in used.

In the case, the billing for the TEM service is calculated as below: 

<table>
    <tr>
        <th>Category</th><th>Spec</th><th>Duration (one minute minimum charge)</th><th>Amount</th>
    </tr>
    <tr>
        <td>Environment fee</td><td>One</td><td>30 mins (Aug/1/2022 10:29:40 - Aug/1/2022 10:00:10 = 29 mins 30 secs)</td><td>0.0074628 USD (0.00024876 * 1 * 30)</td>
    </tr>
    <tr>
        <td>Application fee</td><td>Five 1C2GiB instances</td><td>10 mins (Aug/1/2022 10:24:59 - Aug/1/2022 10:15:20 = 9 mins 39 secs </td><td> 0.027622 USD (5 * (1 * 0.00031344 + 2 * 0.0001195) * 10)</td>
    </tr>
</table>

The total cost is 0.0350848 (0.0074628+0.027622) USD.
