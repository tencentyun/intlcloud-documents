### Billing details

The StreamLink service is managed at the flow level in the StreamLink console, and each flow corresponds to a stream transfer link. You can quickly and stably transfer video and comprehensively monitor the quality of the video streams during the transfer in the console. The table below lists its billing details.

| Billable Item | Description | Billing Mode |
| -----------------| ---| --------- |
| Transfer |The transfer fee is charged based on the sum of the peak bandwidth used by each flow in a day. | Daily pay-as-you-go |
| Device running |The device running fee is charged based on the number of inputs and outputs and their running hours in a day. | Daily pay-as-you-go |
| Relaying traffic |If you relay video to third parties, you will be charged based on the amount of traffic relayed in a day. The pricing of relaying traffic varies with region. | Daily pay-as-you-go |

### Transfer

#### Pricing

You can create transfer links in the StreamLink console, which are charged based on the peak bandwidth used in a day.

| Billable Item | Billing Method | Price |
| -----------------| ---| --------- |
| Transfer|Peak outbound bandwidth in a day | 7.6923 USD/Mbps/day |

#### Billing example

Assume that you created flows A and B with StreamLink on January 1, 2022. The bandwidth usage of flow A and flow B peaked at 12:00 noon and 10:00 PM respectively, both reaching 10 Mbps. On January 2, 2022, you would be charged the following transfer fee:
7.6923 (USD/Mbps/day) x 20 (Mbps) = 153.846 USD



### Device running

#### Pricing

The device running cost of StreamLink is as follows:

| Billable Item     | Billing Method                               | Price             |
| ---------- | -------------------------------------- | ---------------- |
| Device running | Sum of the running hours of each input/output| 0.25 USD/input or output/hour |


>!
>- If a flow has 1 input and 3 outputs, the device running cost will quadruple.
>- If your task contains a primary flow and a backup flow, you will be charged the running cost of 2 flows.
>- The device running cost is calculated by the hour and charged on a daily basis, and durations are rounded to the next hour.

#### Billing example

Assume that you created 1 input and 2 outputs and used them for 6 hours on January 1, 2022. On January 2, 2022, you would be charged the following device running cost:

3 (number of inputs and outputs) x 6 (hours) x 0.25 (USD/hour) = 4.5 USD



### Relaying traffic

#### Pricing

If you use StreamLink to relay video to third parties, you will be charged relaying traffic fees. Relaying traffic is priced as follows:

| Region     | City     | Traffic Tier (Daily) | List Price (USD/GB) |
| :------- | -------- | ---------------- | ----------------- |
| Asia Pacific | Shanghai   | 0-300 GB          | 0.51              |
| Asia Pacific | Shanghai   | 300 GB - 1.5 TB       | 0.486             |
| Asia Pacific | Shanghai   | 1.5-5 TB        | 0.462             |
| Asia Pacific | Shanghai   |  ≥ 5 TB              | 0.438             |
| Asia Pacific | Chengdu   | 0-300 GB            | 0.402             |
| Asia Pacific | Chengdu   | 300 GB - 1.5 TB      | 0.378             |
| Asia Pacific | Chengdu   | 1.5-5 TB        | 0.354             |
| Asia Pacific | Chengdu   | ≥5TB             | 0.342             |
| Asia Pacific | Jakarta | 0-300 GB           | 0.198             |
| Asia Pacific | Jakarta | 300 GB - 1.5 TB     | 0.186             |
| Asia Pacific | Jakarta | 1.5-5 TB         | 0.174             |
| Asia Pacific | Jakarta | ≥5TB             | 0.162             |
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

>! For nodes outside the above listed regions, the pricing for “Others” applies.
