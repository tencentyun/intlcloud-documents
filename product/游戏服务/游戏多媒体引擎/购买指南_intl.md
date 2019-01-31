The Game Multimedia Engine (GME) currently provides voice chat, voice messaging and speech-to-text functions at the following prices.


## Voice Chat Service
Standard quality is billed by voice DAU and HD quality is billed by voice duration.

- We recommend standard sound quality for battle and leisure games.
- We recommend HD sound quality for live voice broadcasting and online karaoke.

### Free Quota
Details regarding the two billing methods and respective free quota offered is as follows:
- Billed by voice DAUs: free of charge if the daily DAU is below 100.
- Billed by voice duration: free of charge if the daily duration is below 300 minutes.

If the quota above is exceeded, fees will be charged on the basis of the usage.

> If an app has the voice duration of 150 minutes on a day, no fees will be charged. If the duration exceeds 1,000 minutes, the billable duration would be 1,000 minutes. Fee = 1,000 minutes * 0.0059/minute = CNY 5.9 (based on the unit price of CNY 0.0059/minute for the voice duration).


### Price List
<table>
   <tr>
      <td rowspan="8">Billed by Voice DAUs</td>
      <td rowspan="4">Payment Range</td>
      <td rowspan="2">Voice DAUs</td>
      <td>In Mainland China (USD/DAU/day)</td>
      <td>Outside Mainland China (USD/DAU/day)</td>
   </tr>
   <tr>
      <td>0.0015</td>
      <td>0.0072</td>
   </tr>
   <tr>
      <td >Free</td>
      <td colspan="4">DAUs ≤ 100</td>
   </tr>
</table>



<table>
   <tr>
      <td rowspan="3">Billed by Voice Duration</td>
      <td rowspan="2">Payment Range</td>
      <td colspan="4">Unit Price (USD/1,000 minutes)</td>
   </tr>
   <td colspan="2">0.94</td>
   <tr>
      <td>Free</td>
      <td >Duration ≤ 300 Minutes</td>
   </tr>
</table>



>
- A user who enters the room in the app is counted as a voice DAU, and the total number of voice DAUs is calculated based on the deduplicated openIDs (openID is a unique identifier of the user in the app, and one user is associated with one openID).
- Voice duration is calculated based on the time a user enters and exits the room. If user A enters a voice room at 12:00, user B enters the room at 12:30, and both of them exit the room at 12:40, the duration of voice use would be 50 minutes in total (40 minutes for user A and 10 minutes for user B).

## Voice Messaging and Speech-to-text Service
Voice messaging and speech-to-text service is billed by voice messaging DAUs.

### Price List

<table>
   <tr>
      <td>Price Mode</td>
      <td>Supported Languages</td>
      <td>Unit Price (USD/DAU/day)</td>
   </tr>
   <tr>
      <td  rowspan="2">Billed by Voice Messaging DAUs</td>
      <td >Only Simplified Chinese and English</td>
      <td>0.0019 </td>
   </tr>
   <tr>
      <td >All Languages</td>
      <td>0.078 </td>
   </tr>
   </tr>
</table>



> A user who receives or sends a voice message in the app is counted as a voice messaging DAU, and the total number of voice messaging DAUs is calculated based on the deduplicated openIDs (openID is a unique identifier of the user in the app, and one user is associated with one openID).

## Voice Filtering Service

Voice filtering service is billed by filtered audio length. Voice filtering service is still in beta test. Contact the Business Manager if you wish to use this service.

### Price List

| Price Mode | Unit Price (USD/1,000 minutes) |
| -------------------- | ------------------- |
| Billed by Filtered Audio Length | 0.7 |
