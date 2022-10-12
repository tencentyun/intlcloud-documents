Game Multimedia Engine (GME) provides Voice Chat, Voice Messaging and Voice-to-Text services at the following prices.


## Voice Chat
Voice Chat is a pay-as-you-go service billed by voice duration on a monthly basis.

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
</table>
 

>!
>
>- Voice duration is calculated based on the time a user enters and exits the room. If user A enters a voice room at 12:00, user B enters the room at 12:30, and both of them exit the room at 12:40, the duration of voice use would be 50 minutes in total (40 minutes for user A and 10 minutes for user B).


## Voice Messaging
Voice Messaging is billed by the number of daily active users.

### Pricing

<table>
   <tr>
      <td>Billing Mode</td>
      <td>Service Mode</td>
      <td>Unit Price (USD/user/day)</td>
   </tr>
   <tr>
      <td  rowspan="2">Billed by number of users</td>
      <td >Standard</td>
      <td>0.0019 </td>
   </tr>
   <tr>
      <td >Enhanced (Note that this mode was discontinued from September 5, 2022.)</td>
      <td>0.078 </td>
   </tr>
   </tr>
</table>


>?
>- A user who receives or sends a voice message in the application is counted as a voice message DAU, and the total number of voice message DAUs is calculated based on the deduplicated `openID`. `openID` is a unique identifier of a user in an application. One user corresponds to one `openID`.



<dx-alert infotype="notice" title="Changes on Billing Mode">
Starting from September 5, 2022, Voice Messaging and Voice-to-Text are billed separately.
</dx-alert>



## Voice-to-Text

Voice-to-Text supports daily or monthly payment. Daily payment is set by default. If you want to switch to monthly payment, please submit a ticket.

### Pricing
<table>
   <tr>
      <td>Billing Mode</td>
      <td>USD/15 seconds</td>
   </tr>
   <tr>
      <td  rowspan="1">Billed by the duration of the audio or audio stream</td>
      <td> 0.006 (Billed per 15 seconds. Requests shorten than 15 seconds are rounded up to 15 seconds.) </td>
   </tr>
   </tr>
</table>

<dx-alert infotype="notice" title="Changes on Billing Mode">
The above billing plan takes effect from September 5, 2022.
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


>?
>
>- This feature is now only available to beta users. To join the beta, please submit a ticket.


## Overdue Policy
When your account becomes overdue, the GME service will be suspended 24 hours later. If the payment is not made within 168 hours (7 days), all GEM resources will be released permanently. 

## Overdue Payment Alert
Alert notifications for overdue payment will be sent through email, SMS, and Message Center to the Tencent Cloud account creator and all collaborators on the day of and after expiration.
