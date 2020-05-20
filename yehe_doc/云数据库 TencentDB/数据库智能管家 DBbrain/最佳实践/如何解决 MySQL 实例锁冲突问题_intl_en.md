## Problem Description
Lock conflict is a problem frequently faced by MySQL database businesses, and its symptoms vary by scenario. In some scenarios, it may directly result in business crash, while in other scenarios, it may be hard to perceive and cause problems such as incorrect and messy data.
The variety, complexity, and imperceptibility of lock conflict scenarios create issues that require a skilled DBA to resolve. Troubleshooting such issues is also time-consuming.

The exception diagnosis feature of DBbrain includes dozens of lock diagnoses such as deadlocks, row lock waits, table locks, read-only locks, DDL/SELECT/DML lock waits, and SQL MDL lock waits, helping you easily solve lock conflicts in an efficient and professional manner.
This document uses the common row lock wait and deadlock as examples to describe how you can use DBbrain to solve a lock conflict.

## Solution
### Scenario 1. Row lock wait

#### Step 1. View the row lock wait event
- **Method 1:**
 1. Log in to the [DBbrain Console](https://console.cloud.tencent.com/dbbrain/instance), select **Instance Management** on the left sidebar, and select **Exception Alarm**.
 2. Select the time period to be queried and select "Row lock wait" in the "Item" column for filtering.
 3. The list will display the row lock wait events of the instance. Click **Details** in the "Operation" column to access the event details page.
![](https://main.qcloudimg.com/raw/a9b09b6b723d6df693a3654b222def0c.png)

- **Method 2:**
 1. Log in to the [DBbrain Console](https://console.cloud.tencent.com/dbbrain/instance), select **Diagnosis and Optimization** on the left sidebar, and select **Exception Diagnosis**.
 2. Select the target instance above and select "Real-Time" (the data is updated dynamically by default) or "Historical" (you can customize the time period).
 3. Check whether there are row lock wait events in the "Diagnosis Prompt" section. You can click an event to access its details page.
![](https://main.qcloudimg.com/raw/31806bae0356b94489b01b399943ade3.png)

#### Step 2. Solve the row lock wait event
1. On the "Symptom Description" tab on the event details page, you can view the database statement running conditions when the row lock wait event occurs.
![](https://main.qcloudimg.com/raw/a01cf1ebb26d92a997703436b3a1d204.png)
2. Switch to the "Intelligent Analysis" tab and view the cause of the row lock wait event.
 - In the row lock wait transaction, you can clearly view the status of blocked transaction statements. For example, the DELETE statement in the figure below is in LOCK WAIT state.
![](https://main.qcloudimg.com/raw/1d39abe23badd37899d64cefc52fc8d5.png)
 - Based on the holdlock transaction result, quickly locate the current status and ID of the transaction with a row lock.
 ![](https://main.qcloudimg.com/raw/c3956864cdeadcae2edee848b6341c72.png)
 - The performance monitoring curve displays the trends of the number of row lock waits.
 ![](https://main.qcloudimg.com/raw/73fd907fe4560135a3704d03955d67bf.png)
3. Switch to the "Expert Suggestion" tab and solve the lock conflict problem as prompted. For example, you can run the `kill` command to kill the session `3965158` and release the lock.
 ![](https://main.qcloudimg.com/raw/3fd46bb10462385a8198183e33a24bbc.png)

### Scenario 2. Deadlock
>Since MySQL has deadlock monitoring and automatic transaction rollback capabilities, most deadlock scenarios can heal themselves and are imperceptible to the business. However, problems such as system crash or data inconsistency may occur due to fragile business logic or extreme conditions. Therefore, you should pay attention to deadlocks.

#### Step 1. View the deadlock event
- **Method 1:**
 1. Log in to the [DBbrain Console](https://console.cloud.tencent.com/dbbrain/instance), select **Instance Management** on the left sidebar, and select **Exception Alarm**.
 2. Select the time period to be queried and select "Deadlock" in the "Diagnosis Item" column for filtering.
 3. The list will display the deadlock events of the instance. Click **Details** in the "Operation" column to access the event details page.
![](https://main.qcloudimg.com/raw/862578b3080d5b6eed8e4c4b176a2cf6.png)

- **Method 2:**
 1. Log in to the [DBbrain Console](https://console.cloud.tencent.com/dbbrain/instance), select **Diagnosis and Optimization** on the left sidebar, and select **Exception Diagnosis**.
 2. Select the target instance above and select "Real-Time" (the data is updated dynamically by default) or "Historical" (you can customize the time period).
 3. Check whether there are deadlock events in the "Diagnosis Prompt" section. You can click an event to access its details page.
 ![](https://main.qcloudimg.com/raw/21ff51331c23b38b5b562840f9089e0c.png)

#### Step 2. Solve the deadlock event
In the "Symptom Description" tab on the event details page, you can analyze the following information and optimize the corresponding statements to solve the deadlock event:
- Occurrence time and source IP for future traceability.
- Two SQL statements with deadlocks. For example, the two INSERT INTO statements below.
- Which statement is rolled back (Rollback) and which statement is properly executed (Normal) based on the `Status` field value.
- (Optional) Specific lock hold and type based on `LockRequest` and `LockHold`.

![](https://main.qcloudimg.com/raw/a01ec3e215d894b27af2615e47782a65.png)
 

