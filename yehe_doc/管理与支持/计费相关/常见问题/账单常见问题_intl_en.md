### What are the fields "Bill Number", "Bill Date", and "Due Date" in PDF bills?

- Bill Number: The ID of a bill, which is composed of bill year, bill month, and a 10-digit random number.
- Bill Date: The 10th day of the month in which the PDF bill file is generated. If the bill has been rerun (for example, if the bill was adjusted), this field indicates the date when the new bill file is generated.
- Due Date: The 10th day of the next month following the Bill Date. The due date may be postponed as otherwise specified.

### Why do I have a negative bill?

Charges are indicated by positive numbers, and refunds, including refunds for downgrading, are indicated by negative numbers. For some products or projects, your refund amount during a billing period may be more than the amount of charges, hence the negative bill.

### What is the precision difference for monthly billing?

Billing data allows eight decimal places, but the actual amount you are charged (deduction) is rounded to two decimal places. As a result, there may be a difference between the higher-precision billing amount and the lower-precision deduction. The system calculates the difference, for which there are two cases:

Case 1: Positive difference
If the higher-precision billing amount (a) is smaller than the lower-precision deduction (b), it indicates that you were overcharged by the amount of b minus a, in which case you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) for compensation.

Case 2: Negative difference
If the higher-precision billing amount (a) is greater than the lower-precision deduction (b), it indicates that you were undercharged by the amount of a minus b. If this occurs, we will not request that you pay the undercharged amount.

### Do CVM expenses cover bandwidth costs?

- If you use a bandwidth package, your bandwidth costs are billed under BWP and are not included in your CVM expenses.
- If you use the pay-as-you-go mode (bill-by-bandwidth/traffic), your CVM expenses include bandwidth costs, which you can view in **L3: Bill Details**.

### How do I view the costs of IDC bandwidth packages, CDN, and COS by tag?

CDN tags are bound to domains, but the product is billed at the account level, so you cannot view CDN costs by tag in bills.
COS tags are bound to buckets, but the product is billed at the account level, so you cannot view COS costs by tag in bills.
To view the costs of IDC bandwidth packages, CDN, or COS by tag, please [download bill details](https://console.cloud.tencent.com/expense/bill/dosageDownload).

### How do I view project-specific costs of IDC bandwidth packages, CDN, and COS?

IDC bandwidth packages, CDN, and COS do not support project-specific billing. Their costs are collectively treated as those of the default project in bills.

- To view the project-specific costs of IDC bandwidth packages and CDN, please [download bill details](https://console.cloud.tencent.com/expense/bill/dosageDownload).
- To view the bucket-specific costs of COS, please [download bill details](https://console.cloud.tencent.com/expense/bill/dosageDownload).

### How do I view the costs of live streaming products by tag?

The tags of live streaming products are bound to domains, but the products are billed at the application level, so you cannot view their costs by tag in bills.

### After tagging instances and setting cost allocation tags, when can I see the tags in my bills?

Tagging takes effect immediately, but bill data is updated only once every 24 hours, so you may not see your tags immediately.

### Why am I unable to find some of my billed instances in the console pages of the corresponding products?

If you can’t find a billed instance in the corresponding console page, it’s probably because the instance was returned or it was terminated after it expired.
Each instance in the bill has a transaction ID. If an instance is prepaid, it also has an order ID. You can go to the Order Management page to view the purchase time, purchaser, purchased duration, and start/end time of an instance.

### Are CBS and CVM instances in a bill associated with each other?

CVM and CBS are independent products. There are two cases for their presentation in bills:

- If you purchase cloud storage along with a CVM, the storage you purchase will be displayed as a component of the CVM in your bill. The CVM and storage will have the same instance name and project name.
- If you purchase a CVM and expand its storage space later, the new storage you purchase, which needs to be attached to the CVM manually, will not be associated with the CVM.

In your bill, the two will be presented as separate instances and will not be associated with each other.

### How will the costs of an instance be billed after I assign the instance to a new project or change the name of its current project?

If you assign an instance to a new project, the costs of the instance that are incurred after the change will belong to the new project.
In other words, the costs of an instance are billed under whichever project the instance belongs to at the time of cost deduction.

### When will data in **Bill Overview** and **Bill by Instance** be updated after a deduction occurs?

Data in **Bill Overview** and **Bill by Instance** is cached and is refreshed every 24 hours. You can view real-time billing data in **Bill Details**.

### Why is “Instance Name” blank in my bills?

Bills can display the instance names of only some products. For products whose instance names are not displayed in bills, you can use instance IDs to distinguish one from another. For more information, go the corresponding product page in the console or view the documentation of the product.

### What should I do if my bill for a month is markedly higher than the previous month?

1. Check if you purchased notably more instances than usual or renewed your instances more than once in the month.
2. Check if your discounts were applied successfully and whether there was a price increase.
3. If the higher billing amount is due to higher renewal costs, but you renewed your instances only once, check if you used “Same-Date Renewal”, which may result in increased renewal costs.

### In what cases are “Component List Price”, “Original Cost”, and “Discount Rate” not displayed in bills?

1. If you have signed a contract with Tencent Cloud and the price specified in the contract is applied, to avoid any confusion, we will not include “Component List Price”, “Original Cost”, or “Discount Rate” in your bills.
2. You can view list prices on our website.
