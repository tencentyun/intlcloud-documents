This document describes instance parameters that cannot be modified due to instance specification limits and their required values.

## Notes
Setting the following parameters will use system resources. To prevent the database use from being affected by parameter values, configure them as needed.

>!Some are key parameters, and changing them may affect your use or the normal running of the instance. Therefore, exercise caution when modifying key parameters.

## Limits on Parameter Values Restricted by Specification

| Specification\Parameter | max_replication_slots | max_wal_senders | max_worker_processes | max_logical_replication_workers | max_parallel_workers |
| --------- | --------------------- | --------------- | -------------------- | ------------------------------- | -------------------- |
| 1C2GiB    | [10-10]               | [27-27]         | [4-10]               | [4-8]                           | [0-2]                |
| 2C4GiB    | [10-10]               | [27-27]         | [4-12]               | [4-8]                           | [0-4]                |
| 2C6GiB    | [10-10]               | [27-27]         | [4-12]               | [4-8]                           | [0-4]                |
| 4C8GiB    | [10-10]               | [27-27]         | [4-18]               | [4-10]                          | [0-8]                |
| 4C16GiB   | [10-10]               | [27-27]         | [4-18]               | [4-10]                          | [0-8]                |
| 6C24GiB   | [10-20]               | [27-27]         | [4-32]               | [4-20]                          | [0-12]               |
| 8C32GiB   | [10-20]               | [27-27]         | [4-36]               | [4-20]                          | [0-16]               |
| 8C48GiB   | [10-20]               | [27-27]         | [4-36]               | [4-20]                          | [0-16]               |
| 12C64GiB  | [10-40]               | [27-40]         | [4-64]               | [4--40]                         | [0-24]               |
| 16C96GiB  | [10-40]               | [27-40]         | [4-72]               | [4--40]                         | [0-32]               |
| 20C128GiB | [10-40]               | [27-40]         | [4-80]               | [4--40]                         | [0-40]               |
| 28C240GiB | [10-60]               | [27-60]         | [4-116]              | [4--60]                         | [0-56]               |
| 48C480GiB | [10-60]               | [27-60]         | [4-156]              | [4--60]                         | [0-96]               |

