Before reading this document, you need to learn about CVM's [Overview of Billing Methods for Public Network](https://cloud.tencent.com/document/product/213/10578).
This document describes the billing methods of the exclusive public network. For more information on the billing methods of the shared network, please see [Billing of Shared Public Network](https://cloud.tencent.com/document/product/213/10580).

## Bill-by-traffic
The network fees billed by traffic depend only on the outbound traffic of a single CVM, regardless of the CVM billing method (prepaid or postpaid). You can set the maximum bandwidth for the CVM. Packet loss occurs when the instantaneous bandwidth exceeds this limit.

Bill-by-traffic is simple and pay-as-you-go. The network cost depends on the outbound traffic per unit time. This mode is suitable for customers with fluctuating network requirements to cut cost.

### Billing standard
The unit price of the traffic varies by regions. The details are shown as follows:

| Region | Price | 
|---------|---------|
| Mainland China,Hong Kong | 0.12 USD/GB | 
| Singapore,Silicon Valley,Virginia,Toronto,Frankfurt| 0.08 USD/GB | 
| Bangkok,Mumbai| 0.1 USD/GB |
| Tokyo,Moscow| 0.13 USD/GB |

### Purchase procedure
 
In the **Select a region and a model** step, select **Prepaid** or **Postpaid** as the **billing method**; in the **Select a storage and a network** step, select **Bill-by-traffic** as the **bandwidth-based billing method**. Network costs are billed separately based on the actual traffic usage. The billing is accurate to seconds and is settled on an hourly basis.

### Network adjustment
This billing method supports adjusting (upgrading or degrading) the bandwidth cap at any time and the change takes effect in real time.

### Billing description
Bill-by-traffic is calculated based on the actual outbound traffic. You can prevent traffic overflow in a short time by setting the maximum bandwidth.

### Bandwidth cap options
**Bandwidth cap**: The options vary with different payment methods and CVM configurations. For more information, please see [Bandwidth Cap of Public Network](https://cloud.tencent.com/document/product/213/12523).

>**Note:**
>The postpaid bill-by-traffic mode of the exclusive network is available for prepaid and postpaid CVMs.


