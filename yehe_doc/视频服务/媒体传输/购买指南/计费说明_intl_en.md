### Overview

StreamLink services are managed at the flow level in the StreamLink console. Each flow may include multiple transfer connections with different input and output regions. You can quickly and stably transfer media using StreamLink and comprehensively monitor the stream quality in the console. The billable items of StreamLink are as follows:

| Billable Item | Description | Billing Mode |
| -----------------| ---| --------- |
| Transfer |Transfer fees are charged based on the sum of the peak bandwidth used by each connection in a day. | Daily pay-as-you-go |
| Device running |Device running fees are charged for each input and output based on the task duration. | Daily pay-as-you-go |
| Relaying traffic |If you relay data to third parties, a relaying traffic fee will be charged based on the amount of outbound traffic consumed. The price varies with the output region. | Daily pay-as-you-go |

### Transfer

#### Pricing

In StreamLink, a connection is a transfer between each input region and output region of a flow. The system calculates the peak bandwidth of each active connection in a day and add them up. The transfer fee for each flow is calculated separately. If you configure failover, when the system calculates the transfer fee, the primary connection and backup connection will be considered one connection.

| Billable Item | Billed By| Price |
| -----------------| ---| --------- |
| Transfer|The peak bandwidth of each active connection in a day. | 7.6923 USD/Mbps/day |

#### Billing example

Assume that on January 1, 2023, you created two flows (flow A and flow B) and added a connection (an input and an output) for each of them. The connection of flow A reached a peak bandwidth of 10 Mbps at noon, and the connection of flow B reached a peak bandwidth of 10 Mbps at 22:00 PM. On January 2, 2023, the following transfer fee would be billed:
7.6923 (USD/Mbps/day) x 20 (Mbps) = 153.846 USD


### Device Running

#### Pricing

Device running fees are charged for each input and output based on the task duration.

| Billable Item     | Billed By                               | Price             |
| ---------- | -------------------------------------- | ---------------- |
| Device running | The active hours of each input/output. | 0.25 USD/hour |

>!
>- If a flow has one input and three outputs, the device running cost will quadruple.
>- The device running cost is calculated separately for the primary and backup flow.
>- Task duration is calculated by the hour (rounded to the next hour). Fees are billed daily.

#### Billing example

Assume that you created a task with one input and two outputs on January 1, 2023. The task lasted for six hours. On January 2, 2023, the following device running fee would be billed:

3 (number of inputs and outputs) x 6 (hours) x 0.25 (USD/hour) = 4.5 USD

### Relaying Traffic

#### Pricing

Relaying traffic fees will be incurred if you use StreamLink to relay streams to a third-party service. The fees are charged based on the outbound traffic. The price varies with the outbound region.

| Region     | City     | Traffic Tier (Daily) | List Price (USD/GB) |
| :------- | -------- | ---------------- | ----------------- |
| Asia Pacific     | Shanghai     | 0-300 GB          | 0.51              |
| Asia Pacific     | Shanghai     | 300 GB - 1.5 TB      | 0.486            |
| Asia Pacific     | Shanghai     | 1.5-5 TB      | 0.462            |
| Asia Pacific     | Shanghai     | ≥ 5 TB             | 0.438             |
| Asia Pacific     | Chengdu     | 0-300 GB          | 0.402             |
| Asia Pacific     | Chengdu     | 300 GB - 1.5 TB      | 0.378            |
| Asia Pacific     | Chengdu     | 1.5-5 TB      | 0.354            |
| Asia Pacific     | Chengdu     | ≥ 5 TB             | 0.342             |
| Asia Pacific     | Jakarta   | 0-300 GB          | 0.198             |
| Asia Pacific     | Jakarta   | 300 GB - 1.5 TB          | 0.186            |
| Asia Pacific     | Jakarta   | 1.5-5 TB          | 0.174            |
| Asia Pacific     | Jakarta   | ≥ 5 TB             | 0.162             |
| Asia Pacific     | Hong Kong     | 0-300 GB          | 0.1176            |
| Asia Pacific     | Hong Kong     | 300 GB - 1.5 TB      | 0.0833            |
| Asia Pacific     | Hong Kong     | 1.5-5 TB      | 0.0804            |
| Asia Pacific     | Hong Kong     | ≥ 5 TB             | 0.0784            |
| Asia Pacific     | Singapore   | 0-300 GB          | 0.1200            |
| Asia Pacific     | Singapore   | 300 GB - 1.5 TB          | 0.0850            |
| Asia Pacific     | Singapore   | 1.5-5 TB          | 0.0820            |
| Asia Pacific     | Singapore   | ≥ 5 TB             | 0.0800            |
| Asia Pacific     | Tokyo     | 0-300 GB          | 0.1368            |
| Asia Pacific     | Tokyo     | 300 GB - 1.5 TB      | 0.1068            |
| Asia Pacific     | Tokyo     | 1.5-5 TB      | 0.1032            |
| Asia Pacific     | Tokyo     | ≥ 5 TB             | 0.1008            |
| Asia Pacific     | Seoul     | 0-300 GB          | 0.1260            |
| Asia Pacific     | Seoul     | 300 GB - 1.5 TB      | 0.1220            |
| Asia Pacific     | Seoul     | 1.5-5 TB      | 0.1170            |
| Asia Pacific     | Seoul     | ≥ 5 TB             | 0.1080            |
| Asia Pacific     | Bangkok     | 0-300 GB          | 0.1093            |
| Asia Pacific     | Bangkok     | 300 GB - 1.5 TB      | 0.0850            |
| Asia Pacific     | Bangkok     | 1.5-5 TB      | 0.0820            |
| Asia Pacific     | Bangkok     | ≥ 5 TB             | 0.0800            |
| Asia Pacific     | Mumbai     | 0-300 GB          | 0.1093            |
| Asia Pacific     | Mumbai     | 300 GB - 1.5 TB      | 0.0850            |
| Asia Pacific     | Mumbai     | 1.5-5 TB        | 0.0820            |
| Asia Pacific     | Mumbai     | ≥ 5 TB             | 0.0800            |
| US     | Santa Clara | 0-300 GB          | 0.0900            |
| US     | Santa Clara | 300 GB - 1.5 TB          | 0.0850            |
| US     | Santa Clara | 1.5-5 TB          | 0.0700            |
| US     | Santa Clara |  ≥ 5 TB          | 0.0500            |
| Europe     | Frankfurt | 0-300 GB          | 0.0900            |
| Europe     | Frankfurt | 300 GB - 1.5 TB          | 0.0850            |
| Europe     | Frankfurt | 1.5-5 TB          | 0.0700            |
| Europe     | Frankfurt | ≥ 5 TB             | 0.0500            |
| South America   | Sao Paulo    | 0-300 GB          | 0.1500            |
| South America   | Sao Paulo    | 300 GB - 1.5 TB          | 0.1380            |
| South America   | Sao Paulo    | 1.5-5 TB          | 0.1260            |
| South America   | Sao Paulo   | ≥ 5 TB             | 0.1140            |
| Others | -        | 0-300 GB          | 0.1500            |
| Others | -        | 300 GB - 1.5 TB      | 0.1380            |
| Others | -        | 1.5-5 TB        | 0.1260            |
| Others | -        | ≥ 5 TB             | 0.1140            |

>! For nodes outside the above listed regions, the pricing for "Others" applies.
