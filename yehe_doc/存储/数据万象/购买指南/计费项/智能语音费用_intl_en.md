CI provides various audio processing services such as speech recognition, text-to-speech, and voice/sound separation.

## Smart Audio Fees

Smart audio fees refer to the fees incurred by using [smart audio features](https://www.tencentcloud.com/document/product/1045/49894) such as speech recognition, text-to-speech, and noise reduction.

| Billable Item               | Description                                                   | Billing Cycle | Applicable Billing Mode                                         |
| :----------- | :------------------------------------------------------- | :------- | :------------- |
| Voice/Sound separation fees       | Fees incurred by using the voice/sound separation service. Such fees are charged by the **output file duration**.     | Monthly | Pay-as-you-go |
| Text-to-speech fees       | Fees incurred by using the text-to-speech service. Such fees are charged by the **number of input characters**.       | Monthly | Pay-as-you-go |
| Noise reduction fees       | Fees incurred by using the noise reduction service. Such fees are charged by the **audio processing duration**.     | Monthly | Pay-as-you-go |

## Smart Audio Pricing

### Text-to-speech pricing

| Number of Input Characters | Price (USD/10,000 Characters) |
| :---------------------- | :------------------ |
| 0 < input characters ≤ 190,000       | 0.4422              |
| 190,000 < input characters ≤ 990,000    | 0.4127              |
| 990,000 < input characters ≤ 9,990,000   | 0.3832              |
| 9,990,000 < input characters ≤ 39,990,000 | 0.3538              |
| Input characters > 39,990,000         | 0.3243              |

> ?
>
> The text-to-speech service is billed in a cumulative manner at tiered prices.
> For example, if you use the text-to-speech service for 890,000 characters this month, you need to pay 19 * 0.4422 + (89 - 19) * 0.4127 = 37.2908 USD.

### Pricing of other features

| Feature | Price |
| :------- | :--------------- |
| Voice/Sound separation       | 0.012 USD/min |
| Noise reduction | 0.01194 USD/min |

## Billing Example

You operate an online audio processing website. Visitors can upload their own videos to the website for noise reduction and voice/sound separation and then download output voice files. You store the website content in a COS bucket in **Guangzhou region** and use the **CI** service.

### Demand

10,000 hours of fast speech recognition and 5,000 minutes of voice/sound separation per month.

### Monthly Fees Calculation

| Item | Free Tier | Unit Price | Billable Usage | Fees (Unit Price * Billable Usage) |
| :----------- | :------- | :--------------- | :------------- | :--------------------- |
| Noise reduction     | 0        | 0.01194 USD/min | 0.01194*10,000 | 119.4 USD             |
| Voice/Sound separation | 0        | 0.012 USD/min   | 0.012*5000     | 60 USD                |
| **Monthly fees**   | -        | -                | -              | **179.4 USD**            |

> ?After you understand the composition of smart audio fees and the description of billable items, you can evaluate the required amount of resources based on your own business needs and then use the [CI price calculator](https://intl.cloud.tencent.com/pricing/ci) to calculate fees and export the budget list.
