Join operations are common in actual use cases. This document demonstrates how to make aggregate calculations after joining with a dimension table based on the steps described earlier for single-table data aggregation.
1. Create a dimension table in CDB
```
 CREATE TABLE `dim_page` (
  `page_id` varchar(32) NOT NULL,
  `page_name` varchar(32) NOT NULL,
  PRIMARY KEY (`page_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 
```
2. Add data to the dimension table
![](https://main.qcloudimg.com/raw/f512d88911729c8a9baecd0a8ee2add5.png)
3. Create a result table
 ```
 CREATE TABLE `demo_join_sink` (
  `record_time` varchar(32) NOT NULL,
  `page_name` varchar(32) NOT NULL,
  `pv` bigint(20) NOT NULL,
  `uv` bigint(20) NOT NULL,
  PRIMARY KEY (`record_time`,`page_name`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8
```
4. Create a Topic 
 Use the earlier steps to create a topic in the project as the output streams of join results, to record the number of pv and uv aggregated by record_time and page_name.
 ![](https://main.qcloudimg.com/raw/d52ea278487645f5e6100ee12bd2b278.png)
5. Create an Integrator
 Bind the new integrator to the demo_join_sink table you just created, and start the integrator.
  Add the following code to earlier code to complete the CDB information. 
 ```
 CREATE TABLE `dimPage` (
  `page_id` VARCHAR,
  `page_name` VARCHAR,
  PRIMARY KEY(`page_id`)
 ) WITH (
  `type` = 'cdb',
  `instanceId` = '',
  `user` = '',
  `password` = '',
  `database` = '',
  `table` = 'dim_page'
);
CREATE TABLE `demoJoinSink` (
  `record_time` VARCHAR,
  `page_name` VARCHAR,
  `pv` BIGINT,
  `uv` BIGINT,
  PRIMARY KEY ( `record_time`, `page_name` )
) WITH (
  `type` = 'cdp',
  `project` = 'demo',
  `topic` = 'demoJoinSink'
);

 INSERT INTO demoJoinSink
 SELECT
  SUBSTRING(a.record_time, 1, 16) as record_time,
  b.page_name as page_name,
  count(a.user_id) as pv,
  count(DISTINCT a.user_id) as uv
FROM demoSource a
JOIN dimPage b
on a.page_id = b.page_id
GROUP BY SUBSTRING(a.record_time, 1, 16),b.page_name;
```

6. Debug, Save and Launch
 By performing the earlier steps for debugging, saving and launching, you can see the calculation results from joining the two tables.

