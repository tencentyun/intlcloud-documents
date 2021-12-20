
The Spring Festival Gala red packet campaign involves interactions between four major systems, namely, WeChat, WeChat Pay, red packet system, and Tenpay, which are described in detail below:

- Red packet system: it allows users to send, grab, and open personal red packets and view related lists.
- Tenpay: it supports payment of orders, high-performance storage of asynchronously credited transactions, and real-time display of user account balance and bills.
- WeChat: it ensures the quality of WeChat user access over the internet.
- WeChat Pay: it is the entry to online transactions.
  

![](https://mc.qcloudimg.com/static/img/4e497929b188b4ddc76fe43934d9c126/image.png)

Distributed transaction processing similar to the red packet system is the key focus. For example, **user A sends a red packet of 10 USD to user B** with the following steps involved:
1. Read the balance of user A's account
2. Deduct 10 USD from user A's account (debit)
3. Write the result to user A's account (ack)
4. Read the balance of user B's account
5. Open the red packet sent by user A to user B and read the amount
6. Add 10 USD to user B's account (credit)
7. Write the result to user B's account
   

To ensure data consistency, the steps above have only two results: all steps either succeed or fail and then get rolled back. In this process, the distributed lock mechanism needs to be applied to the accounts of both user A and user B to avoid dirty data. In the WeChat red packet system, which is a huge distributed cluster, this issue may become extremely complicated.

Fortunately, the WeChat red packet system utilizes TDMQ for CMQ to avoid excessive overheads caused by distributed transactions. In the same scenario where user A sends a 10 USD red packet to user B with TDMQ for CMQ used, things are much simpler as follows:

- In step 7 above, user B opens the red packet and finds 10 USD in it. However, the final crediting may fail due to high concurrency pressure on that day.
- The red packet system forwards all the requests with crediting failures to TDMQ for CMQ. When the account balance fails to be updated for user B, the client on the mobile phone will display the waiting state. Then, the account system will continuously pull messages from TDMQ for CMQ to retry updating. TDMQ for CMQ ensures that the 10 USD crediting message will never be lost until it is fetched out.
- On Chinese New Year's Eve, user actions of sending and opening red packets and crediting are all converted into billions of requests. If a traditional transaction method is used, the concurrency pressure will be aggravated and crash the system.
- TDMQ for CMQ ensures reliable storage and transfer of red packet messages and can write three copies in real time to avoid data loss. When fund crediting fails, the operation can be retried multiple times so as to avoid disadvantages of traditional methods such as rollback upon failure and frequent database polling.
