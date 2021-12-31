Tencent Cloud Face Recognition API calls are billed by the number of calls. Calls in the current month will be settled at the beginning of the next month.


## Pricing

| Monthly API Calls	|0 < Calls ≤ 3 million 	|3 million < Calls ≤ 15 million	| Calls > 15 million |
|------|------|-------|-------|
| Face detection and analysis 	|0.0005 USD/call	|0.0004 USD/call	|0.0003 USD/call|
| Facial feature localization	|0.0008 USD/call	|0.0006 USD/call |	0.0004 USD/call |
| Face comparison |	0.0008 USD/call	|0.0006 USD/call |	0.0004 USD/call |
| Face verification 	|0.0008 USD/call 	|0.0006 USD/call |	0.0004 USD/call |
| Face search |	0.0008 USD/call 	|0.0006 USD/call |	0.0004 USD/call |
| Group management 	|0.0008 USD/call |	0.0006 USD/call |	0.0004 USD/call |


>!
>- There are multiple [group management](https://intl.cloud.tencent.com/document/product/1059/36941#.E4.BA.BA.E5.91.98.E5.BA.93.E7.AE.A1.E7.90.86.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3) APIs. Only [CreatePerson](https://intl.cloud.tencent.com/document/product/1059/36964) API and [CreateFace](https://intl.cloud.tencent.com/document/product/1059/36966) API incur fees, and their calls will be combined into group management calls.
>- All [face verification APIs](https://intl.cloud.tencent.com/document/product/1059/36941#.E4.BA.BA.E8.84.B8.E9.AA.8C.E8.AF.81.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3) incur fees, and their calls will be combined into face verification calls.
>- All [face search APIs](https://intl.cloud.tencent.com/document/product/1059/36941#.E4.BA.BA.E8.84.B8.E6.90.9C.E7.B4.A2.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3) incur fees, and their calls will be combined into face search calls.

## Settlement method

After the total number of monthly API calls reaches a tier, all calls will be billed at the unit price of the tier. The higher the tier, the lower the unit price.

Bills for the current month will be pushed on the 1st day of the next month and automatically settled by the system.

