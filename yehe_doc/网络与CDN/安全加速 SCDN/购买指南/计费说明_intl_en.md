Integrating with Tencent Cloud CDN and ECDN services, Tencent Cloud SCDN can deliver an all-round protection for your business.

## Billing Overview

SCDN billable items are listed in the following table:

| Billable Item          | Description                                                         | Required         | Billing Method                                                     | Billing Rule                                                     |
| ----------------- | ------------------------------------------------------------ | ---------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| CDN/ECDN service | Basic service fee covering traffic, bandwidth, and the number of requests       | Yes               | [CDN Billing](https://buy.intl.cloud.tencent.com/pricing/cdn)/[ECDN Billing](https://intl.cloud.tencent.com/product/ecdn) | [CDN Billing](https://buy.intl.cloud.tencent.com/pricing/cdn)/[ECDN Billing](https://intl.cloud.tencent.com/product/ecdn) |
| SCDN plan  | The base plan is available in basic edition and standard edition and includes 20 basic protected domain names, basic web attack protection limit, and DDoS/CC attack base protection. The bot protection plan includes a basic bot protection limit. | Yes | Prepaid in the monthly subscription billing mode, with auto-renewal supported. | Monthly subscription for up to 36 months. |
| Elastic protection | When the DDoS/CC/bot attacks exceed the base protection limit of an SCDN plan, excessive protection will be charged in a pay-as-you-go manner. | According to the actual elastic protection peak. | Postpaid and settled on a daily basis. The total consumption generated from 00:00:00 to 23:59:59 on a day will be calculated and charged before 18:00 the next day. | Tiered pricing. |
| Domain name extension pack | When the number of domain names that need to be connected to SCDN exceeds the number supported by a plan, you can purchase domain name extension packs to connect more domain names. | No | Prepaid in the monthly subscription billing mode, with auto-renewal supported. | Purchasable as needed, with the same expiration time as the SCDN plan. |

> !For more information on product purchase and usage, [contact us](https://intl.cloud.tencent.com/contact-sales).

## CDN/ECDN Service Fee

To enable SCDN, you need to connect your domain names to CDN/ECDN and enable the service. CDN and ECDN services are charged based on their product pricing. You can choose a billing mode suitable for your business form. For the billing details of CDN and ECDN, see the following:

- [CDN Pricing](https://buy.intl.cloud.tencent.com/pricing/cdn)
- [ECDN Pricing](https://intl.cloud.tencent.com/product/ecdn)

## SCDN Plan

An SCDN plan is prepaid in the monthly subscription billing mode for up to 36 months and supports auto-renewal. SCDN provides multiple plan editions for your choice based on your business and security requirements.

### SCDN plan (Chinese mainland)

| Plan                | Basic | Standard |
| ----------------------- | -------------- | -------------- |
| Domain names provided with basic protection  | 20             | 20             |
| DDoS protection (Gbps)   | 10             | 20             |
| CC protection (QPS)      | 60,000         | 60,000         |
| Web protection (QPS)     | 2,500          | 5,000          |
| Elastic protection                | Unavailable         | Available           |
| *Price* (USD/month)** | 542.86         | 2,811.43        |

> ?
>
> 1. The number of protected domain names can be added by purchasing domain name extension packs.
> 2. A standard SCDN plan supports elastic protection, while a basic SCDN plan doesn't. The excessive protection is postpaid at the unit price in the corresponding tier reached by the daily attack defense peak.

### Basic bot protection plan

| Plan                | Description |
| ----------------------- | -------- |
| Basic bot protection (QPS)     | 1,000     |
| **Price (USD/month)** | 142.86   |

> ?
>
> 1. The basic bot protection plan is optional.
> 2. You need to purchase an **SCDN plan** before purchasing a basic bot protection plan.
> 3. The purchase duration of the basic bot protection plan cannot be longer than that of the **SCDN plan**.



## Elastic Protection

After you purchase a standard SCDN plan, elastic protection will be enabled when DDoS/CC/bot attacks exceed the protection limit.

### Elastic DDoS/CC protection

SCDN provides protection capabilities of up to 1 Tbps (for DDoS attacks) or 1500,000 QPS (for CC attacks). It is postpaid at the unit price in the corresponding tier reached by the daily attack defense peak as listed below:

| Daily DDoS Peak Tier            | Daily CC Peak Tier                    | Price (USD/Day) |
| -------------------------- | --------------------------------- | --------------- |
| 20 Gbps - 30 Gbps (inclusive)    | 60,000 QPS - 100,000 QPS (inclusive)   | 225.71          |
| 30 Gbps - 40 Gbps (inclusive)   | 100,000 QPS - 130,000 QPS (inclusive)  | 397.14          |
| 40 Gbps - 50 Gbps (inclusive)    | 130,000 QPS - 160,000 QPS (inclusive)  | 568.57          |
| 50 Gbps - 60 Gbps (inclusive)   | 160,000 QPS - 200,000 QPS (inclusive)  | 740.00          |
| 60 Gbps - 70 Gbps (inclusive)    | 200,000 QPS - 230,000 QPS (inclusive)  | 1,168.57         |
| 70 Gbps - 80 Gbps (inclusive)   | 230,000 QPS - 260,000 QPS (inclusive)  | 1,454.29         |
| 80 Gbps - 100 Gbps (inclusive)   | 260,000 QPS - 300,000 QPS (inclusive)  | 1,668.57         |
| 100 Gbps - 150 Gbps (inclusive)  | 300,000 QPS - 450,000 QPS (inclusive)  | 2,097.14         |
| 150 Gbps - 200 Gbps (inclusive)  | 450,000 QPS - 600,000 QPS (inclusive)  | 2,382.86         |
| 200 Gbps - 300 Gbps (inclusive)  | 600,000 QPS - 800,000 QPS (inclusive)  | 3,097.14         |
| 300 Gbps - 500 Gbps (inclusive)  | 800,000 QPS - 1,000,000 QPS (inclusive) | 3,525.71         |
| 500 Gbps - 1,000 Gbps (inclusive) | 1,000,000 QPS - 1,500,000 QPS (inclusive) | 5,240.00         |

> !
>
> 1. If you purchase a standard SCDN plan, elastic protection against DDoS/CC attacks will be enabled by default.
> 2. When both DDoS attacks and CC attacks exceed the protection limit of the SCDN plan and the daily peaks fall into different tiers, the higher tier price shall prevail.
> 3. WAF doesn't support elastic protection for now. If the QPS protection limit of the plan is exceeded, no protection will be conducted.

### Elastic bot protection

Elastic bot protection supports the pay-as-you-go billing mode and is settled on a daily basis:

| QPS Tier   | Price (USD/QPS/Day) |
| -------------- | ------------------- |
| 0 - 10,000 QPS  | 0.0286              |
| > 10,000 QPS | 0.0143              |

> !
>
> 1. Purchase any SCDN plan (basic/standard) to enable **elastic bot protection** optionally.
> 2. Elastic bot protection is not enabled by default. You can enable it by yourself after purchasing a basic plan.



## Domain Name Extension Pack

An SCDN plan supports connecting 20 protected acceleration domain names by default. You can connect more domain names by purchasing a **domain name extension pack**. Each pack includes 10 domain names. It is prepaid in the monthly subscription billing mode and has the same validity period as the plan.

Up to 50 domain name extension packs can be purchased for one SCDN plan (that is, a maximum of 520 protected acceleration domain names can be connected) for up to 36 months, and their auto-renewal configuration is the same as that of the plan. The pack price is as follows:

| Value-Added Service | Price (USD/Unit/Month) |
| --------------------------- | ------------------ |
| Domain name extension pack (10 additional domain names) | 142.86 |

> ! In addition to purchasing domain name extension packs when activating a plan, you can also purchase or remove domain name extension packs subsequently according to your business needs. Remove packs are non-refundable.

## VIP Customer Billing Plan

If you spend more than USD 15,000 on Tencent Cloud CDN or ECDN services per month, you can [contact us](https://intl.cloud.tencent.com/contact-sales) to customize an optimal plan.
