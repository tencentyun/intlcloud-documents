## Problem Description
Lock conflict is a problem frequently faced by MySQL database businesses, and its symptoms vary by scenario. In some scenarios, it may directly result in business crash, while in other scenarios, it may be hard to perceive and cause problems such as incorrect and messy data.
The variety, complexity, and imperceptibility of lock conflict scenarios create issues that require a skilled DBA to resolve. Troubleshooting such issues is also time-consuming.

The exception diagnosis feature of DBbrain includes dozens of lock diagnoses such as deadlocks, row lock waits, table locks, read-only locks, DDL/SELECT/DML lock waits, and SQL MDL lock waits, helping you easily solve lock conflicts in an efficient and professional manner.
This document uses the common row lock wait and deadlock as examples to describe how you can use DBbrain to solve a lock conflict.

## Solution
### Scenario 1. Row lock wait

#### Step 1. View the row lock wait event
- **Method 1:**
 1. Log in to the [DBbrain Console](https://console.cloud.tencent.com/dbbrain/instance) and select **Monitoring & Alarm** > **Exception Alarm** on the left sidebar.
 2. Select the time period to be queried and select "Row lock wait" in the "Item" column for filtering.
 3. The list will display the row lock wait events of the instance. Click **Details** in the "Operation" column to access the event details page.


- **Method 2:**
 1. Log in to the [DBbrain Console](https://console.cloud.tencent.com/dbbrain/instance), select **Diagnosis and Optimization** on the left sidebar, and select **Exception Diagnosis**.
 2. Select the target instance above and select "Real-Time" (the data is updated dynamically by default) or "Historical" (you can customize the time period).
 3. Check whether there are row lock wait events in the "Diagnosis Prompt" section. You can click an event to access its details page.


#### Step 2. Solve the row lock wait event
1. On the "Symptom Description" tab on the event details page, you can view the database statement running conditions when the row lock wait event occurs.

2. Switch to the "Intelligent Analysis" tab and view the cause of the row lock wait event.
 - In the row lock wait transaction, you can clearly view the status of blocked transaction statements. For example, the DELETE statement in the figure below is in LOCK WAIT state.

 - Based on the holdlock transaction result, quickly locate the current status and ID of the transaction with a row lock.

 - The performance monitoring curve displays the trends of the number of row lock waits.

3. Switch to the "Expert Suggestion" tab and solve the lock conflict problem as prompted. For example, you can run the `kill` command to kill the session `3965158` and release the lock.


### Scenario 2. Deadlock
>!Since MySQL has deadlock monitoring and automatic transaction rollback capabilities, most deadlock scenarios can heal themselves and are imperceptible to the business. However, problems such as system crash or data inconsistency may occur due to fragile business logic or extreme conditions. Therefore, you should pay attention to deadlocks.

#### Step 1. View the deadlock event
- **Method 1:**
 1. Log in to the [DBbrain Console](https://console.cloud.tencent.com/dbbrain/instance) and select **Monitoring & Alarm** > **Exception Alarm** on the left sidebar.
 2. Select the time period to be queried and select "Deadlock" in the "Diagnosis Item" column for filtering.
 3. The list will display the deadlock events of the instance. Click **Details** in the "Operation" column to access the event details page.


- **Method 2:**
 1. Log in to the [DBbrain Console](https://console.cloud.tencent.com/dbbrain/instance), select **Diagnosis and Optimization** on the left sidebar, and select **Exception Diagnosis**.
 2. Select the target instance above and select "Real-Time" (the data is updated dynamically by default) or "Historical" (you can customize the time period).
 3. Check whether there are deadlock events in the "Diagnosis Prompt" section. You can click an event to access its details page.


#### Step 2. Solve the deadlock event
In the "Symptom Description" tab on the event details page, you can analyze the following information and optimize the corresponding statements to solve the deadlock event:
- Occurrence time and source IP for future traceability.
- Two SQL statements with deadlocks. For example, the two INSERT INTO statements below.
- Which statement is rolled back (Rollback) and which statement is properly executed (Normal) based on the `Status` field value.
- (Optional) Specific lock hold and type based on `LockRequest` and `LockHold`.


 

