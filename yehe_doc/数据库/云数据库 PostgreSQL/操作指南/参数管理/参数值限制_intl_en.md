This document describes instance parameters that cannot be modified due to instance specification limits and their required values.

## Notes
Setting the following parameters will use system resources. To prevent the database use from being affected by parameter values, configure them as needed.

>!Some are key parameters, and changing them may affect your use or the normal running of the instance. Therefore, exercise caution when modifying key parameters.

## Limits on Parameter Values Restricted by Specification

| Specification\Parameter | max_replication_slots | max_wal_senders | max_worker_processes | max_logical_replication_workers | max_parallel_workers |
| --------- | --------------------- | --------------- | -------------------- | ------------------------------- | -------------------- |
| 1C2GiB    | [10-100]              | [27-150]         | [4-300]               | [4-150]                           | [0-2]                |
| 2C4GiB    | [10-100]              | [27-150]         | [4-300]               | [4-150]                           | [0-4]                |
| 2C6GiB    | [10-150]             | [27-200]         | [4-400]               | [4-200]                           | [0-8]                |
| 4C8GiB    | [10-150]             | [27-200]         | [4-400]               | [4-200]                          | [0-8]                |
| 4C16GiB   |[10-150]              | [27-200]         | [4-400]               | [4-200]                          | [0-8]                |
| 6C24GiB   | [10-200]              | [27-250]         | [4-500]               | [4-250]                          | [0-12]               |
| 8C32GiB   | [10-200]              | [27-250]         | [4-500]               | [4-250]                          | [0-16]               |
| 8C48GiB   | [10-200]              | [27-250]         | [4-500]               | [4-250]                          | [0-16]               |
| 12C64GiB  | [10-400]               | [27-450]         | [4-900]               | [4--450]                         | [0-24]               |
| 16C96GiB  | [10-400]               | [27-450]         | [4-900]               | [4--450]                         | [0-32]               |
| 20C128GiB | [10-500]               | [27-450]         | [4-900]               | [4--450]                         | [0-40]               |
| 28C240GiB | [10-600]               | [27-650]         | [4-1300]              | [4--650]                         | [0-56]               |
| 48C480GiB | [10-600]               | [27-650]         | [4-1300]              | [4--650]                         | [0-96]               |
