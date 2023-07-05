Game Multimedia Engine (GME) provides Voice Chat, Voice Messaging and Speech-to-Text services at the following prices.


## Voice Chat
Voice Chat is a pay-as-you-go service billed by voice duration on a monthly basis.

### Pricing

<table>
   <tr>
      <th>Billing Mode</th>
      <th>Sound Quality</th>
      <th>Monthly Peak PCU</th>
      <th>Unit Price (USD/5,000 PCUs)</th>
   </tr>
   <tr>
      <td  rowspan="5">Billed by voice PCU</td>
      <td  rowspan="5">Standard</td>
      <td> ≤ 5,000</td>
      <td>3,000</td>
   </tr>
   <tr>
      <td>5,000 < PCUs ≤ 50,000</td>
      <td>1,870</td>
   </tr>
   <tr>
      <td>50,000 < PCUs ≤ 100,000</td>
      <td>1,560</td>
   </tr>
   <tr>
      <td>100,000 < PCUs ≤ 300,000</td>
      <td>1,250</td>
   </tr>
   <tr>
      <td> > 300,000</td>
      <td>Contact your Tencent Cloud rep</td>
   </tr>
</table>
 

>!
>- Daily PCU refers to the highest number of concurrent online users for the day, and monthly peak PCU refers to the highest daily PCU value for the month. For example, if the daily PCU is 5,400 on the 2nd day and below 5,400 for the rest of the month, the monthly peak PCU will be 5,400.
>- For services billed by PCU, fees will be charged per 5,000 PCUs. Values below 5,000 will be calculated as 5,000. For example, if the monthly peak PCU is 5,400, then the fees for the month will be 3,000 USD + 1,870 USD.


## Voice Messaging
Voice Messaging is billed by the number of daily active users.

### Pricing

<table>
   <tr>
      <td>Billing Mode</td>
      <td>Unit Price (USD/DAU/Day)</td>
   </tr>
   <tr>
      <td>Billed by voice message DAU</td>
      <td>0.0019 </td>
   </tr>
   </tr>
</table>


>?
>
>- A user who receives or sends a voice message in the application is counted as a voice message DAU, and the total number of voice message DAUs is calculated based on the deduplicated `openID`. `openID` is a unique identifier of a user in an application. One user corresponds to one `openID`.







## Speech-to-Text

Speech-to-Text supports daily or monthly payment. Daily payment is set by default. If you want to switch to monthly payment, please [submit a ticket](https://console.tencentcloud.com/workorder/category).

### Pricing
<table>
   <tr>
      <td>Billing Mode</td>
      <td>Unit Price (USD/15 Seconds)</td>
   </tr>
   <tr>
      <td  rowspan="1">Billed by the duration of the audio or audio stream</td>
      <td> 0.006 (Billed per 15 seconds. Requests shorter than 15 seconds are rounded up to 15 seconds.) </td>
   </tr>
   </tr>
</table>




## Text Translation Service
The Text Translation service is billed by the number of characters that need to be translated.

### Pricing
<table>
   <tr>
      <td>Billing Mode</td>
      <td>Unit Price (USD/1 Million Characters)</td>
   </tr>
   <tr>
      <td  rowspan="1">Billed by number of characters</td>
      <td> 20 </td>
   </tr>
   </tr>
</table>


>?
>
>- This feature is now only available to beta users. To join the beta, please [submit a ticket](https://console.tencentcloud.com/workorder/category).


## Text-to-Speech Service


>?This feature hasn't been officially launched. To use it, contact the channel manager or [submit a ticket](https://console.tencentcloud.com/workorder/category) to query the price.
>


## Overdue Policy
When your account becomes overdue, the GME service will be suspended 24 hours later. If the payment is not made within 168 hours (7 days), all GEM resources will be released permanently. 

## Overdue Payment Alert
Alert notifications for overdue payment will be sent through email, SMS, and Message Center to the Tencent Cloud account creator and all collaborators on the day of and after expiration.
