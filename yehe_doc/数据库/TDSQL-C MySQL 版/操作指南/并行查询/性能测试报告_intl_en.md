This document describes the performance test report of TDSQL-C for MySQL parallel query.

## Standard performance test report
- Dataset: TPC-H 
- Tested data volume: 100 GB
- Parallel threads: 16
- Query: Q1, Q3, Q4, Q6, Q9, Q12, Q14, and Q19 performance acceleration ratio

**Execution timetable**

| Query | Non-Parallel Execution Time (s) | 16-Thread Parallel Query Time (s) | Acceleration Ratio |
|---------|---------|---------|---------|
| Q1 | 1,376.96 | 197.25 | 12.84 |
| Q3 | 366.33 | 37.64 | 9.73 |
| Q4 | 92.81 | 6.58 | 14.1 |
| Q6 | 283.83 | 26.05 | 10.9 |
| Q9 | 673.87 | 45.96 | 14.66 |
| Q12 | 361.2 | 35.7 | 10.12 |
| Q14 | 65.02 | 5.7 | 11.41 |
| Q19 | 20.55 | 1.87 | 11.0 |

**Execution time acceleration ratio**
![](https://staticintl.cloudcachetci.com/yehe/backend-news/sFsM878_TDSQL-C%20MySQL%20%E7%89%88_%E4%BA%A7%E5%93%81%E7%9B%AE%E5%BD%95_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US-5.png)

**Conclusion**
The parallel query capability leverages multiple compute cores to greatly shorten the response time of large queries.
