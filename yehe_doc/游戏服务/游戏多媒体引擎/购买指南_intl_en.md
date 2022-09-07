Game Multimedia Engine (GME) provides services such as voice chat, voice message, speech-to-text conversion and text translation. The services are billed by usage. The billing details are as follows.

>! If another billing method is agreed with your sales rep, please refer to the contract.

## Voice Chat

Voice chat is a pay-as-you-go service billed by voice duration on a monthly basis.

### Pricing

<table>
   <tr>
      <th>Billing Mode</th>
      <th>Monthly Voice Duration</th>
      <th>Unit Price (USD/min)</th>
   </tr>
   <tr>
      <td  rowspan="2">Billed by voice duration</td>
      <td> < 10,000 minutes</td>
      <td>Free of charge</td>
   </tr>
   <tr>
      <td> ≥ 10,000 minutes</td>
      <td>0.00094 </td>
   </tr>
</table>   

#### Billing details

- Voice duration is calculated based on the time a user enters and exits the room. For example, if user A enters a voice room at 12:00, user B enters the room at 12:30, and both of them exit the room at 12:40, the duration of voice use would be 50 minutes in total (40 minutes for user A and 10 minutes for user B).
- 10,000-minute free package per month is available for voice chat. For example, if the voice duration for the current month is 50,000 minutes, the monthly fees should be `(50,000-10,000) × 0.00094 = 37.6 USD`.



## Voice Message Service

Voice Message Service is a pay-as-you-go service billed by voice message DAUs on a daily basis.

### Pricing

<table>
   <tr>
      <th>Billing Mode</th>
      <th>Service Mode</th>
      <th>Unit Price (USD/person/day)</th>
   </tr>
   <tr>
      <td  rowspan="8">Billed by voice message DAUs</td>
      <td  >Standard</td>
      <td>0.0019 </td>
   </tr>
   <tr>
      <td >Enhanced</td>
      <td>0.078 </td>
   </tr>
</table>

### Billing details

- A user who receives or sends a voice message in the application is counted as a voice message DAU, and the total number of voice message DAUs is calculated based on the deduplicated `openID`. `openID` is a unique identifier of a user in an application. One user corresponds to one `openID`.
- Only Chinese, Korean and English are available for the standard mode, and all languages are available for the enhanced mode. For details, see [Language Parameter Reference List](https://www.tencentcloud.com/zh/document/product/607/30260).
- You can select standard mode or enhanced mode for an application when activating the service, and change the mode later in the console.
- After the voice message DAUs reach a certain range, all usage of the application is billed by the unit price for that range. For example, in standard mode, the voice message DAUs of that day is 48,000, the unit price per person is 0.0019 USD/person/day, so the fees for that day is `48,000 × 0.0019 = 91.2 USD`.

>! Starting from September 5, 2022 (UTC +8), the voice message and speech-to-text conversion services are billed separately. The voice message service is billed by DAUs. The speech-to-text conversion service is billed by voice duration and supports all languages, and the cost is USD 0.006/15 seconds (each voice duration is rounded up to the nearest number in increment of 15 seconds).


## Text Translation Service
The text translation service is billed by the number of characters that are detected and translated.

### Pricing
<table>
   <tr>
      <th>Billing Mode</th>
      <th>Unit Price (USD/1 million characters)</th>
   </tr>
   <tr>
      <td>Billed by the number of characters detected and translated</td>
      <td>20</td>
   </tr>
</table>   

### Billing details
- All characters you passed in, including the whitespace characters, are billed.
- If language detection is needed, the number of characters detected is the number of characters you passed in.
- The number of characters translated is the number of characters you passed in multiplied by the number of target languages. For example, the number of characters you passed in is 100, and they are translated into English, German and Spanish. So the number of target languages is three, and the number of characters translated is `100 × 3=300`.
- The billing unit of text translation is one million characters. The number of characters less than one million is counted upwards to one million.


>? This feature has not been launched. You can submit a ticket to apply for using it.



## Service Suspension/Release Policy

Your GME service will be suspended 24 hours after your account falls into arrears. Your GME resources will be terminated and repossessed 168 hours (7 days) after the service is suspended. For service continuity, please make sure that your account balance is always sufficient. 

## Alert for Overdue Payment

Alert notifications for arrears will be sent through email, SMS, and Message Center to the Tencent Cloud account creator and all collaborators on the day of and after expiration of the daily pay-as-you-go GME resources.