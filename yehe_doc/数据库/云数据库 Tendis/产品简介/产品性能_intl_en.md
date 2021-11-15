
### TencentDB for Tendis Hybrid Storage Edition
- Instance specification: 64 GB Redis, 512 GB (SSD cloud disk) Tendis
- Test parameters: `redis-benchmark -d 128 -r 150000000 -c 600`
- Test results:

| Test Case        | Eviction Not Triggered<br>(Writes) | Eviction Triggered<br>(Writes)  | Hot Data Reads<br>(Eviction Not Triggered) | Hot Data Reads<br>(Eviction Triggered)(Cache Hit Rate 70%) | Eviction Triggered When Memory Is Full<br>(Writes)(-c 30) | Hot and Cold Data Reads<br>(Cache Hit Rate 52%)) |
|-------------|------------|-----------|-----------|---------------------|------------------|----------------|
| QPS         | 220,000 queries/sec | 177,162 queries/sec | 350,000 queries/sec | 230,000 queries/sec           | 94,000 queries/sec        | 119,000 queries/sec        |
| redis\_cpu  | 99%        | 99%       | 66%       | 99%                 | 55%              | 64%            |
| tendis\_cpu | 99%     | 96%       | -        | 33%                 | -               | -             |
| 1-ms delay     | 62.08%    | 55.28%   | 99%       | 37.76%             | 99.86%          | 97.79%        |
| 10-ms delay    | 97.99%    | 88.80%   | 99.99%   | 95.83%             | 100%             | 99.99%        |
| Average delay        | 2 ms        | 3.4 ms    | 0.9 ms    | 2 ms                 | 0.16 ms          |  -              |
| Delay in 99% test cases       | 11 ms       | 32 ms      | 1 ms       | 34 ms                | 1 ms              | 2 ms            |
| Maximum delay        | 20 ms       |-           | 5 ms       | 351 ms               | 13 ms             | 20 ms           |
| Maximum delay (write speed limit triggered)  | 1,915 ms     | 433 ms     | -        | -                  | -               | -             |
