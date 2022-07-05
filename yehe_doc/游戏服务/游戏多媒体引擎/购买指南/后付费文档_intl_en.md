Game Multimedia Engine (GME) provides Voice Chat, Voice Messaging and Speech-to-Text services at the following prices.


## Voice Chat Service
The Voice Chat service is billed monthly by either voice duration or voice Peak Concurrent Users (PCU) as detailed below:
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
      <td>HD sound quality</td>
      <td> < 10,000 minutes</td>
      <td>Free of charge</td>
   </tr>
   <tr>
      <td>HD sound quality</td>
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
      <td><5,000</td>
      <td>3,000</td>
   </tr>
   <tr>
      <td>5,000 ≤ PCUs < 50,000</td>
      <td>1,870</td>
   </tr>
   <tr>
      <td>50,000 ≤ PCUs < 100,000</td>
      <td>1,560</td>
   </tr>
   <tr>
      <td>100,000 ≤ PCUs < 300,000</td>
      <td>1,250</td>
   </tr>
   <tr>
      <td>≥ 300,000</td>
      <td>Contact your Tencent Cloud rep</td>
   </tr>
</table>
 

>- Voice duration is calculated based on the time a user enters and exits the room. If user A enters a voice room at 12:00, user B enters the room at 12:30, and both of them exit the room at 12:40, the duration of voice use would be 50 minutes in total (40 minutes for user A and 10 minutes for user B).

>- Daily PCU refers to the highest number of concurrent online users for the day, and monthly peak PCU refers to the highest daily PCU value for the month. For example, if the daily PCU is 5,400 on the 2nd day and below 5,400 for the rest of the month, the monthly peak PCU will be 5,400.
>- For services billed by PCU, fees will be charged per 5,000 PCUs. Values below 5,000 will be calculated as 5,000. For example, if the monthly peak PCU is 5,400, then the fees for the month will be 3,000 USD + 1,870 USD.


## Voice Messaging and Speech-to-Text Services
Voice messaging and speech-to-text services are billed by voice message DAU.

### Pricing

<table>
   <tr>
      <td>Billing Mode</td>
      <td>Supported Languages</td>
      <td>Unit Price (USD/DAU/day)</td>
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



>- A user who receives or sends a voice message in the application is counted as a voice message DAU, and the total number of voice message DAUs is calculated based on the duplicated `openID`. `openID` is a unique identifier of a user in an application. One user corresponds to one `openID`.
>- The standard mode only supports Chinese Mandarin, Korean and English. For more languages, please use the enhanced mode. For details, see [Supported Languages](https://intl.cloud.tencent.com/document/product/607/30260).


<dx-alert infotype="notice" title="Changes on Billing Mode">
Starting from July 1, 2022 (UTC +8), the Voice Messaging and Speech-to-Text services are billed separately. The Voice Messaging service is billed by DAU. The Speech-to-Text service is billed by voice durations, and the cost is USD 0.006/15 seconds (each voice duration is rounded up to the nearest number in increment of 15 seconds).
</dx-alert>


## Text Translation Service
The Text Translation service is billed by the number of characters that need to be translated.

<table>
   <tr>
      <td>Billing Mode</td>
      <td>USD/1 million characters</td>
   </tr>
   <tr>
      <td  rowspan="1">Billed by number of characters</td>
      <td> 20 </td>
   </tr>
   </tr>
</table>

>- This feature has not been launched. You can submit a ticket to apply for using it.


## Service Suspension/Release Policy
Your GME service will be suspended 24 hours after your account falls into arrears. Your GME resources will be terminated and repossessed 168 hours (7 days) after the service is suspended. For service continuity, please make sure that your account balance is always sufficient.

## Alert for Overdue Payment
Alert notifications for arrears will be sent through email, SMS, and Message Center to the Tencent Cloud account creator and all collaborators on the day of and after expiration of the daily pay-as-you-go GME resources.