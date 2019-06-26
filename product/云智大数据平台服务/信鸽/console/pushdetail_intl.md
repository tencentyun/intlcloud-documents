## Feature Overview

The push details feature helps you track task delivery progress and time, push conversion rate, coverage, and push timeliness. Currently, it supports data analysis for full push and tag push.

## Interface Overview

### Delivery Progress

Real-time task delivery statistics update after task delivery.

### Push Conversion Analysis

The analysis of push conversion rate can be performed for Android and iOS separately.

### Android Push

**Planned pushes**: The number of devices that were connected to the server within the past 30 days for the current app 
**Online devices**: The number of devices connected to the server during the push validity period (messages can be successfully pushed only after the device establishes a connection with the server)  
**Arrivals**: The number of message services that reaches the devices  
**Displays**: The number of message displays, checked via calling the system's message display API  
**Taps**: The number of taps on the notification bar messages  

### iOS Push

**Planned pushes**: The number of all valid devices in the system (if the tokens returned by APNs (Apple Push Message service) are invalid, the system will clean the invalid devices every day)  
**Server deliveries**: The number of devices to which the TPNS server actually delivers messages  
**APNs receipts**: The number of devices that received the messages as per the return of APNs  
**Taps**: The number of taps on the notification bar messages  

### Coverage Analysis

Coverage analysis measures the coverage of full push by comparing the push arrivals and the DAUs of the app. (Currently, this is supported only for Android pushes.)  

**Daily active coverage**: Arrivals of the push task/DAUs today of the push task  
**3-day active coverage**: Arrivals of the push task/deduplicated DAUs in the last three days of the push task  

### Push Timeliness Analysis

Push timeliness analysis subdivides push statistics at the minute and hour levels and supports hourly statistics for up to 24 hours.  

