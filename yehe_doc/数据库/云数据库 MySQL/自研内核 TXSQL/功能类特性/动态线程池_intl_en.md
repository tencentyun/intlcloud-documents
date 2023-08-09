## Overview
The thread pool (Thread_pool) uses a certain number of worker threads to process connection requests, which is typically used in scenarios with online transaction processing (OLTP) workloads. However, when many requests are slow queries, worker threads will be blocked by high-latency operations and fail to quickly respond to new requests. As a result, the system throughput of the thread pool mode is lower than that of the traditional one-thread-per-connection (Per_thread) mode.

The Per_thread and Thread_pool modes have their advantages and disadvantages, so the system needs to flexibly switch between them based on business types. Unfortunately, the mode switch must be completed by restarting the server (during peak hours in most cases), adversely affecting the business.

To allow users to flexibly switch between Per_thread and Thread_pool, TencentDB for MySQL has introduced the optimization of thread pool dynamic switch, that is, to enable or disable the thread pool without restarting the database service.

## Supported Versions
- Kernel version: MySQL 8.0 20201230 and above.
- Kernel version: MySQL 5.7 20201230 and above.

## Use Cases
This feature is suitable for the business which is sensitive to performance and needs to flexibly change the database working mode based on the business type.

## Performance Impact 
- Switching from the thread pool mode to the one-thread-per-connection mode won't block queries or affect database performance.
- Switching from the one-thread-per-connection mode to the thread pool mode under extremely high QPS and persistent high pressure may block requests because the thread pool is disabled before the switch.
  - Solution 1: you can increase the `thread_pool_oversubscribe` parameter and decrease the `thread_pool_stall_limit` parameter to quickly enable the thread pool. After the blocked SQL queries are processed, you can restore the parameters to their original values as needed.
  - Solution 2: if SQL queries start to be blocked, you can suspend or reduce service traffic for a few seconds, wait for thread pool enablement to complete, and then resume the continuous high-pressure service traffic.

## Instructions
You can use the `thread_handling_switch_mode` parameter to control whether to dynamically change the thread working mode. Parameter values are described as follows:

| Valid Value   | Description                                               |
| -------- | -------------------------------------------------- |
| disabled | The mode cannot be changed dynamically.                                   |
| stable    | The mode can only be changed for new connections.                                     |
| fast       | (Default value) The mode can be changed for new connections and new requests.                      |
| sharp    | Active connections will be killed in order to force the user to reconnect so that the mode can be changed quickly.    |

The `show threadpool status` command displays the following new status:
- connections_moved_from_per_thread: the number of connections switched from Per_thread to Thread_pool.
- connections_moved_to_per_thread: the number of connections switched from Thread_pool to Per_thread.
- events_consumed: the total number of events consumed by the worker thread group in each thread pool. After the thread working mode is switched from Thread_pool to Per_thread, the total number of events won't increase any more.
- average_wait_usecs_in_queue: the average time each event waits in the queue.

The `show full processlist` command displays the following new status:
- Moved_to_per_thread: the number of times that the connection is switched to Per_thread.
- Moved_to_thread_pool: the number of times that the connection is switched to Thread_pool.

## Parameter Status Description
Thread pool parameters are described as follows:

| Parameter                                  | Effective Immediately | Type    | Default Value | Valid Values/Value Range      | Description                                                         |
| ------------------------------- | ------------ | ---- | --------------- | --------------------------- | ------------------------------- |
| thread_pool_idle_timeout        | Yes          | uint | 60              | [1, UINT_MAX]               | If there are no network event to handle, the worker thread will wait for `thread_pool_idle_timeout` seconds before being killed |
| thread_pool_oversubscribe       | Yes          | uint | 3               | [1,1000]                    | The maximum number of worker threads allowed in a worker thread group                          |
| thread_pool_size                | Yes          | uint | The number of CPUs on the current machine | [1,1000]                    | The number of thread groups                  |
| thread_pool_stall_limit         | Yes          | uint | 500             | [10, UINT_MAX]              | The timer thread checks all thread groups every `thread_pool_stall_limit` milliseconds.<br>If a thread group has no listener, neither high nor low priority queue is empty, and no new I/O network event occurs, the thread group is considered stalled. The timer thread will wake up a sleeping thread or create a new thread to relieve the thread group's pressure. |
| thread_pool_max_threads         | Yes          | uint | 100000          | [1,100000]                  | The total number of worker threads in the thread pool                               |
| thread_pool_high_prio_mode      | Yes, session | enum | transactions    | transactions\statement\none | The high priority queue supports three modes: <li>transactions: only when there is one statement that already starts a transaction and the ticket (`thread_pool_high_prio_tickets`) held by the connection of this statement is not zero, the connection can enter the high priority queue. After a connection has entered the priority queue `thread_pool_high_prio_tickets` times, it will be placed into the ordinary queue.<li>statement: all connections enter the high priority queue.<li>none: all connections enter the low priority queue.</li> |
| thread_pool_high_prio_tickets   | Yes, session | uint | UINT_MAX        | [0, UINT_MAX]               | The value of the ticket assigned to each connection in `transactions` mode        |
| threadpool_workaround_epoll_bug | Yes          | bool | false           | true/false                  | Whether to bypass the epoll bug of Linux 2.x (which was fixed in Linux 3)          |

The `show threadpool status` command displays the following status:

| Status                            | Description                                                         |
| --------------------------------- | ------------------------------------------------------------ |
| groupid                               | Thread group ID                                                     |
| connection_count                | The number of user connections in the thread group                                             |
| thread_count                      | The number of worker threads in the thread group                                           |
| havelistener                       | Whether the thread group has a listener                                   |
| active_thread_count               | The number of active worker threads in the thread group                                       |
| waiting_thread_count              | The number of worker threads calling wait_begin in the thread group         |
| waiting_threads_size              | The number of sleeping worker threads waiting to be woken up in the thread group when there is no network event to handle (such worker threads will wait for `thread_pool_idle_timeout` seconds before being automatically killed)  |
| queue_size                             | The length of the ordinary queue of the thread group                                     |
| high_prio_queue_size              | The length of the high priority queue of the thread group                                       |
| get_high_prio_queue_num           | The total number of times that events in the thread group are removed from the high priority queue                     |
| get_normal_queue_num              | The total number of times that events in the thread group are removed from the ordinary queue                   |
| create_thread_num                  | The total number of worker threads created in the thread group                                 |
| wake_thread_num                    | The total number of worker threads in the thread group awakened from the waiting_threads queue                |
| oversubscribed_num                | The number of times that worker threads are ready to go to sleep because the thread group is oversubscribed |
| mysql_cond_timedwait_num     | The total number of times that worker threads in the thread group enter the waiting_threads queue                 |
| check_stall_nolistener             | The total number of times that no listener is detected in the thread group in the stall check performed by the timer thread    |
| check_stall_stall                     | The total number of times that the thread group is considered stalled in the stall check performed by the timer thread  |
| max_req_latency_us                | The maximum time in milliseconds for a user connection to wait in the queue in the thread group               |
| conns_timeout_killed               | The total number of times that user connections in the thread group are killed because there has been no new message on the client for the threshold period (net_wait_timeout)   |
| connections_moved_in               | The total number of connections migrated from other thread groups to this thread group                          |
| connections_moved_out             | The total number of connections migrated from this thread group to other thread groups                         |
| connections_moved_from_per_thread | The total number of connections switched from the one-thread-per-connection mode to this thread group        |
| connections_moved_to_per_thread     | The total number of connections switched from this thread group to the one-thread-per-connection mode      |
| events_consumed                          | The total number of events processed by the thread group                                     |
| average_wait_usecs_in_queue       | The average waiting time of all events in the queue in the thread group                     |



