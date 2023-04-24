## Live Clipping

The fees incurred for editing out a clip before a live stream ends.
Below are the pricing details:

| Billable Item       | Price (USD/Min) | Billed By                   |
| :----------- | :---------------- | -------------------------- |
| Real-time clipping | 0.00098            | The duration of the output file. |

#### Billing details

- **Billable items**: Real-time clipping.
- **Billing rules**: Fees are incurred for creating a clip before a live stream ends.
- **Formula**: Live clipping fees = The duration of the file generated (min) x The unit price (USD).

#### Billing example

Suppose you used the ** Real-time clipping** feature on January 1 and generated a 100-min clip. On January 2, you would need to pay the following live clipping fee:

0.00098 (USD/min) x 100 (min) = 0.098 (USD)

To learn more about live clipping, see [Live Stream Clipping](https://www.tencentcloud.com/document/product/266/49280).



## Client Upload Acceleration

The fees incurred for using the client upload acceleration feature (global network acceleration or QUIC transmission) are based on the volume of traffic accelerated.
Below are the pricing details:

| Type     | Price         |
| :----------- | :----------- |
| Global network transmission | 0.072 USD/GB |
| QUIC transmission    | 0.086 USD/GB |

#### Billing details

- **Billable items**: Global network acceleration traffic and QUIC transmission traffic
- **Billing rules**: Client upload acceleration fees are charged based on the volume of traffic consumed when files are uploaded from clients.
- **Formula**: Client upload acceleration fees = Global network acceleration traffic (GB) x Unit price (USD/GB) + QUIC transmission traffic (GB) x Unit price (USD/GB)

#### Billing example

Suppose you used the global network acceleration feature to upload 550 GB of data and used the QUIC transmission feature to upload 100 GB of data. The upload acceleration fee incurred would be 550 (GB) x 0.072 (USD/GB) +100 (GB) x 0.086 (USD/GB) = 48.2 (USD).

To learn more about client upload acceleration, see [Client Upload Acceleration](https://www.tencentcloud.com/document/product/266/49083).

## UGSV SDK License

About UGSV licenses:

- You can apply for a 28-day trial license for UGSV Standard for free.
- The acceleration, storage, and traffic resources you use with the UGSV SDK are billed according to the billing rules of VOD.
- Licenses are not refundable once activated.


#### Pricing

| Edition               | Validity Period | Price (USD) |
| ------------------ | ------ | ------------ |
| Trial     | 28 days   | 0            |
| Lite     | 1 year    | 1,899          |
| Standard     | 1 year    | 9,999         |

To learn about the features of different editions, see [SDK Download](https://intl.cloud.tencent.com/document/product/1069/37914).
