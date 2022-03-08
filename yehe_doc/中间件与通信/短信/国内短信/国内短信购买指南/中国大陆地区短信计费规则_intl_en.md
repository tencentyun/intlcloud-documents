## SMS Length Calculation Rule


- SMS length = number of characters in SMS signature + number of characters in SMS body, as detailed below:
 [] are counted into the number of characters in the SMS signature; for example, [ABC] is counted as five characters.
- One letter, digit, punctuation mark (both fullwidth and halfwidth forms), or space is counted as 1 character.
- Some special symbols are counted as multiple characters; for example, an emoji is counted as two characters. When creating templates and sending bulk SMS messages, you need to pay special attention to the billable character count displayed in the console If there are special symbols in the template or SMS body.
- If a Chinese Mainland SMS message (signature + body) contains no more than 70 characters, it will be billed as one message; otherwise, it will be billed as multiple messages based on the standard of 67 characters per message, but it will still be displayed as one message.

 

For example, if an SMS message contains 150 characters, it will be billed as three messages (67 + 67 + 16 characters).

- A single SMS message can contain up to 500 characters.


>! Due to the different policies of carriers in different regions, Chinese Mainland SMS messages must carry a signature enclosed in [].

## Billing Mode

 Chinese Mainland SMS is billed by the number of successfully sent SMS messages according to specific content length rules.

## Payment Method

 Chinese Mainland SMS is daily pay-as-you-go by the number of SMS messages according to specific content length rules. General vouchers do not apply. The payment for a day is deducted at 8:00 AM the next day as detailed in the bill. For more information, see [Pricing Details](https://intl.cloud.tencent.com/document/product/382/45479).
## Billing Details

 Before the 3rd day of each month, Tencent Cloud will provide you with a detailed Chinese Mainland SMS bill for last month. You can click **Details** for the SMS service in Tencent Cloud console > **Billing Center** > **[Transactions](https://console.cloud.tencent.com/expense/transactions)** to view the billing details. You can also export reports for financial reporting and bookkeeping.

## Overdue Payment

 Chinese Mainland SMS is pay-as-you-go with a daily billing cycle. The payment for a day is deducted at 8:00 AM the next day. If payment fails due to insufficient balance, you will receive a payment overdue notification via SMS. If you fail to make the payment within 12 hours, the service will be suspended.

The service will resume when you have sufficient balance in your Tencent Cloud account. You shall be responsible for any consequences caused by service suspension due to overdue payment.