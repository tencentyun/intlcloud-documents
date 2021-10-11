GME currently provides voice chat and voice messaging and speech-to-text features at the following prices.


## Voice Chat Service
Voice chat is billed monthly by either voice duration or voice Peak Concurrent Users (PCU) as detailed below:
- The sound quality is HD by default for services billed by voice duration, and cannot be switched to standard.
- The sound quality is standard by default for services billed by voice PCU, and cannot be switched to HD.
- We recommend standard sound quality for battle and leisure games, and HD quality for voice live streaming and online karaoke.

#### Price list

<table>
   <tr>
      <th>Billing Mode</th>
      <th>Sound Quality</th>
      <th>Monthly Voice Duration</th>
      <th>Unit Price (USD/Minute)</th>
   </tr>
   <tr>
      <td  rowspan="2">Billed by voice duration</td>
      <td>HD</td>
      <td> < 10,000 minutes</td>
      <td>Free</td>
   </tr>
   <tr>
      <td>HD</td>
      <td>≥ 10,000 minutes</td>
      <td>0.00094 </td>
   </tr>
   <tr>
      <th>Billing Mode</th>
      <th>Sound Quality</th>
      <th>Monthly Peak PCU</th>
      <th>Unit Price (USD/5,000 PCUs)</th>
   </tr>
   <tr>
      <td  rowspan="5">Billed by voice PCU</td>
      <td  rowspan="5">Standard</td>
      <td>< 5,000</td>
      <td>3000 </td>
   </tr>
   <tr>
      <td>5,000 ≤ PCUs < 50,000</td>
      <td>1870 </td>
   </tr>
   <tr>
      <td>50,000 ≤ PCUs < 100,000</td>
      <td>1560</td>
   </tr>
   <tr>
      <td>100,000 ≤ PCUs < 300,000</td>
      <td>1250</td>
   </tr>
   <tr>
      <td>≥ 300,000</td>
      <td>Contact your Tencent Cloud rep</td>
   </tr>
</table>
 

>Voice duration is calculated based on the time when a user enters and exits the room. If user A enters a voice room at 12:00, user B enters the room at 12:30, and both of them exit the room at 12:40, the voice duration will be 50 minutes in total (40 minutes for user A and 10 minutes for user B).

>Daily PCU refers to the highest number of concurrent online users for the day, and monthly peak PCU refers to the highest daily PCU value for the month. For example, if the daily PCU is 5,400 on the 2nd day and below 5,400 for the rest of the month, the monthly peak PCU will be 5,400.

>For services billed by PCU, fees will be charged per 5,000 PCUs. Values below 5,000 will be calculated as 5,000. For example, if the monthly peak PCU is 5,400, then the fees for the month will be 3000 USD + 1870 USD.


## Voice Messaging and Speech-to-Text Services
Voice messaging and speech-to-text services are billed by voice message DAU.

### Pricing

<table>
   <tr>
      <td>Billing Mode</td>
      <td>Supported Languages</td>
      <td>Unit Price (USD/DAU/Day)</td>
   </tr>
   <tr>
      <td  rowspan="2">Billed by voice message DAU</td>
      <td >Standard</td>
      <td>0.0019 </td>
   </tr>
   <tr>
      <td >Enhanced</td>
      <td>0.078 </td>
   </tr>
   </tr>
</table>



>- A user who receives or sends a voice message in the application is counted as a voice message DAU, and the total number of voice message DAUs is calculated based on the deduplicated `openID`. `openID` is a unique identifier of a user in an application. One user corresponds to one `openID`.
>- The standard mode only supports Simplified Chinese, Korean, and English. The enhanced mode supports all languages. For more information, see [Language Parameter Reference List](https://intl.cloud.tencent.com/document/product/607/30260).


## Service Suspension/Termination Policy
Your GME service will be suspended 24 hours after your account becomes overdue. Your GME resources will be terminated and repossessed 168 hours (7 days) after service suspension. Please ensure that your account balance stays positive to avoid service interruptions.

## Overdue Payment Alerts
Overdue payment alerts will be sent via email, SMS, and the Message Center to the Tencent Cloud account creator and all collaborators on the day your account becomes overdue.
